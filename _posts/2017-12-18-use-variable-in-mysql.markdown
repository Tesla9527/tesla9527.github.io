---
layout:     post
title:      "Mysql脚本中使用变量"
subtitle:   ""
date:       2017-12-18
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - mysql
---

```sql
set @myVariable := "Test";
update my_table set my_field = @myVariable
```