---
layout:     post
title:      "使用jsonpath_ng库解析json文件"
subtitle:   ""
date:       2021-06-15
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
    - jsonpath_ng
---


```python
from jsonpath_ng import parse

json_data = {
    "lemon": {
        "teachers": [
            {
                "id": "101",
                "name": "华华",
                "addr": "湖南长沙",
                "age": 25
            },
             {
                "id": "102",
                "name": "韬哥",
                "age": 28
            },
            {
                "id": "103",
                "name": "Happy",
                "addr": "广东深圳",
                "age": 16
            },
             {
                "id": "104",
                "name": "歪歪",
                "addr": "广东广州",
                "age": 29,
                "$ddd": 'hehe'
            }
        ],
        "salesmans": [
            {
                "id": "105",
                "name": "毛毛",
                "age": 17
            },
             {
                "id": "106",
                "name": "大树",
                "age": 27,
                "$ddd": 'haha'
            }
        ]
    },
 "avg": 25
}

result1 = [match.value for match in parse('$..name').find(json_data)]
print(result1)

result2 = [match.value for match in parse("$..'$ddd'").find(json_data)]
print(result2)
```

上面的脚本，第1个是找到所有key=name的值，第2个是找到所有key=$ddd的值。因为parse中的开头已经有$符号了,所以如果要找的key中也包含$符号的话，就得把值加上引号。（我是在解析open api 3.0版本时遇到的这种情况）


输出

```
['华华', '韬哥', 'Happy', '歪歪', '毛毛', '大树']
['hehe', 'haha']
```

