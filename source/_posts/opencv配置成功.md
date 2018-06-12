---
title: opencv配置成功
tags: opencv
date: 2018-02-26 21:11:00
---

----------

opencv3.31+vs2015配置成功
----------

> ![这里写图片描述](http://img.blog.csdn.net/20180226010411877?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3dpdGNoX2xvdmVfY2FzZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

----------


> 话说，这是我半年前就想做的东西，经历过太多次失败，可能是自己脑子愚钝，哎，感慨涕零。
> 科普一下：vs2015就不用介绍了吧。
> opencv是何物呢？
> ![这里写图片描述](https://gss3.bdstatic.com/-Po3dSag_xI4khGkpoWK1HF6hhy/baike/w=268;g=0/sign=8adb9aa2b219ebc4c078719fba1da8c1/37d12f2eb9389b50bc2845958435e5dde6116e26.jpg)
>       ***OpenCV***  是一个基于BSD许可（开源）发行的跨平台计算机视觉库，可以运行在Linux、Windows、Android和Mac OS操作系统上。它轻量级而且高效——由一系列 C 函数和少量 C++ 类构成，同时提供了Python、Ruby、MATLAB等语言的接口，实现了图像处理和计算机视觉方面的很多通用算法。
OpenCV用C++语言编写，它的主要接口也是C++语言，但是依然保留了大量的C语言接口。该库也有大量的Python、Java and MATLAB/OCTAVE（版本2.5）的接口。这些语言的API接口函数可以通过在线文档获得。如今也提供对于C#、Ch、Ruby的支持。

----------


> 工作领域：
1、人机互动
2、物体识别
3、图像分割
4、人脸识别
5、动作识别
6、运动跟踪
7、机器人
8、运动分析
9、机器视觉
10、结构分析
11、汽车安全驾驶

----------

> 好的，记录一下自己遇到的坑。风萧萧兮易水寒，想想都后怕。。。。。。

<!--more-->


# 软件版本问题

> 大概在半年之前我看的这位大神的教程进行配置opencv和cv2010，
> [http://blog.csdn.net/poem_qianmo/article/details/19809337](http://blog.csdn.net/poem_qianmo/article/details/19809337)
> 哎，无奈，总结如下，opencv到今天2018年2月已经更新到3.31版本，更新了什么功能不再考究，暂且讨论最基本的安装问题。
> opencv不再支持x86格式，在其安装包里也找不到相关文件，而且其对应文件为vc14，这句话就是说，适用于vs2015.以我的概念就是说--现在的opencv最好安装在vs2015上面（或者更高版本），其他版本我没有测试。
> 之前我在笔记本上装了vs2010，哎磕磕绊绊到放弃也没能装上这神奇的软件。最后就搁置了。
> 现在老师又给了我一台笔记本，又鼓起勇气再尝试一把，熬了几个夜晚（网速太慢），下载vs2015用了一夜，安装2015用了一下午，调试用了好几个小时。
> 最尴尬的问题就是我先测试的还是vs2010，现在想来，真是笨，结果还是失败了，然后卸载2010用了好久，而且卸载不完全，导致2015安装的时候出现bug两者发生了冲突。



----------
## 环境配置问题 ##

> 这套环境我配置了不少于5便，现在背都能背下来。。。
> 目前我成功的配置教程如下--[https://www.cnblogs.com/linshuhe/p/5764394.html](https://www.cnblogs.com/linshuhe/p/5764394.html)配置环境一定要认真！
> 包括：opencv环境变量配置，vs2010支持文件的配置，w32窗体运行程序的属性管理器的配置，链接器的配置等等。
> 此教程是正确的，起码我成功了。

----------
## 调试出错问题 ##

> 我调试的时候并没有出现太多错误，唯一就是，无法打开.exe文件，（这个是怎么解决的我也迷糊了，忘记了），另一个就是报错说

```
0x00007FFEE17E3FB8 处(位于 opencv.exe 中)有未经处理的异常: Microsoft C++ 异常: cv::Exception，位于内存位置 0x000000856230F880 处。

```

> 这个问题是很好解决的，那就是图片位置放错了，有的教程说放在工程目录下，其实不然！
> 需要放在和.cpp同一级的文件夹里才行。
> 

----------


> *真正成功运行opencv的截图！！！*
> ![这里写图片描述](http://img.blog.csdn.net/20180226014025618?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3dpdGNoX2xvdmVfY2FzZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

----------

```
今天睡早一点，好几天都是4点才睡，快不行了，身体是革命的本钱！
可是我好慌，懂得东西太少，基础不牢，不专一，哎。
------2018年2月26日.随笔。
下一篇博客更新python学习进度！
```