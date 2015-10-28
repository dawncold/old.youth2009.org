---
layout: post
title: "extend in jquery"
date: 2013-02-16 20:02
comments: true
categories: work@honovation jquery
---

jquery中的extend方法可以扩展一个{}，今天用到了。写了一组配置文件：

{% codeblock %}
var options = {
	data:1,
	data2:2
};

console.log($.extend(options, {data3:3}));
console.log(options);
{% endcodeblock %}
这样的结果就是在extend之后optons已经被加入了data3这个key-value，因为默认extend使用的是deep copy，你可以`$.extend(false, options, {data3:3})`，这样就能够得到暂时的并且扩展了的options。
