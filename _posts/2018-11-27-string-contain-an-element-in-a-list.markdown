---
layout:     post
title:      "python判断字符串是否包含list中的元素"
subtitle:   ""
date:       2018-11-27
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - Python
---
如下：
```python
def containsAny(seq, aset):
    return True if any(i in seq for i in aset) else False
a = '我爱卓依婷'
list_b = ['爱', 'Timi']
list_c = ['不爱']
list_d = ['婷']
list_e = ['依婷']
print(containsAny(a, list_b))
print(containsAny(a, list_c))
print(containsAny(a, list_d))
print(containsAny(a, list_e))
```

输出：
```
True
False
True
True
```