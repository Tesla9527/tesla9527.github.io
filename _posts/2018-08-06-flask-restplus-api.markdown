---
layout:     post
title:      "使用flask-restplus编写api"
subtitle:   ""
date:       2018-08-06
author:     "Tesla9527"
header-img: "img/post-bg-ArrowPeng.jpg"
catalog:    false
tags:
    - Python
    - flask-restplus    
---

现在web开发大多采用前后端分离的方式，路由的控制权限都交给前端，而后端只提供api服务。前端只管调用后端api，而不用管后端api是怎么实现的。

后端api的编写方式很多，可以使用java，也可以使用python等等。鉴于老夫最近一直在研究python，所以就选择python吧。其实flask的扩展很多，也可以直接写前端页面，但是我还是喜欢前后端分离，前端就用前端框架来写，更专业一些。

使用flask-restplus的一个最简单的例子:
```python
from flask import Flask
from flask_restplus import Resource, Api

app = Flask(__name__)                  #  Create a Flask WSGI application
api = Api(app)                         #  Create a Flask-RESTPlus API

@api.route('/hello')                   #  Create a URL route to this resource
class HelloWorld(Resource):            #  Create a RESTful resource
    def get(self):                     #  Create GET endpoint
        return {'hello': 'world'}

if __name__ == '__main__':
    app.run(debug=True)                #  Start a development server
```

启动后进入http://127.0.0.1:5000/,api的Swagger文档展示页面如下：
![img](/img/in-post/restplus/Swagger.png)

