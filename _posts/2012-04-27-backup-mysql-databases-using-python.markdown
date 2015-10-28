---
layout: post
title: 用python备份mysql
comments: true
date: 2012-04-27 20:44
categories: python mysql
---

备份数据库的重要性不想多说了。


{% codeblock lang:python %}
#! /usr/bin/env python
# coding: utf-8

import os
import sys
from datetime import *
import time

#mysql's path
mysql_path = '/usr/local/mysql/bin/'
#edit this if your mysql username and password is not like this:
mysql_username = 'root'
mysql_password = 'xxxxxx'
#backup path
backup_path = 'mysqlbackup/'

def validate_backup_path():
if os.path.exists(backup_path) == False:
print "I create a directory here: %s " % backup_path
os.mkdir(backup_path)

def backup_all_databases():
filename = "all_%s.sql" % (datetime.utcfromtimestamp(time.time()))
os.system("%smysqldump -u%s -p%s --all-databases > '%s%s'" % (mysql_path, mysql_username, mysql_password, backup_path, filename))

if __name__ == "__main__":
validate_backup_path()
backup_all_databases()
print "finish!!!"
{% endcodeblock %}

这个是修改了一次的备份脚本，本来是分数据库备份的，无奈制定了分数据库备份需要输入密码，这就不容易加入cron来自动完成了，不过听说在my.cnf中加入mysqldump的设置可以避免输入账号密码，这也算是一个办法吧，不过还是本着简化的思想，只导出所有数据库出来就好，配合着上一篇的dropbox自动备份，这样VPS的灾备就稍稍好些了：）