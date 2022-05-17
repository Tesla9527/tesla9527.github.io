---
layout:     post
title:      "通过qbittorrent的api来控制种子"
subtitle:   ""
date:       2022-03-26
author:     "Tesla9527"
header-img: "img/taeyeon3"
tags:
    - python
---


背景：我想把斐讯N1小钢炮，每天固定时间重启。但如果重启时，种子是进行中的状态，可能会导致重启后种子出错。但如果是暂停状态重启，就不会出问题。于是找到了qBittorrent的api，通过这种方式，可以在脚本中控制种子状态。


```python
import requests

s = requests.Session()

# 接口文档说明
# https://github.com/qbittorrent/qBittorrent/wiki/WebUI-API-(qBittorrent-4.1)

base_url = 'http://ip:port/api/v2'
# 登录
payload = "username=admin&password=adminadmin"
headers = {'content-type': "application/x-www-form-urlencoded"}
response = s.post(base_url + "/auth/login", data=payload, headers=headers)

# 获取所有种子信息
response = s.get(base_url + '/torrents/info')
print(response.text)

# 暂停所有种子
response = s.get(base_url + '/torrents/pause', params={'hashes': 'all'})
print(response.status_code)

# 恢复所有种子
response = s.get(base_url + '/torrents/resume', params={'hashes': 'all'})
print(response.status_code)
```
