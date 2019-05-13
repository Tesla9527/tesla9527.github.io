---
layout:     post
title:      "驾考交通学习网自动挂视频脚本"
subtitle:   ""
date:       2019-05-14
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - 外挂
---

转载的原文链接：[https://blog.csdn.net/Dante_003/article/details/79353070](https://blog.csdn.net/Dante_003/article/details/79353070)

最近在江苏交通学习网上学习16个学时的教学视频，时间太长了。就在网上找到了这个外挂，可以在一个视频播放完毕后自动点击下一页。

用IE浏览器打开网站登录并进去学习视频的播放页面后，点击F12，输入如下脚本，点击执行。

![img](/img/in-post/jsjtxx/sample.png)

```javascript
var __index = 0;
var __intervalIndex = 0;
var dot = '.';
__intervalIndex = setInterval(function() {

    var __btnNext = getElementsByClassName('dfss_down')[0];


    if (__index > 6) {
        console.clear();
        __index = 0;
        dot = '';
    }

    if (__btnNext != null && __btnNext.childNodes[0] != null) {
        __btnNext.childNodes[0].click();
    } else {
        console.clear();
        console.log('playing' + dot);
    }
    __index = __index + 1;
    dot += '.';
}, 1000);


function getElementsByClassName(className) {
    var all = document.all ? document.all : document.getElementsByTagName('*');
    var elements = new Array();
    for (var e = 0; e < all.length; e++) {
        if (all[e].className == className) {
            elements[elements.length] = all[e];
            break;
        }
    }
    return elements;
}
```