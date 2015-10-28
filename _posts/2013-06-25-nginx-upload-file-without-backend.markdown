---
layout: post
title: "nginx-upload-file-without-backend"
date: 2013-06-25 23:09
comments: true
categories: dev nginx
---

以前用了nginx-upload-module，不过这个module的作者不打算继续更新了，导致nginx版本高于1.3.9就无法使用这个module来处理上传文件。本着不引入更多依赖并且使用一个比较成熟方法的前提，只有client_body_in_file_only，这是nginx buildin方法。

原本用upload-module的时候在location / 中有个if，如果发现有multipart就会处理一下，再pass回去。处理完后会多出两个参数，比如image.name和image.path，其中image是file input的name。然后back-end就直接那path和name来处理文件了，临时文件会放在一个固定的地方。

由于client_body_in_file_only只能放在server、http、location中，得专门建立一个location而不能放在if中。

{% codeblock %}
location ^~ /upload/ {
  client_body_temp_path      /tmp/;
  client_body_in_file_only   on;
  client_body_buffer_size    128K;
  client_max_body_size       1000M;

  proxy_pass_request_headers on;
  proxy_set_header           X-FILE $request_body_file; 
  proxy_set_body             off;
  proxy_redirect             off;
  proxy_pass                 http://backend/
}
{% endcodeblock %}
这样以upload开头的就会做这样处理，上传的文件path会放在header中，至于name该怎么办，我是把name的值作为query string拼在了form的action中，在上传开始前得到文件名，然后拼上去。

需要注意的是，client_body_in_file_only不支持RFC2388，也就是说multipart不管用，你可以考虑用ajax上传插件来做上传，注意插件里的multipart设为false。上传插件推荐JQuery-File-Upload。

依赖，越少越好。