---
layout: post
title: LVM+RAID实践
comments: true
date: 2012-10-08 14:09
categories: lvm
---
两块256Gb SSD，做RAID1，用LVM管理，方便日后动态扩容等。

0.分区，因为是SSD，需要注意4K对齐问题，否则对SSD的寿命和性能有影响：

{% codeblock lang:bash %}
fdisk /dev/sda
fdisk /dev/sdb
{% endcodeblock %}

1.创建PV

{% codeblock lang:bash %}
sudo pvcreate /dev/sd{a1,b1}
{% endcodeblock %}

2.创建VG

{% codeblock lang:bash %}
sudo vgcreate -s 16M vg0 /dev/sd{a1,b1}
{% endcodeblock %}

3.创建LV
{% codeblock lang:bash %}
sudo lvcreate -n lv0 vg0 -m 1 -lxxxx --corelog
{% endcodeblock %}
