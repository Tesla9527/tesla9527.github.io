---
layout:     post
title:      "使用pandas和pandasql筛选excel中的数据"
subtitle:   ""
date:       2018-07-14
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python    
    - Pandas
    - Pandasql
---

最近的测试工作中有涉及到埋数。在金融行业的风控体系测试中，我们需要调用各种第三方接口，比如人行征信，算话，汇法，芝麻分等等。在测试过程中，我们是无法调用实时接口去查询真实数据的。一来这些接口的调用查询需要花钱，二来我们无法预先知道我们查询出的结果是什么样的。在测试中，我们需要知道我们的期望结果。正因为这样，我们需要在测试数据库中预埋数据，测试时通过接口查询本地数据即可。

在设计完测试场景后，我们就一个场景一个场景的准备数据。这些数据涉及到了很多张数据表，在人工准备数据的时候，我们是按照场景准备的数据，但只要是人操作的东西，就有可能会出错。为了达到我们准备的数据有正确的期望结果，我们需要对这些数据进行提取验证。

准备的数据通常是放在Excel中的，虽然在Excel中也可以写VBA一类的脚本来提取数据，但是本人用VBA写过一次Excel的数据操作，但不是非常熟练。所以转向到了通过python来实现。通过一番Google，发现通过pandas和pandasql这2个模块就可以完成任务了。

pandas用来读取Excel中的数据到DataFrame对象中，每一个DataFrame对象可以看做一张数据库中的数据表。pandasql可以对DataFrame对象执行sql操作，包括多表组合查询等等。最终再使用pandas将查询出来的结果（也是DataFrame对象）写入Excel。

示例脚本如下：
```python
import pandas as pd
from pandasql import *


pysqldf = lambda q: sqldf(q, globals())

RESULT_INFO = pd.read_excel("sample.xlsx", sheet_name = "RESULT_INFO")
NUMREADER_INFO = pd.read_excel("sample.xlsx", sheet_name = "NUMREADER_INFO")

a = """
	select r.NAME, n.NUM_READER, r.REPORT_CREATE_TIME from RESULT_INFO r Left Join NUMREADER_INFO n
	where r.REPORT_SN = n.REPORT_ID;
	"""
result = pysqldf(a)
print(result)
print(type(result))

result.to_excel("result.xlsx")
```

命令行输出结果示例：
```
PS D:\Tesla\Pandas> python .\mytest.py
    NAME  NUM_READER   REPORT_CREATE_TIME
0     杨磊       922.0  2016.12.15 21:48:20
1    莫林霖       819.0  2017.01.12 22:33:33
2    陈大成       950.0  2017.01.12 20:17:04
3    吴婷婷       500.0  2017.01.13 09:23:46
4    侯国平       719.0  2017.02.23 13:44:42
5    王丽丽       760.0  2017.02.23 13:44:54
```

Excel输出结果示例：
![img](/img/in-post/pandas/pandas_result.png)