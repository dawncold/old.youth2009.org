---
layout: post
title: python中的泡菜
comments: true
date: 2011-06-05 18:59
categories: python
---

刚刚得知pickle的意思是泡菜，而这篇文章可不打算讲解泡菜的制作方法，只是说明一下python语言中的pickle模块。 这个模块说是能够存储任何python对象，而且还能取出来再使用，有pickle和cPickle两个模块，功能是一样的，只是后者用C语言实现，据说速度比前者快1000倍。那么我们就用后者吧！！！


{% codeblock %}
#! /usr/bin/python
# -*- coding:utf-8 -*-
# Filename : pickling.py

import cPickle as p

shoplistfile = 'shoplist.dat'

shoplist = ['apple mac book pro','iphone4']

f = file(shoplistfile,'w')
p.dump(shoplist, f)
f.close()

print 'ok,we can read the data from '+shoplistfile+':'

f = file(shoplistfile)
from_file = p.load(f)
print from_file
{% endcodeblock %}

首先定义了一个列表，想要把列表存储到文件中，再打开取出列表。 p作为cPickle的别名了。用dump方法把shoplist存储到f指向的文件中。 后面用load方法从f指向的文件取出数据给了from_file这个变量，而取出的就是我们存起来的那个列表，于是再输出。