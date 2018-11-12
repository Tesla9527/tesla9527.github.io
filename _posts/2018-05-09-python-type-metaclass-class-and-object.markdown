---
layout:     post
title:      "python世界中的type，元类，类与对象"
subtitle:   ""
date:       2018-05-09
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    true
tags:
    - Python
---
>python里面的有些概念，我理解的一直迷迷糊糊的。准备在这篇博客里面整理一下。

python里有一句话叫做一切皆对象。
我们看看类的定义：
类(Class): 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。

然后是对象的定义：
对象：通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法。

既然一切皆对象，那么类也是对象;对象是类的实例，也就可以说成是对象是对象的实例，感觉怪怪的...

经过在网上的搜索，找到了一篇文章，写的实在是太精彩了，所以我就转载过来了。

文章出处：[两句话掌握python最难知识点——元类](https://segmentfault.com/a/1190000011447445)

---

## 两句话掌握python最难知识点——元类

千万不要被所谓“元类是99%的python程序员不会用到的特性”这类的说辞吓住。**因为每个中国人，都是天生的元类使用者**

学懂元类，你只需要知道两句话：

* 道生一，一生二，二生三，三生万物
* 我是谁？我从哪来里？我要到哪里去？

在python世界，拥有一个永恒的道，那就是“type”，请记在脑海中，type就是道。如此广袤无垠的python生态圈，都是由type产生出来的。
道生一，一生二，二生三，三生万物。

* 道 即是 type
* 一 即是 metaclass(元类，或者叫类生成器)
* 二 即是 class(类，或者叫实例生成器)
* 三 即是 instance(实例)
* 万物 即是 实例的各种属性与方法，我们平常使用python时，调用的就是它们

道和一，是我们今天讨论的命题，而二、三、和万物，则是我们常常使用的类、实例、属性和方法，用hello world来举例：

```python
# 创建一个Hello类，拥有属性say_hello ----二的起源
class Hello():
    def say_hello(self, name='world'):
        print('Hello, %s.' % name)

# 从Hello类创建一个实例hello ----二生三
hello = Hello()

# 使用hello调用方法say_hello ----三生万物
hello.say_hello()
```

输出效果：

```python
Hello, world.
```

**这就是一个标准的“二生三，三生万物”过程**。 从类到我们可以调用的方法，用了这两步。
那我们不由自主要问，类从何而来呢？回到代码的第一行。
class Hello其实是一个函数的“语义化简称”，只为了让代码更浅显易懂，它的另一个写法是：

```python
def fn(self, name='world'): # 假如我们有一个函数叫fn
    print('Hello, %s.' % name)
    
Hello = type('Hello', (object,), dict(say_hello=fn)) # 通过type创建Hello class ---- 神秘的“道”，可以点化一切，这次我们直接从“道”生出了“二”
```

这样的写法，就和之前的Class Hello写法作用完全相同，你可以试试创建实例并调用

```python
# 从Hello类创建一个实例hello ----二生三，完全一样
hello = Hello()

# 使用hello调用方法say_hello ----三生万物，完全一样
hello.say_hello()
```

输出效果：

```
Hello, world. ----调用结果完全一样。
```

我们回头看一眼最精彩的地方，**道直接生出了二**：

```python
Hello = type('Hello', (object,), dict(say_hello=fn))
```

这就是“道”，python世界的起源，你可以为此而惊叹。
注意它的三个参数！暗合人类的三大永恒命题：我是谁，我从哪里来，我要到哪里去。

* 第一个参数：我是谁。 在这里，我需要一个区分于其它一切的命名，以上的实例将我命名为“Hello”
* 第二个参数：我从哪里来。在这里，我需要知道从哪里来，也就是我的“父类”，以上实例中我的父类是“object”——python中一种非常初级的类。
* 第三个参数：我要到哪里去。在这里，我们将需要调用的方法和属性包含到一个字典里，再作为参数传入。以上实例中，我们有一个say_hello方法包装进了字典中。

值得注意的是，三大永恒命题，是一切类，一切实例，甚至一切实例属性与方法都具有的。理所应当，它们的“创造者”，道和一，即type和元类，也具有这三个参数。但平常，类的三大永恒命题并不作为参数传入，而是以如下方式传入

```python
class Hello(object):
# class 后声明“我是谁”
# 小括号内声明“我来自哪里”
# 内声明“我要到哪里去”
    def say_hello():
        pass
```

* 造物主，可以直接创造单个的人，但这是一件苦役。造物主会先创造“人”这一物种，再批量创造具体的个人。并将三大永恒命题，一直传递下去。
* “道”可以直接生出“二”，但它会先生出“一”，再批量地制造“二”。
* type可以直接生成类（class），但也可以先生成元类（metaclass），再使用元类批量定制类（class）。

## 元类——道生一，一生二

一般来说，元类均被命名后缀为Metalass。想象一下，我们需要一个可以自动打招呼的元类，它里面的类方法呢，有时需要say_Hello，有时需要say_Hi，有时又需要say_Sayolala，有时需要say_Nihao。
如果每个内置的say_xxx都需要在类里面声明一次，那将是多么可怕的苦役！ 不如使用**元类**来解决问题。
以下是创建一个专门“打招呼”用的元类代码：

```python
class SayMetaClass(type):
    def __new__(cls, name, bases, attrs):
        attrs['say_'+name] = lambda self,value,saying=name: print(saying+','+value+'!')
        return type.__new__(cls, name, bases, attrs)
```

记住两点：

1. 元类是由type衍生而出,所以父类需要传入type,(**道生一，所以一必须包含道**);
2. 元类的操作都在__new__中完成，它的第一个参数是将创建的类，之后的参数即是三大永恒命题：我是谁，我从哪里来，我将到哪里去。它返回的对象也是三大永恒命题，**接下来，这3个参数将一直陪伴我们。**

在__new__中，我只进行了一个操作，就是

```python
attrs['say_'+name] = lambda self,value,saying=name: print(saying+','+value+'!')
```

它跟据类的名字，创建了一个类方法。比如我们由元类创建的类叫“Hello”，那创建时就自动有了一个叫“say_Hello”的类方法，然后又将类的名字“Hello”作为默认参数saying，传到了方法里面。然后把hello方法调用时的传参作为value传进去，最终打印出来。

那么，一个元类是怎么从创建到调用的呢？
来！一起根据道生一、一生二、二生三、三生万物的准则，走进元类的生命周期吧！

```python
# 道生一：传入type
class SayMetaClass(type):

    # 传入三大永恒命题：类名称、父类、属性
    def __new__(cls, name, bases, attrs):
        # 创造“天赋”
        attrs['say_'+name] = lambda self,value,saying=name: print(saying+','+value+'!')
        # 传承三大永恒命题：类名称、父类、属性
        return type.__new__(cls, name, bases, attrs)

# 一生二：创建类
class Hello(object, metaclass=SayMetaClass):
    pass

# 二生三：创建实列
hello = Hello()

# 三生万物：调用实例方法
hello.say_Hello('world!')
```

输出为

```
Hello, world!
```

**注意：通过元类创建的类，第一个参数是父类，第二个参数是metaclass**

普通人出生都不会说话，但有的人出生就会打招呼说“Hello”，“你好”,“sayolala”，这就是天赋的力量。它会给我们面向对象的编程省下无数的麻烦。

现在，保持元类不变，我们还可以继续创建Sayolala， Nihao类，如下：

```python
# 一生二：创建类
class Sayolala(object, metaclass=SayMetaClass):
    pass

# 二生三：创建实列
s = Sayolala()

# 三生万物：调用实例方法
s.say_Sayolala('japan!')
```

输出

```
Sayolala, japan!
```

也可以说中文

```python
# 一生二：创建类
class Nihao(object, metaclass=SayMetaClass):
    pass

# 二生三：创建实列
n = Nihao()

# 三生万物：调用实例方法
n.say_Nihao('中华!')
```

输出

```
Nihao, 中华!
```

再来一个小例子：
```python
# 道生一
class ListMetaclass(type):
    def __new__(cls, name, bases, attrs):
        # 天赋：通过add方法将值绑定
        attrs['add'] = lambda self, value: self.append(value)
        return type.__new__(cls, name, bases, attrs)
        
# 一生二
class MyList(list, metaclass=ListMetaclass):
    pass
    
# 二生三
L = MyList()

# 三生万物
L.add(1)
```

现在我们打印一下L

```
print(L)

>>> [1]
```

而普通的list没有add()方法

```
L2 = list()
L2.add(1)

>>>AttributeError: 'list' object has no attribute 'add'
```

太棒了！学到这里，你是不是已经体验到了造物主的乐趣？python世界的一切，尽在掌握。

## 年轻的造物主，请随我一起开创新世界。

我们选择两个领域，一个是Django的核心思想，“Object Relational Mapping”，即对象-关系映射，简称ORM。这是Django的一大难点，但学完了元类，一切变得清晰。你对Django的理解将更上一层楼！另一个领域是爬虫领域（黑客领域），一个自动搜索网络上的可用代理，然后换着IP去突破别的人反爬虫限制。
**这两项技能非常有用，也非常好玩！**

## 挑战一：通过元类创建ORM
准备工作，创建一个Field类

```python
class Field(object):

    def __init__(self, name, column_type):
        self.name = name
        self.column_type = column_type

    def __str__(self):
        return '<%s:%s>' % (self.__class__.__name__, self.name)
```

它的作用是

在Field类实例化时将得到两个参数，name和column_type，它们将被绑定为Field的私有属性，如果要将Field转化为字符串时，将返回“Field:XXX” ， XXX是传入的name名称。

准备工作：创建StringField和IntergerField

```python
class StringField(Field):

    def __init__(self, name):
        super(StringField, self).__init__(name, 'varchar(100)')

class IntegerField(Field):

    def __init__(self, name):
        super(IntegerField, self).__init__(name, 'bigint')
```

它的作用是

在StringField,IntegerField实例初始化时，时自动调用父类的初始化方式。

### 道生一

```python
class ModelMetaclass(type):

    def __new__(cls, name, bases, attrs):
        if name=='Model':
            return type.__new__(cls, name, bases, attrs)
        print('Found model: %s' % name)
        mappings = dict()
        for k, v in attrs.items():
            if isinstance(v, Field):
                print('Found mapping: %s ==> %s' % (k, v))
                mappings[k] = v
        for k in mappings.keys():
            attrs.pop(k)
        attrs['__mappings__'] = mappings # 保存属性和列的映射关系
        attrs['__table__'] = name # 假设表名和类名一致
        return type.__new__(cls, name, bases, attrs)
```

它做了以下几件事

* 创建一个新的字典mapping
* 将每一个类的属性，通过.items()遍历其键值对。如果值是Field类，则打印键值，并将这一对键值绑定到mapping字典上。
* 将刚刚传入值为Field类的属性删除。
* 创建一个专门的__mappings__属性，保存字典mapping。
* 创建一个专门的__table__属性，保存传入的类的名称。

### 一生二

```python
class Model(dict, metaclass=ModelMetaclass):

    def __init__(self, **kwarg):
        super(Model, self).__init__(**kwarg)

    def __getattr__(self, key):
        try:
            return self[key]
        except KeyError:
            raise AttributeError("'Model' object has no attribute '%s'" % key)

    def __setattr__(self, key, value):
        self[key] = value

    # 模拟建表操作
    def save(self):
        fields = []
        args = []
        for k, v in self.__mappings__.items():
            fields.append(v.name)
            args.append(getattr(self, k, None))
        sql = 'insert into %s (%s) values (%s)' % (self.__table__, ','.join(fields), ','.join([str(i) for i in args]))
        print('SQL: %s' % sql)
        print('ARGS: %s' % str(args))
```

如果从Model创建一个子类User：

```python
class User(Model):
    # 定义类的属性到列的映射：
    id = IntegerField('id')
    name = StringField('username')
    email = StringField('email')
    password = StringField('password')
```

这时
id= IntegerField('id')就会自动解析为：
Model.__setattr__(self, 'id', IntegerField('id'))
因为IntergerField('id')是Field的子类的实例，自动触发元类的__new__，所以将IntergerField('id')存入__mappings__并删除这个键值对。

### 二生三、三生万物

当你初始化一个实例的时候并调用save()方法时候

```python
u = User(id=12345, name='Batman', email='batman@nasa.org', password='iamback')
u.save()
```

这时先完成了二生三的过程：

1. 先调用Model.__setattr__，将键值载入私有对象
2. 然后调用元类的“天赋”，ModelMetaclass.__new__，将Model中的私有对象，只要是Field的实例，都自动存入u.__mappings__。

**接下来完成了三生万物的过程：**

通过u.save()模拟数据库存入操作。这里我们仅仅做了一下遍历__mappings__操作，虚拟了sql并打印，在现实情况下是通过输入sql语句与数据库来运行。

输出结果为

```python
Found model: User
Found mapping: name ==> <StringField:username>
Found mapping: password ==> <StringField:password>
Found mapping: id ==> <IntegerField:id>
Found mapping: email ==> <StringField:email>
SQL: insert into User (username,password,id,email) values (Batman,iamback,12345,batman@nasa.org)
ARGS: ['Batman', 'iamback', 12345, 'batman@nasa.org']
```

年轻的造物主，你已经和我一起体验了由“道”演化“万物”的伟大历程，这也是Django中的Model版块核心原理。
接下来，请和我一起进行更好玩的爬虫实战（嗯，你现在已经是初级黑客了）：网络代理的爬取吧！

## 挑战二：网络代理的爬取

### 准备工作，先爬个页面玩玩

请确保已安装requests和pyquery这两个包。

```python
# 文件：get_page.py
import requests

base_headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.71 Safari/537.36',
    'Accept-Encoding': 'gzip, deflate, sdch',
    'Accept-Language': 'zh-CN,zh;q=0.8'
}


def get_page(url):
    headers = dict(base_headers)
    print('Getting', url)
    try:
        r = requests.get(url, headers=headers)
        print('Getting result', url, r.status_code)
        if r.status_code == 200:
            return r.text
    except ConnectionError:
        print('Crawling Failed', url)
        return None
```

这里，我们利用request包，把百度的源码爬了出来。

试一试抓百度

把这一段粘在get_page.py后面，试完删除

```python
if(__name__ == '__main__'):
    rs = get_page('https://www.baidu.com')
    print('result:\r\n', rs)
```

试一试抓代理

把这一段粘在get_page.py后面，试完删除

```python
if(__name__ == '__main__'):
    from pyquery import PyQuery as pq
    start_url = 'http://www.proxy360.cn/Region/China'
    print('Crawling', start_url)
    html = get_page(start_url)
    if html:
        doc = pq(html)
        lines = doc('div[name="list_proxy_ip"]').items()
        for line in lines:
            ip = line.find('.tbBottomLine:nth-child(1)').text()
            port = line.find('.tbBottomLine:nth-child(2)').text()
            print(ip+':'+port)
```

接下来进入正题：使用元类批量抓取代理

### 批量处理抓取代理

```python
from getpage import get_page
from pyquery import PyQuery as pq


# 道生一：创建抽取代理的metaclass
class ProxyMetaclass(type):
    """
        元类，在FreeProxyGetter类中加入
        __CrawlFunc__和__CrawlFuncCount__
        两个参数，分别表示爬虫函数，和爬虫函数的数量。
    """
    def __new__(cls, name, bases, attrs):
        count = 0
        attrs['__CrawlFunc__'] = []
        attrs['__CrawlName__'] = []
        for k, v in attrs.items():
            if 'crawl_' in k:
                attrs['__CrawlName__'].append(k)
                attrs['__CrawlFunc__'].append(v)
                count += 1
        for k in attrs['__CrawlName__']:
            attrs.pop(k)
        attrs['__CrawlFuncCount__'] = count
        return type.__new__(cls, name, bases, attrs)


# 一生二：创建代理获取类

class ProxyGetter(object, metaclass=ProxyMetaclass):
    def get_raw_proxies(self, site):
        proxies = []
        print('Site', site)
        for func in self.__CrawlFunc__:
            if func.__name__==site:
                this_page_proxies = func(self)
                for proxy in this_page_proxies:
                    print('Getting', proxy, 'from', site)
                    proxies.append(proxy)
        return proxies


    def crawl_daili66(self, page_count=4):
        start_url = 'http://www.66ip.cn/{}.html'
        urls = [start_url.format(page) for page in range(1, page_count + 1)]
        for url in urls:
            print('Crawling', url)
            html = get_page(url)
            if html:
                doc = pq(html)
                trs = doc('.containerbox table tr:gt(0)').items()
                for tr in trs:
                    ip = tr.find('td:nth-child(1)').text()
                    port = tr.find('td:nth-child(2)').text()
                    yield ':'.join([ip, port])

    def crawl_proxy360(self):
        start_url = 'http://www.proxy360.cn/Region/China'
        print('Crawling', start_url)
        html = get_page(start_url)
        if html:
            doc = pq(html)
            lines = doc('div[name="list_proxy_ip"]').items()
            for line in lines:
                ip = line.find('.tbBottomLine:nth-child(1)').text()
                port = line.find('.tbBottomLine:nth-child(2)').text()
                yield ':'.join([ip, port])

    def crawl_goubanjia(self):
        start_url = 'http://www.goubanjia.com/free/gngn/index.shtml'
        html = get_page(start_url)
        if html:
            doc = pq(html)
            tds = doc('td.ip').items()
            for td in tds:
                td.find('p').remove()
                yield td.text().replace(' ', '')


if __name__ == '__main__':
    # 二生三：实例化ProxyGetter
    crawler = ProxyGetter()
    print(crawler.__CrawlName__)
    # 三生万物
    for site_label in range(crawler.__CrawlFuncCount__):
        site = crawler.__CrawlName__[site_label]
        myProxies = crawler.get_raw_proxies(site)
```

道生一：元类的__new__中，做了四件事：

* 将“crawl_”开头的类方法的名称推入ProxyGetter.__CrawlName__
* 将“crawl_”开头的类方法的本身推入ProxyGetter.__CrawlFunc__
* 计算符合“crawl_”开头的类方法个数
* 删除所有符合“crawl_”开头的类方法

怎么样？是不是和之前创建ORM的__mappings__过程极为相似？

一生二：类里面定义了使用pyquery抓取页面元素的方法

分别从三个免费代理网站抓取了页面上显示的全部代理。

如果对yield用法不熟悉，可以查看：[廖雪峰的python教程：生成器](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014317799226173f45ce40636141b6abc8424e12b5fb27000)

二生三：创建实例对象crawler

略

三生万物：遍历每一个__CrawlFunc__

1. 在ProxyGetter.__CrawlName__上面，获取可以抓取的的网址名。
2. 触发类方法ProxyGetter.get_raw_proxies(site)
3. 遍历ProxyGetter.__CrawlFunc__,如果方法名和网址名称相同的，则执行这一个方法
4. 把每个网址获取到的代理整合成数组输出。

年轻的造物主，创造世界的工具已经在你手上，请你将它的威力发挥到极致！

请记住挥动工具的口诀：

* 道生一，一生二，二生三，三生万物
* 我是谁，我来自哪里，我要到哪里去

---

在stackoverflow上有一个回答，也是相当精彩。

链接：[https://stackoverflow.com/questions/100003/what-are-metaclasses-in-python](https://stackoverflow.com/questions/100003/what-are-metaclasses-in-python)

## 自我理解
看完上面网友的文章之后，我尝试着进行自我理解。拿python的数据类型来分析，

```python
# python标准数据类型
print(type(1))  # int类型
print(type(3.14))  # float类型
print(type(True))  # bool类型
print(type(1j))  # complex类型
print(type('I love you...'))  # str类型
print(type([1, 1, 2, 3, 5]))  # list类型
print(type((1, 2, 3)))  # tuple类型
print(type({1, 2, 3}))  # set类型
print(type({'name': 'Tesla', 'age': 28}))  # dict类型
print('---------------')
# 定义一个类对象
class Robot():
    pass
print('类对象内存地址：' + str(id(Robot)))
print(type(Robot))  # 打印类对象的类型
# 生成一个实例对象
robot_timi = Robot()
print('实例对象内存地址：' + str(id(robot_timi)))
print(type(robot_timi))  # 打印实例对象的类型
# 定义一个元类
class SayMetaClass(type):

    def __new__(cls, name, bases, attrs):
        attrs[
            'say_' + name] = lambda self, value, saying=name: print(saying + ',' + value + '!')
        return type.__new__(cls, name, bases, attrs)
print(id(SayMetaClass)) # 打印自定义元类地址
print(id(int)) # 打印int类地址
print(id(bool)) # 打印bool类地址
print(id(type)) # 打印元类的地址（type is actually its own metaclass.）
```

输出：
```
<class 'int'>
<class 'float'>
<class 'bool'>
<class 'complex'>
<class 'str'>
<class 'list'>
<class 'tuple'>
<class 'set'>
<class 'dict'>
---------------
类对象内存地址：91853792
<class 'type'>
实例对象内存地址：91439856
<class '__main__.Robot'>
91854264
1707859304
1707806184
1707878328
```
以上输出中，我们将类对象和实例对象在内存中的地址都打出来了，这也说明了类和实例都是对象。不仅如此，元类在内存中的地址也打印出来了，而元类都是通过type生成的，type是自身的元类。

我们再来看看wiki上对于计算机科学中对象的定义：

[https://en.wikipedia.org/wiki/Object_(computer_science)](https://en.wikipedia.org/wiki/Object_(computer_science))

In computer science, an object can be a variable, a data structure, a function, or a method, and as such, is a location in memory having a value and referenced by an identifier.

朋友帮忙找到了另外一篇关于python中一切皆对象的文章：

[https://mail.python.org/pipermail/python-list/2015-June/691689.html](https://mail.python.org/pipermail/python-list/2015-June/691689.html)

Everything in Python is an object because Python has no "primitive"
or "unboxed" types, no machine values. This has nothing to do with
metaclasses. Even if Python had no metaclasses, it could still be true
that "everything is an object".

感觉是想说，没有什么原生类型，所有对象都有 方法 与 数据成员 的,即使是 int 这个的类型,而 c++ , java 这样的，int 类型 是没有成员的

我们再来看看另外一个例子：

```python
class AAA():
    aaa = 10

# 情形1
obj1 = AAA()
obj2 = AAA()
print(obj1.aaa, obj2.aaa, AAA.aaa)

# 情形2
obj1.aaa += 2
print(obj1.aaa, obj2.aaa, AAA.aaa)

# 情形3
AAA.aaa += 3
print(obj1.aaa, obj2.aaa, AAA.aaa)

print(id(AAA.aaa))
print(id(obj1.aaa))
print(id(obj2.aaa))
```

输出：

```
10 10 10  
12 10 10  
12 13 13  
1707988208
1707988192
1707988208
```

可以看到，id(AAA.aaa)与id(obj2.aaa)的值是一样的，说明他们指向的都是AAA类对象的属性aaa，而实例对象obj1想要更改类对象AAA的属性aaa的值，所以给ojb1单独绑定了一个他自己的属性aaa，并指向了另一块内存地址。


### 结论

好吧，我认可了，python里面一切皆对象...