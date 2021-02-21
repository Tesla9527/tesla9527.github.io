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

设备：J1900软路由，软路由usb3.0口挂载移动硬盘

固件：[https://downloads.openwrt.org/releases/19.07.7/targets/x86/64/](https://downloads.openwrt.org/releases/19.07.7/targets/x86/64/)下的combined-squashfs.img.gz

使用网线连接的测试结果如下：

读取速度

![img](/img/in-post/openwrt-samba/1.png)

写入速度

![img](/img/in-post/openwrt-samba/2.png)

在安卓手机上使用CX文件管理器或者VLC播放器，通过samba服务播放视频，真的是丝般顺滑。之前下载的TCL 4K演示片，播放的时候也是指哪打哪，随意拖动。以前用斐讯N1通过samba播放这个片子的时候，每次都会卡顿的。看来usb3.0是必须的啊。

安装samba和挂载硬盘
1.首先替换镜像源，要不然速度很慢
在openwrt页面上进入System->Software，点击Configure opkg，在弹出框中的opkg/distfeeds.conf部分进行替换
原始内容:
```
src/gz openwrt_core http://downloads.openwrt.org/releases/19.07.7/targets/x86/64/packages
src/gz openwrt_base http://downloads.openwrt.org/releases/19.07.7/packages/x86_64/base
src/gz openwrt_freifunk http://downloads.openwrt.org/releases/19.07.7/packages/x86_64/freifunk
src/gz openwrt_luci http://downloads.openwrt.org/releases/19.07.7/packages/x86_64/luci
src/gz openwrt_packages http://downloads.openwrt.org/releases/19.07.7/packages/x86_64/packages
src/gz openwrt_routing http://downloads.openwrt.org/releases/19.07.7/packages/x86_64/routing
src/gz openwrt_telephony http://downloads.openwrt.org/releases/19.07.7/packages/x86_64/telephony
```

替换后的内容:
```
src/gz openwrt_core http://mirrors.ustc.edu.cn/openwrt/releases/19.07.7/targets/x86/64/packages
src/gz openwrt_base http://mirrors.ustc.edu.cn/openwrt/releases/19.07.7/packages/x86_64/base
src/gz openwrt_freifunk http://mirrors.ustc.edu.cn/openwrt/releases/19.07.7/packages/x86_64/freifunk
src/gz openwrt_luci http://mirrors.ustc.edu.cn/openwrt/releases/19.07.7/packages/x86_64/luci
src/gz openwrt_packages http://mirrors.ustc.edu.cn/openwrt/releases/19.07.7/packages/x86_64/packages
src/gz openwrt_routing http://mirrors.ustc.edu.cn/openwrt/releases/19.07.7/packages/x86_64/routing
src/gz openwrt_telephony http://mirrors.ustc.edu.cn/openwrt/releases/19.07.7/packages/x86_64/telephony
```
2.安装文件
opkg update                             #更新软件列表
opkg install block-mount                #挂载点菜单
opkg install kmod-usb-storage           #安装usb驱动
opkg install luci-app-samba4            #SAMBA网络共享服务
opkg install kmod-fs-ext4               #挂载ext4
opkg install kmod-fs-vfat               #挂载FAT
opkg install ntfs-3g                    #挂载NTFS
opkg install kmod-usb-ohci
opkg install kmod-usb-uhci

3.重启
reboot

重启完毕后，在web界面中就能看到System->Mount Points和Services->Network Shares

4.斐讯N1远程挂载samba目录
```
mount -t cifs -o username=*,password=*,vers=2.0,dir_mode=0777,file_mode=0777 //ip/分享文件夹名称 /media/qb
```
注意：一定要写dir_mode=0777,file_mode=0777，要不然qbittorrent下载的时候没有写入权限