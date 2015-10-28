---
layout: post
title: "incrby in redis"
date: 2013-02-02 13:26
comments: true
categories: work@honovation redis
---

redis中的incrby可以让value+1，用这个的好处是：当你用setex给一个key设置了timeout之后，如果要再改变里面的值，比如加1，你再set回去的话就会丢掉timeout，这时用incrby就可以喽。

再没用incrby的时候我用了ttl先取出timeout的值，再用一遍setex附带上ttl，显得好傻。
