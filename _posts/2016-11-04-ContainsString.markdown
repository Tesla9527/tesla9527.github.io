---
layout:     post
title:      "sql函数-判断某个字符串（符号分隔）是否包含另外一个字符串"
subtitle:   ""
date:       2016-11-04
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - MS SQL Server
---
```sql
USE [Demo.Test];
GO

/****** Object:  UserDefinedFunction [dbo].[ContainsString]    Script Date: 2016/11/4 16:57:35 ******/
SET ANSI_NULLS ON;
GO

SET QUOTED_IDENTIFIER ON;
GO


-- =============================================
-- Author:		Freem
-- Create date: 2016-10
-- Description:	<Description, ,>
-- =============================================
CREATE FUNCTION [dbo].[ContainsString]
    (
      -- Add the parameters for the function here
      @sourceStr NVARCHAR(1000) ,
      @destStr NVARCHAR(50)
    )
RETURNS INT
AS
    BEGIN
	-- Declare the return variable here
        DECLARE @result INT = 0;
        DECLARE @singleStr NVARCHAR(100);

	-- Add the T-SQL statements to compute the return value here
        WHILE ( @result = 0
                AND CHARINDEX(',', @sourceStr, 1) > 0
              )
            BEGIN
                SET @singleStr = SUBSTRING(@sourceStr, 1,
                                           CHARINDEX(',', @sourceStr) - 1);
                IF ( @destStr = @singleStr )
                    SET @result = 1;

                SET @sourceStr = SUBSTRING(@sourceStr,
                                           CHARINDEX(',', @sourceStr, 1) + 1,
                                           LEN(@sourceStr));
            END;

        IF ( @destStr = @sourceStr )
            SET @result = 1;

	-- Return the result of the function
        RETURN @result;

    END;


GO
```
