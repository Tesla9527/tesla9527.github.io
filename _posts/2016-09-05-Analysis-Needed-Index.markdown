---
layout:     post
title:      "分析需要的索引"
subtitle:   ""
date:       2016-09-05
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - MS SQL Server
---
```sql
SELECT  avg_total_user_cost * avg_user_impact * ( user_seeks + user_scans ) AS PossibleImprovement ,
        last_user_seek ,
        last_user_scan ,
        statement AS Object ,
        'CREATE INDEX [IDX_' + CONVERT(VARCHAR, GS.group_handle) + '_'
        + CONVERT(VARCHAR, D.index_handle) + '_'
        + REPLACE(REPLACE(REPLACE([statement], ']', ''), '[', ''), '.', '')
        + ']' + ' ON ' + [statement] + ' (' + ISNULL(equality_columns, '')
        + CASE WHEN equality_columns IS NOT NULL
                    AND inequality_columns IS
      NOT NULL THEN ','
               ELSE ''
          END + ISNULL(inequality_columns, '') + ')' + ISNULL(' INCLUDE ('
                                                              + included_columns
                                                              + ')', '') AS Create_Index_Syntax
FROM    sys.dm_db_missing_index_groups AS G
        INNER JOIN sys.dm_db_missing_index_group_stats AS GS ON GS.group_handle = G.index_group_handle
        INNER JOIN sys.dm_db_missing_index_details AS D ON G.index_handle = D.index_handle
ORDER BY PossibleImprovement DESC;
```
