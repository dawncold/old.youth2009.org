---
layout: post
title: LXC实践
comments: true
date: 2012-10-08 20:46
categories: lxc
---
这里的LXC是基于Ubuntu12.04的，在其他系统下可能不太一样。

0.安装lxc

{% codeblock lang:bash %}
sudo apt-get install lxc
{% endcodeblock %}

1.修改lxc的mirror，不修改的话下载一个ubuntu景象会非常慢！！！

{% codeblock lang:bash %}
sudo emacs /etc/default/lxc
第三行的mirror注释去掉，并修改为cn.archive.ubuntu.com，这样就非常快了
{% endcodeblock %}

2.创建lxc容器，t表示模板中的名字，n表示这个容器的名字（可自定义）

{% codeblock lang:bash %}
sudo lxc-create -t ubuntu -n ubuntu_container
{% endcodeblock %}

3.启动容器

{% codeblock lang:bash %}
sudo lxc-start -n ubuntu_container
{% endcodeblock %}

启动后就会出现登录ubuntu的界面，刚刚创建好容器后会给出一个提示，帐号密码都是ubuntu，登录进去就可以使用了。

猜想lxc的用法可能是对于部署的某个进程使用lxc隔离，这并不能做vps用，lxc只是轻量虚拟化，针对进程来的，所以还是单机在使用，如果做vps就得用vmware、xen、openvz这样的东西了。
