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

if __name__ == '__main__':
    app.run(debug=True)
```

执行效果如下：
```
PS D:\flask_blog> python .\flaskblog.py
 * Serving Flask app "flaskblog" (lazy loading)
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 658-297-446
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

到这里突然想写一些题外话，那就是我为什么要学习flask。作为一名软件测试人员，我学了这个东西不一定能用在工作中，而且制作网站的方式很多，可以使用flask，也可以使用Django，这是基于python的，当然java，C#等编程语言也可以写网站。其实工作中需要的软件测试技术我都已经会了，如果是想在工作中更进一步的话，倒不如更加深入地学习业务知识来的实在。但话说回来，工作都是比较重复的事情，现有知识应付工作是足够的。抛开功利心不讲，我想我学习flask的原因，就是因为想学吧。就像以前念书一样，有的人是为了考高分而努力念书，有的人是单纯地因为喜欢念书。在人生道路的不断学习过程中，我们总是在不断地解锁新技能。我想如果能够享受这些学习过程，享受总结知识带给自己的快感与充实，那应该是更好的。