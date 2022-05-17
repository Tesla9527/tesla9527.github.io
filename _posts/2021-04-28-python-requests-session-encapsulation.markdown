---
layout:     post
title:      "requests库的session封装"
subtitle:   ""
date:       2021-04-28
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
---


```python
import requests
import json


class HttpClient:
    def __init__(self, api_ip, api_headers):
        self.__session = requests.Session()
        self.__api_ip = api_ip
        self.__headers = api_headers

    def update_headers(self, api_headers):
        self.__headers.update(api_headers)

    def get(self, path, **kwargs):
        return self.__request(path, 'GET', **kwargs)

    def post(self, path, **kwargs):
        return self.__request(path, 'POST', **kwargs)

    def put(self, path, **kwargs):
        return self.__request(path, "PUT", **kwargs)

    def delete(self, path, **kwargs):
        return self.__request(path, "DELETE", **kwargs)

    def patch(self, path, **kwargs):
        return self.__request(path, "PATCH", **kwargs)

    def __request(self, path, method, **kwargs):
        url = self.__api_ip + path
        headers = kwargs.get("headers")
        if headers:
            self.__headers.update(headers)
        kwargs.update({"headers": self.__headers})
        if method == "GET":
            rp = self.__session.get(url, **kwargs)
        elif method == "POST":
            rp = self.__session.post(url, **kwargs)
        elif method == "PUT":
            rp = self.__session.put(url, **kwargs)
        elif method == "DELETE":
            rp = self.__session.delete(url, **kwargs)
        elif method == "PATCH":
            rp = self.__session.patch(url, **kwargs)
        print(f'请求url:{rp.request.url}')
        print(f'请求头:{rp.request.headers}')
        print(f'请求方法:{rp.request.method}')
        body = rp.request.body
        body = body.encode("utf-8").decode("unicode_escape") if body is not None else None
        print(f'请求体:{body}\n')
        print(f'响应码:{rp.status_code}')
        try:
            rp_data = json.loads(rp.text) if rp.text != '' else ''
            print(f'响应体:{rp_data}')
            return(rp.status_code, rp_data)
        except:
            return(rp.status_code, rp.content)

'''需要定义全局变量的放在这里，最好定义一个初始值'''
class global_var():
    base_url = 'http://qq.com'
    headers = {'Content-Type': 'application/json'}
    session = HttpClient(base_url, headers)

# 对于每个全局变量，都需要定义get_value和set_value接口，用来外部调用
def set_session(headers):
    global_var.session.update_headers(headers)
def get_session():
    return global_var.session
```