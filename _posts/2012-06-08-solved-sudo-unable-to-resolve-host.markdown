---
layout: post
title: sudo 出现unable to resolve host 解决方法
comments: true
date: 2012-06-08 16:23
categories: vps
---

执行一句sudo xxx会发现：（HOSTNAME就是你的hostname了）


{% codeblock lang:bash %}
sudo ：unable to resolve host HOSTNAME
{% endcodeblock %}

这样修复：(编辑/etc/hosts，修改127.0.0.1那行，把你的hostname加入到那行的最后即可)


{% codeblock lang:bash %}
127.0.0.1               localhost.localdomain localhost HOSTNAME
{% endcodeblock %}

希望vpsee的admin能在iso中修复这个问题

