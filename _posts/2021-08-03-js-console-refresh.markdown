---
layout:     post
title:      "浏览器console控制台自动刷新js代码"
subtitle:   ""
date:       2021-08-03
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - js
---

转载至：[https://prodigyu.com/721](https://prodigyu.com/721)

浏览器F12打开控制台，粘贴以下代码回车，提示输出刷新的时间间隔就可以开始自动刷新了。

```js
timeout=prompt("Set timeout (Second):");
count=0
current=location.href;
if(timeout>0)
setTimeout('reload()',1000*timeout);
else
location.replace(current);
function reload(){
setTimeout('reload()',1000*timeout);
count++;
console.log('每（'+timeout+'）秒自动刷新,刷新次数：'+count);
fr4me='<frameset cols=\'*\'>\n<frame src=\''+current+'\'/>';
fr4me+='</frameset>';
with(document){write(fr4me);void(close())};
}
```
