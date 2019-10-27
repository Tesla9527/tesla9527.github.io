---
layout:     post
title:      "python读excel自动生成word"
subtitle:   ""
date:       2019-10-28
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - python
    - 软件测试
---

软件测试时，有时候需要在word中做案例截图。首先在word里要有案例描述，期望结果等相关信息。而用例的编写，很多都是用excel编写的。下面的方法就是读取excel中的内容，自动生成word。之后就只需要把案例截图贴上就可以了。

代码如下：

```python
import openpyxl
from docx import Document
from docx.oxml.ns import qn


wb_obj = openpyxl.load_workbook("test_cases.xlsx")
sheet_obj = wb_obj.active
max_row = sheet_obj.max_row
result = []
for i in range(2,max_row+1):
    result.append({"Title":sheet_obj.cell(row = i, column = 1).value,
                   "Description":sheet_obj.cell(row = i, column = 2).value,
                   "Steps":sheet_obj.cell(row = i, column = 3).value,
                   "Excepted result":sheet_obj.cell(row = i, column = 4).value})

try:
    for i in result:
        print(i)
        document = Document()
        document.styles['Normal'].font.name = u'宋体'
        document.styles['Normal']._element.rPr.rFonts.set(qn('w:eastAsia'), u'宋体')
        table = document.add_table(rows=4, cols=2, style='Table Grid')
        runner = table.cell(0,0).paragraphs[0].add_run("案例标题")
        runner.bold = True
        table.cell(0,1).text = i["Title"]
        runner = table.cell(1,0).paragraphs[0].add_run("案例描述")
        runner.bold = True
        table.cell(1,1).text = i["Description"]
        runner = table.cell(2,0).paragraphs[0].add_run("案例步骤")
        runner.bold = True
        table.cell(2,1).text = i["Steps"]
        runner = table.cell(3,0).paragraphs[0].add_run("期望结果")
        runner.bold = True
        table.cell(3,1).text = i["Excepted result"]
        table.cell(0,0).width = 1097280    # 1.2 * 914400
        table.cell(1,0).width = 1097280
        table.cell(2,0).width = 1097280
        table.cell(3,0).width = 1097280
        table.cell(0,1).width = 4846320    # 5.3 * 914400 
        table.cell(1,1).width = 4846320
        table.cell(2,1).width = 4846320
        table.cell(3,1).width = 4846320
        document.add_paragraph('\n')
        p = document.add_paragraph()
        runner = p.add_run("测试记录：")
        runner.bold = True
        runner.add_break()
        document.save(i["Title"] + '.docx')
except Exception as e:
    print(e)
```

excel中的案例编写如下：
![img](/img/in-post/python-excel-word/1.png)

生成的word列表如下
![img](/img/in-post/python-excel-word/2.png)

生成的word内容如下：
![img](/img/in-post/python-excel-word/3.png)