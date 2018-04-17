---
layout:     post
title:      "python获取unix时间戳"
subtitle:   ""
date:       2018-04-16
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python
---
>unix时间戳是从1970年1月1日（UTC/GMT的午夜）开始所经过的秒数，不考虑闰秒。

10位时间戳获取方法
```python
import time


t = time.time()
print(t)
print(int(t)) #10位时间戳
```

13位时间戳获取方法
```python
import time


millis = int(round(time.time() * 1000))
print(millis) #13位时间戳
```