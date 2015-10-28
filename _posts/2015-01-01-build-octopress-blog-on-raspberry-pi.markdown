---
layout: post
title: "host-octopress-blog-on-raspberry-pi"
date: 2015-01-01 20:25:24 +0800
comments: true
categories: play
---

First post on 2015!

I have a raspberry pi several months ago, and I often use it to recording temp and humidity, uploading to a cloud host, but after a home movement, it had been stored in my drawer. Last day of 2014, while waiting 2015, I want build it and host an external disk for MacBookPro backup(Time Machine), but failed for power supply, normal power supply is not enough for raspi, so I should buy another USB Hub powered by itself.

My raspi used a wireless NIC to connecting with my router(OpenWrt), but I want use a ethernet cable for it, so it can get a unique IP on Internet, but when I pluged it, the wireless NIC would down, because of ifplugd or something else, so I keep the wireless NIC working and add some rules on route, port forward, WAN 80 to rasp 80, WAN 443 to rasp 443.

Install nginx via`sudo apt-get install nginx`, remove default site`rm /etc/nginx/sites-enable/default`, add conf in `/etc/nginx/conf.d`, like this:

{% codeblock %}
server {
	listen 80;
	server_name dawncold.me;
	return 301 https://$server_name$request_uri;
}

# HTTPS server

server {
	listen 443 ssl;
	server_name dawncold.me;

	root /usr/share/nginx/dawncold.me;
	index index.html index.htm;

	ssl on;
	ssl_certificate /usr/share/nginx/dawncold.me/dawncold.me.crt;
	ssl_certificate_key /usr/share/nginx/dawncold.me/dawncold.me.key;

	ssl_session_timeout 5m;

	ssl_protocols SSLv3 TLSv1;
	ssl_ciphers ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv3:+EXP;
	ssl_prefer_server_ciphers on;

	location / {
		try_files $uri $uri/ =404;
	}
}
{% endcodeblock %}

I got a SSL certificate from nc.me(github student pack), so I rewrite HTTP to HTTPS.

start nginx via `sudo nginx` or reload config via `sudo nginx -s reload`.

Oh, your should update your domain A record to your router WAN ip address, you can write a script or use your router buildin DDNS function.

Octopress supported rsync publishment, so edit your Rakefile and enter your raspi ssh account and nginx html root path, like `/usr/share/nginx/www`.

publish to github and rasp: `rake gen_deploy rsync` or only to raspi: `rake rsync`.