---
layout:     post
title:      "解决scrapy安装失败"
subtitle:   ""
date:       2018-03-30
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python
---
>最近学习爬虫，安装scrapy时报错。

一开始看到安装失败的提示，以为需要安装 Microsoft Visual C++ 14.0，根据后面的链接打开之后下载地址又跳转到Visual Studio的下载地址，坑爹呢...
![img](/img/in-post/scrapy/1.jpg)

后来在网上找到资料，说是单独下载twisted的whl文件进行pip安装就可以
![img](/img/in-post/scrapy/2.jpg)

一开始下错了版本
![img](/img/in-post/scrapy/3.jpg)

更换版本后成功安装
![img](/img/in-post/scrapy/4.jpg)

![img](/img/in-post/scrapy/5.jpg)

scrapy成功安装
![img](/img/in-post/scrapy/6.jpg)