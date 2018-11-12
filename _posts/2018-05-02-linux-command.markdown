---
layout:     post
title:      "Linux命令汇总"
subtitle:   ""
date:       2018-05-02
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
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

##### 列出目录下文件大小的详细信息
ll -h
```
[tesla9527@instance-1 home]$ ll --help
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

-h, --human-readable  with -l, print sizes in human readable format(e.g., 1K 234M 2G)
```

示例：
```
[tesla9527@instance-1 home]$ ll -h
total 12M
-rw-r--r--. 1 root      root      12M Sep  7 02:05 opensslrpm.tgz
```

##### 清空文件

truncate -s 0 myfile.txt
```
s or –size: specifies the size to which the file needs to be truncated, in bytes
```

##### 查看程序所在位置

which programname

示例：
```
[tesla9527@instance-1 ~]$ which ping
/usr/bin/ping
```
