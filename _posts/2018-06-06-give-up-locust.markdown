---
layout:     post
title:      "放弃使用locust进行压测"
subtitle:   ""
date:       2018-06-06
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - locust
---

由于loadrunner比较笨重，所以经过Google后找到了Locust这个模块，脚本写起来也确实很爽的，因为都是用python写的。但是最近发现了一个问题，就是施压能力上不去。虽说官方号称使用协程，并发能力超级高，但是我们还是用实际数据说话，同样的一个接口，我用loadrunner能压出来800的同步并发，但是locust却最多只能到200，怎么提高并发用户数都上不去，而且我也很怀疑它的响应时间统计的对不对。

对于一个压测工具来说，施压能力是其心脏，既然这个能力不行，还是果断放弃吧，不管官方吹嘘的有多么厉害。

可以loadrunner还是很重，对于互联网时代，使用loadrunner有一种回到石器时代的感觉。所以接下来需要花一点时间，看看有什么能够通过纯写脚本来实现的压测工具或方案。