---
layout:     post
title:      "python世界中的type，元类，类与对象"
subtitle:   ""
date:       2018-05-09
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    true
tags:
    - Python
---
>python里面的有些概念，我理解的一直迷迷糊糊的。准备在这篇博客里面整理一下。

python里有一句话叫做一切皆对象。
我们看看类的定义：
类(Class): 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。

然后是对象的定义：
对象：通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法。

既然一切皆对象，那么类也是对象;对象是类的实例，也就可以说成是对象是对象的实例，感觉怪怪的...

经过在网上的搜索，找到了一篇文章，写的实在是太精彩了，所以我就转载过来了。

文章出处：[两句话掌握python最难知识点——元类](https://segmentfault.com/a/1190000011447445)

千万不要被所谓“元类是99%的python程序员不会用到的特性”这类的说辞吓住。因为每个中国人，都是天生的元类使用者，
学懂元类，你只需要知道两句话：
道生一，一生二，二生三，三生万物
我是谁？我从哪来里？我要到哪里去？
在python世界，拥有一个永恒的道，那就是“type”，请记在脑海中，type就是道。如此广袤无垠的python生态圈，都是由type产生出来的。
道生一，一生二，二生三，三生万物。
道 即是 type
一 即是 metaclass(元类，或者叫类生成器)
二 即是 class(类，或者叫实例生成器)
三 即是 instance(实例)
万物 即是 实例的各种属性与方法，我们平常使用python时，调用的就是它们。

道和一，是我们今天讨论的命题，而二、三、和万物，则是我们常常使用的类、实例、属性和方法，用hello world来举例：
```python
# 创建一个Hello类，拥有属性say_hello ----二的起源
class Hello():
    def say_hello(self, name='world'):
        print('Hello, %s.' % name)


# 从Hello类创建一个实例hello ----二生三
hello = Hello()

# 使用hello调用方法say_hello ----三生万物
hello.say_hello()
```
输出效果：
```
Hello, world.
```
这就是一个标准的“二生三，三生万物”过程。 从类到我们可以调用的方法，用了这两步。
那我们不由自主要问，类从何而来呢？回到代码的第一行。
class Hello其实是一个函数的“语义化简称”，只为了让代码更浅显易懂，它的另一个写法是：
```python
def fn(self, name='world'): # 假如我们有一个函数叫fn
    print('Hello, %s.' % name)
    
Hello = type('Hello', (object,), dict(say_hello=fn)) # 通过type创建Hello class ---- 神秘的“道”，可以点化一切，这次我们直接从“道”生出了“二”
```
这样的写法，就和之前的Class Hello写法作用完全相同，你可以试试创建实例并调用
```python
# 从Hello类创建一个实例hello ----二生三，完全一样
hello = Hello()

# 使用hello调用方法say_hello ----三生万物，完全一样
hello.say_hello()
```
输出效果：
```
Hello, world. ----调用结果完全一样。
```
我们回头看一眼最精彩的地方，道直接生出了二：