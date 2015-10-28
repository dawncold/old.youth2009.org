---
layout: post
title: "basestring-and-str-in-python2x"
date: 2013-08-08 21:39
comments: true
categories: work@honovation python
---

今天在代码中发现原本过滤str的一个func被写成了过滤basestring，于是查了下basestring和str的区别：(在3.0之前)

{% codeblock %}
		   object
             |
             |
         basestring
            / \
           /   \
         str  unicode
{% endcodeblock %}

3.0之前python中有plain string和unicode string，前者是ascii中的那些字符，后者就是所有字符了，因为historical legacy。。。python出现的时候还木有unicode，所以很多python的lib是需要慢慢转换的，当然到了3.0就会不复存在了，全是unicode。

这样的话就清楚了，str代表了那些ascii字符，unicode就是全部的字符，他们都继承自basestring。basestring是从python2.3开始引入的。
