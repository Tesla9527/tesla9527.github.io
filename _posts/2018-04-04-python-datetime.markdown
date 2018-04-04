---
layout:     post
title:      "python datetime"
subtitle:   ""
date:       2018-04-04
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python
---
python datetime模块用strftime 格式化时间
```python
from datetime import datetime
print(datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
```
输出结果：
![img](/img/in-post/python-datetime/datetime01.png)