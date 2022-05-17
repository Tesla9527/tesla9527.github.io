---
layout:     post
title:      "linux使用python脚本同步日期时间"
subtitle:   ""
date:       2021-08-30
author:     "Tesla9527"
header-img: "img/iu1.jpg"
tags:
    - python
    - ntplib
---

安装ntplib包

```
pip install ntplib
```


新建python脚本并执行

```python
import time
import os

try:
    import ntplib
    client = ntplib.NTPClient()
    response = client.request('pool.ntp.org')
    os.system('date ' + time.strftime('%m%d%H%M%Y.%S',time.localtime(response.tx_time)))
except:
    print('Could not sync with time server.')

print('Done.')
```

