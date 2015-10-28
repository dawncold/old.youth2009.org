---
layout: post
title: "Encoder error -2 when writing image file Error"
date: 2013-02-17 23:25
comments: true
categories: work@honovation
---

今天编辑们在上传一张图的时候出了500错误，他们觉得是图片太大了，传给我看了下果然很大，高度13000+，大约7Mb，本地调试确实是在save的时候出问题，具体错误就是`Encoder error -2 when writing image file Error`，github上的pilkit中有这个issue，是因为默认的maxblock不够大了，其实PIL中还有个SAFEMAXBLOCK，但那也只是1024*1024，对于这张图仍然不够大。具体的方法就是取出图片width和height的最大值，再来个平方。。。

{% codeblock %}
try:
	save porcess
except IOError:
	old_block = PIL.ImageFile.MAXBLOCK
	PIL.ImageFile.MAXBLOCK = max(image.size) ** 2
	try:
		save process
	finally:
		PIL.ImageFile.MAXBLOCK = old_block
{% endcodeblock %}

这样试过后就好了。。。真要命啊这个max block
