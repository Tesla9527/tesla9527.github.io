---
layout:     post
title:      "使用requests下载图片"
subtitle:   ""
date:       2020-10-16
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
---

转载至：[原文地址](https://towardsdatascience.com/how-to-download-an-image-using-python-38a75cfa21c)

```python
import requests
import shutil


image_url = "https://cdn.pixabay.com/photo/2020/02/06/09/39/summer-4823612_960_720.jpg"
filename = image_url.split("/")[-1]
r = requests.get(image_url, stream = True)
if r.status_code == 200:
    r.raw.decode_content = True
    with open(filename,'wb') as f:
        shutil.copyfileobj(r.raw, f)
    print('Image sucessfully Downloaded: ',filename)
else:
    print('Image Couldn\'t be retreived')
```