---
layout:     post
title:      "export dict/list to csv in python(转载)"
subtitle:   ""
date:       2017-09-07
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - python
---

原文地址：
[http://www.idiotinside.com/2015/04/14/export-dict-to-csv-list-to-csv-in-python/](http://www.idiotinside.com/2015/04/14/export-dict-to-csv-list-to-csv-in-python/)

我们可以拿数据库来做对比，数据库中的数据是一行一行的，csv中也一样，每行的数据中每个值应该都对应的是一个key，所以我们把每行的数据装在一个字典dict中，最后再把所有的
字典数据装在一个列表list中，这样不论是我们读代码，还是将数据输出到csv都非常的清晰易懂了。

需要注意的是，要想输出的csv不要每行数据之后都换一行，需要在DictWriter的参数中加如下2个delimiter=',', lineterminator='\n'
writer = csv.DictWriter(csvfile, fieldnames=fieldnames, delimiter=',', lineterminator='\n')
