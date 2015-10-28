---
layout: post
title: python中的sort方法
comments: true
date: 2012-10-04 14:58
categories: python
---
打算从今天开始自习再学学Python的基础，选了Google提供的Python课程，学到list部分，有个练习题目要求针对一组tuples排序，根据tuples的最后一个元素排序，有个hint，可以用key=function这种方法，于是搜索了一番，在Python的wiki中找到这个key方法的描述：

从Python2.4以后list.sort()和sorted()方法都提供了一个key可选参数，传入一个function用来决定排序需要的key。这个key就是所排序元素的权值，最终就是根据权值来排序了。你也可以自己写一个方法，就是那种用def来定义的方法，不过要求接受一个参数，返回一个值，接受的参数就是这个集合（list、dict、tuple）中的某个元素。我是这样写的，it works：

{% codeblock %}
def sort_last(tuples):
 # +++your code here+++
 tuples.sort(key = lambda t: t[-1])
 return tuples
{% endcodeblock %}

根据tuple中最后一个排序。
