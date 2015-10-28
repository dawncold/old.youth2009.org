---
layout: post
title: "Object.keys-and-JSON-in-IE6"
date: 2013-12-08 14:52:12 +0800
comments: true
categories: js work@honovation
---

下单页面用到了js中的JSON和Object.keys，都是坑。

JSON虽然是build-in的JSON parser和stringify方法，但IE6，7，8(Q)都是无法使用的，如果用jQuery的话，可以用jQuery的parseJSON来解析，但stringify的话需要依赖第三方库或者自己实现，我用了JSON3.js这个库。首选build-in的parse和stringify方法，如果没有就实现。github地址：[https://github.com/bestiejs/json3](https://github.com/bestiejs/json3)

同样的Object.keys()因为不能在IE9下使用，因为要取一个Object的keys数量，有的时候是用Object的keys列表，所以以后为了兼容，就只能：

{% codeblock lang:js %}
var keys = [];
for(var p in obj) {
	if(obj.hasOwnProperty(p)) {
		keys.push(p);
	}
}
{% endcodeblock %}
