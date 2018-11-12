---
layout:     post
title:      "pandas读取excel的sheet问题"
subtitle:   ""
date:       2018-08-02
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    false
tags:
    - Pandas    
---

之前采用的方式如下
```
RESULT_INFO = pd.read_excel("sample.xlsx", sheet_name = "RESULT_INFO")
```

脚本本来运行的好好的，结果把脚本给另外一个同事后，就出现了虽然我在后面指定了sheet_name，但是读取的仍然是第一个sheet的问题。what the fuck!后来Google出来了解决方案，采用如下方式读取完美解决问题，而且如果要读取多个sheet的话，也不用每次都重新读取整个excel文件，而是首先将excel读取出来后放入到对象里面，然后都到这个对象里面去取sheet。

解决方案链接：[https://stackoverflow.com/questions/26521266/using-pandas-to-pd-read-excel-for-multiple-worksheets-of-the-same-workbook](https://stackoverflow.com/questions/26521266/using-pandas-to-pd-read-excel-for-multiple-worksheets-of-the-same-workbook)

```python
xls = pd.ExcelFile('path_to_file.xls')
df1 = pd.read_excel(xls, 'Sheet1')
df2 = pd.read_excel(xls, 'Sheet2')
```