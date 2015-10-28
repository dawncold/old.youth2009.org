---
layout: post
title: python中的*和**
comments: true
date: 2011-07-09 14:44
categories: python
---

在python的函数参数中，可以在变量名称前面加一个或者两个星号代表不一样的变量类型：

在stack overflow上看到有人问这两个的区别了，就转载过来答案吧：

>If the form *identifier is present, it is initialized to a tuple receiving any excess positional parameters, defaulting to the empty tuple. If the form **identifier is present, it is initialized to a new dictionary receiving any excess keyword arguments, defaulting to a new empty dictionary.

加一个星号代表这个参数是一个tuple类型；加两个则是一个dictionary类型，很好用。