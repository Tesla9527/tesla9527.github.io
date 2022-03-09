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


Python2中的round()是四舍五入法，而Python3中的round()是银行家舍入法。


Python3中round()函数银行家舍入法举例（不推荐使用，会有精度误差）


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

Python3中使用decimal进行舍入（推荐使用）

```python
print(decimal.Decimal('2.8250').quantize(decimal.Decimal('.00'), rounding='ROUND_HALF_UP'))  # 四舍五入法
print(decimal.Decimal('2.8250').quantize(decimal.Decimal('.00'), rounding='ROUND_HALF_EVEN'))  # 银行家舍入法
```

输出

```
2.83
2.82
```


参考文章

[https://www.yudelei.com/index.php/47.html](https://www.yudelei.com/index.php/47.html)

[https://www.pynote.net/archives/765](https://www.pynote.net/archives/765)

[https://cloud.tencent.com/developer/article/1426211](https://cloud.tencent.com/developer/article/1426211)
