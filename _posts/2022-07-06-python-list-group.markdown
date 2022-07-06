---
layout:     post
title:      "python将列表元素按指定数目分组"
subtitle:   ""
date:       2022-07-06
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
---


转载至
[https://blog.csdn.net/weixin_34049948/article/details/86002037](https://blog.csdn.net/weixin_34049948/article/details/86002037)


```python
a = [1,2,3,4,5,6,7,8,9,10,11]
step = 5
b = [a[i:i+step] for i in range(0,len(a),step)]
print(b)
```


输出

```
[[1, 2, 3, 4, 5], [6, 7, 8, 9, 10], [11]]
```