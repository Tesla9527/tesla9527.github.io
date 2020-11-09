---
layout:     post
title:      "使用fastapi编写后端接口"
subtitle:   ""
date:       2020-11-09
author:     "Tesla9527"
header-img: "img/vancleefarpels.jpg"
catalog:    false
tags:
    - python
    - fastapi
---


测试方式：
1.新建一个main.py文件，在命令行中执行python main.py
2.在浏览器中进入http://127.0.0.1:9000/docs
3.可以在swagger页面进行测试，也可以导入到postman中进行测试，也可用于接口测试学习。

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

# home page
@app.get("/", tags=["Root"])
async def root():
    return {"message": "Welcome to the book library！"}

# get all books
@app.get("/books/", tags=["Book"])
async def get_all_books():
    return fake_db

# get a single book
@app.get("/books/{book_id}", tags=["Book"])
async def get_single_book(book_id : str):
    if book_id in fake_db.keys():
        return fake_db[book_id]
    else:
        return {"message": "book not found !"}

# create a single book
@app.post("/books/", tags=["Book"])
async def create_book(book: Book):
    book_id = int(max(fake_db.keys()).lstrip('book')) + 1
    book_id = 'book' + str(book_id)
    fake_db[book_id] = book
    return fake_db[book_id]

# update a single book
@app.put("/books/{book_id}", tags=["Book"])
async def update_book(book_id: str, book: Book):
    fake_db[book_id] = book
    return fake_db[book_id]

# delete a single book
@app.delete("/books/{book_id}", tags=["Book"])
async def delete_book(book_id: str):
    del fake_db[book_id]
    return fake_db

if __name__ == '__main__':
    import uvicorn
    uvicorn.run(app, host='127.0.0.1', port=9000)

```

swagger页面截图：

![img](/img/in-post/python-fastapi/1.png)