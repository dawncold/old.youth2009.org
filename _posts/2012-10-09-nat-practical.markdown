---
layout: post
title: NAT实践
comments: true
date: 2012-10-09 14:09
categories: lxc
---
昨天用LXC建立了不少container，分别用来做webserver、databaseserver等等，让这些container运行着各自程序启动后如果有外部访问，就会通过iptables把请求发送到各自的地方，这里需要宿主机器做NAT。比如访问80端口，我会把请求转发到内部10.0.3.20这台container来处理，相应的response也会返回过去。这样就做到了服务隔离。

{% codeblock lang:bash %}
sudo iptables -t nat -A PREROUTING -i eth1 -p tcp --dport 80 -j DNAT --to 10.0.3.20
sudo iptables -t nat -A POSTROUTING -o eth1 -s 10.0.3.20 -j SNAT --to 200.200.200.25
{% endcodeblock %}

这样就把进入的请求都发到了10.0.3.20这台container上去处理。

![nat](http://pic.yupoo.com/dawncold0/CkkIbzDr/medish.jpg)

只默认开了一个nginx，就这样的效果。
