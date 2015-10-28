---
layout: post
title: "mailing list in postfix"
date: 2015-01-08 19:20:14 +0800
comments: true
categories: parttime
---

Too simple to making a mailing list in postfix, just define a mailing list name and recipients in `/etc/postfix/virtual`, like this: `dev-group dev1@company.com dev2@company.com dev3@company.com`, after that, generate the virtual db by `postmap /etc/postfix/virtual`.

Don't forget add `virtual_alias_maps=hash:/etc/postfix/virtual` in your `main.cf` file, and restart postfix finally.

I think I need study postfix systemally, just build a private smtp/imap server.