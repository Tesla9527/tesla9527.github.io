---
layout:     post
title:      "python—itchat下载拼接微信好友头像图"
subtitle:   ""
date:       2018-04-05
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python
---
转载至[https://zhuanlan.zhihu.com/p/34290391](https://zhuanlan.zhihu.com/p/34290391)
getHeadImgs.py，执行完该python文件后，会将好友的头像图片下载到指定目录
```python
import itchat
import time


itchat.auto_login()
for friend in itchat.get_friends(update=True)[0:]:
    #可以用此句print查看好友的微信名、备注名、性别、省份、个性签名（1：男 2：女 0：性别不详）
    print(friend['NickName'],friend['RemarkName'],friend['Sex'],friend['Province'],friend['Signature'])
    img = itchat.get_head_img(userName=friend["UserName"])
    path = "D:/Tesla/HeadImages/"+friend['NickName']+"("+friend['RemarkName']+").jpg"
    try:
        with open(path,'wb') as f:
            f.write(img)
            time.sleep(0.05)
    except Exception as e:
        print(repr(e))
itchat.run()
```

jointHeadImgs.py，执行完该python文件后，好友的图片就拼接起来啦
```python
import os
from math import sqrt
from PIL import Image


#path是存放好友头像图的文件夹的路径
path = 'D:/Tesla/HeadImages/'
pathList = []
for item in os.listdir(path):
    imgPath = os.path.join(path,item)
    pathList.append(imgPath)
total = len(pathList)#total是好友头像图片总数
line = int(sqrt(total))#line是拼接图片的行数（即每一行包含的图片数量）
NewImage = Image.new('RGB', (128*line,128*line))
x = y = 0
for item in pathList:
    try:
        img = Image.open(item)
        img = img.resize((128,128),Image.ANTIALIAS)
        NewImage.paste(img, (x * 128 , y * 128))
        x += 1
    except IOError:
        print("第%d行,%d列文件读取失败！IOError:%s" % (y,x,item))
        x -= 1
    if x == line:
        x = 0
        y += 1
    if (x+line*y) == line*line:
        break
NewImage.save("D:/Tesla/" +"final.jpg")
```
拼接出来的图片（PS：图侵删）
![img](/img/in-post/final.jpg)