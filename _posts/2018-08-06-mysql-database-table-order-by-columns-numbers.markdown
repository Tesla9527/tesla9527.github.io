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

今天领导让我给一下数据表中字段数比较长的表，本来打算用heidisql直接拍一下序的，结果排序选项没有这个。于是找同事帮忙写了一个查询的sql解决问题。

```sql
SELECT table_schema,table_name, COUNT(1) AS c
FROM information_schema.columns
GROUP BY table_schema,table_name
ORDER BY c DESC
```
