---
layout:     post
title:      "Linux命令汇总"
subtitle:   ""
date:       2018-05-02
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Linux
---

##### 查看Linux版本

lsb_release -a

##### 杀死进程

假设进程的id为9527，则命令为kill -s 9 9527，其中-s 9 指定了传递给进程的信号是９，即强制、尽快终止进程。

##### 切换用户

su username

##### 清空文件

truncate -s 0 myfile.txt
s or –size: specifies the size to which the file needs to be truncated, in bytes
