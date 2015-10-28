---
layout: post
title: "use-change-event-on-checkbox"
date: 2013-07-26 09:07
comments: true
categories: work@honovation js
---

昨天在一个table的第一行放了一个checkbox, 想做一个效果：一开始这个table的每一行都是冻结状态，点击这一行就激活了，顺便会把checkbox选中，当然直接点checkbox也会激活这一行。可惜在bind event的时候，分别给tr和checkbox加了click事件，tr的click会trigger到checkbox上，这样导致的结果就是点tr会触发checkbox的click handler，但同时又触发了tr的click handler，循环导致最后js崩溃。

后来发现在tr的click handler中检查event.target可以不触发这种死循环，但在checkbox click handler中使用prop判断checked状态不准，在stackoverflow中找到解答：jquery1.8中的 click()和真实的click是不一样的，应该在checkbox上用change event，然后一切ok。

解答：[http://stackoverflow.com/questions/7668826/jquery-triggerclick-not-firing-click-event-on-checkbox](http://stackoverflow.com/questions/7668826/jquery-triggerclick-not-firing-click-event-on-checkbox)
