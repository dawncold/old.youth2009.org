---
layout: post
title: Git使用重新学习（分支）
comments: true
date: 2012-01-26 19:36
categories: git study
---

在git中分支是一个变态技能！

创建分支：git branch [branch-name]即可。

git中有个叫master的分支，这是默认的，刚刚创建了一个testing分支，所以这两个指向是一样的，因为刚刚就在master分支下。但是git为何知道我在master呢？因为还有个叫HEAD的默认指针指向了当前正在使用的分支，所以当你切换分支的时候HEAD就会指向新的地方。

切换分支：git checkout [branch-name]（git checkout -b [branch-name]可以实现新建并切换到此分支）切换分支时最好保持暂存区清洁，否则有可能产生冲突阻止你切换。

当我们切换到了testing分支后，再做一些提交，我们的testing分支会继续往下走，但master分支还停留在刚才离开的地方，如果我们需要回去，只需要再切换回master分支即可屏蔽刚才所作的提交，保持文件的原始性。

合并分支：git merge [branch-name]，把分支合并到你现在所在的那个分支中，可别合并反喽，当然我感觉反了也没关系，就是个名字的问题吧？

分支删除用-d开关，git branch -d [branch-name]即可。

合并分支的时候遇到冲突是不可避免的，有些冲突能够自动解决，但还有不少是需要我们手动解决的，此时git会在status中告诉我们，我们打开后就能看到由“=====”分割开的两部分，就是让我们选择，等手动修改好后需要再add进暂存区，此时就能提交了。