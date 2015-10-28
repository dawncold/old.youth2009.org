---
layout: post
title: "ubuntu network configuration"
date: 2012-11-05 20:41
comments: true
categories: work@honovation
---

今天去机房配置了一下测试服务器的network，以便于让所有编辑部的人都能用上新的产品录入功能，据说我们只需要修改gateway到200.200.200.204就可以了，但奇怪的是，今天我登录到了主机上发现gateway就是204了，好奇怪啊。

起初是用GUI来配置的network，但找不到Network Manager的配置文件在哪里，远程的话我们又没有装VNC只有命令行，索性跑去机房搞定。

ubuntu的netwok配置在/etc/network/interfaces中。

{% codeblock lang:bash %}
auto eth0 ##这个应该是决定是否启用这个端口 
iface eth0 inet static ##静态设置IP 
hwaddress ether 52:54:xx:51:xx:xx ##加入MAC地址，记得要放在IP地址之前 
address 202.198.151.17 
netmask 255.255.255.0 
gateway 202.198.151.254
{% endcodeblock %}
这个样基本够我们现在用的了，据说配置好了要用sudo service networking restart，但我每次搞网络都发现重启这个不管用，似乎配置完了就生效了，不要忘记把原先Network Manager中的配置删除掉哦。今天我忘记加第一行auto eth0导致怎么启动都没效果：）
