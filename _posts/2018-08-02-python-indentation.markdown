---
layout:     post
title:      "python的缩进问题"
subtitle:   ""
date:       2018-08-02
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python    
---

今天在使用sublime编写python脚本的时候，在脚本已经通过的情况下，新增了一行print，想打印点东西出来看看，结果就报了unindent does not match any outer indentation level的问题。但是看上去都是Tab缩进啊，而且我也是按的Tab键进行的缩进，结果选中前面的缩进，看到的是小点点，小点点代表的是空格，所以在既有空格又有Tab的情况下，缩进可能就出问题了。

解决方法：选中Tab缩进，全部替换成4个空格；或者选中4个空格，全部替换成Tab。