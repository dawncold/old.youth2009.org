---
layout: post
title: 一个简单的C程序
comments: true
date: 2012-05-30 19:39
categories: c
---

嗯，我是一直喜欢C的，不过没勇气说我从事C方面的开发，因为C是需要很多技巧和底层技术的，我自知这方面的能力不足：（

{% codeblock lang:c %}
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

void strcp(char*, char*);
int main()
{
char* s = "test string...";
char* t = malloc(strlen(s));
strcp(t, s);
printf("%s\n", t);
free(t);

return 0;
}

void strcp(char *s,char *t)  
{  
while(*s++ = *t++);  
{% endcodeblock %}

最漂亮的就是那句strcp的函数了，非常简洁好用：）

