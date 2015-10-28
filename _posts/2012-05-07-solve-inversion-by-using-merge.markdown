---
layout: post
title: 逆序对的求解
comments: true
date: 2012-05-07 17:08
categories: algorithm python
---

今天看到算法导论上关于求解一个序列的逆序对的问题，以前自己在这个地方写着解答方法，不过今天怎么看都不懂了，从网上找了找，大都说得很模糊，不过自己突然有种领悟了的感觉，找了个简单的例子，实验了一下，自己的结论是正确的：）

例子是（2，3，8，6，1）这个序列，找出所有的5个逆序对。最好的方法是nlogn复杂度的利用归并排序的副产品——merge部分统计，统计比较左右列表时，左侧大于右侧时“左侧”列表中剩余数目。

归并的划分应该是这样的，（2，3，8）为左侧，（6，1）为右侧，继续划分为（2，3）和8，右边是6和1。下面就开始合并了，（2，3）和8这边还是（2，3，8），右侧出现一个逆序对，在合并6，1的时候因为作为“左侧”的6要大于1，所以这里有1个逆序对，这里的1就是此时“左侧”序列中的元素个数。

在往下走，要合并（2，3，8）和（1，6），马上就出现了2>1这样的情况，此时会出现（2，1）、（3，1）、（8，1）这几个逆序对，后面还会出现（8，6）这个逆序对，一共就这么5个。

因为原始序列是（2，3，8，6，1），我们需要用到这个原始序列的顺序来判断顺序排在前面的值却大于后面的，这样的机会在每次merge的时候是非常合适的。

这是修改后输出逆序对的归并排序算法，有点可惜哈，这么长的排序算法只让副产品在台前显露了一把！


{% codeblock lang:python %}
#! /usr/bin/env python
# coding: utf-8

def merge(arraylist, first, middle, last):
   temp = []
   i = first
   j = middle + 1
   while i <= middle and j <= last:
       if arraylist[i] <= arraylist[j]:
           temp.append(arraylist[i])
           i += 1
       else:
           for x in arraylist[i:middle + 1]:
               print "(%d,%d)" % (x, arraylist[j])
           temp.append(arraylist[j])
           j += 1
   while i <= middle:
       temp.append(arraylist[i])
       i += 1
   while j <= last:
       temp.append(arraylist[j])
       j += 1
   for i in range(0, last - first + 1):
       arraylist[first + i] = temp[i]

def merge_sort(arraylist, first, last):
   if first < last:
       middle = (first + last) / 2
       merge_sort(arraylist, first, middle)
       merge_sort(arraylist, middle + 1, last)
       merge(arraylist, first, middle, last)

if __name__ == "__main__":
lst = [2,3,8,6,1]
merge_sort(lst, 0, len(lst) - 1)
{% endcodeblock %}

运行结果：


{% codeblock lang:bash %}
(6,1)
(2,1)
(3,1)
(8,1)
(8,6)
{% endcodeblock %}

（我的代码缩进似乎出了点问题，本身这段归并排序也是从网上找来的，所以混合了不少tab和whitespace，弄了好久都是error indent，最后我无奈用whitespace来做缩进，好歹调试通过了！）