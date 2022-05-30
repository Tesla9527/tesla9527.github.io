---
layout:     post
title:      "jenkins中实时输出python脚本的print内容"
subtitle:   ""
date:       2022-05-30
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
    - jenkins
---


参考文章
[https://stackoverflow.com/questions/107705/disable-output-buffering](https://stackoverflow.com/questions/107705/disable-output-buffering)


需求背景

jenkins中python脚本执行时，需要等脚本执行完毕后，内容才会输出。但有时候我们想看实时输出内容。

可以按照上述文章中的回答做如下修改。

```python
import functools
print = functools.partial(print, flush=True)
```

如果print的地方不多的话，也可以直接在使用print方法的时候，加上关键字

```python
print('Hello World!', flush=True)
```