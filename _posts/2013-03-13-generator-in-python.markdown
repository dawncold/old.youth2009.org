---
layout: post
title: "generator-in-python"
date: 2013-03-13 21:52
comments: true
categories: python study
---

今天在代码中遇到一个next方法（python代码），以前从没用过这个，于是简单了解了一下。

next就是iterator了，可以通过iterator来找东西，找到就停下了，如果给了默认值，没找到的话就用默认值。

generator这个东西是很有意思的，比如：

{% codeblock %}
def other_firstn(n):
 num, nums = 0, []
 while num < n:
   nums.append(num)
   num += 1
 return nums
{% endcodeblock %}
可以产生一个list，里面是按顺序的数字，有n个，结果类似于range(n)的返回值。

还有一个版本的firstn：

{% codeblock %}
def firstn(n):
 num = 0
 while num < n:
   yield num
   num += 1
{% endcodeblock %}
这个看起来就很帅了，代码也简洁了很多，yield是十分神奇的表达式，产生了一个num，这里不太好想，不能按照正常的function来思考这个执行顺序了。

总之，如果产生100个数字，你可以一下子弄出100个来，或者你知道规则的话，你就弄出第一个来，然后用的时候按照规则，从第一个一直走下去，也产生了100个。最大的不同就是性能，后者必然速度更快了，前提是数量要足够多！写了一个简单的性能对比，主要是时间上的，内存上的不容易监控。

{% codeblock %}
# /usr/bin/python
#! -*- coding: utf-8 -*-

import time

def firstn(n):
 num = 0
 while num < n:
   yield num
   num += 1

def other_firstn(n):
 num, nums = 0, []
 while num < n:
   nums.append(num)
   num += 1
 return nums


def timer(func_wrap, func, *args, **kwards):
 s = time.time()
 r = func_wrap(func(*args, **kwards))
 e = time.time()
 print 'return: %s   use %f ms[s: %s, e: %s]' % (r, (e - s), s, e)

def main():
 timer(sum, firstn, 1000000)
 timer(sum, other_firstn, 1000000)
 
 
 
if __name__ == "__main__":
 main()
{% endcodeblock %}
输出结果是：大约会慢1倍
{% codeblock lang:bash %}
dawncold [21:49:11] ~=>$ python 1.py 
return: 499999500000   use 0.137414 ms[s: 1363182552.38, e: 1363182552.52]
return: 499999500000   use 0.290716 ms[s: 1363182552.52, e: 1363182552.81]
{% endcodeblock %}
