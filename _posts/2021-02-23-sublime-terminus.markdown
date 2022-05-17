---
layout:     post
title:      "在sublime中打开命令行"
subtitle:   ""
date:       2021-02-23
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - sublime
---


工具地址：

[https://github.com/randy3k/Terminus](https://github.com/randy3k/Terminus)

使用方法：

1.安装插件Terminus

2.点击Preferences->Package Settings->Terminus->Key Bindings，贴上如下内容

```
[
    {
    "keys": ["ctrl+alt+t"],
    "command": "terminus_open",
    "args": {
        "config_name": "Default",
        "cmd": "powershell",
        "cwd": "${file_path:${folder}}"
        }
    }
]
```

执行ctrl+alt+t，效果如下

![img](/img/in-post/sublime-terminus/1.png)