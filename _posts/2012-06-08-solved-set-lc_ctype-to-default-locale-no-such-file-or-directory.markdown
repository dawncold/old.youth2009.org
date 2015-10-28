---
layout: post
title: ! '解决Cannot set LC_CTYPE to default locale: No such file or directory问题'
comments: true
date: 2012-06-08 16:20
categories: vps
---

刚拿到vps，打算更新一些软件，发现有些warning挺讨厌的，于是就想根除他们！！他们一般是这样的：


{% codeblock lang:bash %}
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_MESSAGES to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
{% endcodeblock %}

我看到我的LANG被设定为zh_CN.utf8，虽然我们是国人，但这个语言习惯不能代表我们的爱国情怀吧，我就改为en_US.utf8了：


{% codeblock lang:bash %}
sudo touch /etc/default/locale
vi /etc/default/locale
{% endcodeblock %}

加入：


{% codeblock lang:bash %}
LANG="en_US.UTF-8"
LANGUAGE="en_US:en"
{% endcodeblock %}

再执行一下locale就发现问题不见了。

希望vpsee的admin能在iso中修正这个事儿～

