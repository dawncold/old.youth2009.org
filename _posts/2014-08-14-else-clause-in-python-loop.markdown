---
layout: post
title: "else clause in python loop"
date: 2014-08-14 22:07:09 +0800
comments: true
categories: dev
---

both in while and for loop, if in loop body, no break, no return, no exception is raised, statements in else block will be executed.

{% codeblock %}
for x in []:
     print x
else:
     print ‘xxx’
{% endcodeblock %}
this example will print ‘xxx’, even nothing in list and this loop is not executed.