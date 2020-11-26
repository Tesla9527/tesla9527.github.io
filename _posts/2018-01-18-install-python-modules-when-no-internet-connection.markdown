---
layout:     post
title:      "断网环境安装python模块"
subtitle:   ""
date:       2018-01-18
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - python
---
python的安装还是在联网的情况下通过pip最方便，但有些场景我们没有外网，自己尝试了多种方法，都很麻烦。最后采用如下方式解决：在一台联网的机器上安装好需要的模块，然后将Lib目录打包拷贝到没有外网的机器上的Lib目录下，就ok了。

后来想用python的locust来做压测，于是也按照上面的方式把文件拷贝过去了，把locust.exe所在的目录也全部拷贝过去了，但是发现在命令行里面执行locust的时候报错failed to create process,真是蛋疼,难道还缺少了什么文件，或者是注册表里面没有注册？最后采用源码安装的方式解决了。但是又遇到了一个坑，启动locust之后，使用http://127.0.0.1:8089, 竟然进不去，最后改为http://localhost:8089/竟然进去了，我也不知道为什么就可以了。。。