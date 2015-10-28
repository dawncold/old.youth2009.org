---
layout: post
title: "optimize shadowsocks NAT rules"
date: 2015-01-11 23:46:08 +0800
comments: true
categories: play
---

Few days ago, I upgraded my OpenWrt box to latest version, there is a new style(Bootstrap) interface and I like it very much(too long lived old world).

Also I found a shadowsocks [special version](https://github.com/shadowsocks/openwrt-shadowsocks) for openwrt, it includs China main IP blocks, some requests within this IP range, you could bypass shadowsocks, and this IP blocks is from `apnic`, very precise but a little long for openwrt, 4000+lines.

I think the most counted IP block I would use it in the future very soon, so I can sort them desc.

`iptables -t nat -xvnL SS_SPEC_WAN_AC | tail -n+12 | head -n -1 | sort -crnsk 1,1 | awk '{ print $NF }' > /etc/shadowsocks/ignore.list`

`tail -n+12` means display results from the first 12 row to the end, first 11 rows includes two lines heads, one line shadowsocks server IP, eight lines internal IP blocks; 

`head -n -1` means display results except last line(doesn't work on MacOS), and last line is default shadowsocks redirect rule, so keep it at the same place.

`sort -crnsk 1,1` means `c`heck first, `r`everse result, `n`umerical value(converted from input string), `s`table sort, `k 1,1` sort key (start a key at POS1, end it at POS2 (origin 1))

`awk print $NF`, print the last column, that's very cool.

rewrite the results to ignore.list, and restart shadowsocks, it will use the sorted IP blocks, maybe fast than before 0.xx ms!