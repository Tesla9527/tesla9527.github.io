---
layout:     post
title:      "locust实战"
subtitle:   ""
date:       2018-01-25
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - 性能测试
---

安装最新版Locust

    pip install git+git://github.com/locustio/locust.git@master#egg=locustio


```python
from locust import HttpLocust, TaskSet, task
from datetime import datetime
import random
from re import search
import queue
import csv


class UserBehavior(TaskSet):
    @task
    def chushen(self):
        query = """报文内容"""
        apply_no = 'yc' + datetime.now().strftime("%Y%m%d%H%M%S") + str(random.randrange(10000001, 90000009))
        try:
            test_data = self.locust.user_data_queue.get()
        except queue.Empty:
            print("test data run out, test ended.")
            exit(0)
	# 替换报文中需要替换的值	
        query = query.replace('APPLY_NO_Value', apply_no)
        query = query.replace('CLIENT_NAME_Value', test_data['UserName'])
        query = query.replace('MOBILE_Value', test_data['Mobile'])
        query = query.replace('GLOBAL_ID_Value', test_data['GlobalId'])
        with self.client.post("/ESBServer", data=query, catch_response=True) as rp:
            rp.encoding = 'utf-8'
            response_code = search("""<RET_CODE attr="field">(.*)</RET_CODE>""", rp.text).group(1)
            response_msg = search("""<RET_MSG attr="field">(.*)</RET_MSG>""", rp.text).group(1)
            output = "申请单号: " + apply_no + " 响应码: " + response_code + " 响应信息: " + str(response_msg)
            if response_code == '000000':
                rp.success()                
            else:
                rp.failure("初审失败 | " + output)
            print(output)
        self.locust.user_data_queue.put_nowait(test_data)


class WebsiteUser(HttpLocust):
    task_set = UserBehavior
    host = "http://ip:endpoint"
    csv_file = r"dir\testdata.csv"
    user_data_queue = queue.Queue()
    with open(csv_file, encoding='utf-8') as csvfile:
        reader = csv.DictReader(csvfile)
        for row in reader:
            user_data_queue.put_nowait(
                {'GlobalId': row['GlobalId'], 'UserName': row['UserName'], 'Mobile': row['Mobile']})
```