---
layout:     post
title:      "将字符串中的空格替换"
subtitle:   ""
date:       2018-12-29
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - Python
    - 爬虫
---
在写爬虫的时候，有时候需要把返回的数据做处理。有一种情况是，返回的内容中有很多空格或者乱七八糟的不知名'空格'，所以需要把这些空格去掉或替换掉，试了多种办法，如下办法最好用。

[https://stackoverflow.com/questions/8270092/remove-all-whitespace-in-a-string-in-python](https://stackoverflow.com/questions/8270092/remove-all-whitespace-in-a-string-in-python)

```python
a = r'   卓依婷	张宇			 伍佰'
b = " ".join(a.split())
print(b)
```

结果：
```
卓依婷 张宇 伍佰
[Finished in 0.5s]
```