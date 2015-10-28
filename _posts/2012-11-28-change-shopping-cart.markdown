---
layout: post
title: "change shopping cart"
date: 2012-11-28 23:21
comments: true
categories: work@honovation
---

今天taowen给我们show了一个很fancy的日志处理过程，当然是in the future的，深度打动了wanglei，由于是刚刚吃过饭，站着听久了难免会发困，主要听来的意思就是app的log会自己在local记录，然后发送json给syslog，后面接上logstash做一个处理，再往后就是接入各种图表啊、search啊这样的终端app，如果能完全跑起来应该是足够玄的。不知道成形的互联网电商们会不会也是这样做的。

我主要在修改shopping cart，临下班eric过来和我做了一点东西，后来taowen觉得shopping cart有redis和db两种不同实现很不爽，我倒是没那么强烈，不过如果要改全db对我的工作量会加大。回家后吃了饭感觉身体还好，就修改成全db吧，看看是什么效果。

好在都过了测试，但我删掉了一个功能，所以测试文件也进行了修改，没问题：）

明天应该会把手上的issue全部弄好，哦对了，今天花了挺长时间在Set-Cookie，弄了半天发现就只有几行增加，真是不全局看的话，工作量就会无形的被自己放大。。。
