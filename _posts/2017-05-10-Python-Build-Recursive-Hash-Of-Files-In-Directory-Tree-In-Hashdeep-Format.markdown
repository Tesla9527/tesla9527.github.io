---
layout:     post
title:      "使用Python的hashdeep检测目录中所有文件的hash值"
subtitle:   ""
date:       2017-05-10
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - python
---
使用的是[https://gist.github.com/techtonik/5175896](https://gist.github.com/techtonik/5175896),下面我只是增加了一下对比

```python
import os
import os.path as osp
import hashlib


def filehash(filepath):
    blocksize = 64 * 1024
    sha = hashlib.sha256()
    with open(filepath, 'rb') as fp:
        while True:
            data = fp.read(blocksize)
            if not data:
                break
            sha.update(data)
    return sha.hexdigest()


def get_recursive_hash(dir_root):
    print('size,sha256,filename')
    hash_list = []
    for root, dirs, files in os.walk(dir_root):
        for fpath in [osp.join(root, f) for f in files]:
            size = osp.getsize(fpath)
            sha = filehash(fpath)
            name = osp.relpath(fpath, dir_root)
            hash_list.append({'size': size, 'sha': sha, 'name':name})
	print hash_list
    return hash_list


def compare_recursive_hash(dir1, dir2):
    hash_list1 = get_recursive_hash(dir1)
    hash_list2 = get_recursive_hash(dir2)
    if hash_list1 == hash_list2:
        print('hash same')
        return True
    else:
        print('hash not same')
        return False


compare_recursive_hash('E:\\dir1\\', 'E:\\dir2\\')
```


