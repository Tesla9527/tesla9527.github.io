---
layout:     post
title:      "Win11创建本地账户并设置samba共享"
subtitle:   ""
date:       2022-04-16
author:     "Tesla9527"
header-img: "img/todaybing4.jpg"
tags:
    - win11
    - samba
---



需求： 影视下载到win11电脑上，投影仪通过win11的samba共享读取资源并播放。

1.新建win11本地账号

使用管理员权限打开命令提示符，在CMD中输入以下命令：

```cmd
net user username password /add
```

其中“username”是你的账户名，“password”是账户的密码

2.选择要共享的文件夹，在共享中添加上一步新建的用户。

3.windows功能中开启SMB 1.0/CIFS 文件共享支持（有些播放器只支持samba 1.0）

4.samba突然不能连接的问题

今天突然samba不能连接了

![img](/img/in-post/win11-create-local-account/1.jpg)

![img](/img/in-post/win11-create-local-account/2.jpg)

一开始都从samba本身的问题上去查原因，一度怀疑samba的稳定性。后来发现竟然是账号的密码过期了。修改密码后立马可以访问了。

5.设置本地账户密码永不过期的方法

[https://blog.csdn.net/rainforest_c/article/details/122818217](https://blog.csdn.net/rainforest_c/article/details/122818217)


效果：

![img](/img/in-post/win11-create-local-account/3.jpg)
