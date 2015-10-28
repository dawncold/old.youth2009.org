---
layout: post
title: 安装mysql的Ruby驱动遇到的问题
comments: true
date: 2012-02-09 20:08
categories: study ruby
---

{% codeblock lang:bash %}
dawncold@tianzhenmatoMacBook-Pro ~$ gem install mysql
Fetching: mysql-2.8.1.gem (100%)
Building native extensions.  This could take a while...
ERROR:  Error installing mysql:
ERROR: Failed to build gem native extension.

       /usr/local/Cellar/ruby/1.9.3-p0/bin/ruby extconf.rb
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lm... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lz... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lsocket... no
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lnsl... no
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lmygcc... no
checking for mysql_query() in -lmysqlclient... no
*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of
necessary libraries and/or headers.  Check the mkmf.log file for more
details.  You may need configuration options.

Provided configuration options:
--with-opt-dir
--without-opt-dir
--with-opt-include
--without-opt-include=${opt-dir}/include
--with-opt-lib
--without-opt-lib=${opt-dir}/lib
--with-make-prog
--without-make-prog
--srcdir=.
--curdir
--ruby=/usr/local/Cellar/ruby/1.9.3-p0/bin/ruby
--with-mysql-config
--without-mysql-config
--with-mysql-dir
--without-mysql-dir
--with-mysql-include
--without-mysql-include=${mysql-dir}/include
--with-mysql-lib
--without-mysql-lib=${mysql-dir}/lib
--with-mysqlclientlib
--without-mysqlclientlib
--with-mlib
--without-mlib
--with-mysqlclientlib
--without-mysqlclientlib
--with-zlib
--without-zlib
--with-mysqlclientlib
--without-mysqlclientlib
--with-socketlib
--without-socketlib
--with-mysqlclientlib
--without-mysqlclientlib
--with-nsllib
--without-nsllib
--with-mysqlclientlib
--without-mysqlclientlib
--with-mygcclib
--without-mygcclib
--with-mysqlclientlib
--without-mysqlclientlib


Gem files will remain installed in /usr/local/Cellar/ruby/1.9.3-p0/lib/ruby/gems/1.9.1/gems/mysql-2.8.1 for inspection.
Results logged to /usr/local/Cellar/ruby/1.9.3-p0/lib/ruby/gems/1.9.1/gems/mysql-2.8.1/ext/mysql_api/gem_make.out
{% endcodeblock %}

是Mac平台，安装了MySQL5.5.20，搜索了一番，似乎是因为已经安装了mysql没有指定已安装的mysql路径出现的问题，于是指定一个过去：

{% codeblock lang:bash %}
gem install mysql -- --with-mysql-dir=/usr/local/mysql
{% endcodeblock %}

一开始的那两个“--”不能省略，而且发现参数中那个等号左右最好别带空格，我是代码习惯了等号周围加空格，在这里竟然会出错。

我已经解决问题了，成功安装mysql的ruby驱动，如果仍然遇到问题，可以试试参考[这里](http://blog.bmn.name/2008/02/rails-gem-install-mysql-throws-error-extconfrb-failed/)（同样感谢这里）。