---
layout: post
title: "role in postgresql"
date: 2014-08-14 22:08:20 +0800
comments: true
categories: dev
---

In PostgreSQL versions before 8.1, users and groups were distinct kinds of entities, but now only role, it is user or group or both.

if you create a role using “CREATE ROLE r1”, r1 is not a user, only a generic role, it is likely a group, you can not find it in pg_user, only in pg_roles table, but if you grant LOGIN privilege to r1, it will be appear in pg_user table.

After installed postgresql cluster, you need execute initdb, and it will create a default role with superuser privilege, costomarily this role(user) named postgres

Role’s attributes: login, superuser, database creation, role creation, initiating replication, password

CREATE USER r1 == CREATE ROLE r1 LOGIN

Tip: It is good practice to create a role that has the CREATEDB and CREATEROLE privileges, but is not a superuser, and then use this role for all routine management of databases and roles. This approach avoids the dangers of operating as a superuser for tasks that do not really require it.


examples:


CREATE ROLE joe LOGIN INHERIT;
CREATE ROLE admin NOINHERIT;
CREATE ROLE wheel NOINHERIT;
GRANT admin TO joe;
GRANT wheel TO admin;



joe can access admin privilege by using “SET ROLE admin”, or if joe has the INHERIT, joe can access privilege directly from admin, if joe want to use these privileges, joe must “SET ROLE admin”. Joe can not access privilege from wheel, because admin has the NOINHERIT, admin can not get these privileges, so as joe.