---
layout:     post
title:      "站点文件每日备份"
subtitle:   ""
date:       2016-07-17
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - Powershell
---
每次给站点发布新版本时，都要备份一下当前版本。每次手工来操作真的很麻烦。还好可以用脚本来实现自动备份。

备份脚本如下：

```powershell
#Step 1: back up site file 'Dfv.Bpm' to a fixed folder with timestamp.
Add-Type -Assembly "System.IO.Compression.FileSystem" ;
$dt = Get-Date -uformat "%Y-%m-%d@%H-%M-%S"
$siteName = 'Dfv.Bpm'
$bakFile = "C:\SiteFileBackup\$($siteName)_$($dt).zip"
[System.IO.Compression.ZipFile]::CreateFromDirectory("C:\inetpub\wwwroot\Dfv.Bpm", $bakFile);
```
