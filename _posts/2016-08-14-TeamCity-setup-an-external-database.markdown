---
layout:     post
title:      "How to setup an external database in teamcity"
subtitle:   ""
date:       2016-08-14
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - TeamCity
---

今天看到Teamcity提示我说我目前使用的是Teamcity的internal的database，如果用一个external的database的话，会有很多好处。于是就想办法去实现这个。

按照Teamcity官网文档中的流程就可以实现，其中需要提到的是在配置<TeamCity Data Directory>\config\database.properties的时候，要按照下面的配置：

![img](/img/in-post/teamcity13.jpg)

我模糊掉的第一个地方填数据库所在的server ip，第二个填数据库登录账号，第三个填数据库登录密码。
