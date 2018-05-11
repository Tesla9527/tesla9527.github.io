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
        print('self对象： %s' %self)
        print('self对象的类型： %s' %type(self))
        print('self对象在内存中的地址： %s' %id(self))
    def say():
    	print('Are you ok?')

robot_timi = Robot()
robot_timi.prt()
print('------------------------')
print('robot_timi实例对象: %s' %robot_timi)
print('robot_timi实例对象的类型: %s' %type(robot_timi))
print('robot_timi实例对象在内存中的地址: %s' %id(robot_timi))
print('------------------------')

robot_wubai = Robot()
robot_wubai.prt()
print('------------------------')
print('robot_wubai实例对象: %s' %robot_wubai)
print('robot_wubai实例对象的类型: %s' %type(robot_wubai))
print('robot_wubai实例对象在内存中的地址: %s' %id(robot_wubai))

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
self对象： <__main__.Robot object at 0x04997450>
self对象的类型： <class '__main__.Robot'>
self对象在内存中的地址： 77165648
------------------------
robot_timi实例对象: <__main__.Robot object at 0x04997450>
robot_timi实例对象的类型: <class '__main__.Robot'>
robot_timi实例对象在内存中的地址: 77165648
------------------------
self对象： <__main__.Robot object at 0x04E542F0>
self对象的类型： <class '__main__.Robot'>
self对象在内存中的地址： 82133744
------------------------
robot_wubai实例对象: <__main__.Robot object at 0x04E542F0>
robot_wubai实例对象的类型: <class '__main__.Robot'>
robot_wubai实例对象在内存中的地址: 82133744
------------------------
<class '__main__.Robot'>
<class 'type'>
82547680
<function Robot.prt at 0x04EC0DF8>
82578936
<function Robot.say at 0x04EC0DB0>
```

通过输出，我们可以看到self的内存地址和实例对象的内存地址是一样的，所以self代表的是实例对象。