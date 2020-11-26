---
layout:     post
title:      "压缩MS SQL Server数据库的log文件"
subtitle:   ""
date:       2016-12-27
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - MS SQL Server
---
Sql Server数据库的log文件增长的太快了，今天准备还原正在开发的库到阿里云上，发现ldf文件已经有45.5G了，完全没有空间去还原，也想过直接删掉log文件，但是没有成功。

后来用Visual Studio的Schema Compare和SSMS的Import Data解决了这个问题。

	1. 新建一个新的空库
	2. 使用Visual Studio的Schema Compare来对比原始库和新库，update之后会将原始库的Schema，PK，Index，Procedure，Function等等全都复制到新库上
	3. 使用SSMS的Import Data从原始库导入数据到新库

再后来找到一个比较简便的方法,总结下来就是：

	1. 将备份模式修改为Simple模式
	2. 选择Tasks->Shrink->File
	3. 文件类型选择Log
	4. Shrink action选择第一个Release unused space，点击OK
	5. 将备份模式修改为Full模式
	
小乐提供了通过脚本的方式压缩数据库：

```sql
USE [Weixin.Kia]; 
GO

-- Truncate the log by changing the database recovery model to SIMPLE.

ALTER DATABASE [Weixin.Kia] SET RECOVERY SIMPLE;

GO

-- Shrink the trun cated log file to 1 MB.

DBCC SHRINKFILE ([Weixin.Kia_Log], 1024); 
GO

-- Reset the database recovery model.

ALTER DATABASE [Weixin.Kia] SET RECOVERY FULL; 
GO
```