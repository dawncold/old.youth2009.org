---
layout: post
title: python中dict格式化
comments: true
date: 2012-10-04 17:54
categories: python
---
最近在工作中遇到过写SQL的问题，参数是直接传递进去的，比如这样：

{% codeblock %}
db().execute('SELECT * FROM xxx WHERE id = %(id)s', id=get_id())
{% endcodeblock %}

今天细看Google提供的Python课程发现一个叫DictFormatting的部分，里面就有类似这样的语法，现在才明白。以前用过Python的格式化输出，其实这个dict的格式化和字符串的类似，就是在字符串格式化的基础之上加入了dict的key，%s是表示这里有字符串，而%(xxx)s是表示字符串，而且是以xxx为key的字符串，这个value就是从字典中给出。一半会在这样一个字符串后加“% dictname”表示值从dictname这个字典中给出，这不就是和字符串格式化一样么。
