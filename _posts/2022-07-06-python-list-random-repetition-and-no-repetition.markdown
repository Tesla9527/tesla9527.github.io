---
layout:     post
title:      "python从列表中取随机数，可重复和不可重复"
subtitle:   ""
date:       2022-07-06
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
---


```python
import random

a = [1,2,3,4,5,6,7,8,9,10,11]
print(random.choice(a))  # 随机取1个
print(random.choices(a, k=3)) # 随机取3个，元素可能重复
print(random.sample(a, k=3)) # 随机取3个，元素不重复
```


输出

```
10
[8, 8, 5]
[9, 7, 10]
```