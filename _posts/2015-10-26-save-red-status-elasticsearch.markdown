---
layout: post
title: "save red status elasticsearch"
date: 2015-10-26 22:49:13 +0800
comments: true
categories: dev
---

Someday when I use Kibana, I got an error all shards failed, so I look through office guide and some posts on the Internet.

Maybe the memory limit results in some primary shards can not be loaded by elasticsearch. If one or all primary shards are unsigned, your elasticsearch cluster will be in red status, if all primary shards are loaded, your cluster status will be yellow, if all shards are loaded, the green status you will be get.

The data is stored in `index` in elasticsearch, the `index` will be divided into some shards, the shards are `primary` and `replica` kind, you can have no replica, but you can have no primary. replica shards will be stored on the other nodes in cluster, but in default setting, you have only two nodes, one is data store node, another one is a client node, and the default setting of index is 2 or 3 replicas for each primary shard, you can update all index setting to disabling this config.