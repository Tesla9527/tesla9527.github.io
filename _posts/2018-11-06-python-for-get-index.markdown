---
layout:     post
title:      "python获取for循环的下标"
subtitle:   ""
date:       2018-11-06
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
tags:
    - python
---
只获取list中的元素：

```python
a = ['卓依婷', '伍佰', '张宇']
for i in a:
    print(i)
```

输出：
```
卓依婷
伍佰
张宇
[Finished in 0.3s]
```

同时获取list中的index和元素：
```python
a = ['卓依婷', '伍佰', '张宇']
for index, i in enumerate(a):
    print(f'{index} - {i}')
```

输出：
```
0 - 卓依婷
1 - 伍佰
2 - 张宇
[Finished in 0.3s]
```	
