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

设备：J1900软路由，软路由usb3.0口挂载U盘

固件：[https://downloads.openwrt.org/releases/19.07.7/targets/x86/64/](https://downloads.openwrt.org/releases/19.07.7/targets/x86/64/)下的combined-squashfs.img.gz

使用网线连接的测试结果如下：

读取速度

![img](/img/in-post/openwrt-samba/1.png)

写入速度

![img](/img/in-post/openwrt-samba/2.png)

在安卓手机上使用CX文件管理器或者VLC播放器，通过samba服务播放视频，真的是丝般顺滑。之前下载的TCL 4K演示片，播放的时候也是指哪打哪，随意拖动。以前用斐讯N1通过samba播放这个片子的时候，每次都会卡顿的。看来usb3.0是必须的啊。