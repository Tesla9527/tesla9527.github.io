---
layout:     post
title:      "使用python启动httpserver"
subtitle:   ""
date:       2018-06-12
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    false
tags:
    - python
---

在使用vuejs写完前端后，执行npm run build编译出可用在生产环境的文件。但是提示说必须通过http的方式打开，通过本地文件的方式打开看不到效果的。于是找了一下怎么样在本地起一个http server，后来发现python就可以实现，非常方便。

在命令行切换到编译出来的前端文件目录，比如说目录是D:\Projects\products\dist，那么我们执行如下2步就可以了：

```
1. cd D:\Projects\products\dist
2. python -m http.server
```