---
layout:     post
title:      "使用pipenv配置python虚拟环境"
subtitle:   ""
date:       2018-08-14
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    false
tags:
    - Python
    - Pipenv
---

文章链接：[https://docs.pipenv.org/](https://docs.pipenv.org/)

其实我自己平时在使用python的时候，都没有使用虚拟环境。为什么呢？因为那都是些我自己使用的脚本，不是那些项目代码。所以能用就行。但是如果是使用python开发项目，比如说flask web项目时，是会用到很多模块的，当我们把这个项目部署到服务器时，我们也需要安装这些模块，这时候我们总得知道使用的是哪些版本的模块吧？所以在真正的项目开发中，使用虚拟环境还是非常有必要的。

Kenneth Reitz大神写的这个虚拟环境工具pipenv比之前的virtualenv要好用一些，那就用这个吧。

需要注意的是，在windows中安装pipenv时，要使用管理员权限打开powershell，要不然安装完pipenv后，无法将pipenv当成exe文件在命令行中执行。

安装过程如下：

```
PS D:\myproject> pip install pipenv
Collecting pipenv
  Using cached https://files.pythonhosted.org/packages/eb/64/9b2747d54f2008ac3dfe86c0b1c8ec126042726fd8a540d5208d26732701/pipenv-2018.7.1-py3-none-any.whl
Requirement already satisfied: virtualenv in c:\users\tesla lau\appdata\local\programs\python\python37-32\lib\site-packages (from pipenv) (16.0.0)
Requirement already satisfied: setuptools>=36.2.1 in c:\users\tesla lau\appdata\local\programs\python\python37-32\lib\site-packages (from pipenv) (39.0.1)
Requirement already satisfied: virtualenv-clone>=0.2.5 in c:\users\tesla lau\appdata\local\programs\python\python37-32\lib\site-packages (from pipenv) (0.3.0)
Requirement already satisfied: pip>=9.0.1 in c:\users\tesla lau\appdata\local\programs\python\python37-32\lib\site-packages (from pipenv) (18.0)
Requirement already satisfied: certifi in c:\users\tesla lau\appdata\local\programs\python\python37-32\lib\site-packages (from pipenv) (2018.8.13)
Installing collected packages: pipenv
Successfully installed pipenv-2018.7.1
PS D:\myproject> pipenv --version
pipenv, version 2018.7.1
PS D:\myproject> pipenv install requests
Creating a virtualenv for this project...
Pipfile: D:\myproject\Pipfile
Using c:\users\tesla lau\appdata\local\programs\python\python37-32\python.exe (3.7.0) to create virtualenv...
Already using interpreter c:\users\tesla lau\appdata\local\programs\python\python37-32\python.exe
Using base prefix 'c:\\users\\tesla lau\\appdata\\local\\programs\\python\\python37-32'
c:\users\tesla lau\appdata\local\programs\python\python37-32\lib\site-packages\virtualenv.py:1041: DeprecationWarning: the imp module is deprecated in favour of importlib; see the module's documentation for alternative uses
  import imp
New python executable in D:\python_virtual_env\myproject-1qCvww8S\Scripts\python.exe
Installing setuptools, pip, wheel...done.
Setting project for myproject-1qCvww8S to D:\myproject

Virtualenv location: D:\python_virtual_env\myproject-1qCvww8S
Creating a Pipfile for this project...
Installing requests...
Collecting requests
  Downloading https://files.pythonhosted.org/packages/65/47/7e02164a2a3db50ed6d8a6ab1d6d60b69c4c3fdf57a284257925dfc12bda/requests-2.19.1-py2.py3-none-any.whl (91kB)
Collecting certifi>=2017.4.17 (from requests)
  Downloading https://files.pythonhosted.org/packages/16/1f/50d729c104b21c1042aa51560da6141d1cab476ba7015d92b2111c8db841/certifi-2018.8.13-py2.py3-none-any.whl (146kB)
Collecting chardet<3.1.0,>=3.0.2 (from requests)
  Downloading https://files.pythonhosted.org/packages/bc/a9/01ffebfb562e4274b6487b4bb1ddec7ca55ec7510b22e4c51f14098443b8/chardet-3.0.4-py2.py3-none-any.whl (133kB)
Collecting urllib3<1.24,>=1.21.1 (from requests)
  Downloading https://files.pythonhosted.org/packages/bd/c9/6fdd990019071a4a32a5e7cb78a1d92c53851ef4f56f62a3486e6a7d8ffb/urllib3-1.23-py2.py3-none-any.whl (133kB)
Collecting idna<2.8,>=2.5 (from requests)
  Downloading https://files.pythonhosted.org/packages/4b/2a/0276479a4b3caeb8a8c1af2f8e4355746a97fab05a372e4a2c6a6b876165/idna-2.7-py2.py3-none-any.whl (58kB)
Installing collected packages: certifi, chardet, urllib3, idna, requests
Successfully installed certifi-2018.8.13 chardet-3.0.4 idna-2.7 requests-2.19.1 urllib3-1.23

Adding requests to Pipfile's [packages]...
Pipfile.lock not found, creating...
Locking [dev-packages] dependencies...
Locking [packages] dependencies...
Updated Pipfile.lock (444a6d)!
Installing dependencies from Pipfile.lock (444a6d)...
  ================================ 5/5 - 00:00:03
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

安装成功后我们在当前项目目录下新建一个main.py文件，内容如下:
```python
import requests


response = requests.get('https://httpbin.org/ip')
print(f"Your IP is { response.json()['origin'] }")
```

使用pipenv run执行的效果如下:
```
PS D:\myproject> pipenv run python main.py
Your IP is 122.97.178.162
```

使用pipenv shell切换到虚拟环境下的shell然后执行python脚本的效果如下:
```
PS D:\myproject> pipenv shell
Launching subshell in virtual environment…
Windows PowerShell
版权所有 (C) Microsoft Corporation。保留所有权利。

PS D:\myproject> python .\main.py
Your IP is 122.97.178.162
```

虚拟环境下查看python的可执行文件和退出虚拟环境后查看python的可执行文件
```
PS D:\myproject> pipenv shell
Launching subshell in virtual environment…
Windows PowerShell
版权所有 (C) Microsoft Corporation。保留所有权利。


PS D:\myproject> python
Python 3.7.0 (v3.7.0:1bf9cc5093, Jun 27 2018, 04:06:47) [MSC v.1914 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> print(sys.executable)
D:\python_virtual_env\myproject-1qCvww8S\Scripts\python.exe
>>> exit()
PS D:\myproject> exit
PS D:\myproject> python
Python 3.7.0 (v3.7.0:1bf9cc5093, Jun 27 2018, 04:06:47) [MSC v.1914 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> print(sys.executable)
C:\Users\Tesla Lau\AppData\Local\Programs\Python\Python37-32\python.exe
```