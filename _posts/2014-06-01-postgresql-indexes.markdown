---
layout: post
title: "postgresql indexes"
date: 2014-06-01 10:18:27 +0800
comments: true
categories: study
---

#Introduction

Indexes will speed up your read(SELECT) and write(INSERT, UPDATE, DELETE) operation on a table, but they should by removed when a query seldom or never used. Create a bit table's index will spend lot of time. By default, PostgreSQL allows reads (SELECT statements) to occur on the table in parallel with index creation, but writes (INSERT, UPDATE, DELETE) are blocked until the index build is finished. In production environments this is often unacceptable. It is possible to allow writes to occur in parallel with index creation, but there are several caveats to be aware of — for more information see [Building Indexes Concurrently](http://www.postgresql.org/docs/9.3/static/sql-createindex.html#SQL-CREATEINDEX-CONCURRENTLY).

#Index Types

PostgreSQL provides several index types: B-tree, Hash, GiST, SP-GiST and GIN. By default, the CREATE INDEX command creates B-tree indexes, which fit the most common situations.

#Multicolumn index

Currently, only the B-tree, GiST and GIN index types support multicolumn indexes. Up to 32 columns can be specified. (This limit can be altered when building PostgreSQL; see the file pg_config_manual.h.)

if your frequently query is like this: `SELECT name FROM test2 WHERE major = constant AND minor = constant;`, your need create an index on table test2 with `major`, `minor` columns: `CREATE INDEX test2_mm_idx ON test2 (major, minor);`

The order is important in multicolumn index:
	
>A multicolumn B-tree index can be used with query conditions that involve any subset of the index's columns, but the index is most efficient when there are constraints on the leading (leftmost) columns. The exact rule is that equality constraints on leading columns, plus any inequality constraints on the first column that does not have an equality constraint, will be used to limit the portion of the index that is scanned. Constraints on columns to the right of these columns are checked in the index, so they save visits to the table proper, but they do not reduce the portion of the index that has to be scanned. For example, given an index on (a, b, c) and a query condition WHERE a = 5 AND b >= 42 AND c < 77, the index would have to be scanned from the first entry with a = 5 and b = 42 up through the last entry with a = 5. Index entries with c >= 77 would be skipped, but they'd still have to be scanned through. This index could in principle be used for queries that have constraints on b and/or c with no constraint on a — but the entire index would have to be scanned, so in most cases the planner would prefer a sequential table scan over using the index.
	
#Order By

By default, B-tree indexes store their entries in ascending order with nulls last.

#Combining Multiple Indexes

little difficult just trade off to decide which indexes to provide. Sometimes multicolumn indexes are best, but sometimes it's better to create separate indexes and rely on the index-combination feature.

#Index on Expressions

This kind of index, not a specific column, it's an expression: `CREATE INDEX people_names ON people ((first_name || ' ' || last_name));`

#Partial Index

`CREATE INDEX idx_xxx ON table(name) WHERE NOT deleted` this index only enables to rows which deleted is `TRUE`