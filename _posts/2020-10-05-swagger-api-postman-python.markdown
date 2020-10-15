---
layout:     post
title:      "将swagger的api导入到postman并生成python脚本"
subtitle:   ""
date:       2020-10-15
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - Python
    - API
    - swagger
---

现在的接口开发，都比较标准，都能自动生成swagger文档。本来在swagger页面也可以直接调试接口，但是我们要进一步编写接口测试脚本的话，还是要做相关的工作。可以直接从头手写，也可以通过工具转化，在效率提升上应该还是有点帮助的。

下面是转化的过程。我以fastapi生成的swagger文档为例。

1. 找到swagger的链接
![img](/img/in-post/swagger-api-postman-python/1.png)

2. 在postman中填入链接并导入
![img](/img/in-post/swagger-api-postman-python/2.png)

![img](/img/in-post/swagger-api-postman-python/3.png)

![img](/img/in-post/swagger-api-postman-python/4.png)

3. 在选中的接口中，点击code，在弹出框中选择Python - Requests
![img](/img/in-post/swagger-api-postman-python/5.png)

![img](/img/in-post/swagger-api-postman-python/6.png)
