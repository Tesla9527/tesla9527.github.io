---
layout:     post
title:      "Win11创建本地账户并设置samba共享"
subtitle:   ""
date:       2022-04-16
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - win11
    - samba
---



需求： 影视下载到win11电脑上，投影仪通过win11的samba共享读取资源并播放。

1. 新建win11本地账号

使用管理员权限打开命令提示符，在CMD中输入以下命令：

```cmd
net user username password /add
```

其中“username”是你的账户名，“password”是账户的密码

2. 选择要共享的文件夹，在共享中添加上一步新建的用户。

3. windows功能中开启SMB 1.0/CIFS 文件共享支持（有些播放器只支持samba 1.0）
