---
layout:     post
title:      "python计算hash值"
subtitle:   ""
date:       2020-07-01
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
tags:
    - python
---

```python
import hashlib


def CalcSha1(filepath):
    with open(filepath,'rb') as f:
        sha1obj = hashlib.sha1()
        sha1obj.update(f.read())
        hash = sha1obj.hexdigest()
        print(hash)
        return hash
 
def CalcMD5(filepath):
    with open(filepath,'rb') as f:
        md5obj = hashlib.md5()
        md5obj.update(f.read())
        hash = md5obj.hexdigest()
        print(hash)
        return hash

CalcSha1('file.txt')
```