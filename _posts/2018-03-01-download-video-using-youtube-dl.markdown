---
layout:     post
title:      "使用youtube-dl模块下载网络视频"
subtitle:   ""
date:       2018-03-01
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
catalog:    false
tags:
    - Python
---
youtube-dl地址：[https://github.com/rg3/youtube-dl](https://github.com/rg3/youtube-dl)

以前使用过you-get模块来下载视频，但是经常会出现一些问题，特别是下载国内的视频。后来使用youtube-dl模块来下载，发现好用不少，而且还可以下载1080P的视频，很赞。

## 下载youtube视频示例

比如说我们要下载卓依婷的这个视频，且是1080P的
![img](/img/in-post/youtube/3.jpg)

1. 获取视频信息

	youtube-dl -F "https://www.youtube.com/watch?v=8h30JgKkZQI"

![img](/img/in-post/youtube/1.jpg)

2. 执行下载（如果要下载1080P的，需要安装ffmpeg）

	youtube-dl -f 137+140 "https://www.youtube.com/watch?v=8h30JgKkZQI"

![img](/img/in-post/youtube/2.jpg)

---

