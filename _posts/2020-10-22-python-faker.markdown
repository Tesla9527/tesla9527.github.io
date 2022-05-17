---
layout:     post
title:      "使用python的faker库造假数据"
subtitle:   ""
date:       2020-10-22
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
---

测试脚本

```python
from faker import Faker
fake = Faker('zh_CN')
for _ in range(3):
    print(fake.name(),fake.ssn(),fake.company(),fake.job(),fake.phone_number())
```

测试结果

```
张超 360424197003262601 良诺网络有限公司 网站编辑 15510231406
白旭 140601195710064707 浙大万朋科技有限公司 金融产品销售 14749658388
黄海燕 211302193611108655 佳禾网络有限公司 房地产中介/置业顾问 13711126308
```
