---
layout:     post
title:      "python获取字典中的所有value"
subtitle:   ""
date:       2022-03-30
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - python
---


```python
json_data = {"name": "卓依婷", "addr": "中国台湾"}
print(list(json_data.values()))
```

输出

```
['卓依婷', '中国台湾']
```