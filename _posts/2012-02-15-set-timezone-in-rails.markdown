---
layout: post
title: 设置Rails中的timezone
comments: true
date: 2012-02-15 14:37
categories: study ror
---

Timezone是很关键的东西哦，特别是某些app根据时间来作出不同反映的时候设置好Timezone就是必须的了。

没设置之前，插入到数据库中的时间都是utc时间，晚8小时，修改两处就差不多正常了：）编辑config/application.rb，我用的是Rails3.2.1


{% codeblock lang:ruby %}
config.active_record.default_timezone = :local  
config.time_zone = 'Beijing'
{% endcodeblock %}

为何我说差不多呢，原因如下：


{% codeblock lang:ruby %}
irb(main):001:0> Fpwd.store(1)
 Fpwd Load (0.2ms)  SELECT "fpwds".* FROM "fpwds" WHERE "fpwds"."user_id" = 1 LIMIT 1
 SQL (2.7ms)  DELETE FROM "fpwds" WHERE "fpwds"."user_id" = 1
  (0.1ms)  begin transaction
Binary data inserted for `string` type on column `randstring`
 SQL (429.6ms)  INSERT INTO "fpwds" ("created_at", "randstring", "updated_at", "user_id") VALUES (?, ?, ?, ?)  [["created_at", Wed, 15 Feb 2012 14:29:35 CST +08:00], ["randstring", "87e685e0d2ab37143fae248083822ffea600f577"], ["updated_at", Wed, 15 Feb 2012 14:29:35 CST +08:00], ["user_id", 1]]
  (1.4ms)  commit transaction
=<Fpwd user_id: 1, randstring: "87e685e0d2ab37143fae248083822ffea600f577", created_at: "2012-02-15 06:29:35", updated_at: "2012-02-15 06:29:35">
{% endcodeblock %}
最后的返回值那里还是晚了8小时，我用sqlite3查看的时候时间是正常的，所以这里怀疑是ruby的时间问题了，好在app中已经正常！