---
layout:     post
title:      "断网环境使用pip安装python模块"
subtitle:   ""
date:       2018-09-08
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    false
tags:
    - python
---

文章链接：[https://stackoverflow.com/questions/36725843/installing-python-packages-without-internet-and-using-source-code-as-tar-gz-and](https://stackoverflow.com/questions/36725843/installing-python-packages-without-internet-and-using-source-code-as-tar-gz-and)

之前写过一篇如何在断网环境下安装python模块的文章，主要方法是在一台有网络连接的电脑上安装好，然后将site-package里面的东西拷贝过去，如果有些模块还有可执行命令的(比如locust)，就用源码安装的方式再安装一遍。这种方法虽然可行，但也不是最方便地。最近需要在一台断网的linux(centos7)里面安装locust，找到了上面链接里面的方法，亲测更好用。

如果说我们要断网安装requests，步骤如下:

1. 在联网的机器上使用pip下载requests及其所有依赖包,完成后所有的包安装文件都被下载到我们指定的目录了。
```
PS D:\ddd> pip download requests -d "D:\ddd"
Collecting requests
  Using cached https://files.pythonhosted.org/packages/65/47/7e02164a2a3db50ed6d8a6ab1d6d60b69c4c3fdf57a284257925dfc12bda/requests-2.19.1-py2.py3-none-any.whl
  Saved d:\ddd\requests-2.19.1-py2.py3-none-any.whl
Collecting idna<2.8,>=2.5 (from requests)
  Using cached https://files.pythonhosted.org/packages/4b/2a/0276479a4b3caeb8a8c1af2f8e4355746a97fab05a372e4a2c6a6b876165/idna-2.7-py2.py3-none-any.whl
  Saved d:\ddd\idna-2.7-py2.py3-none-any.whl
Collecting certifi>=2017.4.17 (from requests)
  Using cached https://files.pythonhosted.org/packages/df/f7/04fee6ac349e915b82171f8e23cee63644d83663b34c539f7a09aed18f9e/certifi-2018.8.24-py2.py3-none-any.whl
  Saved d:\ddd\certifi-2018.8.24-py2.py3-none-any.whl
Collecting urllib3<1.24,>=1.21.1 (from requests)
  Using cached https://files.pythonhosted.org/packages/bd/c9/6fdd990019071a4a32a5e7cb78a1d92c53851ef4f56f62a3486e6a7d8ffb/urllib3-1.23-py2.py3-none-any.whl
  Saved d:\ddd\urllib3-1.23-py2.py3-none-any.whl
Collecting chardet<3.1.0,>=3.0.2 (from requests)
  Using cached https://files.pythonhosted.org/packages/bc/a9/01ffebfb562e4274b6487b4bb1ddec7ca55ec7510b22e4c51f14098443b8/chardet-3.0.4-py2.py3-none-any.whl
  Saved d:\ddd\chardet-3.0.4-py2.py3-none-any.whl
Successfully downloaded requests idna certifi urllib3 chardet
```

2. 将下载好的包安装文件拷贝到断网机器上，使用pip安装
```
PS D:\ddd> pip install .\requests-2.19.1-py2.py3-none-any.whl -f ./ --no-index
Looking in links: ./
Processing d:\ddd\requests-2.19.1-py2.py3-none-any.whl
Requirement already satisfied: urllib3<1.24,>=1.21.1 in c:\users\tesla lau\appdata\local\programs\python\python37-32\lib\site-packages (from requests==2.19.1) (1.23)
Requirement already satisfied: certifi>=2017.4.17 in c:\users\tesla lau\appdata\local\programs\python\python37-32\lib\site-packages (from requests==2.19.1) (2018.8.13)
Requirement already satisfied: idna<2.8,>=2.5 in c:\users\tesla lau\appdata\local\programs\python\python37-32\lib\site-packages (from requests==2.19.1) (2.7)
Requirement already satisfied: chardet<3.1.0,>=3.0.2 in c:\users\tesla lau\appdata\local\programs\python\python37-32\lib\site-packages (from requests==2.19.1) (3.0.4)
Installing collected packages: requests
Successfully installed requests-2.19.1
```

亲测在linux和windows上都有效，enjoy!