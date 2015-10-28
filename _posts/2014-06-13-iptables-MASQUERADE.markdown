---
layout: post
title: "iptables MASQUERADE"
date: 2014-06-13 20:50:30 +0800
comments: true
categories: dev
---

If you need private hosts communicate with external network, maybe some LXC contaners want to using apt-get, you need add a iptables rule like this:

{% codeblock %}
iptables -t nat -A POSTROUTING -s 10.24.1.0/24 ! -d 10.24.1.0/24 -j MASQUERADE
{% endcodeblock %}

This rule allows network traffic from 10.24.1.x, and destination is not 10.24.1.x, maybe it wants to communicating with 10.24.2.x, but that doesn't cover in this post, we assumed it want to communicating with Google, the host has an external ip like 200.200.200.200, iptables can convert IP from 10.24.1.x to IP from 200.200.200.200, like the host request Google.