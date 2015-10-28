---
layout: post
title: "sort and uniq count"
date: 2015-08-27 19:41:46 +0800
comments: true
categories: study
---

I got some logs which recorded someone IP address and the URL it requests, I want to summary how many unique IP addresses request some specified URL, and request counts for one IP address.

so I filter out specified URL rows:
```
grep URL_PATH *.log
```

then I got these rows:
```
...
[ 2015-08-26T23:59:59+08:00 ] 14.219.202.241 /xx
[ 2015-08-26T23:59:59+08:00 ] 14.219.202.241 /xx
[ 2015-08-26T23:59:59+08:00 ] 14.219.202.241 /xx
[ 2015-08-26T23:59:59+08:00 ] 14.219.202.241 /xx
[ 2015-08-26T23:59:59+08:00 ] 14.219.202.241 /xx
[ 2015-08-26T23:59:59+08:00 ] 14.219.202.241 /xx
...
```
then I use `awk` print the fourth column:
```
grep URL_PATH *.log | awk '{print $4}'
```

then I got these IPs, I stored these IPs to a file, then `sort` and `uniq`, the `uniq` excepts a sorted file, the `-c` option means count these rows:
```
sort ips | uniq -c
```
then I got some unique rows with counts, but I want sort these rows order by counts desc:

```
sort ips | uniq -c | sort -k1nr -k2
```
the `-k1nr` means the KEY starts with first field, and as (n)umber, and (r)everse, the `-k2` means ends with second field. The `field` means the column in your data.