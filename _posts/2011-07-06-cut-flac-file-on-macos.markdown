---
layout: post
title: mac下分割flac文件
comments: true
date: 2011-07-06 13:59
categories: mac
---

原来我有很多ape和flac音乐的，在windows时代用foobar软件播放音乐很快乐，但在mac下，就有点儿别扭了，cog可以打开cue文件，并且播放也没问题，就是不能分割，这让人很头疼啊！ 从[这里](http://broadeno.wordpress.com/2009/06/16/%E5%A6%82%E4%BD%95%E5%9C%A8mac%E7%B3%BB%E7%BB%9F%E9%87%8C%E5%88%86%E5%89%B2flac%E9%9F%B3%E4%B9%90%E6%96%87%E4%BB%B6%EF%BC%8C%E5%B9%B6%E8%BD%AC%E6%8D%A2%E4%B8%BAwav)找了些办法，应该可以！ 安装macports这个软件，希望用源代码的方式安装，否则如果用官方的dmg文件安装，到最后一步运行安装脚本的时候你会发现进度条总是停留在最后不动，打开install的日志一看，有很多记录，听其他人说最后在下载一些包的信息文件，就像是一个索引镜像吧，断了网还好。1423s过后，安装完了。 

`sudo port install cuetools`

这样就安装好了cuetools和shntool这两个软件，其中缺失的依赖软件也被macports自动安装上了，只是在下载的时候没有进度，很可恶，如果又兴趣可以看这里学着改改macports的fetch部分，至少能看看下载了多少，心里也有个数！ 下面进行分割：


{% codeblock lang:bash %}
dawncold@tianzhenmatoMacBook-Pro Music$ cuebreakpoints 手嶌葵\(Teshima.Aoi\).-.\[The.Rose～I.Love.Cinemas～\].专辑.\(FLAC\).cue | shnsplit -o flac 手嶌葵\(Teshima.Aoi\).-.\[The.Rose～I.Love.Cinemas～\].专辑.\(FLAC\).flac 
Splitting [手嶌葵(Teshima.Aoi).-.[The.Rose～I.Love.Cinemas～].专辑.(FLAC).flac] (34:12.18) --> [split-track01.flac] (3:56.27) : 100% OK
Splitting [手嶌葵(Teshima.Aoi).-.[The.Rose～I.Love.Cinemas～].专辑.(FLAC).flac] (34:12.18) --> [split-track02.flac] (3:21.71) : 100% OK
Splitting [手嶌葵(Teshima.Aoi).-.[The.Rose～I.Love.Cinemas～].专辑.(FLAC).flac] (34:12.18) --> [split-track03.flac] (5:36.65) : 100% OK
Splitting [手嶌葵(Teshima.Aoi).-.[The.Rose～I.Love.Cinemas～].专辑.(FLAC).flac] (34:12.18) --> [split-track04.flac] (2:56.00) : 100% OK
Splitting [手嶌葵(Teshima.Aoi).-.[The.Rose～I.Love.Cinemas～].专辑.(FLAC).flac] (34:12.18) --> [split-track05.flac] (2:57.12) : 100% OK
Splitting [手嶌葵(Teshima.Aoi).-.[The.Rose～I.Love.Cinemas～].专辑.(FLAC).flac] (34:12.18) --> [split-track06.flac] (4:31.59) : 100% OK
Splitting [手嶌葵(Teshima.Aoi).-.[The.Rose～I.Love.Cinemas～].专辑.(FLAC).flac] (34:12.18) --> [split-track07.flac] (4:03.01) : 100% OK
Splitting [手嶌葵(Teshima.Aoi).-.[The.Rose～I.Love.Cinemas～].专辑.(FLAC).flac] (34:12.18) --> [split-track08.flac] (3:14.16) : 100% OK
Splitting [手嶌葵(Teshima.Aoi).-.[The.Rose～I.Love.Cinemas～].专辑.(FLAC).flac] (34:12.18) --> [split-track09.flac] (3:34.67) : 100% OK
{% endcodeblock %}
文件名有点差劲，也许可以配合cueprint和shnsplit的o参数可以实现完美的转换。