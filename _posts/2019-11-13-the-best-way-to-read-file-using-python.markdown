---
layout:     post
title:      "Python读文件的最佳方式"
subtitle:   ""
date:       2019-11-13
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - Python
---

最近的测试过程中，需要读一个大文件，然后再生成一个大文件。一开始我担心一下子把文件全部载入会导致OOM（out of memory）的问题，还特意看了怎么在读文件的时候使用生成器，这样就可以避免OOM的问题。也确实实现了。但后来发现其实python自带的open方法，打开的文件对象本身就是一个迭代器，在使用for循环去读取内容时，是加载一条到内存中处理完后再加载一条到内存中，这样子循环处理，也就不会有OOM的问题了。

而且也没必要使用csv模块来打开文件，直接用open方法打开txt文件就可以了。
```python
f = open('myfile.txt')
for line in f:
    print(line.rstrip())
```

最简单的方法，也是最有效的方法，nice！