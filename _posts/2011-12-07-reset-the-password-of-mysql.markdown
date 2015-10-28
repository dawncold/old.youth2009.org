---
layout: post
title: 重置MySQL密码
comments: true
date: 2011-12-07 17:46
categories: mysql
---

前几天在Mac系统下装了MySQL，装完后是默认没有给root用户带密码的，于是出于安全考虑我就加上了密码，加密码的方式如下：

{% codeblock lang:bash %}
mysqladmin -u root password "mysqlpassword"
{% endcodeblock %}

很明显引号内的是root用户的新密码。

但在使用的时候我一时想不起来密码了，于是搜索到了官方的Reset the password of MySQL，但看着好麻烦，没有尝试，在[这里](http://huoding.com/2011/06/12/85)找到了方法，贴出来主要代码：

先停止mysql的服务，用下面这句启动mysql：


{% codeblock lang:sql %}
mysqld_safe --skip-grant-tables --skip-networking &

{% endcodeblock %}

用SQL语句修改root的密码：


{% codeblock lang:sql %}
UPDATE mysql.user SET Password=PASSWORD('...') WHERE User='...' AND Host= '...';
FLUSH PRIVILEGES;
{% endcodeblock %}

单引号内的东西自己补充吧，第一个是新密码，第二个写root，第三个用localhost就可以了。