---
layout:     post
title:      "Pycharm虚拟环境中手动安装whl文件的python包"
subtitle:   ""
date:       2022-06-02
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
    - pycharm
    - whl
---


转载至
[https://www.csdn.net/tags/MtTakg2sNDUyNTYtYmxvZwO0O0OO0O0O.html](https://www.csdn.net/tags/MtTakg2sNDUyNTYtYmxvZwO0O0OO0O0O.html)


新手如我在pycharm通过pip install xxx的时候会遇到报错，然后在网上找到的wheel文件下载后不会安装，这里记录一下方法：

1.pip安装失败在terminal第一行报错的位置附近，会有xxx包的下载地址，点进去之后直接下载这个包的whl文件；
或者在网上自行搜索所需包的whl文件；

2.下载好之后，把whl文件放到需要该包所用环境的路径下（Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/venv/scripts/xxx.whl）
注意：.whl放在scripts/的目录下

3.进入该项目，在terminal中写入pip install xxx.whl(注意名称是下载的包的全称一字不差）

大功告成！