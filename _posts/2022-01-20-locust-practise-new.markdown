---
layout:     post
title:      "locust实战(新版)"
subtitle:   ""
date:       2022-01-20
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - 性能测试
---

1、阅读locust官网。官网对locust的使用方法做了非常详细的解说，看完官网资料，基本就没啥问题了。

[https://locust.io/](https://locust.io/)

2、性能测试场景，参考我之前的文章，一般按照这几个场景步骤来，也没啥问题了。

[https://tesla9527.github.io/2017/11/26/design-performance-testing-scenario/](https://tesla9527.github.io/2017/11/26/design-performance-testing-scenario/)

3、新建1个测试文件，比如说locust_file.py，将下面的例子复制粘贴进入。老夫最喜欢的还是复制粘贴。

```python
from locust import HttpUser, task


class WebsiteUser(HttpUser):
    @task
    def test_add(self):
        with self.client.post("/add", json={"content":"123456"}, catch_response=True) as rp:
            if rp.status_code == 200:
                print(rp.text)
                rp.success()
            else:
                rp.failure(f"出现了错误: {rp.text}")
```

4、打开终端，进入locust_file.py所在的目录，执行如下命令，在浏览器中打开终端中提示的路径，输入参数，开始测试。

```
locust -f locust_file.py
```
