---
layout: post
title: "return-value-in-jquery-json-datatype"
date: 2014-01-23 18:57:21 +0800
comments: true
categories:  dev
---

向api server发送请求做一件事的时候，比如修改密码，server做完后没有返回值，response code是200。这在原来的时候没问题，“原来”是指ajax的dataType未指定的时候，jQuery会自己猜测用什么，但这次指定了server的response是json，所以，即便是看到200 code也未能调用OnSuccess，空返回值对于json是不合法的，于是返回一个什么东西就好，当然要先to_json再返回。