---
layout: post
title: "dive-into-tornado"
date: 2014-03-27 21:22:58 +0800
comments: true
categories: dev
---

早就有这样的计划，要深入了解自己在用的工具，veil算一个，tornado算一个，flask算一个……当然还有好多，总得一个个看一番，好在这些库都写得足够简单，不至于一下子看不懂，而且借助pycharm这样优秀的工具，一步步跟踪代码也给深入理解框架极大的帮助，所以，开始吧。（也好久都没更新过技术博客的内容了）

终于可以再让Mac发挥发挥余热了，pycharm用的社区版，估计对于学习够用了。tornado升级到了稳定的3.2版，也是目前的最新版，先慢慢研读官方的文档，再慢慢看完api。

在写hello，world例子的时候，处理GET我直接就下意识返回了想要的字符串，没想到运行起来是500 error，仔细一看原来官方的例子中处理GET是要调用`self.write('xxx')`，然后我就看了下self.write做了什么，self是我定义的class，但这个class继承自tornado.web.RequestHandler, 于是看tornado.web.RequestHandler的write做什么，write的参数叫chunk，并不是简单的叫str之类的东西，也就是说不限于str，有可能是些别的东西，比如注释中说如果你write了一个dict，tornado会转换成JSON，并且把Content-Type给你设置好，现在的veil也支持了这个优秀特性。还提到了list不会被转换成JSON格式，因为一个漏洞（坑），具体看[这里](http://haacked.com/archive/2008/11/20/anatomy-of-a-subtle-json-vulnerability.aspx/)，简单讲，就是用script的src指向一个网站需要登陆后才能访问的地址，因为你如果登陆过的话，cookie信息会随之发送到这个地址，此时如果你去了一个邪恶的网站，他里面有些脚本，引用刚刚提到的你需要登陆的网址，你浏览器会把你的一些信息带上，请求这个地址，这个地址会返回一些你的个人资料，比如是用JSON的array回给你，但邪恶网站把javascript array的constructor改写了，你拿到JSON的array会被自动转成js array，这样邪恶网站会收集到你的信息，然后再发送回自己一个接受数据的接口就可以了。避免方法就是：返回JSON的时候用对象方式；这种关键信息用POST提交，script标签只会发送GET请求；现代高级浏览器都不会有问题，大可放心。转换成了byte string（就是str）放入chunk_buffer，一起写到output。

我们的handler很简单，实现了get方法，然后write了一个字符串，但后来呢？或许应该从另一条路看起——从url被映射到handler看起。