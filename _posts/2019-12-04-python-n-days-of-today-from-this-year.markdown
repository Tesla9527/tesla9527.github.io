---
layout:     post
title:      "Python计算给定日期是该年的第几天"
subtitle:   ""
date:       2019-12-04
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - Python
---

##计算给定日期是该年的第几天

```python
def count(year,month,day):
    count = 0
    #判断该年是平年还是闰年
    if year%400==0 or (year%4==0 and year%100!=0):
        print(f'{year}年是闰年，2月份有29天！')
        li1 = [31,29,31,30,31,30,31,31,30,31,30,31]
        for i in range(month-1):
            count += li1[i]
        return count+day
    else:
        print(f'{year}年是平年，2月份有28天！')
        li2 = [31,28,31,30,31,30,31,31,30,31,30,31]
        for i in range(month-1):
            count += li2[i]
        return count+day

if __name__ == "__main__":
    today = [2022,7,2]
    count = count(today[0],today[1],today[2])
    print(f'{today[0]}年{today[1]}月{today[2]}日是今年的第{count}天！')
```

测试结果：
```
2022年是平年，2月份有28天！
2022年7月2日是今年的第183天！
[Finished in 0.3s]
```