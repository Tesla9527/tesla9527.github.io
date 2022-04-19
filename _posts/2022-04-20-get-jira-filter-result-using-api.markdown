---
layout:     post
title:      "使用jira的api获取jql结果"
subtitle:   ""
date:       2022-04-20
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - jira
    - python
---


需求背景： 所在公司，员工的任务和工时都登记在jira上，每个季度需要拉取数据。

[接口说明](https://developer.atlassian.com/cloud/jira/platform/rest/v2/api-group-issue-search/#api-rest-api-2-search-post)

实现如下：

```python
import requests
from requests.auth import HTTPBasicAuth
import json
import copy
import pandas as pd

url = "https://your-domain/rest/api/2/search"

auth = HTTPBasicAuth("your-account", "your-password")

headers = {"Accept": "application/json", "Content-Type": "application/json"}

users = ['zhangsan', 'lisi']

payload = {
  "expand": ["names", "schema", "operations"],
  "jql": "created >= 2022-01-01 AND created <= 2022-03-31 AND assignee in (user) ORDER BY created DESC",
  "maxResults": 1000,
  # "fieldsByKeys": False,
  "fields": [
    "issuetype",
    "summary",
    "key",
    "assignee",
    "timespent"
  ],
  "startAt": 0
}

print('开始获取数据...')

issues_total = []
for i in users:
   tmp = copy.deepcopy(payload)
   tmp['jql'] = tmp['jql'].replace('user', i)
   response = requests.post(url, data=json.dumps(tmp), headers=headers, auth=auth)
   # print(response.text)
   
   issues = list(map(lambda x: {'issuetype': x['fields']['issuetype']['name'],
   'summary': x['fields']['summary'],
   'key': x['key'],
   'assignee': x['fields']['assignee']['displayName'],
   'timespent': round(x['fields']['timespent'] / 3600, 2) if x['fields']['timespent'] is not None else 0}, 
   json.loads(response.text)['issues']))
   print(issues)
   issues_total += issues
print(len(issues_total))


final_df = pd.DataFrame(issues_total, columns=['issuetype','summary','key', 'assignee', 'timespent'])
final_df.to_excel("统计.xlsx")
```