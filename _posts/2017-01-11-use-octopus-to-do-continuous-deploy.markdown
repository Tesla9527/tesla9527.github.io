---
layout:     post
title:      "使用Octopus做持续部署"
subtitle:   ""
date:       2017-01-11
author:     "Tesla9527"
header-img: "img/home-bg-art.jpg"
tags:
    - octopus
---

>在使用TeamCity做完开发过程中的持续集成后，在部署的时候发现很多动作都是重复的，就想是不是也可以自动化掉。后来遇到了Octopus，感觉恰好可以解决这个问题。

2017-01-11，在测试环境安装完Octopus之后，用安装过程中配置的域账号登陆，一直没有Dashboard，提示没有权限，按照教程强行更新设置账号为管理员，还是不行。
后来在我本地安装的时候，使用local账号，结果可以看到Dashboard。至于之前使用域账号为什么不行，已经给官方发了邮件，等待回复中。

2017-01-23，VS中在想要发布的工程下添加OctoPack，执行下面的命令后成功地生成了nuget包，并且用NeGet Package Explorer成功打开。

```
msbuild E:\Yooya\Sl.Bpm\Bpm.Hmgd.Com-branch\Bpm.Hmgd.Com.sln /t:Build /p:RunOctoPack=true
```

一般来说，和采用publish方式生成的文件一样，但是我们这个工程有点特殊，需要将cs文件也当成和html、js一样的文件发布出来。所以在cs文件的属性中，将Build Action
从Compile改为Content就解决了这个问题。

修改前：
![img](/img/in-post/Octopus1.jpg)
修改后：
![img](/img/in-post/Octopus2.jpg)

最后生成的Nuget包就包含了cs文件：
![img](/img/in-post/Octopus3.jpg)

2017-02-03，我们的项目比较特别，需要某些cs文件content include的同时compile include，所以只能放弃Nuget包，改用之前的zip包了。虽然和Nuget包比起来，
稍微损失了一点性能，但还是能将部署的过程自动化掉。

2017-02-05，成功地将TeamCity生成的zip包push到Octopus，并且也可以通过TeamCity中的Octopus Create Release这个step来自动的deploy。但是我觉得既然用了
Octopus，那么部署的事情还是完全交给Octopus来做比较好。TeamCity只要负责把生成好的包push给Octopus就好了。

2017-02-06，终于将自动触发部署也搞定了，接下来把配置的步骤重新整理一下。

1. 在TeamCity中配置好版本号
![img](/img/in-post/Octopus4.jpg)

2. 添加OctopusDeploy: Push packages这个步骤，用来将生成的zip包push到Octopus的服务器中
![img](/img/in-post/Octopus5.jpg)

3. 在Octopus的项目设置中选择Release versioning，如下图。这一步很重要，可以保证生成的Release的版本和push过来的zip包的版本一致。
![img](/img/in-post/Octopus6.jpg)

4. 在Variables中配置需要替换的连接字符串
![img](/img/in-post/Octopus7.jpg)

5. 在Process中添加部署的步骤。这个比较简单，参考官网的说明就可以。

6. 在Triggers中设置Automatic Release Creation，可以保证有新的zip包push过来后，能自动生成Release。
![img](/img/in-post/Octopus8.jpg)

7. 在Library Lifecycles中添加Phases，如下图。这一步很重要，可以保证自动生成Release后能进一步的自动Deploy
![img](/img/in-post/Octopus9.jpg)
