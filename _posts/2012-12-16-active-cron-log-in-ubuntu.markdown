---
layout: post
title: "active cron log in Ubuntu"
date: 2012-12-16 15:41
comments: true
categories: bnly
---

bnly.org使用crontab来不断fetch和send，这看起来很傻，不过挺容易搭建。目前send过程每分钟一次，fetch过程10分钟一次。

在ubuntu下默认没有cron的日志，需要这样开启：

{% codeblock %}
vi /etc/rsyslog.d/50-default.conf
解除cron的注释
service rsyslog restart
service cron restart
{% endcodeblock %}
这样就可以在/var/log/下找到cron.log查看了。
