---
layout: post
title: sqlite3的rowcount
comments: true
date: 2012-05-14 17:00
categories: sql
---

最近写了一个todo的webapp，在用户登陆的时候是select数据库中的内容进行对比判断，当然如果select的内容是0那就表示用户登陆失败了，可能账号或者密码写错了，数据库用的sqlite3，在python的api中发现有cursor.rowcount可用，于是就这么判断一下是不是有数据被select出来了，没想到这样判断是错误的。

select的rowcount永远为-1，哎，这里着实坑了我一番啊～

只好cursor.fetchone()先，然后判断得到的内容是不是None。

从[这里](http://stackoverflow.com/questions/839069/cursor-rowcount-always-1-in-sqlite3-in-python3k)得到的答案。