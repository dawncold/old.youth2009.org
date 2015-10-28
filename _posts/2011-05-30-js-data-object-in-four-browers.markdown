---
layout: post
title: 四种浏览器下的JS日期对象
comments: true
date: 2011-05-30 22:20
categories: js
---

测试浏览器为：IE8、Chrome、Firefox、Safari，除了IE，都是最新版本，不多说了，都兼容的创建Data的方式是这样的：


{% codeblock %}
var da = '2000-01-01 00:00:00';
var da_array = da.split(' ');
var da_1 = da_array[0].split('-');
var da_2 = da_array[1].split(':');
alert(new Date(da_1[0],da_1[1],da_1[2],da_2[0],da_2[1],da_2[2]));
{% endcodeblock %}
