---
layout: post
title: mysql中的中文乱码
comments: true
date: 2011-01-27 23:20
categories: mysql
---

从mysql中返回的内容如果是中文的，而页面用了utf-8的编码，那么会出现一些“问号”，就是乱码了！应该将mysql中表的编码改为utf8_unicode_ci，各字段改为utf8_unicode_ci。在PHP中执行SQL查询前执行`SQLCONNECT.query(SET NAMES utf8);`这条SQL语句。