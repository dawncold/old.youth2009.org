---
layout: post
title: "about-Sorted"
date: 2013-03-16 12:54
comments: true
categories: sortedapp iphone-dev
---

早就考虑做这么一个app，不过拖延到现在了，再次佩服一下我的拖延症。

Sorted是这样一个app，安装上之后就会跟踪你使用手机上app的习惯，根据使用频率给桌面的app排序，估计等你用一段时间之后，第一页的apps就是最常用的了。

当然，这需要你的iPhone jailbreaken。

刚刚用iFile找到了存放app list的地方，在/User/Library/SpringBoard/IconState.plist，plist就像是python中的dict，里面两个key分别是：buttonBar、iconLists。

buttonBar中有个list，是底部Dock上的app标识，例如有：com.apple.mobilephone、com.apple.MobileSMS等。

iconLists中又是一个list，内容也是list，每个list表示桌面某一页上的apps。

不过有个问题是：如果我手动修改了这里的值，比如我交换某页两个app的位置，回到桌面并不会立刻看到效果，如果要看效果，需要respring...就是重启SpringBoard，这是我不能接受的。需要再看SpringBoard的私有api有没有提供这方面的支持了。
