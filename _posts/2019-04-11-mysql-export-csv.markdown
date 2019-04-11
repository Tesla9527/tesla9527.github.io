---
layout:     post
title:      "mysql导出csv解决科学计数法问题"
subtitle:   ""
date:       2019-04-11
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
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