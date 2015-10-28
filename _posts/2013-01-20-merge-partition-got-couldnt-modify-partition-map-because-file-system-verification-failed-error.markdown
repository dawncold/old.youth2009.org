---
layout: post
title: "merge partition got Couldn’t modify partition map because file system verification failed error"
date: 2013-01-20 19:36
categories: mac
---

前几天需要把本机的VMware虚拟机文件拷到工作机器上用，但文件比较大，有30G，U盘不行，无线共享太慢，网线直连无奈工作机器百兆网卡不给力还是慢，分割了我的TimeMachine备份盘，但用完后再合并划分出去的分区就出问题了，提示：

Couldn’t modify partition map because file system verification failed error

此时可以Verify一下这个硬盘，如果有错误就repair，相信这里没问题的都应该可以再合并了吧，我这里还是出问题了，在提示repair complete之后出现了一个错误，好像是boot什么的错误，建议我reformat，再弄backup file，backup file too many？？记不清楚了，再合并一次分区，不行的话果断erase掉，再backup，反正现在backup都用不上，趁着清理一下也好。
