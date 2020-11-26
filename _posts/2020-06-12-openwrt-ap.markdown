---
layout:     post
title:      "wifi路由器设置为AP模式"
subtitle:   ""
date:       2020-06-12
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
tags:
    - 路由器
---

我的wifi路由器是斐讯K2P，最开始是采用网线连接软路由Lan口和wifi路由器wan口的方式，可以成功上网，就没有继续折腾了。最近发现wifi信号有不太稳的情况，于是决定将K2P设置为AP的方式，应该会好一些。

AP的设置方式（转载至恩山论坛）：

[https://www.right.com.cn/forum/thread-255351-1-1.html](https://www.right.com.cn/forum/thread-255351-1-1.html)

两个路由器组成局域网的方法：

一，A B路由器用有线方式连接
1. 保证A能上网，其它设置均在B路由器中设置
2. A与B先不相连，通过电脑连接B路由器LAN口，进入B路由设置界面，关闭B的DHCP功能！设置路由B的LAN口IP地址，必须与A的LAN口IP在一个网段，比如A的IP是192.168.5.1，那么就设B路由的IP为192.168.5.X(2-50,不在A的DHCP地址池中就好)，子网掩码255.255.255.0，DNS网关和本地DNS可以设置成192.168.5.1，保存后路由会重启。重启后设置好B路由的无线参数，无线名称与A路由不同，相同不能实现无线漫游！       
3. 网线直接连接A的LAN口与B的LAN口，B就成为一个交换机或无线交换机，所有接入A，B路由的设备均由A路由进行分配IP。
进入A路由的方式：输入192.168.5.1
进入B路由的方式：输入192.168.5.X（前面B设置的LAN口IP）

这里A相当于软路由或者主路由，B相当于wifi路由器，设置完后，wifi路由器就以AP方式运行了。
![img](/img/in-post/openwrt/ap.jpg)
