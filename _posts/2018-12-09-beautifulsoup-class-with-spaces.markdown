---
layout:     post
title:      "BeautifulSoup提取有空格的class的标签中的内容"
subtitle:   ""
date:       2018-12-09
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - Python
    - BeautifulSoup
---
爬虫中很重要的一点就是对爬下来的内容进行提取。我的标题其实应该是取的有问题的，我在搜索这个问题的时候，看到stackoverflow上有回答说HTML class can't contain spaces. This element has multiple classes. Searching by either of these classes works。但是我不想使用这个答案中所有的使用其中任意一个class进行搜索的方式，因为我觉得很有可能其他地方也存在这个名字的class，会导致我在定位标签的时候不准确，可能定位到其他标签上了。所以我还是喜欢该问题中的另一个回答。

原链接：[https://stackoverflow.com/questions/46718366/beautifulsoup-and-class-with-spaces](https://stackoverflow.com/questions/46718366/beautifulsoup-and-class-with-spaces)

我测试了一下，发现还是蛮好用的。
```python
from bs4 import BeautifulSoup as soup


html = '''
<tr class="admin-bookings-table-row bookings-history-row  paid   ">张学友张学友我们爱你!</tr>
<tr class="admin-bookings-table-row  nope  paid   ">我爱黎明我爱黎明!</tr>
<h1 class="admin-bookings-table-row  nope  paid   ">我爱卓依婷!</h1>
'''
soup = soup(html, 'lxml')
a = soup.select('tr.admin-bookings-table-row.bookings-history-row.paid')[0]
b = soup.select('tr.admin-bookings-table-row.nope.paid')[0]
c = soup.select('h1.admin-bookings-table-row.nope.paid')[0]
print(a.text, b.text, c.text)
```

输出：
```
张学友张学友我们爱你! 我爱黎明我爱黎明! 我爱卓依婷!
[Finished in 0.7s]
```