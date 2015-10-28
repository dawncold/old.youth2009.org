---
layout: post
title: "suds-literal-soap"
date: 2013-07-08 22:16
comments: true
categories: work@honovation
---

SAP的接口就是和别人给的不一样，style为literal，最明显的地方就是operation中的参数是literal，原先的参数是一个object，按照原先的方法调用时发现传递过去的值都被放在了第一个参数中，很是不解。后来才知道这样的operation需要用keywords的那种传值方法——`**suds_client.dict(object)`，用suds的client的dict方法把构造的对象变成dict，再用`**`。

又被坑了一下。
