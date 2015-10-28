---
layout: post
title: "搭建4pm.la的数据库服务器"
date: 2013-07-04 21:54
comments: true
categories: 4pm.la
---

原来用MySQL比较多，现在工作上主要用PostgreSQL，对于低级的应用来说，选什么数据库都差不多，但也要为以后发展做准备，不过我暂时看不到那么远，PG作为一个开源的数据库来说，还算是比MySQL有优势一点，所以就用这个了。

在Mac上安装的时候有个locale的选择，我选了这个：

![locale select](http://pic.yupoo.com/dawncold0/CZ9bpp9U/medish.jpg)

然后下载了pgAdmin作为GUI工具，结合PG的CLI一起使用比较好。使用psql登陆数据库可以用：`psql -h localhost -U postgres -W`
	
	其中
	-h db host
	-U db user
	-W use password

pgAdmin用起来感觉超差，目测是java写的，有点小卡，远不如在Ubuntu上的体验。

创建一个网站用的用户，可以用createuser这条命令，或者连上PG后写CREATE USER这种SQL，官方文档介绍两者没什么差别。createuser只是包装了一下SQL而已。（[官方文档](http://www.postgresql.org/docs/current/static/app-createuser.html)）

`createuser -dEeP -h localhost -U postgres -W xxx`

	其中
	-d can create db
	-E encrypted user's password
	-e echo SQL command
	-P can not create role

创建一个数据库，同样可以用包装了CREATE DATABASE的createdb。([官方文档](http://www.postgresql.org/docs/9.2/static/app-createdb.html)）

`createdb -e -E UTF8 -l zh_CN.UTF-8 -O OWNER -h localhost -U postgres -W DBNAME`

	其中
	-e echo SQL command
	-E use encoding
	-l set locale, included LC_COLLATE and LC_CTYPE
	-O db's owner
	
看到篇不错的文章，介绍PG的ROLE、USER、SCHEMA、TABLESPACE、DATABASE等概念的关系：[这里](http://blog.csdn.net/kanon_lgt/article/details/5931522)

生产环境用的Ubuntu12.04.2，在创建数据库的时候制定locale，但没有zh_CN这个locale，于是需要安装：`/usr/shard/locales/install-language-pack zh_CN`，安装完了最好能重启机器，不然的话好像createdb一直会报错说zh_CN.UTF-8这个locale不正确。重启了之后再创建db就ok了，但告诉你说collection你选了zh_CN的，和默认模板template1的en_US冲突，提示是换成template0模板，于是加了参数`-T`:`createdb -e -E UTF8 -l "zh_CN.UTF-8" -O :OWNER -T template0 -h localhost -U postgres -W :DBNAME`