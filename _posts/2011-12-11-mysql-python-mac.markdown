---
layout: post
title: mac下的MySQL-python问题
comments: true
date: 2011-12-11 14:19
categories: python
---

刚刚在学习web.py这个框架，找了一个不错的例子准备自己运行起来看看，结果一调试出现了MySQLdb没找到的情况，于是从官方（[http://sourceforge.net/projects/mysql-python/](http://sourceforge.net/projects/mysql-python/)）下载源码准备编译安装，最好不要用easy_install安装了，因为还得修改几个地方才能正常编译安装。

由于是mac系统，MySQL是使用的官方提供的dmg安装包装的，但不知为何MySQLdb的安装脚本找不到位置，于是修改MySQLdb的setup_posix.py，26行有个mysql_config.path = ...，修改成你本机中mysql_config所在的地址，比如我的是/usr/local/mysql/bin/mysql_config，保存后分别执行：


{% codeblock lang:bash %}
sudo python setup.py build
sudo python setup.py install
{% endcodeblock %}

安装后最好用python的shell加载一下MySQLdb看看能否正常使用，通常是不行的，因为我就遇到这么个情况，提示缺少image，具体是这样提示的：


{% codeblock lang:bash %}
File "/Library/Python/2.7/site-packages/MySQL_python-1.2.3-py2.7-macosx-10.7-intel.egg/MySQLdb/__init__.py", line 19, in <module>
   import _mysql
ImportError: dlopen(/Library/Python/2.7/site-packages/MySQL_python-1.2.3-py2.7-macosx-10.7-intel.egg/_mysql.so, 2): Library not loaded: libmysqlclient.18.dylib
 Referenced from: /Library/Python/2.7/site-packages/MySQL_python-1.2.3-py2.7-macosx-10.7-intel.egg/_mysql.so
 Reason: image not found
{% endcodeblock %}

于是用Google搜索问题，从[这里](http://alexbraunstein.com/2011/08/12/library-loaded-libmysqlclient-18-dylib/)找到了解决方案：

在~/.bash_profile中加入这样的一句：


{% codeblock lang:bash %}
export DYLD_LIBRARY_PATH=/usr/local/mysql/lib:$DYLD_LIBRARY_PATH
{% endcodeblock %}

然后quit掉terminal再进入一次让这个环境变量更新一下，再次使用MySQLdb就没问题了。