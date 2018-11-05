---
layout:     post
title:      "使用python下载网络图片"
subtitle:   ""
date:       2018-11-05
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    true
tags:
    - Python
---
>在帮朋友写爬虫去爬取数据时，遇到下载网络图片的问题。按照之前爬取小姐姐图片的方法，总会有某些图片下载下来后显示无效图片，后来在网上找到了另外一个方法，所有图片都能顺利地下载下来了。在此记录一下，之后遇到下载图片的需求时，就按照后面的方法来。

## 下载后显示无效图片的方法

```python
from requests_html import HTMLSession

session = HTMLSession()
img = 'https://www.louisvuitton.cn/images/is/image/lv/1/PP_VP_L/路易威登-200ml-旅行装香水盒-epi-订制服务--LS0156_PM2_Front view.jpg'
img_r = session.get(img, stream=True)
img_name = 'test.jpg'

f = open(img_name, 'wb')
f.write(img_r.content)
f.close()
```

## 下载成功的方法

```python
import requests


img = 'https://www.louisvuitton.cn/images/is/image/lv/1/PP_VP_L/路易威登-200ml-旅行装香水盒-epi-订制服务--LS0156_PM2_Front view.jpg'
with open('pic1.jpg', 'wb') as handle:
    response = requests.get(img, stream=True)
    if not response.ok:
        print(response)
    for block in response.iter_content(1024):
        if not block:
            break
        handle.write(block)
```