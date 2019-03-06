---
layout:     post
title:      "python的可变对象与不可变对象"
subtitle:   ""
date:       2019-03-06
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - python
---

Python3 中有六个标准的数据类型：

1. Number（数字）
2. String（字符串）
3. List（列表）
4. Tuple（元组）
5. Set（集合）
6. Dictionary（字典）

Python3 的六个标准数据类型中：

1. 不可变数据（3 个）：Number（数字）、String（字符串）、Tuple（元组）；
2. 可变数据（3 个）：List（列表）、Dictionary（字典）、Set（集合）。

---

验证可变与不可变

```python
print('验证字符串strings是不可变对象:')
a = 'love'
print(id(a))
a = 'hate'
print(id(a))
print(id('love'))

print('验证元组tuples是不可变对象:')
b = (1,2,3)
print(id(b))
b = (1,2,3,4)
print(id(b))
print(id((1,2,3)))

print('验证数字numbers是不可变对象:')
c = 1
print(id(c))
c = 2
print(id(c))
print(id(1))

print('验证列表list是可变对象:')
d = [1,2,3]
print(id(d))
d.append(4)
print(id(d))

print('验证字典Dictionary是可变对象:')
e = {'name': 'Tesla Lau', 'age': '30'}
print(id(e))
e['age'] = 29
print(id(e))

print('验证集合Set是可变对象:')
f = {'Tesla', 'Timi', 'Wubai'}
print(id(f))
f.add('Michael')
print(id(f))
```

输出
```
验证字符串strings是不可变对象:
15649856
15649984
15649856
验证元组tuples是不可变对象:
54484304
54242640
54484304
验证数字numbers是不可变对象:
257374464
257374480
257374464
验证列表list是可变对象:
15349160
15349160
验证字典Dictionary是可变对象:
15681360
15681360
验证集合Set是可变对象:
15694464
15694464
[Finished in 0.5s]
```

这里的可变不可变，是指内存中的那块内容（value）是否可以被改变。如果是不可变类型，在对对象本身操作的时候，必须在内存中新申请一块区域(因为老区域不可变)。如果是可变类型，对对象操作的时候，不需要再在其他地方申请内存，只需要在此对象后面连续申请(+/-)即可，也就是它的address会保持不变，但区域会变长或者变短。