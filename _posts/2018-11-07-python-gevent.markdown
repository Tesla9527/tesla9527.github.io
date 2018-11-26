---
layout:     post
title:      "使用协程gevent提升爬虫速度"
subtitle:   ""
date:       2018-11-07
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    false
tags:
    - Python
---
不采用gevent时：

```python
from requests_html import HTMLSession
import time


home_url = 'https://www.gucci.cn/zh/'
session = HTMLSession()
# 找到产品分类的所有链接
r = session.get(home_url, verify = False)
all_links = list(r.html.links)
classification = list(filter(lambda x: '/zh/ca' in x, all_links))
print(len(classification))

start = time.time()
# 找到所有产品的链接
product_link = []
for i in classification:
    r = session.get('https://www.gucci.cn' + i, verify = False)
    all_links = list(r.html.links)
    p = list(filter(lambda x: '/zh/pr/' in x, all_links))
    p = list(map(lambda x: x[0: x.index('?')], p))
    print(p)
    product_link += p
product_link = list(set(product_link)) # 去重
print(product_link)    
product_num = len(product_link)
print(f'产品总数量为 {product_num}')
end = time.time()
print(f'耗时{end - start}')
```
耗时35.54867911338806

使用gevent时：
```python
import time
import gevent
from gevent import Greenlet
from gevent import monkey
import gevent.pool
monkey.patch_all() # 在进行IO操作时，默认切换协程
from requests_html import HTMLSession
from queue import Queue

 
home_url = 'https://www.gucci.cn/zh/'
session = HTMLSession()
# 找到产品分类的所有链接
r = session.get(home_url, verify = False)
all_links = list(r.html.links)
classification = list(filter(lambda x: '/zh/ca' in x, all_links))
print(len(classification))

q = Queue()
def get_product_link(i):
    r = session.get('https://www.gucci.cn' + i, verify = False)
    all_links = list(r.html.links)
    p = list(filter(lambda x: '/zh/pr/' in x, all_links))
    p = list(map(lambda x: x[0: x.index('?')], p))
    q.put(p)
    print(p)
start = time.time()
pool = gevent.pool.Pool(10)
threads = [pool.spawn(get_product_link, i) for i in classification]
gevent.joinall(threads)
product_link = list(q.queue)
result = []
for i in product_link:
    result += i
result = list(set(result)) # 去重
print(result)    
product_num = len(result)
print(f'产品总数量为 {product_num}')
end = time.time()
print(f'使用协程耗时{end - start}')
```
使用协程耗时7.928228139877319s
