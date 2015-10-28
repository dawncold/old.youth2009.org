---
layout: post
title: centos5上ppp、pptpd配置VPN
comments: true
date: 2011-08-13 17:53
categories: vps
---

安装ppp：


{% codeblock lang:bash %}
yum install ppp
{% endcodeblock %}

下载pptpd：

{% codeblock lang:bash %}
wget -c http://poptop.sourceforge.net/yum/stable/packages/pptpd-1.3.4-1.rhel5.1.x86_64.rpm
{% endcodeblock %}

安装pptpd：


{% codeblock lang:bash %}
rpm -ivh pptpd-1.3.4-1.rhel5.1.x86_64.rpm
{% endcodeblock %}

修改参数：


{% codeblock lang:bash %}
vi /etc/ppp/options.pptpd
{% endcodeblock %}

ms-dns 8.8.8.8和ms-dns 8.8.4.4(这里用了Google的dns，你可以用别的)

加入分配IP等信息：


{% codeblock lang:bash %}
vi /etc/pptpd.conf
{% endcodeblock %}

localip 192.168.0.1

remoteip 192.168.0.2-30(意思是连接上分配一个2～30的地址)

加入账号密码：


{% codeblock lang:bash %}
vi /etc/ppp/chap-secrets
{% endcodeblock %}

用空格分开：USERNAME pptpd PASSWORD *   (最后的这个星号意思是不指定IP，自动分给你一个，pptpd是在配置文件中写的一个服务名称，默认就是这个，不用再修改了，你需要更改的就是大写的两组值)

修改转发参数：


{% codeblock lang:bash %}
vi /etc/sysctl.conf
{% endcodeblock %}

把net.ipv4.ip_forward = 0改正1保存退出


{% codeblock lang:bash %}
/sbin/sysctl -p
使刚才配置的转发参数生效，你能够看到系统打印出的参数列表，应该能够看到ip_forward = 1了
{% endcodeblock %}

启动pptpd：


{% codeblock lang:bash %}
/sbin/services pptpd start

{% endcodeblock %}

配置iptables内容：


{% codeblock lang:bash %}
/sbin/iptables -A INPUT -p tcp --dport 1723 -j ACCEPT
/sbin/iptables -A INPUT -p tcp --dport 47 -j ACCEPT
/sbin/iptables -A INPUT -p gre -j ACCEPT
/sbin/iptables -t nat -A POSTROUTING -s 192.168.0.0/24 -o eth0 -j MASQUERADE
{% endcodeblock %}

解释一下，前两行是开启1723和47端口，第三行是允许GRE协议，最后一行是设置转发到eth0轮询。至于这个轮询的概念我就不太清楚了。转发到eth0也就是说把请求发送到了网卡eth0，这个可以在/sbin/ifconfig看到网卡的名字。

保存iptables规则，重启iptables：


{% codeblock lang:bash %}
/etc/init.d/iptables save
/etc/init.d/iptables restart
如果原有iptables内容可能会和现有的冲突，所以发现问题后先检查一下这里，毕竟iptables是控制连接的所有出口
{% endcodeblock %}

下面这两条根据需要执行吧：


{% codeblock lang:bash %}
/sbin/chkconfig pptpd on
/sbin/chkconfig iptables on
{% endcodeblock %}

分别是让pptpd和iptables机器再次重启后也能运行。

工作都完成了，连接上试试吧，用pptp方式连接哦，别的方式没用过，应该是不行的。有时候连接上不能访问网页建议断开几次再连接上试试，我曾更改了mtu，发现没什么作用，应该不出问题默认的都能用，服务器一般建立的ppp0、1、2……这些的mtu都是1496，本机对应的是1444，具体算法不想深究。