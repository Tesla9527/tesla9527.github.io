---
layout:     post
title:      "python中文转拼音"
subtitle:   ""
date:       2022-02-15
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - python
---

```python
from xpinyin import Pinyin

p = Pinyin()
print(p.get_pinyin('卓依婷'))
```

输出

```
zhuo-yi-ting
```