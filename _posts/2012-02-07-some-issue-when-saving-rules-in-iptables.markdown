---
layout: post
title: 保存iptables规则遇到的问题
comments: true
date: 2012-02-07 18:03
categories: vps
---

开了vps竟然没开vpn简直是罪过了，只是因为前段时间vps升级到了centos6，挺多东西支持不好，于是安装vpn也就失败了，现在已经没问题了，刚刚用iPad测试了vpn可用。

在保存iptables规则的时候遇到这样的问题：

{% codeblock lang:bash %}
iptables: Saving firewall rules to /etc/sysconfig/iptables: /etc/init.d/iptables: line 268: restorecon: command not found
{% endcodeblock %}

当然你可能会看到中文的提示（我的就是），意思是一样的。从[这里](http://www.live-in.org/archives/1112.html)得到了解决方案：

安装一个包包：

{% codeblock lang:bash %}
yum install policycoreutils
{% endcodeblock %}

行了，剩下就没遇到问题了：)