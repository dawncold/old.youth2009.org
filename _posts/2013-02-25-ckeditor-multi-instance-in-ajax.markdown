---
layout: post
title: "ckeditor multi instance in ajax"
date: 2013-02-25 19:54
comments: true
categories: work@honovation js
---

初始化ckeditor后再用ajax刷掉页面，如果此时再次初始化它就会报错，说你要初始化的那个已经存在了。。。

此时需要检测一下是否已经存在，如果存在就remove掉：

{% codeblock lang:javascript %}
if(CKEDITOR.instances['description']) {
	CKEDITOR.remove(CKEDITOR.instances['description']);
}
CKEDITOR.replace('description')

其中description是一个textarea的name。
{% endcodeblock %}
