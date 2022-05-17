---
layout:     post
title:      "postman安装老版本，并防止更新检查"
subtitle:   ""
date:       2021-04-25
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - postman
---


最新版postman在我的电脑上，文字显示有bug，经常错乱看不清楚，老版本postman对我也够用，所以就找了一下如何安装老版本。


1、 下载地址

[https://www.filepuma.com/download/postman_64bit_6.4.2-20323/](https://www.filepuma.com/download/postman_64bit_6.4.2-20323/)

2、 在hosts中添加记录，防止检查更新

```
0.0.0.0         dl.pstmn.io
0.0.0.0         sync-v3.getpostman.com
0.0.0.0         getpostman.com
```

host文件的地址为: C:\Windows\System32\drivers\etc