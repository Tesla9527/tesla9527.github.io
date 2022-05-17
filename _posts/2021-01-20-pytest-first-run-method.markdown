---
layout:     post
title:      "pytest定义1个所有测试案例执行前执行的方法"
subtitle:   ""
date:       2021-01-20
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
    - pytest
---


在脚本的根目录中建立conftest.py文件，文件内容如下。该方法会在所有测试用例执行前被执行。
```python
@pytest.fixture(scope="session",autouse="true")
def init_var():
    print('我被最先执行了')
```