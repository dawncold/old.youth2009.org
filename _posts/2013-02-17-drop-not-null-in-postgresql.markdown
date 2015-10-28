---
layout: post
title: "drop not null in postgresql"
date: 2013-02-17 23:31
comments: true
categories: work@honovation postgresql
---

要修改带有NOT NULL约束的某列为NULLABLE该如何写SQL呢？

`ALTER TABLE xxx ALTER COLUMN xxx DROP NOT NULL`
