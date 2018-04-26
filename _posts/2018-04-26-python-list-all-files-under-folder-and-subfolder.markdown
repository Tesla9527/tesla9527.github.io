---
layout:     post
title:      "python列出目录（包含子目录）下的所有文件"
subtitle:   ""
date:       2018-04-26
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python
---

脚本如下
```python
import os

root_path = r"E:\Movie"
count = 0
result = []
for path, subdirs, files in os.walk(root_path):
    for name in files:
        file = os.path.join(path, name)
        result.append(file)
        count += 1
print("共", count, "个文件")
print('----------------')
for i in result:
    print(i)
```

运行结果
![img](/img/in-post/python-list-files/1.png)