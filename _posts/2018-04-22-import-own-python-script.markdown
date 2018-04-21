---
layout:     post
title:      "导入自己编写的python脚本"
subtitle:   ""
date:       2018-04-22
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python
---
>在工作中，自己经常用到了编写的一个写入csv文件的方法，但是每次用的时候都要复制到当前需要使用的脚本中，麻烦且冗余，所以查了一下导入自己编写的python脚本的方法，在此记录一下。

我的python脚本都放在Tesla这个工作目录下，不同的文件夹代表了不同的项目。不同项目下的python文件可能都会用到自己编写的一些常用python方法，所以我建了一个MyUtils目录，然后依次是MyUtils的py文件，MyUtils类。想要使用MyUtils类下的方法的话，只需要在头部import就可以，如下：
```python
import sys
sys.path.append("../MyUtils")
from MyUtils import MyUtils
```

MyUtils文件
![img](/img/in-post/import-own-python/2.png)

需要使用MyUtils类下的方法的文件  
![img](/img/in-post/import-own-python/1.png)