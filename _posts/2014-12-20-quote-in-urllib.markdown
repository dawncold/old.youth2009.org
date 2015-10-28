---
layout: post
title: "safe characters of quote method in urllib"
date: 2014-12-20 20:27:59 +0800
comments: true
categories: dev
---

quote accept two arguments: a string and safe characters. If you pass empty to `quote` as the second parameter, it means every characters except preserved characters will be replaced by a % leading characters, e.g. space will be replaced by %20, etc.

In my project, I invoke quote like `quote(params, '')`, and I have imported `unicode_literals`, so I passed a unicode parameter to `quote` method.

What will happen?

Next time you invoke quote with the same `safe` parameter you used before, you may get an error like `UnicodeDecodeError: 'ascii' codec can't decode byte 0xe4 in position 0: ordinal not in range(128)`, urllib will cache the safe parameter(urllib.py 1277 line), it expects a byte type parameter but you pass an unicode one, also, that library didn't check or convert it before it uses.

Best practice, pass a byte parameter like `b''` to `quote` if you have same usage(unicode literals) like me.