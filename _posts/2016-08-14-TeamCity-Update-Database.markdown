---
layout:     post
title:      "使用TeamCity自动更新数据库"
subtitle:   ""
date:       2016-08-14
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - TeamCity
---

在Visual Studio中可以直接在Package Manager Console中执行相关命令就可以了，还好code first提供了一个不错的工具migrate.exe，这样在命令行中就可以完成同样的效果了。

命令行如下：
XCOPY %MigratorToolPath% %StartUpDirectory% /Y
%StartUpDirectory%migrate.exe %MigrationDllFile% /StartUpDirectory=%StartUpDirectory% /connectionString=”Data Source=%Server%;Initial Catalog=%Database%;User ID=sa;PWD=Passw0rd” /connectionProviderName=”System.Data.SqlClient” /verbose

然后再把这里面的变量配置到TeamCity中就好了，参数配置如下：

![img](/img/in-post/teamcity11.jpg)
