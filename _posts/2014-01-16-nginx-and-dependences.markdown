---
layout: post
title: "nginx-and-dependences"
date: 2014-01-16 18:46:33 +0800
comments: true
categories:  dev
---

{% codeblock lang:bash %}
wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.34.tar.gz
wget http://www.openssl.org/source/openssl-1.0.1f.tar.gz
wget http://nginx.org/download/nginx-1.5.8.tar.gz
{% endcodeblock %}

default install pcre and openssl

{% codeblock %}
nginx configure
+gzip


Configuration summary
  + using system PCRE library
  + OpenSSL library is not used
  + md5: using system crypto library
  + sha1: using system crypto library
  + using system zlib library
{% endcodeblock %}
