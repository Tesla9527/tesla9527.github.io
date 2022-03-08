---
layout:     post
title:      "python银行家舍入"
subtitle:   ""
date:       2022-03-08
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - python
---


百度百科关于银行家舍入的说明：
[https://baike.baidu.com/item/银行家舍入/4781630](https://baike.baidu.com/item/银行家舍入/4781630)


Python2中的round()是四舍五入，而Python3中的round()是银行家舍入法。


Python3中round()函数银行家舍入法举例


```python
# 四舍六入五考虑，五后非空就进一，五后为空看奇偶，五前为偶应舍去，五前为奇要进一
print(round(9.8249, 2)) # 四舍
print(round(9.82671, 2)) # 六入
print(round(9.8350, 2)) # 五前为奇要进一
print(round(9.8351, 2)) # 五后非空就进一
print(round(9.8250, 2)) # 五前为偶应舍去
print(round(9.82501, 2)) # 五后非空就进一
```


输出

```
9.82
9.83
9.84
9.84
9.82
9.83
```


参考文章

[https://www.yudelei.com/index.php/47.html](https://www.yudelei.com/index.php/47.html)