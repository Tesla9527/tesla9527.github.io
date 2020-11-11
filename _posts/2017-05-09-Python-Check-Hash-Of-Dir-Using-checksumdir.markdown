---
layout:     post
title:      "使用Python的checksumdir检测目录的hash值"
subtitle:   ""
date:       2017-05-09
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
catalog:    false
tags:
    - python
---
Google一下checksumdir进入官网查看说明。

```python
from checksumdir import dirhash


def check_dir_hash(directory):
    md5hash = dirhash(directory, 'md5')
    sha1hash = dirhash(directory, 'sha1')
    print('directory: %s' % directory)
    print("md5 value : %s" % md5hash)
    print("sha1 value : %s" % sha1hash)
    return {'md5hash': md5hash, 'sha1hash': sha1hash}


def compare_two_dir_hash(directory1, directory2):
    return_data_one = check_dir_hash(directory1)
    md5hash_one = return_data_one['md5hash']
    sha1hash_one = return_data_one['sha1hash']
    return_data_two = check_dir_hash(directory2)
    md5hash_two = return_data_two['md5hash']
    sha1hash_two = return_data_two['sha1hash']
    if md5hash_one == md5hash_two:
        print('md5 same')
    else:
        print('md5 not same')
    if sha1hash_one == sha1hash_two:
        print('sha1hash same')
    else:
        print('sha1hash not same')


compare_two_dir_hash('directory1', 'directory2')
```


