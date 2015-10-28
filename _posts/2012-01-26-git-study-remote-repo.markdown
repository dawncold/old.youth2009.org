---
layout: post
title: Git使用重新学习（远程仓库）
comments: true
date: 2012-01-26 16:08
categories: git study
---

查看当前远程仓库：git remote  -v，加上-v属性能看得内容详细一些。

添加远程仓库：git remote add [shortname] [url]

有了shortname，就相对于给仓库了一个别名，以后可以用别名操作，git fetch xx即可

get fetch xx是获取远程仓库中有而本地没有的数据

提送数据到远程仓库用：git push remote-name branch-name，推送的时候要注意必须没有他人在推送，且没有其他更新才行，如果他人推送了不少更新，你需要先得到更新，合并后再推送。（这里并不是说和svn一样了，只是你可以自己先在本地提交，但推送到远程服务器上时，需要按照先来后到的原则，保证每个人的提交是不冲突的，是最新的。这是我个人的理解）

远程仓库重命名、删除：git remote rename short-name new-name，git remote rm xx

另外git remote show repo-name能够得到不少信息，有哪些要合并啦，哪些已经删除啦，哪些新仓库出现啦等等，这个是需要连接服务器获取的。