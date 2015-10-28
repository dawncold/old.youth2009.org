---
layout: post
title: "checksum functions in MacOs"
date: 2015-08-16 15:22:06 +0800
comments: true
categories: 
---

It's better to calculate checksum for your downloaded files, it can make sure you download that real file from server, not from the ISP proxy server.

In MacOS, you can use `md5` and `shasum` to calculate file checksums.

* calculate a MD5 checksum

`md5 xxx.data`

* calculate a SHA-1 checksum

`shasum -a 1 xxx.data`

* calcuate a SHA-256 checksum

`shasum -a 256 xxx.data`

Thanks for [here](http://notepad2.blogspot.jp/2012/07/mac-os-x-how-to-generate-md5-sha1.html)