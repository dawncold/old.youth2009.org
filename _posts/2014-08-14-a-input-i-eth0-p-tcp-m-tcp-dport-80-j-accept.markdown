---
layout: post
title: "iptables -A INPUT -i eth0 -p tcp -m tcp --dport 80 -j ACCEPT"
date: 2014-08-14 22:05:46 +0800
comments: true
categories: dev
---

what’s the agreement of -m?

not tcp, it’s “tcp --dport 80”

-m matches, using a somewhat complicated "module matching" mechanism.  There are a bunch of pretty cool modules in iptables, for example "recent".