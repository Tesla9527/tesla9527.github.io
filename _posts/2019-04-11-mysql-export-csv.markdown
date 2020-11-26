---
layout:     post
title:      "mysql导出csv解决科学计数法问题"
subtitle:   ""
date:       2019-04-11
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
tags:
    - mysql
    - csv
    - heidisql
---

mysql客户端我一直使用的heidisql，它的数据导出功能也很好用。有一次使用它进行数据导出时，遇到导出的文件有科学计数法，并且当位数大于12位之后还会把后面的数字全部变成0。网上找了各种办法，都比较麻烦。折腾一番后，发现按照下图的设置进行导出就可以完美显示了。
```
1. Output target选择file
2. Output format选择Delimited text
3. Field separator选择逗号,
4. Encloser选择\t
```

![img](/img/in-post/mysql/heidisql-export.png)

数据通过这种模式导出后，如果想要将该数据导回到mysql，可以选择import csv file，该方式会自动将\N的值以NULL的形式导入数据库。导入向导中Control characters可以按照如下方式进行填写:
```
1. Fields terminated by选择,
2. Fields enclosed by选择\t
3. Fields escaped by选择空
4. Lines terminated by选择\r\n
```