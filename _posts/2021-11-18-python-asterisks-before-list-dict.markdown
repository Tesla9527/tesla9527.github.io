---
layout:     post
title:      "python的列表、字典前面加星号或2个星号的用法"
subtitle:   ""
date:       2021-11-18
author:     "Tesla9527"
header-img: "img/iu3.jpg"
tags:
    - python
---


示例：

```python
fruits = ['lemon', 'pear', 'watermelon', 'tomato']
person = {'name': '刘林', 'age': 32, 'height': 172}
print(*fruits) # 列表前面加*作用是将列表解开成独立的参数
print(*person) # 字典前面加*作用是将字典的key解开成独立的参数
print({**person}) # 字典前面加**作用是将字典的键值对解开成独立的参数
print('-----------------------')
print([1,2,3, *fruits])
print([*person, 'weight'])
print({**person, 'weight': 155})

```

输出：
```
lemon pear watermelon tomato
name age height
{'name': '刘林', 'age': 32, 'height': 172}
-----------------------
[1, 2, 3, 'lemon', 'pear', 'watermelon', 'tomato']
['name', 'age', 'height', 'weight']
{'name': '刘林', 'age': 32, 'height': 172, 'weight': 155}
```