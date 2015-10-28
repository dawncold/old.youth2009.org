---
layout: post
title: 删除MacPorts
comments: true
date: 2012-02-04 21:53
categories: mac
---

{% codeblock lang:bash %}
sudo port -f uninstall installed

sudo rm -rf \
/opt/local \
/Applications/DarwinPorts \
/Applications/MacPorts \
/Library/LaunchDaemons/org.macports.* \
/Library/Receipts/DarwinPorts*.pkg \
/Library/Receipts/MacPorts*.pkg \
/Library/StartupItems/DarwinPortsStartup \
/Library/Tcl/darwinports1.0 \
/Library/Tcl/macports1.0 \
~/.macports
{% endcodeblock %}

第一行是删除了用MacPorts安装的软件，第二行是删除MacPorts各种相关文件。

我删除了MacPorts后就开始用Homebrew了。