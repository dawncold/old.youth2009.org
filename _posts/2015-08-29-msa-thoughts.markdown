---
layout: post
title: "MSA thoughts"
date: 2015-08-29 21:51:24 +0800
comments: true
categories: thoughts
---

MSA (Micro Service Architecture) is a methodology of dependencies management. Its core thought is divided a large application into some independent small applications, these small applications can be deployed independent and use different programming language, etc.

I think it's not a new methodology, but a new concept.

We can think you make an application, used some libraries written by others, these libraries are some independent application, they expose some APIs for you, your application import them and call some APIs to fullfill some functions. Generally they will keep same APIs during update and fix bugs, so you can upgrade them and use latest version. You can also copy their codes to your application code base, just like you write all codes, but if they updated, you must copy new codes to your code base, that likes the development without MSA.

So, MSA is a methodology of dependencies management, the example is a small scope of MSA, the real MSA means some independent application, for instance an order service, an logistics service, etc. We may name these order module, logistics module before, but now we name these xxx service.