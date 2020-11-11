---
layout:     post
title:      "Python - Sublime控制台输出中文乱码的解决方案"
subtitle:   ""
date:       2019-11-05
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - sublime
    - python
---

工具 -> 编译系统  -> 新编译系统
```
{  
    "cmd": ["python.exe","-u","$file"],  
    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",  
    "selector": "source.python",  
    "encoding": "cp936" 
}
```
cmd中改为python.exe的实际路径, 保存当前配置文件为: "python3.sublime-build", 然后在工具->编译系统->选择 "python3"