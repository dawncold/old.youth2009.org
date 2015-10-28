---
layout: post
title: dropbox自动备份VPS
comments: true
date: 2012-04-27 17:51
categories: python
---

在<a href="http://www.deepvps.com/dropbox-backup.html" target="_blank">这里看过的文章，感觉很不错，于是发表过来，但发现有点问题，我就自己再改改。

安装linux下的dropbox（我的是32为系统，如果是64位在下面地址末尾加上“_64”即可）：


{% codeblock lang:bash %}
wget -O dropbox.tar.gz http://www.dropbox.com/download?plat=lnx.x86
{% endcodeblock %}

解压后在.dropbox-dist目录中有dropboxd可执行文件，让其在后台执行（就是在执行文件后面加“&”符号）


{% codeblock lang:bash %}
~/.dropbox-dist/dropboxd &
{% endcodeblock %}

此后会出现一个地址，你得复制出来然后在浏览器中打开，之后就是注册或者登陆dropbox，这样就激活了在这台机器上的dropbox，就可以同步文件了。

把需要同步备份的文件软连接到Dropbox这个目录中：


{% codeblock lang:bash %}
cd ~/Dropbox
ln -s /home/wwwroot/
。。。
{% endcodeblock %}

此时dropbox已经在帮你同步了，你可以通过web端观察。

我看到的文章中带着一个自动运行的脚本，用sh写的，我发现在主机上运行没反应，不会sh，会点python，于是我改写了一下，也是可用的：


{% codeblock %}
#! /usr/bin/env python
# coding: utf-8

import sys
import os

def start():
print "Starting Dropbox..."
os.system("~/.dropbox-dist/dropboxd &")


def stop():
print "Stoping Dropbox..."
os.system("pkill dropbox")


def restart():
stop()
start()


if __name__ == "__main__":
action = sys.argv[1]
print "now action: %s" % action
if action == 'start':
start()
elif action == "stop":
stop()
elif action == "restart":
restart()
else:
print "Bad arguments!"
{% endcodeblock %}

相应的crontab配置文件中这样写就好了：


{% codeblock lang:bash %}
#auto dropbox
0 4 * * * python /root/dropbox.py restart
0 5 * * * python /root/dropbox.py stop
{% endcodeblock %}

如果没装crontab（极少情况），这样(也许你用apt-get来做这件事，我的是centos系统，用yum了)：


{% codeblock lang:bash %}
yum -y install crontab
{% endcodeblock %}

python让我很快乐：）

一开始在python用的是exec来执行命令发现不可用，于是用了os.system，查看pydoc才发现exec是执行python code用的……惭愧！