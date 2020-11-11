---
layout:     post
title:      "使用python爬取妹子图"
subtitle:   ""
date:       2018-04-22
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    false
tags:
    - python
---
参考博客[https://blog.csdn.net/baidu_35085676/article/details/68958267](https://blog.csdn.net/baidu_35085676/article/details/68958267),爬取逻辑一样，只是将请求与解析库改为了使用kennethreitz大神的[requests-html](https://github.com/kennethreitz/requests-html/)库

脚本如下：
```python
from requests_html import HTMLSession
import os


home_url = 'http://www.mzitu.com'

# http请求头
HostReferer = {
    'User-Agent': 'Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)',
    'Referer': 'http://www.mzitu.com'
}
# 此请求头破解盗链
PicReferer = {
    'User-Agent': 'Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)',
    'Referer': 'http://i.meizitu.net'
}
path = "E:\\mzitu\\"  # 保存地址
session = HTMLSession()
r = session.get(home_url, headers=HostReferer)
max_page = r.html.find('.page-numbers')[-2].text  # 找到最大页数

page_url = 'http://www.mzitu.com/page/'
for i in range(1, int(max_page) + 1):
    url = page_url + str(i)
    r = session.get(url, headers=HostReferer)
    all_a = r.html.find('.postlist')[0].find(
        'a[target=_blank]')  # 获取当前页的所有a标签元素
    for a in all_a:
        title = a.text
        if title != '':
            print("准备爬取：" + title)
            title_path = title.strip().replace('?', '').replace(
                ':', '')  # 解决win下不能创建带'?',':'的目录的问题
            final_path = path + title_path
            if os.path.exists(final_path):
                flag = 1
            else:
                os.makedirs(final_path)
                flag = 0
            os.chdir(final_path)
            href = list(a.links)[0]  # 获取当前a标签元素的link
            r = session.get(href, headers=HostReferer)
            pic_max = r.html.find('span')[10].text  # 获取当前a标签跳转link后的图片最大页数
            print('图片数: ' + pic_max)
            if(flag == 1 and len(os.listdir(final_path)) >= int(pic_max)):
                print('已经保存完毕，跳过')
                continue
            for num in range(1, int(pic_max) + 1):
                pic = href + '/' + str(num)
                r = session.get(pic, headers=HostReferer)
                pic_url = r.html.find(
                    '.main-image')[0].search('src="{}"')[0]  # 图片的最终url
                print(pic_url)
                html = session.get(pic_url, headers=PicReferer)
                file_name = pic_url.split(r'/')[-1]
                f = open(file_name, 'wb')
                f.write(html.content)
                f.close()
            print('爬取完成: ' + title)
            print('-----------------------------------')
    print('第', i, '页爬取完成')
```

爬取的福利图示例
![img](/img/in-post/mzitu/23a12.jpg)