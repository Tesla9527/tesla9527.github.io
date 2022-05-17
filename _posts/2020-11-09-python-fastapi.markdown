---
layout:     post
title:      "使用fastapi编写后端接口"
subtitle:   ""
date:       2020-11-09
author:     "Tesla9527"
header-img: "img/todaybing1.jpg"
tags:
    - python
    - fastapi
---


测试方式：

1. 新建一个main.py文件，将本文中的脚本内容全部粘贴到main.py文件
2. 起命令行，切换到main.py文件所在目录，执行python main.py
3. 在浏览器中进入http://127.0.0.1:9000/docs
4. 可以在swagger页面进行测试，也可以导入到postman中进行测试，也可用于接口测试学习。

脚本如下：

```python
from typing import Optional
from fastapi import FastAPI
from pydantic import BaseModel


class Book(BaseModel):
    name: str
    author: str
    price: float

fake_db = {
    'book1' : {"name": "射雕英雄传", "author" : "金庸", "price" : 30},
    'book2' : {"name": "寻秦记", "author" : "黄易", "price" : 35},
    'book3' : {"name": "明朝那些事儿", "author" : "当年明月", "price" : 40}
}

app = FastAPI()

@app.get("/", tags=["Root"])
async def root():
    return {"message": "Welcome to the book library！"}

@app.get("/books/", tags=["Book"])
async def get_all_books():
    return fake_db

@app.get("/books/{book_id}", tags=["Book"])
async def get_single_book(book_id : str):
    if book_id in fake_db.keys():
        return fake_db[book_id]
    else:
        return {"message": "book not found !"}

@app.post("/books/", tags=["Book"])
async def create_book(book: Book):
    book_id = int(max(fake_db.keys()).lstrip('book')) + 1
    book_id = 'book' + str(book_id)
    fake_db[book_id] = book
    return fake_db[book_id]

@app.put("/books/{book_id}", tags=["Book"])
async def update_book(book_id: str, book: Book):
    if book_id in fake_db.keys():
        fake_db[book_id] = book
        return fake_db[book_id]
    else:
        return {"message": "book not found !"}

@app.delete("/books/{book_id}", tags=["Book"])
async def delete_book(book_id: str):
    if book_id in fake_db.keys():
        del fake_db[book_id]
        return fake_db
    else:
        return {"message": "book not found !"}

if __name__ == '__main__':
    import uvicorn
    uvicorn.run(app, host='127.0.0.1', port=9000)
```

swagger页面截图：

![img](/img/in-post/python-fastapi/1.png)