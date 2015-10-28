---
layout: post
title: "dog-pile-effect"
date: 2013-05-18 22:48
comments: true
categories: dev
---

如果你的网站该去解决dog pile effect了，那应该有不小的PV了。今天看暴走漫画的架构设计，那是应对1000W PV的一个设计，当然架构这东西每家都不一样，可能这个就他们自己用着适合。里面提到了dog pile effect，这个的意思是：在多request去cache中拿数据的时候，如果发现自己拿的数据是过期了的，那么就要去db中拿新的来。这么看好像没问题，但有前提的——request很多，真的很多，而且确实用cache了（反正我不相信request很多的时候某些数据你不用cache，那得是个多么bt的db才能支撑啊？！）本来用cache的作用就是降低对某些slow query的执行次数，缓解db压力。但过期了，再去db中取这就和没有cache一样了，db会死的。

解决方法有这样的：

* 有专门的job（比如crontab）来更新cache，这样request总是去cache取，不用管过不过期。好处就是简单；坏处是可能做一些没必要的重复计算，没有request你也更新了cache，而且你得确保这个job的执行时间要小于job的间隔，否则会积压很多job。
* request取到数据发现过期，再请求一个update lock，成功拿到锁就可以更新cache，此时其他request也会请求这把锁，但就是请求不到，那就继续返回过期的数据。这是不容忍延迟的情况，如果对数据准确性要求高，那在updating的时候其他request会等，等数据更新了再返回。怎么用取决于environment。

引用自：[http://hype-free.blogspot.jp/2008/05/avoiding-dogpile-effect.html](http://hype-free.blogspot.jp/2008/05/avoiding-dogpile-effect.html)，注意blogspot。。。
