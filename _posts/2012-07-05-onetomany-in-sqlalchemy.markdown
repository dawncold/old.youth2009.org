---
layout: post
title: SQLalchemy中的oneToMany
comments: true
date: 2012-07-05 22:54
categories: python
---

今天在这里遇到些问题，花了一段时间，后来看官方文档解决了，很管用！

各个orm中的关系设置大同小异，一对多的关系中需要在“多”方的列中加入一个外键，指向“一”方，然后在“一”方加入一个存储“多”方的变量（这个orm中需要使用relationship方法声明）。

至此一个单项的OneToMany就弄好了，如果需要加入“反向”，形成双向的关系，那就在刚才的“一”方中存储“多”方的变量中指明backref参数，值就是在“多”方的属性中存储“一”方的这个属性名。我在这里弄错了，受了EJB的影响，以为双方都需要设置，结果弄的重复了，还好看了官方文档。

其他关系请参考[官方文档](http://docs.sqlalchemy.org/en/rel_0_7/orm/relationships.html#sqlalchemy.orm.relationship)

