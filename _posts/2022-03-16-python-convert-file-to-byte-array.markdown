---
layout:     post
title:      "python读取文件并转换成字节数组"
subtitle:   ""
date:       2022-03-16
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
---




```python
import struct


file_object=open('file_path','rb')
aa=file_object.read()
print(aa)
bt=struct.unpack(len(aa)*'B',aa)
print(bt)
file_object.close()
```


参考文章

[https://www.geek-share.com/detail/2717250259.html](https://www.geek-share.com/detail/2717250259.html)
