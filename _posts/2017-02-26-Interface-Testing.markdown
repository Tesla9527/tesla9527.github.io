---
layout:     post
title:      "http接口测试"
subtitle:   ""
date:       2017-02-26
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
catalog:    false
tags:
    - 接口测试
---
>接口测试的目的：项目开发中，接口一般比较早的做好，QA能在UI出现之前对接口进行测试，是对质量比较好的控制。

什么是接口测试？（以下引用云层老师的讲解）

	1.接口是指系统模块与模块或系统与系统间进行交互，一般我们用的多是Http协议的接口，WebService协议的接口，
	还有RPC（Remote Procedure Call Protocal远程过程调用协议的接口）。

	2.不管是哪种接口，其本质就是发送一个request，然后服务器响应后返回一个response，
	然后我们对response进行分析，这就是接口测试。

这段时间在新公司里，参考老大的框架，使用Python把接口测试做完了。其中urllib模块被我换成了requests模块，使用起来会更加方便一点。在文件夹中的__init__.py文件中也去掉了路径的设置，留了
一个空文件，但是却能确保该文件夹下的模块能方便的被其他地方引用。

代码链接：
[https://github.com/Tesla9527/InterfaceTesting](https://github.com/Tesla9527/InterfaceTesting)


集成Jenkins：

接口测试一定要集成CI才能更好的发挥效果，集成起来比较简单，直接通过命令行调用就可以了。

	python your_dir\test_runner.py
	
为了方便在Jenkins中执行时，可以选择一些参数来指定在什么环境下执行哪些test cases，我在test_runner中使用了argparse模块。在上面的代码例子中，我使用了3个参数，
一个是env，用来指定测试环境，一个是port，用来指定测试的端口，一个是suite，用来指定测试套件。在命令行中不加入参数执行上面的命令时，会使用配置的默认参数值来运行，当想传入某些参数执行测试时，
比如传入suite的值，

	python your_dir\test_runner.py -s smoke
	
就会执行smoke test cases。当然这个-s后面具体是传入smoke还是full还是其他值，完全就可以通过Jenkins的参数来传入了。

Jenkins中发布测试报告：

我们在接口测试中使用的是xmlrunner，会生成xml的report。在Jenkins中Post-build Actions，选用Publish JUnit test result report。 Test Report XMLs配置为reports/report*.xml

PS：另外我觉得postman作为测试工具，用在开发对自己所写接口的测试上，还是挺方便的。但是用在专门的接口测试，还是没有直接用代码写来得灵活。

所以接口测试的编写其实是很容易的事情，怎么样能让接口测试从接口的完成，追踪，测试更加的可维护化才能确保做出来的接口测试是有效果的。我觉得用Google Doc来追踪比较好，从接口，到用例，到用例代码化，到状态的标注就可以一目了然了。要不然看到那一片的接口测试代码，我们是不清楚到底测试覆盖的怎么样的。
