---
layout: default
title: "Brixel CTF winter edition 2020 wp"
tags: ctf
---

# Brixel CTF winter edition 2020

> 题目花样非常有意思，虽然题目难度不算太高，但是因为某些不可抗力的因素止步前一百了。出题人环境配的也是非常厉害，之前划过的大小比赛基本上都是用docker搭建的同一个服务器分了若干个端口，头一次见这种把题目直接搭在了出题人战队主页的子目录下的，而且保护的非常到位。

### Programming（编程）

##### keep walking

![keep_walking](/images/brixel/keep_walking.png)

程序要求很简单，奈何自己没文化，一段shell走天下。

```shell
#!/bin/bash

answer1=1
for((x=1;x<=525;x++))
do
    y=$x
    let answer=$x*$y+$answer1+3
    echo "$answer = $x * $y + $answer1 +3"
    answer1=$answer
done
```

##### A song

![a_song](/images/brixel/a_song.png)

题目说是写了首歌，但是歌词很烂（这里出题人是根据一种用歌词写程序的编程语言）

```
(intro)
Shout "brixelCTF{" !!!

Brixel is a hackerspace
It's not like any other place

Your skill is hopefully the best
This CTF is the test
put your skill into the test
(-and-) let your score be "blessed"

(chorus)
The challenges are serious
Your skill is mysterious
Build your skill up, up, up (-up,up-)
Knock the challenges down
your skill is true,
your skill is right!
Knock the challenges down
your score is taking flight!

(verse1)
put This CTF into your skill
put Brixel into your Heart (-or not, hey! just chill!-)

the hype is getting to the top,
the beat is ready to drop,
build the hype up!
build the hype up!
build the hype up!

whisper the challenges,
say your score,
Shout the hype, (-and-)
SCREAM YOUR SKILL! (-m-M-M-MONSTERKILL!!-)

(chorus)
The challenges are serious
Your skill is mysterious
Build your skill up, up, up (up,up)
Knock the challenges down
your skill is true,
your skill is right!
Knock the challenges down
your score is taking flight!

(verse2)
Happy Holidays is a wish,
Brixel is wishing you today
Santa is now leaving
(-riding on his sleigh-)

This was fun
This was grand
Turn up your score
Turn up your skill

put your heart into your skill
put your skill into the test
say your score (-because you ARE the best-)

Say Happy Holidays
Say Brixel and "}"

(fin)
```

知道题目立意之后，搜索得到：https://codewithrockstar.com/online

运行即可得到flag

![a_song2](/images/brixel/a_song2.png)

##### QuizB0t

![quiz_bot](/images/brixel/quiz_bot.png)

题目要求答对1000道题即可获取flag，出题人具体要求的编程思路我不是很懂。但是奈何自己没文化，全靠fuzz走天下。

<img src="/images/brixel/quizbot2.png" alt="quizbot2" style="zoom:80%;" />

若是输入错误答案，上一题的正确答案会在下一题时给出。根据这一特性，使用Burp的intruder获取正确答案。

在提交的答案处设置标记，payload类型为数字，条数要>=1000，或者任意条数大于等于1000的字典都可以。

![quizbot3](/images/brixel/quizbot3.png)

使用grep extract对响应包中答案的位置进行匹配

![quiz4](/images/brixel/quiz4.png)

将结果中的答案制作成字典后重置题目的进度再次暴破即可

![quiz5](/images/brixel/quiz5.png)

----

### Forensics（取证）

##### A message from space

![message_space](/images/brixel/message_space.png)

一段音频，听着耳熟，直接上app Robot36

![a_message_from_space](/images/brixel/a_message_from_space.png)

##### Lottery ticket

<img src="/images/brixel/lottery_ticket.png" alt="lottery_ticket" style="zoom:80%;" />

中奖彩票，但是出题人不傻，觉得这张彩票被做了手脚，找到被ps过得数字加和即为flag。

直接丢入steg中灰阶位图分隔即可

<img src="/images/brixel/lottery2.png" alt="lottery2" style="zoom:80%;" />

##### Lost evidence

<img src="/images/brixel/lost_evidence.png" alt="lost_evidence" style="zoom:80%;" />

帮忙找到磁盘中快递小哥不小心删除的可疑证据。

压缩包解压后发现磁盘镜像文件，挂载后发现其中并无任何内容，使用数据恢复软件对其进行恢复。

![evidence1](/images/brixel/evidence1.png)

![evidence2](/images/brixel/evidence2.png)

![evidence3](/images/brixel/evidence3.png)

误删除文件为一段通话录音，其中包含手机拨号按键音，内容如下

![evidence4](/images/brixel/evidence4.png)

其中包含了一段留言内容，加密方式为多点击电话加密，使用解密工具解密![evidence5](/images/brixel/evidence5.png)

明文为“THX FOR THE COCAINE BRUH”（感谢你的高纯可卡因）这里flag就是可卡因的单词。

----

### OSINT（情报收集）

##### A quick search

<img src="/images/brixel/quick_search.png" alt="quick_search" style="zoom:80%;" />

题目给出一张图片，要求说出图片中塔的名字。奈何自己没文化，全靠百度走天下。

百度识图，Eben_Ezer Tower

![quick_search2](/images/brixel/quick_search2.png)

##### Manhunt#1

<img src="/images/brixel/manhunt1.png" alt="manhunt1" style="zoom:80%;" />

出题人说了一个悲惨的故事，让我们把照片的始作俑者找出来。

右键图片属性就看出来了。![manhunt12](/images/brixel/manhunt12.png)

##### Manhunt#2

![manhunt20](/images/brixel/manhunt20.png)

要求我们找出这家伙上次是在谁的手底下做事。名字已经知道了，可以直接在领英查到他的状态。特意查了下“Zelfstandige”的意思是自雇，所以flag为上一家的“pishapasha”

![manhunt22](/images/brixel/manhunt22.png)

##### Manhunt#4

![manhunt40](/images/brixel/manhunt40.png)

题目要求我们找出他的生日，前面的领英页面中有他的推特链接，科学上网在网页端关注下他就可以看到生日了

##### Manhunt#5

![manhunt50](/images/brixel/manhunt50.png)

科学上网后看到他的推特里面说他把自己网站的测试页给删除了，题目让我们给再找回来。

![manhunt55](/images/brixel/manhunt55.png)

推文里面他自以为把站点页面源文件给删除掉了，就没人找得到了“good thing the internet isn't archived, right?”。在OSINT里面，针对某一站点的情报收集，除了常规渗透测试要做的信息收集外，还包含了站点历史快照等的收集。根据URL“http://www.howitshould.be/test-page”寻找站点快照即可发现flag。

<img src="/images/brixel/manhunt56.png" alt="manhunt56" style="zoom:80%;" />

##### Manhunt#6

<img src="/images/brixel/manhunt60.png" alt="manhunt60" style="zoom:80%;" />

题目要求我们给出用户对他Web工作的评价。

打开他站点的主页就看到了几个看不懂的话，翻译过来之后有一个词，诗意：poetry

<img src="/images/brixel/manhunt66.png" alt="manhunt66" style="zoom:80%;" />

##### Manhunt#7

<img src="/images/brixel/manhunt70.png" alt="manhunt70" style="zoom:80%;" />

找出这人的住址。在此人个人主页上有一个联系方式页，进入联系页后根据联系要求输入提交后即可获得住址。

<img src="/images/brixel/manhunt71.png" alt="manhunt71" />

<img src="/images/brixel/manhunt77.png" alt="manhunt72" style="zoom:80%;" />

##### Manhunt#9

<img src="/images/brixel/manhunt90.png" alt="manhunt90" style="zoom:80%;" />

Auth，得咱们自己干了。在他个人主页下方的左下角有个非常小的“Auth”，点击进去后发现这小子是个文明人。

<img src="/images/brixel/manhunt91.png" alt="manhunt91" />

<img src="/images/brixel/manhunt92.png" alt="manhunt91" style="zoom:80%;" />

查看源码，发现猫腻，由此打开github里的auth.php

<img src="/images/brixel/manhunt93.png" alt="manhunt93" />

<img src="/images/brixel/manhunt94.png" alt="manhunt93" style="zoom:80%;" />

源码里的密码已经被删除了，通过git的历史记录找回最初的文件即可找回密码，回到原站点登录即可获取flag。

![manhunt95](/images/brixel/manhunt95.png)

<img src="/images/brixel/manhunt96.png" alt="manhunt96" />

<img src="/images/brixel/manhunt97.png" alt="manhunt96" style="zoom:80%;" />

##### BirdCall

<img src="/images/brixel/birdcall1.png" alt="birdcall1" style="zoom:80%;" />

这题要让我们通过一段鸟叫声来判断鸟的种类，并说出它的拉丁名称。

上法宝

<img src="/images/brixel/birdcalll2.png" alt="birdcall3" style="zoom:80%;" />

![birdcalll2](/images/brixel/birdcall3.png)

flag揍是"ciconia ciconia"

-----

### Internet（Web）

##### Easy

<img src="/images/brixel/easy1.png" alt="easy1" style="zoom:80%;" />

回到主页查看页面源代码就可以啦

<img src="/images/brixel/easy2.png" alt="easy2" style="zoom:80%;" />

##### Hidden Code

<img src="/images/brixel/hiddencode1.png" alt="hiddencode1" style="zoom:80%;" />

题目中给出了出题人团队的主页，让我们输入一段神秘代码，这时页面走过的人物名称就是flag

看到主页

<img src="/images/brixel/hiddencode2.png" alt="hiddencode2" style="zoom:80%;" />

啥叫“konami code”（上上下下左右左右BA）

<img src="/images/brixel/hiddencode3.png" alt="hiddencode3" style="zoom:80%;" />

回到主页中输入神秘代码，flag就是mario

<img src="/images/brixel/hiddencode4.png" alt="hiddencode4" style="zoom:80%;" />

##### robotpia

<img src="/images/brixel/robotpia1.png" alt="robotpia1" style="zoom:80%;" />

在君子协议“robots.txt”里面找到了flag

<img src="/images/brixel/robotpia2.png" alt="robotpia2" />

<img src="/images/brixel/robotpia3.png" alt="robotpia2" style="zoom:80%;" />

##### Discord（签到）

进入到比赛的Discord查看规则即可

<img src="/images/brixel/rule.png" alt="rule" style="zoom:80%;" />

##### login1

<img src="/images/brixel/login10.png" alt="login10" style="zoom:80%;" />

前端认证，密码就在js脚本里面，查看页面源代码

<img src="/images/brixel/login11.png" alt="login11" style="zoom:80%;" />

##### login2

<img src="/images/brixel/login2.png" alt="login2" style="zoom:80%;" />

依然前端认证，这次难度升级只是将原本的密码切片了，按照正确顺序拼回去就行。

##### login3

<img src="/images/brixel/login3.png" alt="login3" style="zoom:80%;" />

这次又是通过本地文件的形式将密码保存到password.txt里面了

##### login4

<img src="/images/brixel/login4.png" alt="login4" style="zoom:80%;" />

将放在password.txt的密码base64解码即可

##### login5

<img src="/images/brixel/login50.png" alt="login50" style="zoom:80%;" />

这次又把密码放回了前端页面中，只不过看上去花哨了许多。通过设置一个字母表数组，然后在按位取出对应字母累加。这里直接把密码弹出来即可。

<img src="/images/brixel/login51.png" alt="login51" style="zoom:80%;" />

##### Browsercheck

<img src="/images/brixel/browsercheck1.png" alt="browsercheck1" style="zoom:80%;" />

该题要求我们修改浏览器请求中的"user-agent"，这里将此修改为页面要求的即可

<img src="/images/brixel/browsercheck2.png" alt="browsercheck2" />

<img src="/images/brixel/browsercheck3.png" alt="browsercheck2" style="zoom:80%;" />

##### Readme（签到）

阅读比赛的新手指引，最下面就免费送分

<img src="/images/brixel/readme.png" alt="readme" style="zoom:67%;" />

##### SnackShack awards

![snack](/images/brixel/snack.png)

打开页面后是个小吃店投票页面，通过Burp直接给它来个5000票

<img src="/images/brixel/SnackShack.png" alt="SnackShack" style="zoom:80%;" />

##### Flat earth

<img src="/images/brixel/faltearth1.png" alt="faltearth1" style="zoom:80%;" />

题目给出了一个信仰地球是平的网站，让我们进入到他的管理页面

通过页面源代码或目录爆破可知道管理页面为admin.php

<img src="/images/brixel/flatearth2.png" alt="flatearth2" style="zoom:80%;" />

进入到登录页面后，爆破用户名时发现sql注入万能口令就进去了

<img src="/images/brixel/flatearth3.png" alt="flatearch4" style="zoom:80%;" />

<img src="/images/brixel/flatearch4.png" alt="flatearth3" style="zoom:80%;" />

##### Hiding in the background

<img src="/images/brixel/hidebackground.png" alt="hidebackground" style="zoom:80%;" />

题目提示说主页背景图片中藏了一个flag，将背景图片下载下了后，使用图像编辑软件打开，将图片上层图层移走就看到flag了

<img src="/images/brixel/hidebackground1.png" alt="hidebackground1" style="zoom:80%;" />

##### Pathfinder#1

又给出了一个不正经邪教网站，还是要进入它的管理页面，这次直接就告诉了管理登录在哪了

<img src="/images/brixel/pathfind10.png" alt="pathfind10" style="zoom:80%;" />

通过浏览其他页面，从url处发现可能会存在本地文件读取的问题

<img src="/images/brixel/pathfind11.png" alt="pathfind11" style="zoom:80%;" />

打开admin登录，发现并非是通过一个登录页进行登录，而是使用了Apache自己的的认证方式，在进行站点目录爆破是也发现admin目录下存在“.htaccess”和“.htpasswd”，这两个文件是配置Apache站点目录访问保护而存在的文件。

![pathfind12](/images/brixel/pathfind12.png)

这里比暴力破解更加有效的方式就是通过本地文件读取直接读取admin目录下的“.htpasswd”文件

<img src="/images/brixel/pathfind13.png" alt="pathfind13" style="zoom:80%;" />

##### Pathfinder#2

<img src="/images/brixel/pathfind20.png" alt="pathfind20" style="zoom:80%;" />

注意题目下方的这一行小字，特意强调了php版本为低于5.4.3的，意味着这里存在nulltype注入问题，使用“%00.php”截断文件后缀读取“.htpasswd”

<img src="/images/brixel/pathfind22.png" alt="pathfind22" style="zoom:80%;" />

----

### Reverse engineering / cracking（逆向/破解）

##### Cookieee!

修改程序运行内存中的数据到百万即可

![cookiee](/images/brixel/cookiee.png)

##### no peeking!

.Net反编译后直接在代码文件中查找flag相关字符串即可

##### android app

app反编译后同样直接在代码文件中查找flag相关字符串即可

----

### Old tech

##### punchcard

早期计算机使用的打孔散点图，上法宝

<img src="/images/brixel/punchcard.png" alt="punchcard" style="zoom:80%;" />

##### Goodbye old friend

一道向刚刚逝去的flash致敬的题目，用flash打开查看元件即可

<img src="/images/brixel/goobye_friends.png" alt="goobye_friends" style="zoom:80%;" />

##### The tape（看了Hint才知道，年轻人根本不会做）

cassette tape揍是磁带，只不过在80年代除了常见的音乐和影像，一些系统、程序和游戏也是把磁带作为载体的。就算是装有程序的磁带放入复读机里面也会出声音，不过有点太好听了就是了。通过翻录这种声音也就完成了程序的拷贝。

使用Audiotap软件将题目所带的音频文件转为磁带格式

![ctf_tape1](/images/brixel/ctf_tape1.png)

使用C64 forever模拟器加载磁带文件

![ctf_tape2](/images/brixel/ctf_tape2.png)

---

### Cryptography（密码学解密）

##### Sea code

听着耳熟，摩斯密码，上法宝

<img src="/images/brixel/seacode.png" alt="seacode" style="zoom:80%;" />

##### Merde

<img src="/images/brixel/merde1.png" alt="merde1" style="zoom:80%;" />

法国人，维吉尼亚密码，上法宝

<img src="/images/brixel/merde2.png" alt="merde2" style="zoom:80%;" />

##### Merda

<img src="/images/brixel/merda1.png" alt="merda1" style="zoom:80%;" />

意大利人，罗马数字5，凯撒密码，上法宝

<img src="/images/brixel/merda2.png" alt="merda2" style="zoom:80%;" />

##### shit

![shit](/images/brixel/shit.png)

base64解码后，在由二进制转字符串

##### Scheiße

<img src="/images/brixel/enigma.png" alt="enigma" style="zoom:80%;" />

德国人，二战，特殊机器，恩尼格码机，上法宝

<img src="/images/brixel/enigma2.png" alt="enigma2" style="zoom:80%;" />

##### flawed

MD5解密即可

<img src="/images/brixel/flawed.png" alt="flawed" style="zoom:80%;" />

##### Don't be salty

加盐MD5

<img src="/images/brixel/salty.png" alt="salty" style="zoom:80%;" />

---

### Steganography

##### Doc-ception

将word文件后缀改为zip后解压，将解压出的word文件后缀改为zip后解压即可发现flag

<img src="/images/brixel/doc_word.png" alt="doc_word" style="zoom:80%;" />

##### Limewire audio

甜甜的小曲儿，用Audacity打开后查看频谱，flag就是hello kitty

<img src="/images/brixel/sweet_song.png" alt="sweet_song" style="zoom:80%;" />

##### Scan me

依次分别是扫描二维码、code128条形码、Ean13条形码、PDF417条形码即可获取falg

##### Rufus the vampire cat

<img src="/images/brixel/rufus.jpg" alt="rufus" style="zoom:80%;" />

直接用steghide解开了

![rufus1](/images/brixel/rufus1.png)