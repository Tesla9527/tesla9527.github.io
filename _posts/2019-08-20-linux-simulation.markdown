---
layout:     post
title:      "模拟Linux资源使用情况"
subtitle:   ""
date:       2019-08-20
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - Linux
---

模拟CPU使用接近100%，如果是多核CPU，将下面脚本同时运行多个就可以。

```python
def deadloop():
    while True:
        pass
deadloop()
```

