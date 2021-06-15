---
layout:     post
title:      "使用jsonpathng库解析json文件"
subtitle:   ""
date:       2021-06-15
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
tags:
    - python
    - jsonpathng
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
                "age": 29
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
                "age": 27
            }
        ]
    },
 "avg": 25
}

result = [match.value for match in parse('$..name').find(json_data)]
print(result)
```