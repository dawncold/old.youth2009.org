---
layout: post
title: "be careful python fdopen"
date: 2015-01-07 23:13:39 +0800
comments: true
categories: dev
---

I have got a bug when I `print` something to `stdout`, I got `Bad file descriptor`, it means my stdout is a bad descriptor, what?!

Core code like this: `logger.StreamHandler(os.fdopen(sys.stdout.fileno(), 'w', 0))`, I want to a unbuffered stdout, so I reopen it by `fdopen`, and reset the buffer size to 0, I still also did same thing to `stderr`, but that is no sense, because of `stderr` is unbuffered normally(but in Python3, it maybe line buffered, in MacOS).

If your `stdout` is reopened by `fdopen`, and its reference count hits zero, it will be collected by Python GC, also your `stdout` will be ate by GC, something wrong will happen after that.

So, be careful with `fdopen` for `stdin`, `stderr`, `stdin`:)