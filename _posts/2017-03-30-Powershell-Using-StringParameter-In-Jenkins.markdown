---
layout:     post
title:      "Jenkins中powershell脚本使用string parameter"
subtitle:   ""
date:       2017-03-30
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - jenkins
---
一直非常喜欢用powershell来写一些脚本，功能非常强大，就拿获取当前日期来说，就比cmd不知道要高到哪里去了。最近公司在用Jenkins做CI，脚本都是用cmd和python来写的。
最近一项打包工作，我觉得用powershell来做比较方便一点。安装完powershell插件后，一开始试了试，觉得竟然用不了Jenkins中的变量，瞬间蛋疼了。本来想改为用cmd来操作，但是
获取日期，zip文件等工作用cmd实在不爽，而且powershell这么强大，不能用在Jenkins里面，岂不是不爽？后来研究了半天，发现是传参的方式和cmd不一样。比如我们定义的String Parameter为Test，值为123.
在cmd里面引用这个参数是%Test%的方式，但是在Powershell里面是$env:Test的方式。






