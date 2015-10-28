---
layout: post
title: sqlite3连接查询和多次select的对比
comments: true
date: 2012-05-14 23:23
categories: python sql
---

通过todo_meta把todo和user联系起来，要查出userid为0～6的所有todo。随机了10W条todo数据进去。

左外连接查询比两次select快10～20%左右。


{% codeblock %}
#! /usr/bin/env python
# coding: utf-8

import sqlite3
import os
import time
import random

def connect():
return sqlite3.connect('./test.db')


def insertProgress(conn, user_id):
cur = conn.execute('INSERT INTO todo(title, date) VALUES(?,?)', ['just test!!!', time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())])
conn.execute('INSERT INTO todo_meta(todo_id, user_id) VALUES(?,?)', [cur.lastrowid, user_id])


def insertManyData(conn):
#reset database
os.system('sqlite3 test.db < schema.sql')

conn.cursor()
counts = [0,0,0,0,0,0]
for i in xrange(100000):
userid = random.choice([0, 1, 2, 3, 4, 5])
counts[userid] += 1
insertProgress(conn, userid)
conn.commit()
conn.close()
print counts

def selectUsingLeftOuterJoin(conn, user_id):
conn.cursor()
cur = conn.execute('SELECT t.title, t.date \
FROM todo t LEFT OUTER JOIN todo_meta tm \
ON tm.todo_id = t.id\WHERE tm.user_id = ?', [user_id])
def selectTwoTimes(conn, user_id):
conn.cursor()
cur = conn.execute('SELECT todo_id FROM todo_meta WHERE user_id = ?', [user_id])
for tid in [row[0] for row in cur.fetchall()]:
cur = conn.execute('SELECT title, date FROM todo WHERE id = ?', [tid])

if __name__ == "__main__":
uids = [0, 1, 2, 3, 4, 5]
insert_time_start = time.time()
insertManyData(connect())
print "Insert Time: %f" % (time.time() - insert_time_start)
select_ULOJ_start = time.time()
for uid in uids:
selectUsingLeftOuterJoin(connect(), uid)
print "Select Using Left Outer Join time: %f" % (time.time() - select_ULOJ_start)
select_two_times = time.time()
for uid in uids:
selectTwoTimes(connect(), uid)
print "Select Two Times time: %f" % (time.time() - select_two_times)
{% endcodeblock %}

schema：

{% codeblock lang:sql %}
drop table if exists todo;
drop table if exists user;
drop table if exists todo_meta;
create table todo (
id integer primary key autoincrement,
title string not null,
date datetime not null
);
create table user (
id integer primary key autoincrement,
email string not null,
password string not null,
nickname string not null,
salt string not null
);
create table todo_meta (
todo_id integer,
user_id integer,
foreign key(todo_id) references todo(id),
foreign key(user_id) references user(id)
);
{% endcodeblock %}

启动脚本就会创建数据库并开始测试。