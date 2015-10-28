---
layout: post
title: 关于UITableView中的cell配置
comments: true
date: 2011-07-29 13:28
categories: iphone-dev
---

都是关于cell的，不知道值得写出来么：

1。在定义cell样式的时候，如果你用UITableViewCellStyleSubtitle来初始化cell，那么设置cell的detailTextLabel的text属性就能看到详细的内容，在textLable的下一行显示着。

2。设定cell：`[cell setAccessoryType: UITableViewCellAccessoryDisclosureIndicator];`这样在每个cell右侧会有小箭头提示，很漂亮。