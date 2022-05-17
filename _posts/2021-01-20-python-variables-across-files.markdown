---
layout:     post
title:      "python跨文件的变量"
subtitle:   ""
date:       2021-01-20
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
---


目录结构如下：

![img](/img/in-post/python-variables-across-files/settings.png)

整体思路：在settings.py文件中定义全局变量，并提供get_value和set_value接口给外部使用

settings.py
```python
class global_var():
    '''需要定义全局变量的放在这里，最好定义一个初始值'''
    base_url = 'https://www.baidu.com'

# 对于每个全局变量，都需要定义get_value和set_value接口
def set_base_url(base_url):
    global_var.base_url = base_url
def get_base_url():
    return global_var.base_url

```

test_m01.py

```python
import pytest
import sys
sys.path.append('.')
sys.path.append('..')
from Config import settings


def test_01():
    print(settings.get_base_url())
    settings.set_base_url('https://www.google.com')
    print(settings.get_base_url())
```

test_m02.py

```python
import pytest
import sys
sys.path.append('.')
sys.path.append('..')
from Config import settings


def test_02():
    print(settings.get_base_url())
    settings.set_base_url('https://www.spacex.com')
    print(settings.get_base_url())
```

test_m03.py

```python
import pytest
import sys
sys.path.append('.')
sys.path.append('..')
from Config import settings


def test_03():
    print(settings.get_base_url())
    settings.set_base_url('https://www.tesla.com')
    print(settings.get_base_url())
```

测试结果：

![img](/img/in-post/python-variables-across-files/test_result.png)