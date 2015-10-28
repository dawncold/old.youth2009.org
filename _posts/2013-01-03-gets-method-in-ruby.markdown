---
layout: post
title: "gets method in ruby"
date: 2013-01-03 20:40
comments: true
categories: study ruby
---

**Important**: Also notice that we're using STDIN.gets instead of plain 'ol gets. That is because if there is stuff in ARGV, the default gets method tries to treat the first one as a file and read from that. To read from the user's input (i.e., stdin) in such a situation, you have to use it STDIN.gets explicitly.
