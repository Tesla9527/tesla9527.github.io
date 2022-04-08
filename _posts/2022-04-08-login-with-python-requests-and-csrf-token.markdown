---
layout:     post
title:      "python实现需要csrf-token的登录认证"
subtitle:   ""
date:       2022-04-08
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - python
---


这篇文章中的回答解释的比较清楚

[https://stackoverflow.com/questions/53032456/login-with-python-requests-and-csrf-token](https://stackoverflow.com/questions/53032456/login-with-python-requests-and-csrf-token)


基本思路是:
1. 先通过get请求，获取到cookies
2. 将cookies更新到requests的session中的headers
3. 使用session发起登录认证请求
4. 更新session中的headers的cookies
5. 第4步完成后，后续的接口请求中的headers一般就不需要更新了。

网站这种设计，感觉是为了防爬虫的，但是感觉效果不太。
