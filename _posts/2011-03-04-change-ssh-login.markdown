---
layout: post
title: 修改ssh登录方式
comments: true
date: 2011-03-04 22:29
categories: vps
---

{% codeblock %}
PasswordAuthentication yes
ChallengeResponseAuthentication no
GSSAPIAuthentication yes
UsePAM no
{% endcodeblock %}

这样就能有的用rsa登录有的用密码登陆了！