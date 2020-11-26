---
layout:     post
title:      "python过滤字符串"
subtitle:   ""
date:       2018-12-08
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
tags:
    - python
---
>最近在爬产品数据的时候，为了做产品的唯一性确定，发现用产品的url链接不行，因为相同的产品可能存在于不同的url里面，后来发现产品的货号可以用来做唯一标示，避免了重复数据的入库。但是货号爬下来后，需要做一下处理，要不然可能货号或者一些符号也被包括在里面。需要把爬下来的货号的string进行过滤，只留下英文字母和数字

我还蛮喜欢filter函数的，里面加上lamada表达式，可以对字符串中的每个字符进行各种条件的判断，进而过滤出我们想要的数据。

```python
import re


crazy_string = '货号：8BN310A5E8F13X3'
a = ''.join(list(filter(lambda x : x.isdigit(), crazy_string))) # 过滤出数字
b = ''.join(list(filter(lambda x : re.search('[a-zA-Z]', x), crazy_string))) # 过滤出英文字母
c = ''.join(list(filter(lambda x : x.isdigit() or re.search('[a-zA-Z]', x), crazy_string))) # 过滤出数字和英文字母
print(a,b,c)
```

输出：
```
831058133 BNAEFX 8BN310A5E8F13X3
[Finished in 0.3s]
```