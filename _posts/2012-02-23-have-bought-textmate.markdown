---
layout: post
title: 买了textmate
comments: true
date: 2012-02-23 19:29
categories: mac
---

截至目前，这是我买得最贵的一款软件了——39欧元（327RMB）

一直在豆瓣Textmate小组中等人家团购，自己也从没在官网试过购买，一看是用的paypal做中转，感觉不靠谱，以前也没试过paypal的支付，没想到这次成功了，先用了张信用卡支付，发现不行，结果换普通银行卡，直接跳转到了银联，然后我又用的信用卡透支……

稍微配置了一下textmate，按照[这里](http://www.lixiaolai.com/archives/10895.html)的方法，其中1.5版本的中文字体那里，建议不要尝试了，不完美，还是等2.0正式发布了吧，听说2.0对于中文字体支持得很好，但我懒得下载测试版来用：）

加入GetBundles：

{% codeblock lang:bash %}
mkdir -p ~/Library/Application\ Support/TextMate/Bundles
cd !$
svn co http://svn.textmate.org/trunk/Review/Bundles/GetBundles.tmbundle/
osascript -e 'tell app "TextMate" to reload bundles'
{% endcodeblock %}

第一次见cd还能这样用，这样简直太方便了！还有最后那句script，多么优美的句子：）

以后就要多用textmate了，先放弃emacs。