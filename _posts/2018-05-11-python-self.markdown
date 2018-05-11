---
layout:     post
title:      "如何理解python中的self"
subtitle:   ""
date:       2018-05-11
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python
---

脚本如下
```python
class Robot():

    def work(self):
        print('self对象： %s' % self)
        print('self对象的类型： %s' % type(self))
        print('self对象在内存中的地址： %s' % id(self))


robot_timi = Robot()
robot_timi.work()
print('------------------------')
print('robot_timi实例对象: %s' % robot_timi)
print('robot_timi实例对象的类型: %s' % type(robot_timi))
print('robot_timi实例对象在内存中的地址: %s' % id(robot_timi))
print('------------------------')

robot_wubai = Robot()
robot_wubai.work()
print('------------------------')
print('robot_wubai实例对象: %s' % robot_wubai)
print('robot_wubai实例对象的类型: %s' % type(robot_wubai))
print('robot_wubai实例对象在内存中的地址: %s' % id(robot_wubai))
```

输出

```
self对象： <__main__.Robot object at 0x05407450>
self对象的类型： <class '__main__.Robot'>
self对象在内存中的地址： 88110160
------------------------
robot_timi实例对象: <__main__.Robot object at 0x05407450>
robot_timi实例对象的类型: <class '__main__.Robot'>
robot_timi实例对象在内存中的地址: 88110160
------------------------
self对象： <__main__.Robot object at 0x058D42F0>
self对象的类型： <class '__main__.Robot'>
self对象在内存中的地址： 93143792
------------------------
robot_wubai实例对象: <__main__.Robot object at 0x058D42F0>
robot_wubai实例对象的类型: <class '__main__.Robot'>
robot_wubai实例对象在内存中的地址: 93143792
```

通过输出，我们可以看到self的内存地址和实例对象的内存地址是一样的，所以self代表的是实例对象。