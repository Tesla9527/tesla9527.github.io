---
layout:     post
title:      "使用pytest和allure做单元测试"
subtitle:   ""
date:       2018-05-15
author:     "Tesla9527"
header-img: "img/home-bg-o.jpg"
catalog:    true
tags:
    - python
---
最近逛TesterHome论坛，看到有网友在用pytest和allure做测试，然后看了一下allure生成的Report，真是漂亮好看啊，比我之前用的HTMLRunner的报告好看多了，在此mark一下。

pytest：[https://docs.pytest.org/en/latest/contents.html#](https://docs.pytest.org/en/latest/contents.html#)

allure: [http://allure.qatools.ru/](http://allure.qatools.ru/)

---

## 编写测试脚本

脚本目录结构如下：
```
- MyTest
  -test_demo.py
  -test_sample.py
```

test_demo.py文件：

```python
import pytest


class TestDemo(object):

    def test_demo_1(self):
        assert 1 + 1 == 2

    def test_demo_2(self):
        assert 1 + 1 == 3
```

test_sample.py文件：

```python
import pytest


class TestSample(object):

    def test_sample_1(self):
        assert 'hello' in 'hello world'

    def test_sample_2(self):
        assert 'OK' in 'are you ok?'
```

## 安装Allure

```
pip install pytest-allure-adaptor
```

## 执行测试
命令行切换到MyTest目录下，执行命令py.test --alluredir report，是不是很方便，不用另外写一个runner文件来收集测试案例。执行完毕之后会在MyTest目录下新增report目录，并生成测试结果的xml文件，生成的xml文件示例：

```xml
<ns0:test-suite xmlns:ns0="urn:model.allure.qatools.yandex.ru" start="1526451488091" stop="1526451488112">
  <name>test_sample</name>
  <labels/>
  <test-cases>
    <test-case start="1526451488091" status="passed" stop="1526451488103">
      <name>TestSample.test_sample_1</name>
      <attachments/>
      <labels>
        <label name="severity" value="normal"/>
        <label name="thread" value="4228-MainThread"/>
        <label name="host" value="DESKTOP-BJD08GQ"/>
        <label name="framework" value="pytest"/>
        <label name="language" value="cpython3"/>
      </labels>
      <steps/>
    </test-case>
    <test-case start="1526451488104" status="failed" stop="1526451488112">
      <name>TestSample.test_sample_2</name>
      <failure>
        <message>AssertionError: assert 'OK' in 'are you ok?'</message>
        <stack-trace>self = &lt;test_sample.TestSample object at 0x06003D30&gt;

    def test_sample_2(self):
&gt;       assert 'OK' in 'are you ok?'
E       AssertionError: assert 'OK' in 'are you ok?'

test_sample.py:11: AssertionError</stack-trace>
      </failure>
      <attachments/>
      <labels>
        <label name="severity" value="normal"/>
        <label name="thread" value="4228-MainThread"/>
        <label name="host" value="DESKTOP-BJD08GQ"/>
        <label name="framework" value="pytest"/>
        <label name="language" value="cpython3"/>
      </labels>
      <steps/>
    </test-case>
  </test-cases>
</ns0:test-suite>
```

## 查看Allure报告
在本地查看Allure报告时，需要安装一下allure的命令工具，安装步骤如下：

* 安装[scoop](http://scoop.sh/)
* 在命令行中执行scoop install allure来安装allure

假设生成的report的目录为D:\Tesla\MyTest\report，在命令行中执行allure serve D:\Tesla\MyTest\report，漂亮的HTML报告就出来啦。
![img](/img/in-post/pytest-allure/allure_report.png)

## 集成CI
Allure报告可以很好的和CI集成，包括Jenkins，TeamCity等等。详细过程参考官网说明就可以了。[https://docs.qameta.io/allure](https://docs.qameta.io/allure)
