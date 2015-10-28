---
layout: post
title: SQLAlchemy中的乱码
comments: true
date: 2012-07-14 09:47
categories: python
---

一开始没怎么关心这个问题，连接数据库的时候我直接这样用的：


{% codeblock %}
mysql://root:@localhost/haolesong
{% endcodeblock %}

在插入数据的时候看到数据库中的内容是乱码，但网页中显示的时候正常，于是我就没怎么关心，不过前天在修改一个值的时候，就是用一段中文替换原先的值，提交数据后网页打不开了，提示unicode编码的xxx问题，相信用Python写网站的人应该会遇得到。

后来在[这里](http://meizhini.iteye.com/blog/294691)发现了解决方法，还有一段长长的分析。我很喜欢这样的文章，对于想直接知道问题答案的人来说一目了然，想知道原理的人也可以直接看下去。

最终就是这样即可：


{% codeblock %}
mysql://root:@localhost/haolesong?charset=utf8
{% endcodeblock %}
