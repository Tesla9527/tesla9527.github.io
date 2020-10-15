---
layout:     post
title:      "sublime将某个字符替换成换行"
subtitle:   ""
date:       2020-10-16
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - sublime
---

1.Ctrl+H调出替换框
2.在Find中输入要替换的字符
3.在Replace中输入Ctrl+Shift+Enter
4.点击Replace All

比如原文件内容为：
```
aaaaaaaaaaaaaaaa我是要替换的字符bbbbbbbbbbbbbbbbb我是要替换的字符cccccccccccccccccc
```

![img](/img/in-post/sublime-replace-change-line/1.png)

执行替换：

![img](/img/in-post/sublime-replace-change-line/2.png)

替换之后为：
```
aaaaaaaaaaaaaaaa
bbbbbbbbbbbbbbbbb
cccccccccccccccccc
```

![img](/img/in-post/sublime-replace-change-line/3.png)
