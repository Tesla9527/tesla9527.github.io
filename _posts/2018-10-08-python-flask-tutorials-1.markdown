---
layout:     post
title:      "Python Flask Tutorials 1 - Getting Started"
subtitle:   ""
date:       2018-10-08
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python
---

参考链接[http://coreyms.com/development/python/python-flask-tutorials-full-series](http://coreyms.com/development/python/python-flask-tutorials-full-series)

本来打算用pipenv安装python虚拟环境的，由于遇到了pipenv的bug，这部分就先搁浅。

在D盘新建目录flask_blog，新建文件flaskblog.py,flaskblog.py的内容如下：

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
    return 'Index Page'

```

打开powershell控制台,执行如下命令：

$env:FLASK_APP = "flaskblog.py"
$env:FLASK_DEBUG=1
flask run

执行效果如下：
```
PS D:\flask_blog> $env:FLASK_APP = "flaskblog.py"
PS D:\flask_blog> $env:FLASK_DEBUG=1
PS D:\flask_blog> flask run
 * Serving Flask app "flaskblog.py" (lazy loading)
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 172-690-645
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
127.0.0.1 - - [08/Oct/2018 15:15:59] "GET / HTTP/1.1" 200 -
 * Detected change in 'D:\\flask_blog\\flaskblog.py', reloading
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 172-690-645
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
127.0.0.1 - - [08/Oct/2018 15:16:13] "GET / HTTP/1.1" 200 -
```