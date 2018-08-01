---
layout:     post
title:      "让python忽略字符串中的转义字符"
subtitle:   ""
date:       2018-08-01
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python    
---

在字符串中使用特殊字符时，python用反斜杠(\)转义字符，但有时我们并不想让转义字符生效，我们只想所见即所得，这种情况下可以用r来定义原始字符串

不使用r时
```python
print('{"CreditScore": "{\"success\":true,\"biz_no\":\"ZM201807313000000874700550325893\",\"zm_score\":\"577\"}"}')
```

输出
```
{"CreditScore": "{"success":true,"biz_no":"ZM201807313000000874700550325893","zm_score":"577"}"}
```

---

使用r时
```python
print(r'{"CreditScore": "{\"success\":true,\"biz_no\":\"ZM201807313000000874700550325893\",\"zm_score\":\"577\"}"}')
```

输出
```
{"CreditScore": "{\"success\":true,\"biz_no\":\"ZM201807313000000874700550325893\",\"zm_score\":\"577\"}"}
```