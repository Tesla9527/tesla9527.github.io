---
layout:     post
title:      "软路由安装官方原版openwrt和samba服务"
subtitle:   ""
date:       2021-02-19
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
tags:
    - openwrt
    - samba
---


之前装过各路大神编译的openwrt固件，总有些不稳定，而且samba传输文件也很慢。今天把固件更新为了官方原版的openwrt固件，然后安装了samba服务。经过测试，效果还是不错的，待后续长时间运行后再看看稳定性如何。

设备：J1900软路由，软路由3.0usb口挂载U盘

固件：[https://downloads.openwrt.org/releases/19.07.7/targets/x86/64/](https://downloads.openwrt.org/releases/19.07.7/targets/x86/64/)下的combined-squashfs.img.gz

使用网线连接的测试结果如下：

读取速度

![img](/img/in-post/openwrt-samba/1.png)

写入速度

![img](/img/in-post/openwrt-samba/2.png)