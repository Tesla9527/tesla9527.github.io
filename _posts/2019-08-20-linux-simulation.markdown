---
layout:     post
title:      "模拟Linux资源使用情况"
subtitle:   ""
date:       2019-08-20
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - linux
---

模拟CPU使用接近100%，如果是多核CPU，将下面脚本同时运行多个就可以。

```python
def deadloop():
    while True:
        pass
deadloop()
```

调用子进程
```python
import subprocess


def run_cmd(cmd):
    try:
        process = subprocess.Popen(cmd, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
        result_f,error_f = process.stdout,process.stderr
        errors = error_f.read()
        if errors:
            raise Exception(errors)
        else:
            result = result_f.read().decode()
            return result
    except Exception as e:
        print('Exception: ' + str(e))
```
