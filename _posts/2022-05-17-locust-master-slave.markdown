---
layout:     post
title:      "locust本机分布式运行"
subtitle:   ""
date:       2022-05-17
author:     "Tesla9527"
header-img: "img/todaybing2.jpg"
tags:
    - python
    - locust
---


例子如下

```python
from locust import FastHttpUser, task


class User(FastHttpUser):
    host = "your_host"

    @task
    def index(self):
        with self.client.get("/xxx",catch_response=True) as rp:
            if rp.status_code == 200:
                rp.success()
            else:
                rp.failure(f"出现了错误: {rp.status_code} - {rp.text}")

    def on_start(self):
    # 虚拟用户启动Task时运行
        print('start 虚拟用户启动Task时运行')
 
    def on_stop(self):
    # 虚拟用户结束Task时运行
        print('end 虚拟用户结束Task时运行')
        self.environment.runner.quit()


if __name__ == "__main__":
    import os
    import multiprocessing
    import requests
    from datetime import datetime

    print("开始运行压测!")
    current_file_name = os.path.basename(__file__)
    os.system(f'start locust -f {current_file_name} --master')
    for i in range(multiprocessing.cpu_count()):
        os.system(f'start locust -f {current_file_name} --worker')

    print(f"开始计时 - {datetime.now()}")
    from threading import Timer
    def stop():
        print(f"停止运行压测! - {datetime.now()}")
        rp = requests.get(url="http://localhost:8089/stop")
        print(f"{rp.status_code} - {rp.text}")
    time = "00:20:00"  # in n seconds stop the runner
    run_time = sum(x * int(t) for x, t in zip([3600, 60, 1], time.split(":"))) 
    t = Timer(run_time, stop)
    t.start()

```
