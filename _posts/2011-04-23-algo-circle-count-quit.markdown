---
layout: post
title: 约瑟夫问题算法
comments: true
date: 2011-04-23 09:54
categories: php algorithm
---

昨晚还在忙碌网站，一个同学发来短信问了这样一个算法问题：一些人手拉手围成一个圈，从一个人开始报数，数到3的人退出，然后下一个人再开始报数，依然是数到3者退出，问最后剩下2个人是哪两个？

这题目看起来不算难，但这要是不靠一个语言的特性来解决，还是有些麻烦的。我说的语言特性就是一个bt数组方法，比如说移除元素啊这样的方法，用纯粹的C语言来写最好了。不过我那位同学是在雪VB.net不知道那里有没有语言特性。我手头上正在写PHP网页，就干脆用PHP写一个出来试试吧：）  


{% codeblock lang:php %}
$circle = array();
$out = 0;
$count = 0;
$n = 0;

for($i = 0;$i < $num;$i++) {
$circle[$i] = $i;
}
while(1) {
$count %= $num;
if($circle[$count] !== -1) {
if(($n % $diff) == ($diff - 1)) {
$circle[$count] = -1;
$out++;
if($out === $num - $sur)
break;
}
$n++;
}
$count++;
}
{% endcodeblock %}

这就是主要代码了，还算是简单吧？去Google了一下，看到有些人的解法都用了好麻烦的链表来抽象，用链表确实更符合客观事实，不过那样写起来，是不是给别人看的呢？！

算法的负责度显然是线性的，感觉还可以吧。