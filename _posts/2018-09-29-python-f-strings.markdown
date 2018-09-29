---
layout:     post
title:      "使用f-strings格式化字符串"
subtitle:   ""
date:       2018-09-29
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python
---

python3.6版本新增了f-strings方法来格式化字符串，我们看一下效果。

示例：
```python
name = 'liu lin'
age = 29
print("Hello, {}. Your age is {}.".format(name,age)) # old way format
print(f"Hello, {name}. Your age is {age}.") # f-strings format
```

输出：
```
Hello, liu lin. Your age is 29.
Hello, liu lin. Your age is 29.
[Finished in 0.2s]
```

f-strings格式化字符串，更快，更简洁。对我来说，将来肯定是首选f-strings。