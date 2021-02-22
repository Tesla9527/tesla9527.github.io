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


之前装过各路大神编译的openwrt固件，总有些不稳定，而且samba传输文件也很慢。今天把固件更新为了官方原版的openwrt固件，然后安装了samba服务。过程如下。

### 替换镜像源
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

### 安装文件

```
opkg update                     #更新软件列表
opkg install block-mount        #挂载点菜单
opkg install kmod-usb-storage   #安装usb驱动
opkg install luci-app-samba4    #SAMBA网络共享服务
opkg install kmod-fs-ext4       #挂载ext4
opkg install kmod-fs-vfat       #挂载FAT
opkg install ntfs-3g            #挂载NTFS
opkg install kmod-usb-ohci
opkg install kmod-usb-uhci
```

### 重启

在终端输入reboot或者在页面上重启，重启完毕后，在web界面中就能看到System->Mount Points和Services->Network Shares

### 斐讯N1远程挂载samba目录
为什么要远程挂载？因为在官方原版的openwrt中安装qbittorrent非常麻烦，openwrt官网上只有安装transmission的教程，没有安装qbittorrent的教程。通过Google搜索出来的安装教程也非常少，安装包也是网友自己编译的。我试了几次没有成功，就放弃了。另外软路由上的transmission，使用起来体验不好，要不就是卡死，要不就是种子丢失，也放弃了。斐讯N1的小钢炮系统，有自带的qbittorrent，就省去了安装的麻烦。通过mount远程的samba，就可以实现通过N1的qbittorrent下载到软路由上挂载的移动硬盘了。而且走的是千兆局域网，软路由接移动硬盘又是用的usb3.0，整体测试下来，速度非常满意。

斐讯N1挂载远程samba的脚本：


```
mount -t cifs -o username=*,password=*,vers=2.0,dir_mode=0777,file_mode=0777 //ip/分享文件夹名称 /media/qb
```

注意点：

1. 一定要写dir_mode=0777,file_mode=0777，要不然qbittorrent下载的时候没有写入权限
2. 语句中一定要加上vers=2.0，要不然会报错。至于vers=2.0代表什么意思，以及不加这个参数的话为什么会报错，我也不清楚。
3. username=*,password=*，这一段是输入软路由samba中的用户名密码
4. //ip/分享文件夹名称，ip是软路由ip，分享文件夹名称是软路由中建立samba分享的时候手工填的目录名称
5. /media/qb，是在斐讯N1中手工建的目录，挂载完成后，软路由中的samba分享目录就挂载到斐讯N1的/media/qb目录了。

### 测试结果
设备：J1900软路由，软路由usb3.0口挂载移动硬盘

固件：[https://downloads.openwrt.org/releases/19.07.7/targets/x86/64/](https://downloads.openwrt.org/releases/19.07.7/targets/x86/64/)下的combined-squashfs.img.gz

使用网线连接的测试结果如下：

读取速度

![img](/img/in-post/openwrt-samba/1.png)

写入速度

![img](/img/in-post/openwrt-samba/2.png)

在安卓手机上使用CX文件管理器或者VLC播放器，通过samba服务播放视频，真的是丝般顺滑。之前下载的TCL 4K演示片，播放的时候也是指哪打哪，随意拖动。以前用斐讯N1通过samba播放这个片子的时候，每次都会卡顿的。

### 优点总结

1. J1900软路由和斐讯N1的功耗都非常低，可以一直开机使用。J1900购买时卖家给的电源是12A5A的，换成斐讯N1的12V2A电源也可以正常使用，一点问题没有。
2. 整个数据流转走的是千兆网络和usb3.0，速度快
3. 没有风扇，完全静音。
