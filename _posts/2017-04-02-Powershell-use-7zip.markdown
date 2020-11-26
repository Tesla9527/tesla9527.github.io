---
layout:     post
title:      "powershell中使用7zip压缩文件（转载）"
subtitle:   ""
date:       2017-04-02
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - Powershell
---
原文地址： [http://stackoverflow.com/questions/25287994/running-7-zip-from-within-a-powershell-script](http://stackoverflow.com/questions/25287994/running-7-zip-from-within-a-powershell-script)

之前有说过powershell可以用.Net里面自带的功能来zip文件，但是不同版本的powershell使用方式不同，那么问题来了，我们机器里面不确定是什么版本的powershell，装了新版本的powershell后，CI工具想要调用新版powershell，
不知道又要做什么配置，非常麻烦。还是安装7zip，通过powershell来调用7zip进行压缩来的稳定。

```powershell
if (-not (test-path "$env:ProgramFiles\7-Zip\7z.exe")) {throw "$env:ProgramFiles\7-Zip\7z.exe needed"} 
set-alias sz "$env:ProgramFiles\7-Zip\7z.exe"  

$Source = "c:\BackupFrom\backMeUp.txt" 
$Target = "c:\BackupFolder\backup.zip"

sz a -mx=9 $Target $Source
```





