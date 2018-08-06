---
layout:     post
title:      "mysql数据表使用表的字段数量排序"
subtitle:   ""
date:       2018-08-06
author:     "Tesla9527"
header-img: "img/post-bg-ArrowPeng.jpg"
catalog:    false
tags:
    - Mysql
---

```mysql
SELECT table_schema,table_name, COUNT(1) AS c
FROM information_schema.columns
GROUP BY table_schema,table_name
ORDER BY c DESC
```
