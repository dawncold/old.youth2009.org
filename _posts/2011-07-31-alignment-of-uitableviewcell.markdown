---
layout: post
title: UITableViewCell的对齐方式
comments: true
date: 2011-07-31 10:05
categories: iphone-dev
---

如果你用了Subtitle的Style，那么设置textAlignment为center就没用了，当然设置textAlignment目前只能针对textLabel来设置，听说在3.0以后的版本对于cell的textAlignment的设置方法废弃了。

刚刚我把cell的style改成了default，然后再设置这些alignment，就能用了，真奇怪用subtitle的方式即使重建了cell，都不能设置alignment到center。但原因是这样的，我引用下官方reference：


>UITableViewCellStyleSubtitle
>A style for a cell with a left-aligned label across the top and a left-aligned label below it in smaller gray text. The iPod application uses cells in this style.

很明确了吧，subtitle就是left-aligned的label，再改也没用。当然还有个value1和value2的style，似乎是专门left-aligned和right-aligned的，不过在他们各自的反方向还有另外的label，最好看官方的说明和多多实践。