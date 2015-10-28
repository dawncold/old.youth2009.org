---
layout: post
title: 用lambda创建函数
comments: true
date: 2011-06-05 19:51
categories: python
---

又是一个bt功能：创建一种函数规则


{% codeblock %}
#!/usr/bin/python
# Filename: lambda.py

def make_repeater(n):
   return lambda s: s*n

twice = make_repeater(2)

print twice('word')
print twice(5)
{% endcodeblock %}

twice就是创建出来的函数规则，参数2传进入构建了lambda表达式中的n，s值需要再指定，于是后面的word字符串和数字5就算是这个s了吧。了解到这种bt方法很有用，不过对于我这样的初学者来说，暂时还看不到前景：）