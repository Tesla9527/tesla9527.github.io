---
layout:     post
title:      "python删除linux中的某些文件夹"
subtitle:   ""
date:       2022-03-16
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
---


背景：使用jenkins跑接口自动化脚本，并使用allure插件生成报告。生成的报告按照BUILD_NUMBER依次增加。jenkins中保留部分构建的插件，对这部分内容不会清理。

需求：删除BUILD_NUMBER比当前BUILD_NUMBER小一定数量的allure结果目录


```python
import os
import shutil

workspace = os.environ['WORKSPACE']
build_number = os.environ['BUILD_NUMBER']
for i in os.listdir(f'{workspace}/result/'):
    if int(build_number) - int(i) > 30:
        shutil.rmtree(f'{workspace}/result/{i}')
```
