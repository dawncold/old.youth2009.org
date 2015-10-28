---
layout: post
title: svn的javahl库
comments: true
date: 2012-06-11 10:17
categories: java
---

今天基本完成了LoveSMS，想checkout一下jdrcom来看看，所以就安装上了svn for eclipse，然后在导入的时候提示缺少javahl库，去了官方查看了一下，说是对于Mac用户，只需要下载他们的bin文件就能解决，我一看才给到1.6.5的版本，而我自己用brew都装到了1.7.5，而且svn插件用的是1.8.x，需要1.7+的svn支持才行，所以就自己重新安装了svn：


{% codeblock lang:bash %}
brew install subversion --universal --java
{% endcodeblock %}

这句是关键哦，当然你得先uninstall已经安装的svn才行。加了java开关就可以告诉svn需要java IDE的库，编译的完成后会继续编译javahl～

会有这样的提示哦：


{% codeblock lang:bash %}
To use Java bindings with various Java IDEs, you might need a universal build:
 brew install subversion --universal --java
==> ./configure --disable-debug --prefix=/usr/local/Cellar/subversion/1.7.5 --with-ssl --with-zlib=/usr --with-sqlite=/usr/local --disable-neon-version-chec
==> make
==> make install
==> make javahl
==> make install-javahl
==> Caveats
You may need to link the Java bindings into the Java Extensions folder:
 sudo mkdir -p /Library/Java/Extensions
 sudo ln -s /usr/local/lib/libsvnjavahl-1.dylib /Library/Java/Extensions/libsvnjavahl-1.dylib
{% endcodeblock %}

自己加入后面的链接就ok了！

