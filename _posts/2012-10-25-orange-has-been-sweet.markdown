---
layout: post
title: "orange has been sweet"
date: 2012-10-25 21:04
comments: true
categories: work@honovation life
---

今天早晨买了一些水果，也买了几个橙子，虽然不便宜，但今晚上吃起来感觉还不错，挺甜的。

怎么总感觉今天有点儿不稳呢，听说ERP的接口搞定了就要去测试了，测试过程不怎么顺利，让别人做事情，而且相隔很远，再加上对方不怎么关心这个有点陈旧的系统，工作就会很难同步，我们一测试就出问题，报告过去后好久才给我改改，再测试，又出问题。目前来看虽然没有完全测试好，但已经暴露出几个问题了，还是比较重要的。

明天需要继续测试剩下的接口，并且要总结问题，发给郑工处理处理，又是漫长的等待，这是必然的，不仅仅是一个周末，估计这块在上线前都会是很紧张的。

这篇文章发表得不容易，generate的时候总出现一个错误:
{% codeblock lang:bash %}
/Users/dawncold/.rvm/rubies/ruby-1.9.3-p286/lib/ruby/1.9.1/psych.rb:203:in `parse': (<unknown>): control characters are not allowed at line 1 column 1 (Psych::SyntaxError)
	from /Users/dawncold/.rvm/rubies/ruby-1.9.3-p286/lib/ruby/1.9.1/psych.rb:203:in `parse_stream'
	from /Users/dawncold/.rvm/rubies/ruby-1.9.3-p286/lib/ruby/1.9.1/psych.rb:151:in `parse'
	from /Users/dawncold/.rvm/rubies/ruby-1.9.3-p286/lib/ruby/1.9.1/psych.rb:127:in `load'
	from /Users/dawncold/.rvm/gems/ruby-1.9.3-p286/gems/jekyll-0.11.2/lib/jekyll/convertible.rb:33:in `read_yaml'
	from /Users/dawncold/.rvm/gems/ruby-1.9.3-p286/gems/jekyll-0.11.2/lib/jekyll/post.rb:39:in `initialize'
	from /Users/dawncold/Documents/Project/work_at_honovation/plugins/preview_unpublished.rb:23:in `new'
	from /Users/dawncold/Documents/Project/work_at_honovation/plugins/preview_unpublished.rb:23:in `block in read_posts'
	from /Users/dawncold/Documents/Project/work_at_honovation/plugins/preview_unpublished.rb:21:in `each'
	from /Users/dawncold/Documents/Project/work_at_honovation/plugins/preview_unpublished.rb:21:in `read_posts'
	from /Users/dawncold/.rvm/gems/ruby-1.9.3-p286/gems/jekyll-0.11.2/lib/jekyll/site.rb:128:in `read_directories'
	from /Users/dawncold/.rvm/gems/ruby-1.9.3-p286/gems/jekyll-0.11.2/lib/jekyll/site.rb:98:in `read'
	from /Users/dawncold/.rvm/gems/ruby-1.9.3-p286/gems/jekyll-0.11.2/lib/jekyll/site.rb:38:in `process'
	from /Users/dawncold/.rvm/gems/ruby-1.9.3-p286/gems/jekyll-0.11.2/bin/jekyll:250:in `<top (required)>'
	from /Users/dawncold/.rvm/gems/ruby-1.9.3-p286/bin/jekyll:23:in `load'
	from /Users/dawncold/.rvm/gems/ruby-1.9.3-p286/bin/jekyll:23:in `<main>'
{% endcodeblock %}
这种错误找起来真是蛋疼，最终是在dev这个字符开始的地方找到的，有个奇怪的字符出现了，看不到，也不占空，但确实有个字符在那里占着地方，或许是输入法在切换的时候遗留到那里的吧。。。可恶！

明天还有新工作，测试完ERP后继续做CMS，王总提出了不少新的东西要改进。
