---
layout: post
title: "linux-study"
date: 2014-11-22 14:14:25 +0800
comments: true
categories: study
---

directory permission x means this directory can be work directory, if you want to write or read a file behind this directory, you must have permission x of this directory.

directory permission w means you can delete or create files or directories behind this

usr = unix software resource

"-" means last work directory(cd /mnt;cd;cd -)

umask means default permission minus this mask, e.g default new directory 777, if mask is 022, then you will get 777-022——>755 directory; default new file 666, is mask is 002, then you will get 666 - 002——>664 file. mask only can be set in (1, 2, 4) every bit, one bit means the sum of one permission group(current/group/others). umask is based on user, default root has a 0022 mask, normal user has a 0002 mask.

lsattr/chattr is available on ext2/ext3 filesystem, add ‘+i’ attribute can lock one file, no edit or delete, even you are root, ‘+a’ attribute can let a file only accept append content, etc.

SUID, SGID, SBIT special permission:
there is a ’s’ on x position of user part, like ‘rws- - - - - -‘. SUID can only set to binary program, if user has x permission of this binary, it can temporarily get the owner permission of this binary, e.g binary ‘passwd’ and /etc/shadow file, shadow only can be updated by root, but every user can change their password via ‘passwd’, it means the user temporarily get owner(root) permission by SUID special permission.
SGID similar as SUID, there will be a ’s’ on x position of group part like ‘rwx- - s - - x’. if a user can execute binary, he will temporarily get owner permission, e.g binary ‘locate’ and file ‘mlocate.db’. SGID can be set on a directory, it means if a user have r and x permission of one directory, and ’s’ set on this directory, this user can create a file which owner group is this directory’s.
SBIT(Sticky BIT) only set to directory, if a directory has this permission, a user who can create file or directory on this directory, the new file or new directory can only delete by root or himself, e.g /tmp directory, root can delete your new file, and you can also delete it, but others can not.
SUID = 4, SGID = 2, SBIT = 1, chmod x755 xxx_file, x means sum of SUID, SGID, SBIT, if omit, this bit is zero, if you set a invalid SUID/SGID/SBIT, there will be upper case S/T, lower case is valid.

find / -size 1M -exec ls -l {} \;     {} means the args from find, “\;” means the end of “exec”, commands in exec can not use alias.

