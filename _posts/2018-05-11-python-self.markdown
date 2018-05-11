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

    def prt(self):
        print('self对象：')
        print(self)
        print('self对象的类型：')
        print(type(self))
        print('self对象在内存中的地址：')
        print(id(self))
    def say():
    	print('Are you ok?')

robot_timi = Robot()
robot_timi.prt()
print('------------------------')
print('robot_timi实例对象:')
print(robot_timi)
print('robot_timi实例对象的类型:')
print(type(robot_timi))
print('robot_timi实例对象在内存中的地址:')
print(id(robot_timi))
print('------------------------')

robot_wubai = Robot()
robot_wubai.prt()
print('------------------------')
print('robot_wubai实例对象:')
print(robot_wubai)
print('robot_wubai实例对象的类型:')
print(type(robot_wubai))
print('robot_wubai实例对象在内存中的地址:')
print(id(robot_wubai))

print('------------------------')
print(Robot)
print(type(Robot))
print(id(Robot))
print(Robot.prt)
print(id(Robot.prt))
print(Robot.say)
```

输出

```
self对象：
<__main__.Robot object at 0x04D77450>
self对象的类型：
<class '__main__.Robot'>
self对象在内存中的地址：
81228880
------------------------
robot_timi实例对象:
<__main__.Robot object at 0x04D77450>
robot_timi实例对象的类型:
<class '__main__.Robot'>
robot_timi实例对象在内存中的地址:
81228880
------------------------
self对象：
<__main__.Robot object at 0x052042F0>
self对象的类型：
<class '__main__.Robot'>
self对象在内存中的地址：
86000368
------------------------
robot_wubai实例对象:
<__main__.Robot object at 0x052042F0>
robot_wubai实例对象的类型:
<class '__main__.Robot'>
robot_wubai实例对象在内存中的地址:
86000368
------------------------
<class '__main__.Robot'>
<class 'type'>
86414304
<function Robot.prt at 0x05270DB0>
86445488
<function Robot.say at 0x05270D68>
```