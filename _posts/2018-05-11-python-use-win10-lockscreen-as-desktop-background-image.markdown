---
layout:     post
title:      "使用win10锁屏图片当桌面背景"
subtitle:   ""
date:       2018-05-11
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    false
tags:
    - Python
---
原文地址：[https://github.com/iamjohnnyzhuang/win-lockfetch](https://github.com/iamjohnnyzhuang/win-lockfetch)

### 1.编写python脚本

将如下python脚本保存
```python
# -*- coding: utf-8 -*-
from PIL import Image
import os, shutil

# win10 锁屏壁纸地址
src = "C:\\Users\\Tesla Lau\\AppData\\Local\\Packages\\Microsoft.Windows.ContentDeliveryManager_cw5n1h2txyewy\\LocalState\\Assets\\"
# 壁纸自定义存放地址
dest = "C:\\Users\\Tesla Lau\\Pictures\\Saved Pictures\\壁纸\\"

if __name__ == "__main__":
    # 过滤相同大小的图片（可能为重复图片）
    sendfiles = set()
    for path, dirs, files in os.walk(src):
        for f in files:
            file = path + f
            filesize = os.path.getsize(file)
            img = Image.open(file).size
            # 过滤小文件 以及 手机壁纸(竖)
            if filesize < 100000 or img[0] // img[1] <= 0 or filesize in sendfiles:
                continue
            sendfiles.add(filesize)
            destfile = dest + f + ".jpg"
            # shutil.copy2(file, unicode(destfile, "utf-8"))
            shutil.copy2(file, destfile)
            print('file ' + f + '.jpg copied')
```

### 2.编写bat文件
```
E:
cd E:\Github\win-lockfetch
python win-lockfetch.py
```

tips:bat文件中的地址需要修改为上面python文件所在路径

### 3.设置开机自动刷新
1. win 键 + r 打开运行窗口
2. 输入 shell:Startup 打开开机会运行的文件窗口
3. 在打开的文件夹下创建vb文件hidecmd.vbs，文件内容如下，其中bat文件路径要改成实际放置的路径，这个可以让运行bat文件时不会弹窗
```
Set oShell = CreateObject ("Wscript.Shell") 
Dim strArgs
strArgs = "cmd /c E:\Github\win-lockfetch\start.bat"
oShell.Run strArgs, 0, false
```

### 4.设置背景图片
每天开机之后，会自动运行上面的脚本，锁屏图片会被复制到python脚本中写的路径，我们设置这个路径为桌面背景即可。