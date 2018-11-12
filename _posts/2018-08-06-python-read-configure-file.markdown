---
layout:     post
title:      "python读取配置文件"
subtitle:   ""
date:       2018-08-06
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    false
tags:
    - Python
---

在研究使用flask-restplus写api的过程中，看到网友写的样例，配置文件是写在python文件中，然后直接导入的。记得之前老夫在用java写自动化框架的时候，配置文件是写在yml文件中的。在python里面是直接写在py文件中，真是方便啊。

举个例子，我们写一个settings.py文件，里面写上我们需要的配置：
```python
# Flask settings
FLASK_SERVER_NAME = 'localhost:8888'
FLASK_DEBUG = True  # Do not use debug mode in production

# Flask-Restplus settings
RESTPLUS_SWAGGER_UI_DOC_EXPANSION = 'list'
RESTPLUS_VALIDATE = True
RESTPLUS_MASK_SWAGGER = False
RESTPLUS_ERROR_404_HELP = False

# SQLAlchemy settings
SQLALCHEMY_DATABASE_URI = 'sqlite:///db.sqlite'
SQLALCHEMY_TRACK_MODIFICATIONS = False
```

然后我们在另一个文件app.py中调用settings.py中的值：
```python
import settings

print(settings)
print(settings.FLASK_SERVER_NAME)
print(settings.FLASK_DEBUG)
print(settings.SQLALCHEMY_DATABASE_URI)
```

输出如下：
```
<module 'settings' from 'D:\\Tesla\\file_merge\\settings.py'>
localhost:8888
True
sqlite:///db.sqlite
[Finished in 0.6s]
```
