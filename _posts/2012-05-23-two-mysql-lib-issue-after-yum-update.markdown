---
layout: post
title: ! 'ldconfig: /usr/lib/libmysqlclient.so.16 is not a symbolic link的问题'
comments: true
date: 2012-05-23 19:50
categories: mysql
---

刚刚用yum升级了系统，发现日志中有很多这样的提示：

{% codeblock lang:bash %}
ldconfig: /usr/lib/libmysqlclient.so.16 is not a symbolic link
ldconfig: /usr/lib/libmysqlclient_r.so.16 is not a symbolic link
{% endcodeblock %}

于是Google了一下，找到一个解决方法，在[这里](http://tiger.im/286.html).

就是重建了两条连接过去即可：


{% codeblock lang:bash %}
ln -sf /usr/local/mysql/lib/mysql/libmysqlclient.so.16 /usr/lib/mysqlclient.so.16
ln -sf /usr/local/mysql/lib/mysql/libmysqlclient_r.so.16 /usr/lib/libmysqlclient_r.so.16
{% endcodeblock %}
