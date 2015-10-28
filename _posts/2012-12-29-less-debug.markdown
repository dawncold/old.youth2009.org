---
layout: post
title: "LESS debug"
date: 2012-12-29 18:04
comments: true
categories: work@honovation
---

默认less使用production的env，但有时候出现语法错误不能正常编译下去很难调试，所以一般使用development的env开发。

在引用less之前加入：

{% codeblock %}
var less={env: "development"};
{% endcodeblock %}

这样就让less成为development环境了。如果不行的话可以使用Chrome的console，直接给less.env赋值，这只是针对上面方法不能用的时候。赋值好后调用`less.refresh()`，可以让less做一次刷新，如果有错误就会在页面顶部出现。
