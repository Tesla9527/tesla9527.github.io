---
layout:     post
title:      "python计时器"
subtitle:   ""
date:       2022-05-17
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - python
---


例子如下

```python
from threading import Timer
from datetime import datetime

def hello():
    print("hello, world")
    print(f'结束计时 - {datetime.now()}')

# 指定10秒后执行hello函数
print(f'开始计时 - {datetime.now()}')
t = Timer(10, hello)
t.start()
```

执行结果

```
开始计时 - 2022-05-17 15:31:28.418243
hello, world
结束计时 - 2022-05-17 15:31:38.429391
[Finished in 10.1s]
```