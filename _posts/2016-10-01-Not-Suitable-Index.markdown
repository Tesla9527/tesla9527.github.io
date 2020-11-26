---
layout:     post
title:      "不适合的索引"
subtitle:   ""
date:       2016-10-01
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - MS SQL Server
---
```sql
SELECT  ind.index_id ,
        obj.name AS TableName ,
        ind.name AS IndexName ,
        ind.type_desc ,
        indUsage.user_seeks ,
        indUsage.user_scans ,
        indUsage.user_lookups ,
        indUsage.user_updates ,
        indUsage.last_user_seek ,
        indUsage.last_user_scan ,
        'drop index [' + ind.name + '] ON [' + obj.name + ']' AS DropIndexCommand
FROM    sys.indexes AS ind
        JOIN sys.objects AS obj ON ind.object_id = obj.object_id
        LEFT JOIN sys.dm_db_index_usage_stats indUsage ON ind.object_id = indUsage.object_id
                                                          AND ind.index_id = indUsage.index_id
WHERE   ind.type_desc <> 'HEAP'
        AND obj.type <> 'S'
        AND OBJECTPROPERTY(obj.object_id, 'isusertable') = 1
        AND ( ISNULL(indUsage.user_seeks, 0) = 0
              AND ISNULL(indUsage.user_scans, 0) = 0
              AND ISNULL(indUsage.user_lookups, 0) = 0
            )
ORDER BY obj.name ,
        ind.name;
GO
```
