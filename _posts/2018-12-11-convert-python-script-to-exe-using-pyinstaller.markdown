---
layout:     post
title:      "使用pyinstaller将python脚本变为exe文件，并使用nssm将exe文件添加到windows服务"
subtitle:   ""
date:       2018-12-11
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - Python
    - Pyinstaller
    - nssm
---
在帮朋友爬取完产品数据后，需要将产品图片用http的方式提供访问已便程序调用，前面博文中介绍说找到了一个python脚本，确实很方便。但是有一个不好的地方就是，因为我要一直提供http服务，所以启动这个脚本后那个控制台就一直在那里挂着，让我看着很不爽。万一被误关掉了呢？所以想到有没有什么办法可以以windows服务的方式在后台运行呢？想到了把python脚本的执行写在bat文件里面，然后把bat文件挂载windows服务里，但是这样做之后服务还是没有起来。今天无意之中在YouTube上看到了Pyinstaller，觉得很不错的，测试了一下，竟然成功了。

Pyinstaller官网地址：
[https://www.pyinstaller.org/index.html](https://www.pyinstaller.org/index.html)

1.安装pyinstaller

```
pip install pyinstaller
```

2.在命令行中切换到python脚本所在的目录，执行以下命令，完成后我们的exe文件就做好啦

```
pyinstaller yourprogram.py
```

![img](/img/in-post/pyinstaller/image_serve.png)

3.在命令行中切换到nssm所在的目录，执行nssm.exe install servicename

4.在弹出的GUI中填上我们做好的exe文件的位置，如果有参数，在参数栏中填入参数，点击确定，完成windows服务的安装

![img](/img/in-post/pyinstaller/image_serve_service.png)