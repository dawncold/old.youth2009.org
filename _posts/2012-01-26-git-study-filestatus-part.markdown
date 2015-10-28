---
layout: post
title: Git使用重新学习（文件状态）
comments: true
date: 2012-01-26 14:47
categories: git study
---

就几个简单的git命令记录一下自己的学习过程，我发现如果自己不随时记录自己学到的东西就会遗忘。

对于一个文件，如果没有被git跟踪，那必然是untracked状态，只有已经是tracked状态后才会有后面的三种状态（unmodified、modified、staged（暂存状态））。

此时你如果add了一个文件进入git，那么git就会开始跟踪，那么此时这个文件是tracked状态，但没有修改，查看状态（git status）会现实new file：xxx，此时提交（commit）就会把文件快照放入历史记录中了。这里的add意思是放入暂存区，后面的add还有不同的意思。

对于已经跟踪的文件，我们修改后再查看状态，就会发现刚刚的文件被放入了一个modified那行中，样子大概是这样的：modified：xxx，同时观察一下上面几行，有这样的提示“Changed but not updated:”，意思就是修改了，但没有放入暂存区，此时需要add的另一层意思——把已修改但没放入暂存区的文件放入暂存区。

git commit -a 选项可以跳过暂存过程，直接把已经跟踪的文件放入历史记录中。

总之就是及时看status，并且要看里面的提示，只有changes to be committed后面的文件才会在commit的时候加入到历史记录中。

删除和移动文件：git rm，git mv。

改名操作与linux下的mv命令用法一样。

删除时如果仅仅希望在git中删除，实际仍然保存文件那么加上--cached选项即可。