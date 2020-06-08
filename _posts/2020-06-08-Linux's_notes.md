---
layout: default
title: "闲暇时间从阿里云大学记的Linux笔记"
tags: 基础知识笔记
---
# Linux 常用基础操作命令

#### 快速上手：

##### 文件目录管理命令：

**`tree`**  用于以树状图列出目录的内容

示例：**`tree /usr/share/wallpapers`**

**`ls`** : 用于显示指定工作目录下的内容

命令格式：**`ls [参数] [目录名]`**

示例：**`ll -a`**

**`pwd`**：获取当前工作目录的绝对路径

**`cd`** ：用于切换工作目录

示例：**`cd /usr/local/etc`** 、**`cd ../..`**

**`touch`**: 用于修改文件或者目录的时间属性，包括存取时间和更改时间。若文件不存在系统会创建一个新文件。

命令格式：**`touch [参数] [文件]`**

示例：**`touch demo1.txt demo2.txt`**创建两个空文件

​			**`touch demo1.txt`**修改demo1.txt的时间记录为当前系统时间

​			**`touch -r demo1.txt demo2.txt`**更新demo2.txt的时间记录，使其和demo1.txt的时间记录相同

**`mkdir`**：用于新建子目录，-p 参数确保目录名称存在，不存在就新建一个

示例：**`mkdir -p a/b/c/d`**

**`rm`**：用于删除一个文件或者目录

命令格式：**`rm [参数] [文件]`**

示例：**`rm -rf demo*`**无需曲儿直接删除文件及其目录下的所有子目录文件

**`cp`**：主要用于复制文件或目录

命令格式：**`cp [参数] [源文件] [目标文件]`**

示例：**`cp -r c a/b/`**将c复制到目录a/b下

**`mv`**：用来为文件或目录改名、或将文件或目录移入其他位置

命令格式：**`mv [参数] [源文件] [目标文件]`**

示例：**`mv a.txt b.txt`**将文件名a.txt改为b.txt

​			**`mv c a/b/c/d/`**将c移动到a/b/c/d下

​			**`mv ./* /tmp`**将当前目录内容全部移动到/tmp目录下

**`rename`** 用字符串替换的方式批量改变文件名

示例：**`rename demo DEMO *`** 将所有文件名中的字符串demo改为大写的字符串DEMO

​			**`rename .txt .text *`**将当前目录下的所有.txt文件后缀都改为text

##### 文件权限管理：

ls命令可以查看Linux系统上的文件、目录和设备的权限

**`ls -l /boot/`**

**`chmod`** 用于修改文件权限mode，-R 参数以递归方式对子目录和文件进行修改

示例：**`chmod u+x test.sh`**将test.sh文件增加属主的执行权限

​			**`chmod u-x test.sh`** 撤销test.sh文件属主的执行权限

​			**`chmod 744 test.sh`**将test.sh文件权限修改为八进制表示的744权限

**`chown`**修改文件的属主和属组，-R 参数以递归的方式对子目录和文件进行修改；**`ls -l`**命令显示的第三、四列就是文件的属主和属组信息。**`chgrp`** 用于修改文件的属组。

##### 文本处理：

**`cat`** 用于查看内容较少的纯文本文件

命令格式：**`cat [选项] [文件]`**

示例：**`for i in $(seq 1 10); do echo $i >> test.txt ; done`**将一个自增序列写入文件中，**`cat test.txt`**查看文件内容

​			**`cat /dev/null > test.txt`**将文件内容清空

**`more`**从前往后分页显示文件内容

示例：**`more +20 /var/log/messages`**从第20页开始分页查看系统日志文件

**`less`** 可以对文件或其他输出进行分页显示，与more命令类似，但是用less可以随意浏览文件，more仅能向前移动，却不能向后移动。

命令格式：**`less [参数] [文件]`**

示例：**`history | less`** 查看命令历史记录并通过less分页显示

**`head`** 用于查看文件开头指定行数的内容

命令格式：**`head [参数] [文件]`**

示例：**`head -5 /etc/passwd`** 查看/etc/passwd文件的前5行内容

**`tail`** 用于查看文档的后N行或持续刷新内容

命令格式：**`tail [参数] [文件]`**

示例：**`tail -f -n 10 /var/log/messages`**查看/var/log/messages系统日志文件的最新10行，并保持实时刷新

**`stat`** 用来显示文件的详细信息，包括inode、atime、mtime、ctime等

示例：**`stat /etc/passwd`** 查看/etc/passwd文件的详细信息

**`wc`** 用于统计指定文本的行数、字数、字节数

命令格式：**`wc [参数][文件]`**

示例：**`wc -l /etc/passwd`**统计/etc/passwd文件的行数

**`file`** 用于辨识文件类型

命令格式：**`file [参数] [文件]`**

示例：**`file /var/log/messages`**查看/var/log/messages文件的文件类型

**`diff`** 用于比较文件的差异

##### 文本文件处理命令：

**`grep`** 用于查找文件里符合条件的字符串

命令格式：**`grep [参数] [正则表达式] [文件]`**

示例：**`grep -n Port /etc/ssh/ssh_config`**查看sshd服务配置文件中监听端口配置所在行编号

​			**`grep -c localhost /etc/hosts`** 查询字符串在文本中出现的行数

​			**`ps -ef | grep sshd`**`ps -ef | grep -v grep | grep sshd`**反向查找，不显示符合条件的行

​			**`grep -r *.sh /etc`**以递归方式查找目录下含有关键字的文件。

​			**`grep 'ntp[0-9].aliyun.com' /etc/ntp.conf`**使用正则表达式匹配httpd配置文件中异常状态码响应的相关配置

**`sed`** sed是一种流编辑器，能够完美的配合正则表达式使用。sed命令不会修改原文件，例如删除命令只表示某些行不打印输出，而不是从源文件中删去。如果要改变源文件，需要使用-i选项。

命令格式：**`sed [参数] [动作] [文件]`**

示例：**`sed '3,$d' /etc/passwd`** 删除第三行到最后一行内容

​			**`sed '$a admin:x:1000:1000:admin:/home/admin:/bin/bash' /etc/passwd`** 在最后一行新增

​			**`sed 's/SELINUX=disabled/SELINUX=enforcing/' /etc/selinux/config`** 替换内容

​			**`sed '1c abcdefg' /etc/passwd`**替换行

**`awk`** 和sed命令类似，awk命令也是逐行扫描文件，寻找含有目标文本的行，如果匹配成功，则会在该行上执行用户想要的操作，反之，则部队其进行任何处理

命令格式：**`awk [参数] [脚本] [文件]`**

示例：**`ifconfig eth0 | awk '/inet/{print $2}'`** 查看本机IP地址

​			**`df -h | awk '/\/$/{print $4}'`** 查看本机剩余磁盘容量

​			**`awk -F: '$3<1000{x++} END{print x}' /etc/passwd`** 统计系统用户个数

​			**`head -3 /etc/passwd | awk  'BEGIN{FS=":";print "name\tuid"}{print $1,"\t"$3}END{print "sum lines "NR}`**输出/etc/passwd文件中前三行记录的用户名和用户uid

​			**`awk -F: '$7!~/nologin$/{print $1,$7}' /etc/passwd`** 输出其中登录Shell不以nologin结尾（对第七个字段做!~反向匹配）的用户名、登录Shell信息。

​			**`netstat -na | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'`** 查看tcp连接数。

​			**`ps -ef | grep httpd | awk {'print $2'} | xargs kill -9`** 关闭指定服务的所有的进程

**`cut`** 主要用来切割字符串，可以对输入的数据进行切割然后输出

命令格式：**`cut [参数] [文件]`**

示例：**`echo "hello world" | cut -b 1,3`** 、**`echo "hello world" | cut -b 1-3`** 按字符进行切割

​			**`echo "hello world" | cut -c 1,3`** 、**`echo "hello world" | cut -c 1-3`** 、**`echo "h和o" | cut -c 2`** 按字符进行切割

​			**`echo "hello,world,ok" | cut -d , -f 1,3`** 、**`echo "hello,world,ok" | cut -d , -f 2-3`** 按指定字符进行切割

**`tr`** 用于对来自标准输入的字符进行替换、验证和删除

命令格式：**`tr [参数] [文本]`**

示例：**`echo "HELLO WORLD" | tr 'A-Z' 'a-z'`**将输入字符由大写转换为小写

​			**`echo "hello 123 world 456" | tr -d '0-9'`** 删除字符

​			**`echo "thissss is     a text linnnnnnnne." | tr -s ' sn'`** 压缩字符

​			**`cat /dev/urandom | tr -dc a-zA-Z0-9 | head -c 13`**产生随机密码

##### 常用系统工作命令：

**`echo`** 用于在终端输出字符串或变量提取后的值

命令格式：**`echo [字符串] [$变量]`**

示例：**`echo "HELLO WORLD"`** 显示普通字符串

​			**`export name="Tom"`** 定义一个临时变量，**`echo $name`**使用echo命令将变量name的值显示到终端

​			**`echo "This is a test text." > test.txt`** 显示结果定向至文件

```bash
# 显示命令执行结果
echo `pwd`
echo $(pwd)
```

**`date`** 用于显示和设置系统的时间和日期

命令格式：**`data [选项] [+格式]`**

示例：**`date`**按照默认格式查看当前系统时间

​			**`date "+%Y-%m-%d %H:%M:%S"`** 按照指定格式查看当前系统时间

​			**`date "+%j"`** 查看今天是当年中的第几天

​			**`date -s "19700101 00:00:00"`** 设置系统时间

​			**`ntpdate time.nist.gov`**用ntpdate从时间服务器更新时间

**`wget`** 在终端中下载文件

命令格式：**`wget [参数]下载地址`**

**`ps`** 用于查看系统中的进程状态，命令格式：**`ps [参数]`**

示例：**`ps -ef |grep sshd`**

**`top`** 动态监视进程活动与系统负载等信息

**`pidof`** 用于查询指定服务进程的PID值，命令格式：**`pidof [服务名称]`**

示例：**`pidof crond`** 查询处crond服务下的所有进程ID

**`kill`**用于终止指定PID的服务进程，命令格式：**`kill [参数] [进程PID]`**

示例：**`kill -9 1247`** 删除PID为1247的进程

**`killall`** 用于终止指定名称的服务对应的全部进程，命令格式：**`kill [进程名称]`**

示例：**`killall crond`**

**`reboot`** 用于重启系统，命令格式：**`reboot [-n] [-w] [-d] [-f] [-i]`**

**`poweroff`** 用来关闭系统

##### 系统状态检测命令：

**`ifconfig`** 用于获取网卡配置与网络状态等信息

**`uname`** 用于查看系统内核与系统版本等信息，命令格式：**`uname -[amnrsv] [--help] [--version]`**

**`uptime`** 用于查看系统的负载信息

**`free`** 用于显示当前系统中内存的使用量信息，命令格式：**`free [-bhkmotV][-s <间隔秒数>]`**

**`who`**显示关于当前在本地系统上的所有用户的信息

示例：**`who`**显示当前登录系统的用户

​			**`who -l -H`** 显示用户登录来源

​			**`who -m -H`**只显示当前用户

​			**`who -q`**精简模式显示

**`last`** 用于显示用户最近登录信息

**`history`**用于显示历史执行过的命令。bash默认记录1000条执行过的历史命令，被记录在~/.bash_history文件中。

示例：**`history 10`** 显示最新10条执行过的命令

​			`history -c`** 清楚历史记录



#### ssh 基于密钥的登陆方式：

**`ssh-keygen -t rsa`** 生成一对公钥私钥

**`ssh-copy-id hostip`** 拷贝公钥到目标公钥

#### Linux中的文件上传与下载：

**`sftp`**

**`lrzsz`** 安装成功后使用 `rz` 上传文件，`sz` 下载文件

#### mount 挂载命令：

**`mount -o loop /挂载设备 /挂载目标`**

**`umount /dev/dev`**  卸载设备

#### service 命令：

**`service --status-all`**  查看系统所有的后台服务进程

**`service [servicename] status`** 查看指定的后台服务进程状态

**`service [servicename] /stop/start/restart`**  指定服务的停止/开启/重启

#### chkconfig 命令：

**`chkconfig httpd on/off`** 使 httpd 服务开机时自启/不自启

#### hostname 命令：

**`hostname`**  查看主机名

**`hostname 主机名`**  临时修改主机名

**`hostnamectl set-hostname 主机名`**  永久修改主机名

修改**`/etc/hostname`** 文件也可永久修改主机名

#### netstat 命令：

**`netstat -nltp`**  监听网络端口状态

#### crontab 定时任务：

**`crontab -l`** 查看当前用户下的定时任务状态

**`crontab -e`**  编辑定时任务配置文件

**`crontab -u user`**  指定用户定时任务

**配置文件内容举例：**（时间格式为：分时日月周）

**`*/1 * * * * date >> date.txt`** 每分钟执行一次`date`命令并将输出定向到 `data.txt`文件中

**`30 21 * * * /usr/local/etc/rc.d/httpd restart`**  每晚的21：30重启 httpd 服务

**`45 4 1,10,22 * * /usr/local/etc/rc.d/httpd restart`**  每月的1、20、22号的4：45重启httpd服务

**`10 1 * * 6,0 /usr/local/etc/rc.d/httpd restart`**  每周六周日的1：10重启 httpd 服务

**`0,30 18-23 * * * /usr/local/etc/rc.d/httpd restart`** 每天18：00至23：00之间每隔30分钟重启 httpd 服务

**`* 23-7/1 * * * /usr/local/etc/rc.d/httpd restart`**  23：00至7：00之间每隔1小时重启httpd服务

**`crontab -r`**  删除当前用户存在的定时服务

#### 监控 CPU 和 GPU的温度（需安装 lm-sensors）

**`sensord-detect`** 开启温度检测

**`sensors`** 显示当前系统硬件的温度信息

#### ps 命令

**`ps aux`** 列出当前正在运行的程序

**`ps aux --sort=%cpu | grep -m 11`**  列出当前最占资源的前十程序

#### di 磁盘信息命令

**`di`**  默认输出

**`di -A`**  打印类似挂载点、特殊设备名称等全部字段

**`di -a`**  打印所有挂载的设备

**`di -c`**  用逗号作为值的分隔符

**`di -g`**  通过千兆字节单位打印大小

**`di -l tmpfs`**  显示特定的文件系统类型的相关信息

**`di -n`**  跳过标题行的输出

**`di -t`** 在文件系统列表底部打印一行总计行

**`di -sr`**  排序输出

**`di -fm`**  指定输出格式打印挂载点的名称

#### echo 命令：

**`echo text`** 屏幕输出打印文本内容

**`echo -e "PATTERN"`** ：**\a**警报声音，**\b**退格键，**\c**不执行换行类似于**`echo -n`**，**\r**回车，**\t**制表符，**"\\"**斜线，**\0nnn**八进制，**\xnn16**十六进制

**`echo`** 中单引号存在强引用会将变量替换，双引号存在弱引用不会将变量替换为字符串，**`echo `** 单独可以分辨变量性质，**``**反向单引号内可执行命令并通过**`echo`** 输出，能够识别内涵的命令变量，**``**=$()。

### 正则表达式：

##### 字符匹配：

```bash
. #匹配单一字符例如grep "r..t" /etc/passwd
[] #匹配指定范围内的任意单个字符如[abc]、[0-9]、[a-z]例如grep "[1-4]" /etc/passwd
[^] #匹配除了指定范围内的任意单个字符
[:alnum:] #字母和数字
[:alpha:] #代表任何英文大小写字符
[:lower:] #小写字母 [:upper:] 大写字母
[:blank:] #空白字符（空格和制表符）
[:space:] #水平和垂直的空白字符
[:cntrl:] #不可打印的控制字符（退格，删除，警铃等）
[:digit:] #十进制数字 [:xdigit:] 十六进制数字
[:graph:] #可打印的空白字符
[:pring:] #可打印字符
[:punct:] #标点符号
```

##### 匹配次数：

```bash

* #匹配前面的字符任意次，包括零次 贪婪模式：尽可能长的匹配
.* #任意长度的任意字符
\? #匹配其前面的字符0或1次
\+ #匹配其前面的字符至少1次
\{n\} #匹配前面的字符n次
\{m,n\} #匹配前面的字符至少m次，至多n次
\{,n\} #匹配前面的字符至多n次
\{n,\} #匹配前面的字符至少n次
```

##### 位置锚定：

```bash
^ #行首锚定，用于模式的最左侧
$ #行尾锚定，用于模式的左右侧
^PATTERN$ #用于模式匹配整行
	^$ #空行
	^[[:space:]]*$ #空白行
\<或\b #词首锚定，用于单词模式的左侧
\>或\b #词尾锚定，用于单词模式的右侧
\<PATTERN\> #匹配整个单词
分组：\(\) #将一个或多个字符捆绑在一起，当作一个整体来处理，如\(root\)\+
分组括号中的模式匹配到的内容会被正则表达式引擎记录于内部的变量中，这些变量的命名方式为：\1,\2,\3,...
\1 #表示从左侧起第一个左括号以及与之匹配右括号之间的模式所匹配到的字符
示例： \(string1\+\(string2\)*\)
       \1：string1\+\(string2\)*
       \2：string2
后向引用：引用前面的分组括号中的模式所匹配的字符，而非模式本身
或者：\|
示例：a\|b：#a或b
      C\|cat：#C或cat
      \(C\|c\)at：#Cat或cat

```



### Linux 命令提示符：

**`cat /etc/*OS-release`** 查看当前系统运行版本

**`echo $PS1`**  显示提示符格式

**PS1="\[\e[1;5;41;33m\][\u@\h \W]\\$\[\e[0m\]"** （修改提示符格式举例）

**\e** \033

**\u** 当前用户

**\h** 主机名简称

**\H**  主机名全称

**\w**  当前工作目录

**\W**  当前工作目录基名

**\t**  24小时格式时间

**\T**  12小时格式时间

**\ !**  命令历史数

**\ #**  开机后的命令历史数



**/etc/motd** 修改此文件内容可实现用户登录后提示信息

**/etc/issue** 修改此文件内容可实现用户登录前提示信息

修改/etc/gdm/custom.conf** 配置文件内容：设置 root 账户开机自动登录

“**AutomaticLoginEnable=true**”

“**AutomaticLogin=root**”

**/etc/profile.d/** 目录下放置全局脚本文件

**/etc/profile** 为系统默认配置文件



**`startx/init PATTERN`** 切换运行模式（级别），**3**为命令行模式，**5**为图形化界面，**0**关机，**6**关机

**`runlevel`** 查看当前运行级别，**`tty`** 查看当前运行窗口



#### 快捷键：

**`Ctrl L`** 清屏

**`Ctrl S`** 锁定屏幕，**`Ctrl Q`** 解锁 （这里的锁定屏幕只是锁定了屏幕的输出打印信息，不影响命令的执行）

**`Ctrl O`** 执行当前命令并重新显示此条命令

**`Ctrl C`** 中止命令

**`Ctrl Z`** 挂起命令

**`Ctrl A`** 将光标移动到行首，**`Ctrl E`** 将光标移动到行尾

**`Ctrl U`**  删除光标前的命令，**`Ctrl K`** 删除光标后的命令



#### 命令格式：

**`which/whereis/type/enable`** 命令查找/查看命令类型及命令种类

**`type command`** 判断命令是内部还是外部命令或是别名

**`enable -n command`**  禁用内部命令

**`enable command`** 启用内部命令

用户家目录下的.bashrc** 文件存放着用户配置的命令别名信息，使用`source .bashrc`** 命令可强制将别名配置保存到内存中。

**`alias 别名='command'`**  设置命令的别名，**/etc/bashrc** 文件中保存系统全局别名等信息

**`alias rm='mv -t /trashbin/'`**  生产环境中尽量不要用到**`rm`**命令，这是非常危险的，可将**`rm`**命令设置别名，移动到“垃圾桶”中

**`unalias 别名`**  取消别名

###### 执行命令的方式：（首先保证为可执行且当前用户具有权限）

**`command`**

**`'command'`**

**`"command"`**

**`\command`**  若存在与命令同名的别名且可执行文件存在于**/bin**或**/usr/bin**目录下，执行原始命令，跳过别名

**`/path/command`**  执行外部命令的原始命令

系统命令存在别名的情况下可在命令前加**\\** ,如**\rm** 可执行**rm**的原始命令

#### 时间命令：

**`date`**  查看当前系统时间

**`date MMDDHHmmYYYY.ss`** 设置时间

**`clock`**  查看当前硬件时钟时间

**`clock -s`**  以硬件时间为准覆盖系统时间

**`clock -w`**  以系统时间为准覆盖硬件时间

**`timedatectl`**  时间命令

**`ntpdate hostaddress`** 与相联网的机器同步时间

#### 电源命令：

**`reboot`**  重启命令

**`reboot -p/-f`** 切断电源/强制重启

**`shutdown`**  关机命令

**`shutdown -r`**  重启，+数字设置时间，**`-c`**  取消当前**`shutdown`**命令，**`-n`**立即关机

#### 查看用户信息：

**`w`**

**`who`**

**`whoami`**

**`id`**

#### screen 会话命令：

**`screen -S 会话名称`** 新建会话

**`screen -ls`**  查看当前可访问的会话列表

**`screen -x 会话名称`** 加入会话

`Ctrl A+D` 暂时退出当前会话，`Ctrl R` 回到原先会话，**`exit`** 命令退出会话

（自我执行会话的意义：可保护远程主机的会话状态）

#### 帮助命令：

**`whatis`** =`man -f`** 显示命令的简短描述

**`makewhatis`** 创建**whatis** 数据库（centos6）

**`mandb`** 创建**whatis**数据库

内部命令查看帮助可以使用**`help`** 查看

外部命令查看帮助需借助于**`man`** 命令

**`man -k keyword`** 搜索有关关键字内容的所有内容，**`-w`** 显示关键字存在路径

**`/keyword`** 打开**`man`** 手册时使用该方式向下查找关键字，**`?keyword`** 向上查找

**/usr/share/doc/** 为软件帮助手册目录

#### history 历史命令：

**`!命令历史编号`** 可执行**`history`**中的命令，**`history`**的变量为**HISTSIZE**存放于**/etc/profile**

**`!!`** 或`!-1`**  可执行历史中的上一条（倒数第一条）命令

**`Ctrl N`**  显示当前历史的下一条命令

**`!string`**  重复最近的上一条以**string** 开头的命令

**`!?string`** 重复最近的上一条包好**string** 的命令

**`!$`**  输出上一条命令的最后一个参数

**`!*`**  输出上一条命令的所有参数

**`^abc`**  将前一个命令中的第一个**abc** 删除

**`^string1^string2`** 将前一个命令中的第一个**string1**替换成**string2**

**`!:gs/string1/string2`** 将前一个命令中的所有**string1**替换成**string2**

**`Ctrl R`** 搜索历史，**`Ctrl G`**退出搜索执行

按住**`Esc`** 后松开，按下**`.`** 显示上一条命令的最后一个参数

同时按住**`Alt`**和**`.`** 显示上一条命令最后参数

先删除用户家目录下的**.bashrc_history**，再执行**`history -c`** 可彻底清除history

命令历史变量：**HISTSIZE** 命令历史记录的条数、**HISTFILE** 指定历史文件、**HISTFILESIZE** 命令历史文件记录历史的条数、**HISTFILEMEFORMAT="%F %T"** 显示时间、**HISTIGNORE="str1:str2*..."** 忽略str1命令，str2开头的历史

控制命令历史的记录方式：**HISTCONTROL**

​	**ignoredups** 默认，忽略重复的命令

​	**ignorespace**  忽略所有以空白开头的命令

​	**ignoreboth**  相当于**ignoredups**和**ignorespace**的组合

​	**erasedups**  删除重复的命令

**export 变量名="值"**

全局配置文件存放在**/etc/profile**文件中，针对账号的配置文件为账号家目录下的**.bash_profile**

### 文件及目录：

文件属性为文件的元数据（metadata），文件内容为文件数据本身

#### 文件类型：

**-** 普通文件

**d** 目录文件

**b**  块设备

**c** 字符设备

**l**  符号链接文件

**p**  管道文件pipe

**s**  套接字文件socket

#### 文件通配符：

***** 匹配零个或多个字符

**?**  匹配任何单个字符

**~**  当前用户家目录

**~user**  用户user家目录

**~+**  当前工作目录

**~-**  前一个工作目录

**[0-9]**  匹配数字范围

**[a-z]**  匹配字母范围

**[user]**  匹配列表中任何一个字符

**[^user]**  匹配列表中的所有字符以外的字符

#### 预定义字符：

**[:digit:]**  任意数字，相当于0-9

**[:lower:]**  任意小写字母

**[:upper:]**  任意大写字母

**[:alpha:]**  任意字母

**[:alnum:]**  任意数字或字母

**[:blank:]**  水平空白字符

**[:space:]**  水平或锤子空白字符

**[:punct:]**  标点符号

**[:print:]**  可打印字符

**[:cntrl:]**  控制（非打印）字符

**[:graph:]**  图形字符

**[:xdigit:]** 十六进制字符



**{}** 可将括号内容与外部内容相互组合如：**file{a,b}.{txt.log}=filea.txt,filea.log,fileb.txt,filea.log...**

**{a..z}=a-z** 字母范围

**{001..20..2}=001 003 ....019**

#### 文件及目录的操作（增、删、改、查）

**`ls`**  列出当前目录下的文件及目录

**`ls -a`**  列出当前文件下的所有文件及目录，包括隐藏文件

**`ls /etc/`**  列出**/etc** 目录下的文件及目录

**`ls -1`**  将文件呈单列显示，**`-S`** 参数将文件按照大小排序，**`-r`** 参数逆序排序，**`-t`**（--time=atime/mtime/ctime）按照时间顺序排序（mtime修改时间/atime访问时间/ctime元数据的修改时间），**`-X`** 按照文件后缀显示

**`ls -aI "[^.]*"`** 或`ls dir/.* -d`** 只显示当前目录隐藏文件

**`ls /etc/*/ -d`**  显示**/etc/**目录下的所有非隐藏目录

**`ls -lhS`** 根据文件大小排序

**`ls -lhSr`**从小到大排序

**`ls -lht`**按照文件修改时间排序

```bash
ls -l / --time-style=+%D |grep `date +%D` #找出今天更新的文件
```



**`pwd`**  显示当前工作目录，**`-P`** 参数显示真实路径，**`-L`** 参数显示链接路径

**`basename`** 命令取文件基名，**`dirname`** 取文件目录名

**`cd`**  切换目录命令，默认执行**`cd`** 切换到家目录

**`cd -P /dir`** 切换到真实路径，**`cd -`** 回到前一目录，**`cd ~user`** 切换到用户user的家目录，**`cd ..`** 切换到上级目录

**`stat filename`**  可查看文件状态信息

**`touch filename`**  创建文件

**`touch -- -a`** 或`touch ./-a`** 或`touch /dir/-a`** 可创建-a文件

```bash
touch `date +%F`.log #生成当前日期的日志文件
```

**`touch -t`** 参数可更改文件时间戳

**`touch -c`**  参数刷新现有文件的时间戳不创建新的空文件

新建文件及目录会在系统中生成对应的节点编号，所以文件不可被新建的情况存在两种：节点编号耗尽与空间资源耗尽同样报错并无法新建文件行为

在同一分区中移动数据不改变数据本身的节点编号及空间占用，在不同分区中移动数据会改变节点编号及分区占用空间。

**`cp`** 拷贝命令

**`-a`** 参数保留原来属性，可用于备份

**`-r`** 参数表示递归，可用于复制目录及子目录内容

**`cp file /dir/file`** 将**file**文件复制到**/dir/file**

**`cp file1{,.bak}`** 创建**file1**的**bak** 备份文件

**`cp /dir/.[^.]* /des`** 将**dir**下的所有隐藏文件复制到**des**中

**`cp /dir/. /des`** 将**dir**下的所有文件复制到**des**中

**`mv`** 移动命令

**`mv a /dir/a`** 将文件**a** 移动到**/dir/a**

**`mv file1 file2`** 将文件**file1** 重命名为**file2**

```bash
rename conf conf.bak* *.conf  #将所有后缀为.conf的文件的后缀改为.conf.bak
```

**`rm`** 删除命令

**`rm file`** 删除文件

**`rm -r dir`** 删除目录

**`-i`** 参数表示带有提示是否要执行删除操作

**`-f`** 参数表示强制执行（危险行为）

**`rm -f *`** 删除当前目录下的文件

**`find . -type of -delete`** 或**`find . -type f -exec rm -f {} \;`**用**`find`**命令查找普通文件并删除or用find命令处理动作将其删除

**`find . -type f | xargs rm -f`** 用于参数列表过长；要删除的文件太多

```bash
rm -f `find . -type f` #删除全部普通文件
for delete in `ls -l`;do rm -f *;done #用for循环语句删除当前目录下的所有类型文件
```



**`touch -- -a`** 或者`touch ./-a`** 创建**-a**文件，**`rm -- -a`** 或者`rm ./-a`** 删除**-a**文件

**`touch '~file'`** 创建**~file**文件，**`rm '~file'`** 删除**~file**文件

**`locate`** 文件查找命令（需从数据库中读取并查找）

**`locate file`** 搜索**file**文件（**`locate`** 命令大多用于搜索系统中固定文件）

**`updatedb`** 更新**mlocate.db**数据库

**`find`** 实时查找系统中的文件

**`find /data -maxdepth 2 -mindepth 2`** 搜索**/data**中深度为2的所有文件

**`find /data -name test.sh`** 精确搜索**/data**中的**test.sh**

**`find /data -name "*test"`** 模糊搜索**/data**中的文件

**`find`** 示例：

```bash
find -name snow.png
find -i name sonw.png
find / -name "*txt"
find /var -name "*log"
find -user joe -group joe
find -user joe -not-group joe
find -user joe -o -user jane
find -not \(-user joe -o -user jane \)
find / -user joe -o -uid 500
```

**`cat、tac、rev`** 文件查看命令

**`more、less`** 分页查看文件内容

**`head`** 命令默认查看文件前10行，可以用**`-n`**参数截取前多少行**n**代替数字，**`-c`** 为取文件前几个字节参数后加数字

**`tail`** 命令默认为查看文件后10行，**`tail -f -n 10 file`**命令常用来追踪文件内容变化，一般用来查看日志信息

**`tail -F -n 10 file`** 同样可用来追踪文件变化，文件丢失后可继续跟踪文件，只要符合文件名存在

**`tailf`** 类似于**`tail -f`** 当文件不增长是并不访问文件

#### 链接文件：

硬链接：针对一个文件，起多个名字。硬链接无法跨分区创建，不支持目录创建硬链接。

软链接支持跨分区，针对原始文件而言，软链接只是相当于原文件的指针。

创建软链接跨目录时，相对路径要针对于要创建软连接的目标位置而言而不是原文件的位置。

软链接与硬链接的区别：

>   1.  是否是同一个文件
>   2.  能否跨分区跨设备
>   3.  文件元数据的链接数是否增长
>   4.  inode number（节点编号）是否相同
>   5.  原始文件删除，链接文件可否正常访问
>   6.  原始文件与链接文件的大小差异
>   7.  是否支持创建目录的链接文件
>   8.  相对路径方式不同

**`ln file hard`** 创建**file**的硬链接**hard**

**`ln -s file soft`** 创建**file**的软链接**soft**

**`diff`** 比较两文件的区别

**`-u`** 参数输出统一的diff格式文件，最适合用于补丁文件

**`patch`** 复制对文件改变

**`-b`** 参数自动备份发生改变的文件

**`diff -u foo.conf foo2.conf > foo.patch`**

**`patch -b foo.conf foo.patch`**

**`paste`** 横向合并命令

**`paste file1 file2`** 横向合并**file1**和**file2**

**`paste -d":" file1 file2`** 以“:” 作为分隔符合并**file1**和**file2**

**`paste -s f1 f2`** 将所有的行合并为一行

#### 文件及目录权限：

```bash
chmod 设置文件权限
chmod who opt per file (who：u g o a,opt：+ - =)
chmod u=,g=,o= file
```

模式法：

**`who：u g o a`**

**`opt: = + -`**

**`per：r w x`**

数字法：（技术存在执行权限，偶数不存在执行权限）

```bash
chmod 数字 file
rwxrw-r-- file
111 110 100 file
7	6	4（二进制转换）
r--
100 4
-w-
010 2
--x
001 1
```

对于文件：

r read 文本文件，看内容

w write 文本文件，修改内容

x excute 程序（二进制，脚本），执行

对于目录：

r read 可浏览文件列表

w write 可创建，删除文件

x excute cd 访问目录内的文件和执行目录切换操作

X`chmod -R a+wX`** 递归操作，只针对子目录与当前目录添加写和执行权限

**`chmod --reference f2 /dir/f1`** 将**f2**的权限复制到**/dir/f1**上

一个目录里的文件能否删除移动或创建由目录权限决定

```bash
chown user file #设置文件的所有者
chgrp group file #设置文件的所有组
chown user.group file #同时修改文件的所属组与所有者（chown user:group file）
```

umask权限：

umask权限+默认权限=666/777

**`umask 022`**修改umask值为022，此时在当前目录下新建文件默认权限为644，新建目录权限为755

若想永久保存umask值，可将配置写入到**~/.bashrc**文件中

umask值计算方式：

对于文件：666-umask，如果结果某位存在奇数位，则奇数位+1

对于目录：777-umask

umask也可使用模式描述方式设置如：**`umask u=rw g=r o=/`**

Linux文件系统上的特殊权限：

SUID权限：继承所有者权限，当执行含有**S**权限的文件时，当前命令权限为SUID权限文件所有者的权限

**`chmod 4755 file`**或**`chmod u+s file`** 给**file**文件赋予当前账号所有者的suid权限（suid权限采用单独计算方式，值为4，后跟文件普通权限）

SUID权限作用于可执行的二进制文件等，当用户执行此文件的时候，会继承此文件所有者的权限

SGID权限：继承所属组权限，作用于可执行的二进制文件等，当用户执行此文件的时候，会继承此文件所属组的权限

当SGID作用于目录上时：该目录机器子目录和文件的所属组继承具有SGID权限目录的所属组权限

**`chmod g+s file`**或**`chmod 2755 file`** 给**file**文件赋予当前账号所有组权限（SGID权限同样采用单独计算方式，值为2）

Sticky权限：粘滞位权限。**`chmod o+t file`**或**`chmod 1755 file`** 赋予**file** Stiky权限

Sticky作用于目录时，对目录内的文件，只能增删改属于用户自己的文件。

```bash
chattr #修改文件的扩展元数据属性
chattr +/-i #增加/删除权限，使得该文件无法被删除修改移动
chattr +/-a #增加/删除权限，使得文件可被追加内容，但无法删除改名
lsattr #查看文件的扩展元数据属性
```

ACL 访问控制列表（mask值为限高线，自定义用户或组acl不能超过mask值）

```bash
setfacl -m u:user/g:group:+/-rww file
setfacl -m u:user:- file #修改acl使得user对file毫无权限
getfacl file #查看file文件的访问控制列表
setfacl -x u:user file #删除对于file和user的访问控制列表
setfacl -b file #清空针对file的所有访问控制列表
setfacl -M/X acl.txt file #读取txt文件内容对file设置增加/删除acl
setfac -R -m d:u:user:rw file #默认修改目录及递归目录内容为acl权限
setfacl -m mask:u:user:r file #修改file相关acl的mask值
getfacl file1 | setfacl --set-file=- file2 #复制file1的acl到file2中
```

ACL访问控制列表生效顺序：所有者，自定义用户，自定义组，其他人

#### 标准输入、标准输出、错误：

**`>`** 为重定向输出，**`>`** 可用来创建空文件：**`> file`**，如果文件已存在**`>`** 则将清空此文件

**`>>`**  为在文件内容后追加

执行**`set -C/+C`** 后，**`>`** 命令（不）执行覆盖，此时**`>|`** 强制覆盖

**`0`** 为输入，**`1`** 为输出，**`2`** 为错误，如：**`cmd 2> error.txt`** 将错误结果输出到**error.txt**文件中

**`ls /dir /error > /out 2> /outerror`** 区分对错输出

**`ls /dir /error > /out 2>&1`**  或`ls /dir /error 2> /out 1>&2`** 或`ls /dir /error &> /out`** 将对错结果全部输出到同一个文件中

**`(cal 02 2002;cal 02 2009) > /output`** 将多个命令结果输出到一个文件中

**`echo password |passwd --stdin user &> /dev/null`** 将修改口令的结果置空

**`touch 文件名`** 可将现存文件刷新时间戳，**`>>`** 创建文件时不会刷新时间戳

**`<`** 为重定向输入

如：**`bc < f1.txt > bc.out`** 将**f1.txt** 文件中的内容计算结果输出到**out**文件中

**`cat < file1 > file2`** 等同于**`copy file1 fiel2`**

标准错误无法通过管道符除非在命令中执行**`2&>1`**  或**`|&`**

**`cat > f1`** 单行重定向，可将键盘输入内容输出到**f1**中，每执行一次回车进行一次定向输出

**`cat > f1 <<b`** 多行重定向，可将键盘输入的多行内容重定向至**f1**，每输入一次**b**重定向一次

**`cat |tee cat.log`** 在重定向的同时将内容打印到屏幕上（会覆盖原文件）

**`cat |tee -a cat.log`** （不会覆盖原文件）

#### 网络设置：

**`nmcli connection modify eth0 connection.autoconnect yes`**  设置网卡自动连接（可写到用户家目录的**.bashrc**或全局配置文件中做永久保存）

**`mii-tool -v eth0`** 或**`ethtool eth0`** 查看网卡信息

**`ss -ntul`**  查看本机端口监听状态

机器的**ttl**值保存在**/proc/sys/net/ipv4/ip_default_ttl**文件中

在终端命令中，可直接**`ping`**通IP地址二进制转换后的数字地址

如：192.168.0.1

11000000101010000000000000000001=3232235521（二进制-十进制）

**`ping 3232235521`** 可通

##### 路由表的构成：

>   1.  目标：数据包发送的目标路径
>   2.  netmask：
>   3.  interface：本路由器的出口
>   4.  gateway：下一跳地址（当路由器处于边界位置且未知网络网关相同时合并为默认路由0.0.0.0，网关为下一跳地址）

**/etc/udev/rules.d/**下存放**“70..net”**命名格式的文件，其中保存着网卡的命名方式

**`dmesg |grep -i eth0`**  或`ethtool -i`** 可查看网卡命令

**`modprobe -f eth`** 卸载网卡驱动，**`modprobe eth`** 重新加载网卡驱动

**`system-config-network-tui`** 网络配置终端图形化界面

**`ifconfig`** 命令，执行此命令默认显示当前系统中活动的网卡信息

**`ifconfig -a`** 显示所有网卡信息

**`ifconfig eth0 1.1.1.1/24`** 或`ifconfig eth0 1.1.1.1 netmask 255.255.255.0`** 临时配置网卡地址

**`ifconfig eth0 up/down`** 启用/禁用网卡。**`ifdown/ifup eth0`** 启用/禁用网卡（针对网卡配置文件存在于**/etc/sysconfig/network-script**中时有效）

**`ifconfig eth0 promisc[-promisc]`** 启用/禁用混杂模式

**`ifconfig eth0 broadcast[-broadcast]`** 启用/禁用广播

**`ip link`** 查看网卡活动状态

**`route -n`** 查看当前系统中存在的路由表信息

**`route add -host 1.1.1.1 gw 2.2.2.2 dev eth0`** 添加仅主机路由等同于**`route add -net 1.1.1.1 netmask 255.255.255.255 gw 2.2.2.2 dev eth0`**

**`route add -net 3.3.3.3 netmask 255.255.255.0 gw 4.4.4.4 dev eth0`** 添加网络路由

**`route add default gw 6.6.6.6`** 添加默认路由等同于**`route add -net 0.0.0.0 netmask 0.0.0.0 gw 6.6.6.6 dev eth0`**

**`route del`** 删除路由记录

**`service network restart`** 或**`systemctl restart network`**重启网络服务

**/etc/sysconfg/network-script** 配置文件举例：（该文件配置生效为永久保存）

```bash
DEVICE=eth0

BOOTPROTO=static

IPADDR=1.1.1.1

PREFIX=16

GATEWAY=1.1.1.3

DNS1=114.114.114.114

DNS2=8.8.8.8

MACADDR=::::

ONBOOT=yes
```



**`tracepath、traceroute、mtr`** 命令可用来跟踪路由

将**/proc/sys/net/ipv4/ip_forward** 置为1可开启路由转发功能，此时机器可充当路由器

```bash
ss -tn #查看当前主机连接状态
ss -tn |wc -l #查看当前主机连接数
ss -tn |tr -s " " : |cut -d: -f6 |tr -d [[:digit:]] #查看当前主机的链接IP
ss -tn |tr -s " " : |cut -d: -f6 |tr -dc '[0-9].\n'
ss -tn |tr -dc '0-9.\n' |tr -s " " : |cut -d: -f6
cat /etc/profile |tr -sc 'a-zA-Z' '\n' |wc -l #计算/etc/profile文件中单词数量
```



#### 文本处理：

**`iconv -f gb2312 test.txt -o output.txt`** 转换文件编码格式为Unicode编码

**`tr`** 转换命令

**`tr 'a-z' 'A-Z'`** 将小写转换为大写

**`tr 'a-c' '1-3'`** 将对应字母与数字转换

**`who > who.log;tr -s " " < who.log`** 将命令**`who`** 结果输出文件中的空格压缩并再次输出到屏幕中

**`who > who.log;tr -s " " + < who.log`** 将命令**`who`** 结果输出文件中的空格压缩并将空格替换为**+**号

**`echo {1..100} > bc.txt;tr " " + < bc.txt > tr.out;bc < tr.out > bc.out`** 计算1-100的累加和

**`tr " " '\n' < f1.txt`** 将**f1.txt**文件中的空格替换为换行

**`echo {1..100} |tr ' ' +|bc`** 计算1-100的累加和

```bash
echo `date +%s`/3600/24 |bc		#计算当前日期天数时间戳
```

**文本处理三剑客：grep、sed、awk**

```bash
grep：文本过滤
--color=auto #对匹配到的文本着色显示
-v：#显示不被PATTERN匹配到的行
-i：#忽略字符大小写
-n：#显示匹配的行号
-c：#统计匹配的行数
-o：#仅显示匹配到的字符串
-q：#静默模式，不输出任何信息
-A#：#after，后#行
-B#：#before，前#行
-C#：#context，前后各#行
-e：#实现多个选项间的逻辑或关系：grep -e 'cat' -e 'dog' file
-w：#匹配整个单词
-E：#相当于egrep，使用ERE
-F：#相当于fgrep，不支持正则表达式
-f file：#根据模式文件处理
--------------------------------------------------------------------
df |grep /dev/sd |tr -s ' '% |cut -d% -f5|sort -nr #查看当前硬盘利用率并排序
nmap -v -sP 192.168.0.1/24 |grep -B1 up |grep report |cut -d" " -f5 > iplist.txt #扫描网段中存活的主机并只显示
grep f1 f2 #取f1与f2文件内容的交集
```

**`egrep`** 及扩展的正则表达式：

**`egrep`**=**`grep -E`**

字符匹配：

```bash
. #任意单个字符
[] #指定范围的字符
[^] #不在指定范围的字符
0-9：[0-9]
10-99：[1-9][0-9]
0-99：[1-9]?[0-9]
100-199：1[0-9]{2}
200-249：2[0-4][0-9]
250-255：25[0-5]
```

次数匹配：

```bash
* #匹配前面字符任意此
? #0或1次
+ #1次或多次
{m} #匹配m次
{m,n} #至少m，至多n次
```

位置锚定：

```bash
^ #行首
$ #行尾
\<，\b #语首
\>，\b #语尾
```

分组：

```bash
()
```

后向引用：

```bash
\1,\2,...
#或者
a|b a或b
C|cat C或cat
(C|c)at Cat或cat
```

取目录基名：**`echo "/etc/rc.d/init.d/functions" |egrep -o "[^/]+$"`**

取目录名：**`echo "/etc/rc.d/init.d/" |egrep -o ".*/[^/]" |egrep -o ".*/"`** 

取IP地址信息：**`ifconfig eth0 |egrep -o "([[:digit:]]{3}.){3}([[:digit:]])"`** 或者**`ifconfig eth0 |grep -o "[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}"`**（基本正则表达式）

sed：stream editor，文本编辑工具

awk：Linux上的实现gawk，文本报告生成器

**`cut`** 命令按列取，例如：**`cut -d: -f1,3,5-7 /etc/passwd`**  根据“:”分列取**/etc/passwd**中的第一列和第五列到第七列

```bash
df |cut -c44-46 #按照字符数取出磁盘利用率
df |tr -s " " % |cut -d% -f5 #取出磁盘利用率
ifconfig eth0 |head -2 |tail -1 |tr -s " " : |cut -d: -f3 #取出网卡地址
ifconfig eth0 |head -2 |tail -1 |tr -dc '[0-9].' |tr -s " " |cut -d" " -f2
```

**`wc`** 文本数据统计工具

**`cut -d " " -f1 /var/log/httpd/access_log|wc -l`**  统计web网站的访问次数

**`seq`** 生成字符串范围

**`seq 63`** 生成1-63数字

**`sort`** 文本内容排序工具，把整理过的文本显示在STDOUT，不改变原始文件

```bash
sort [options] file
-r #执行反向排序
-R #随机排序
-n #执行按数字大小排序
-f #选项忽略（flod）字符串中的字母大小写
-u #选项（独特，unique）删除输出中的重复行
-t c #选项使用c作为字段界定符
-k X #按照使用c字符分割的X列来整理
sort -t: -k1 file #以:作为分隔符按第一列进行正序排序
sort -t: -k1 -r file #逆序排序，同上
sort -t: -k1 -n file #按照数字排序
df |tr -s " " %| cut -d% -f5 |sort -nr |head -1 #查看磁盘最高利用率
cut -d " " -f1 /var/log/httpd/access_log |sort -u |wc -l #查看web服务器访问地址数
```

**`uniq`** 命令：从输入中删除前后相接的重复的行

```bash
-c #显示每行重复出现的次数
-d #仅显示重复过的行
-u #仅显示不曾重复的行
#uniq命令常与sort命令配合使用：
sort userlist.txt |uniq -c
cut -d " " -f1 /var/log/httpd/access_log |sort -n |uniq -c |sort -rn #查看文本服务器访问次数最多的地址并排序
ss -tn |tr -dc '0-9.\n:' |tr -s " " : |cut -d: -f6 |uniq -c |sort -nr #查看当前主机连接数并排序
cat f1 f2 |sort |uniq -d #取两文件交集
cat f1 f2 |sort |uniq -u #取两文件不同的内容
cat f1 f2 |sort -u #取两文件并集
```

**`cut`**和**`paste`**

```bash
#显示文件或STDIN数据的指定列
cut -d: -f1 /etc/passwd
cat /etc/passwd |cut -d: -f7
cut -c2-5 /usr/share/dict/words
#paste合并两个文件的同行好的列到一行
paste [OPSION]...[FILE]
-d 分隔符 #指定分隔符，默认用TAB
-s #所有行合成一行显示
paste f1 f2
paste -s f1 f2
```



### 用户与组：

**`vipw`**=**`vi /etc/passwd`**

**`vigr`**=**`vi /etc/group`**

**`pwck`** 检查**/etc/passwd**文件格式是否正确

**`grpck`** 检查**/etc/gropu** 文件格式是否正确

**/etc/login.defs**中为用户策略配置文件

**`su user`** 切换用户登录，**`exit`** 退出当前用户登录

**`su -u user`** 切换用户登录时同时切换到用户user的家目录

**`su`** 默认切换为root账户，**`su`** 切换root账户登登录时同时切换到root的家目录

**`su - -c 'cat /etc/shadow'`**  使用root账户身份执行当前命令（无需执行用户身份切换）

用户管理命令：

```bash
useradd: useradd user #默认方式创建用户user（创建user用户名及用户组及/home/下家目录）
         useradd -u 1010 user #创建用户user且指定用户user的uid为1010
         useradd -u 1010 -o user #创建用户user指定用户uid创建且忽略uid唯一选项
         useradd -d /dir user #创建用户user时指定用户家目录为/dir
         useradd -r user -s /sbin/nologin #创建系统用户user（家目录不存在且当前用户不能用于登录）
         useradd -c 'user' user #创建用户user时添加描述user
         useradd -g group user #创建用户user时指定主组为group
         useradd -N group user #创建用户user时指定主组为group且不创建新组
         useradd -g group -G Group user #创建用户user时指定主组为group附加组为Group
         useradd -m user #创建用户user时强制创建家目录
         useradd -M user #创建用户user时强制不创建家目录
         useradd 默认值选项配置文件保存在/etc/default/useradd中，可通过useradd -D命令查看
--------------------------------------------------------------------
usermod: usermod -U user #解锁用户user口令，使其可被登录
         usermod -L user #锁定用户user口令，使其不可被登录
         usermod -aG group user #在原有附加组的基础上添加额外的附加组
         usermod -G group user 或 usermod -G "" user #为用户user清空附加组（group为用户名主组）
         usermod -l newuser user #修改用户user的登录名为newuser
--------------------------------------------------------------------
userdel：用户删除命令
		userdel -r user #删除用户user时删除其家目录
--------------------------------------------------------------------
passwd：修改用户口令
		passwd -l user #锁定用户登录口令
		passwd -e user #强制用户user下次登录时修改口令=chage -d 0 user
		passwd -u user #解锁指定用户口令
--------------------------------------------------------------------
chfn user #修改用户user的描述信息
finger user #查看user的描述信息
chfn -f " -o" -p " -h" user #清空用户user的描述信息
groups user #查看用户user属于哪个组
newusers file #可编辑类似于/etc/passwd格式文件保存至file中实现批量添加用户
```

**/etc/skel** 下放置用户默认家目录文件布局

若用户的家目录不慎被删除导致无法执行切换目录操作，可执行**`cp /etc/skel /home/user;chown -R user.user /home/user;chmod 700 /home/user`** 应急修复家目录

组账户管理命令：

```bash
groupadd: groupadd -g 1010 group #指定GID创建组
		  groupadd -r group #创建系统组group
--------------------------------------------------------------------
groupmod: groupmod -n groupname group #修改group组名为groupname
		  groupmod -g 1010 group #修改group组GID为1010
--------------------------------------------------------------------
groupdel：组删除命令（当存在用户主组为当前组时将不能执行删除组的操作）
--------------------------------------------------------------------
groupmems -a/-d user -g group #将user用户添加/删除到group中
groupmems -l -g group #查看组成员
groupmems -a user -g group #添加用户user的附加组
--------------------------------------------------------------------
gpasswd group #给group组设置口令，newgrp group可将当前登录用户临时添加到group组中
gpasswd -a user group #将用户user添加到group组中
gpasswd -d user group #将用户user从group中删除
gpasswd group #修改组的口令
```

### Vim 编辑器：

Vim：

```bash
+# #打开文件后，让光标处于第#行的行首，+默认行尾
+/PATTERN #打开文件后，直接让光标处于第一个被PETTERN匹配的行首
-b file #二进制方式打开文件
-d file1 file2 #比较多个文件
-m file #只读打开文件
ex file 或 vim -e #直接进入ex模式
```

命令模式下：**:wq** 与**:x** 和编辑模式下的**ZZ**相同

扩展命令模式：

```bash
w #写
wq #写入并退出
x #写入并退出
q #退出
q! #不存盘退出
r file #读文件内容到当前文件中
w file #将当前文件内容写入到另一个文件
!command #执行shell命令
r!command #读入命令的输出

```

编辑模式：

```bash
#字符间跳转：
h：左	l：右	j：下	k：上
#command ：跳转由#指定的个数字符
#单词间跳转：
w #下一个单词的词首
e #当前或下一个单词的词尾
b #当前或前一个单词的词首
#command：由#指定一次跳转的单词数
#当前页跳转：
H：页首	M：页中间行 L：页底
zt #将光标所在行移到屏幕顶端
zz #将光标所在行移到屏幕中间
zb #将光标所在行移到屏幕底端
#行尾行首跳转：
^ #跳转至行首的第一个非空白字符
0 #跳转至行首
$ #跳转至行尾
#行间移动：
#G 、扩展命令下：# 跳转至#指定行
G #最后一行
1G、gg #第一行
#句间移动：
) #下一句
( #上一句
#段落间移动：
} #下一段
{ #上一段
#翻屏操作：
Ctrl+f #向文件尾部翻一屏
Ctrl+b #向文件首部翻一屏
Ctrl+d #向文件尾部翻半屏
Ctrl+u #向文件首部翻半屏
#字符编辑：
x #删除光标处的字符，类似于剪切
#x：删除光标处起始的#个字符
xp #交换光标所在处的字符及其后面字符的位置
~ #转换大小写
J #删除当前行后的换行符
#替换命令：
r #替换光标所在处的字符
R #切换成REPLACE模式
#删除命令：
d #删除命令，可结合光标跳转字符，实现范围删除
d$ #删除到行尾
d^ #删除到非空行首
d0 #删除到行首
dw：#删除一个单词
de：#删除光标后一个单词到词尾位置
db：#删除前一个单词
#command
dd #删除光标所在的行
#dd：多行删除
D #从当前光标位置一直删除到行尾，等同于d$
#复制命令：
y #复制，行为相似于d命令
y$：
y0
y^
ye
yw
yb
#command
yy #复制行
#yy：复制多行
Y #复制整行
#改变命令：
c #修改后切换成插入模式
#行为类似于d命令
cc #删除当前行并输入新内容，相当于S
#cc
C #删除当前光标到行尾，并切换到插入模式
```

命令模式：查找

```bash
/ #向下搜索
? #向上搜索
n #与命令同方向
N #与命令反方向
```

命令模式：撤销操作

```bash
u #撤销最近的更改
#u 撤销之前的多次更改
U #撤销光标落在这行后所有此行的更改
按Ctrl+r #重做最后的撤销更改
. #重复前一个操作
n. #重复前一个操作n次
```

特殊命令模式使用：

```bash
100ihaha [ESC] #粘贴“haha”100次
<start position><command><end position>
command:
y 复制、d 删除、gU 变大写、gu 变小写
例如 0y$ 命令意味着：
0 #先到行头
y #从这里开始拷贝
$ #拷贝到本行最后一个字符
ye #从当前位置拷贝到本单词的最后一个字符
di"/( #光标在" "/( )之间，则删除" "/()之间的内容
yi( #光标在()之间，则复制()之间的内容
vi[ #光标在[]之间，则选中[]之间的内容
dtx #删除字符直到遇见光标之后的第一个x字符
ytx #复制字符直到遇见光标之后的第一个x字符

```

扩展命令模式

```bash
#地址定界：start_pos,end_pos
# 具体第#行，例如2表示第2行
#,# 从左侧#表示起始行，到右侧#表示结尾行
#,+# 从左侧#表示的起始行，加上右侧#表示的行数
	例如2,+3表示2到5行
. #当前行
$ #最后一行
	.,$-1 #当前行到倒数第二行
% #全文，相当于1,$
#查找并替换:
s #在扩展模式下完成查找替换操作
	格式：s/要查找订单内容/替换为的内容/修饰符
	要查找的内容：可使用模式
	替换为的内容：不能使用模式，但可以使用“&”引用前面查找时查找到的整个内容如：%s/test/&haha/ #（将会将test变为testhaha）
	修饰符:
	i #忽略大小写
	g #全局替换；默认情况下，每一行值替换第一次出现
	gc #全局替换，每次替换前询问
#查找替换中的分隔符/可替换为其他字符，例如
	s@/etc/@/var@g
	s#/boot#/#i
	%s#\(.*CMD.*\)"#\1 xyz"#  #（将文件中含有CMD的行中的引号中追加一个xyz）
	%s@^[^#]@#&@       #（将文件中非#开头的行添加#）
vim -b file #以二进制打开文件
扩展命令模式下利用xxd命令转换为可读的十六进制：%!xxd
使用：%!xxd -r转换回二进制文件
```

可视化模式：

```bash
#在编辑模式下：
v #面向字符
V #面向行
ctrl+v #面向块
```

多文件模式：

```bash
vim file1 file2 file3...
	:next #下一个
	:prev #前一个
	:first #第一个
	:last #最后一个
	:wall #保存所有
	:qall #退出所有
	:wqall #保存退出所有
多文件分割:vim -o file1 file2（水平分割）
	   vim -O file1 file2（垂直分割）
单文件分割:ctrl+w,s #水平分割
	   ctrl+w,v #垂直分割
	   ctrl+w,q #取消相邻窗口
	   ctrl+w,o #取消全部窗口
```

### 磁盘管理：

**`lsblk`** 查看分区

分区类型：

**MBR**：

主分区：1-4

扩展分区：1

逻辑分区

主分区+扩展分区=4

**GPT**：

最多有128个主分区

**`dd if=/dev/sda of=dpt bs=1 count=64 skip=446`** 本分MBR分区表信息

管理分区：

**`lsblk`** 列出块设备

```bash
#创建分区使用：
	fdisk #创建MBR分区
	gdisk #创建GPT分区
	parted #高级分区操作
#重新设置内存中的内核分区表版本
	partprobe
	partx -a /dev/sda #新增分区时
	partx -d --nr /dev/sda #删除分区时
parted #parted的操作都是实时生效的，需小心使用
用法：parted [options] [device [command []]]
	parted /dev/sdb mklabel|gpt|msdos
	parted /dev/sdb	print
	parted /dev/sdb mkpart primary 1 200
	parted /dev/sdb rm 1
	parted -l #列出分区信息
```

创建ext文件系统：

```bash
mkfs. -t {ext2|ext3|ext4} #指定文件系统类型
-b {1024|2048|4096} #指定块大小
-L 'LABEL' #设置卷标
-j 相当于 -t ext3
-i # #为数据空间中美多少个字节创建一个inode；不应该小于block大学
-N # #指定分区中创建多少个inode
-l #一个inode记录占用的磁盘空间大小，128---4096
-m # #默认5%为管理人员预留空间占总空间的百分比
-O FEATURE[,...] #启用指定特性
-O ^FEATURE #关闭指定特性
```

**`blkid`** 查看文件系统类型

**`tune2fs -l`** 查看ext文件系统元数据

在CentOS6之前的版本中手动创建的分区，默认不具备ACL功能

**`fsck`** 文件系统检查命令

**`mount`** 挂载分区命令

```bash
mount/unmount /dev/sda /mnt #挂载/卸载设备
mount/unmount -U uuid /mnt
-r #参数 只读挂载
-o options #（挂载文件系统的选项），多个选项使用都好分隔
	async #异步模式	
	sync #同步模式，内存更改时，同时写磁盘
	atime/noatime #访问时间，包含目录和文件
	diratime/nodiratime #目录的访问时间戳
	auto/noauto #是否支持自动挂载，是否支持-a选项
	exec/noexec #是否支持在文件系统上运行可执行程序
	dev/nodev #是否支持在文件系统上使用设备文件
	suid/nosuid #是否支持suid和sgid权限
	remount #重新挂载
	ro 只读	rw 读写（默认）
	user/nouser #是否允许普通用户挂在此设备，/etc/fstab使用
	acl/noacl #是否启用此文件系统上的acl功能
	loop/noloop #是否使用loop设备
defaults：相当于rw,suid,dev,exec,auto,nouser,async
```

**`findmnt /mnt`** 判断当前目录是否存在挂载点

一个设备可以同时挂载到多个位置，但一个目录不可以挂载多个设备

**`lsof /mnt/sda1`** 查看当前正在使用挂载分区的用户（**`fuser -v /mnt/sda1`**）

**`fuser -km /mnt/sda1`** 踢出所有正在使用此挂载分区的用户（谨慎使用）

**swap** 交换分区：

```bash
mkswap #格式化分区为swap格式
swapon/off -a #启用/禁用swap分区
	-a #激活所有的交换分区
	-p priority #指定优先级
	/etc/fstab:pri=value
禁用：swapoff [option] [device]
```

将**/home**目录迁移到新分区：

1.  创建并格式化新分区，挂载分区
2.  拷贝**home**目录：**`cp -a /home/. /mnt/home`**
3.  修改**/etc/fstab** 文件永久配置

挂载USB设备：

1.  查看USB设备是否被识别：**`lsusb`**
2.  手动挂载：**`mount /dev/sdb1 /mnt`**

**/misc** 杂项文件夹，可用来加载光盘等

**`systemctl enable autofs`**  实现**/misc/cd**等设备的自动挂载

**`systemctl start autofs`**

执行过上述命令后，可通过**`cd /misc/cd`**命令进入到光盘中

常用工具：

```bash
#文件系统空间占用等信息的查看工具
df [option] [file]
-H #以1000为单位
-T #文件系统类型
-h #human-readable
-i #inodes instead of blocks
-P #以Posix兼容的格式输出
#查看某目录总体空间占用状态
du [option] DIR
-h #human-readable
-s summary --max-depth
```

**`dd`**工具：转换及复制

```bash
用法：dd if=/path/from/src of /path/to/dest
      bs=#：block size #复制单元大小
      count=#：#复制多少个bs
of=file #写到所命名的文件而不是到标准输出
if=file #从所命名的文件读取而不是从标准输入
bs=size #指定块大小（既是ibs也是obs）
ibs=size #一次读size个byte
obs=size #一次写size个byte
cbs=size #一次转化size个byte
skip=blocks #从开头忽略blocks个ibs大小的块
seek=blocks #从开头忽略blocks个obs大小的块
count=n #只拷贝n个记录
dd if=/dev/sda of=/dev/sda #修复硬盘小错误等

dd if=/dev/zero of=/boot/bigfile bs=1M count=800 #创建巨型文件
dd if=/dev/zero of=/swapfile bs=2G count=1 #生成一个大文件
>/dir/file 置空巨型文件
```

##### 磁盘序列：

软RAID：

**`mdadm`**  为软RAID提供管理界面

为空余磁盘添加冗余

结合内核中的**`md`** (multi devices)

RAID设备可命名为**/dev/md0、/dev/md1** 等

**`mdadm`**

```bash
命令的语法格式：mdadm [mode] <raiddevice> [options] <component-devices>
支持的RAID级别：LINEAR,RAID0,RAID1,RAID4,RAID5,RAID6,RAID10
模式：
	创建：-C
	装配：-A
	监控：-F
	管理：-f,-r,-a
<raiddevice>：/dev/md#
<component-devices>：任意块设备
```

LVM逻辑卷：创建

```bash
fdisk /dev/sda /dev/sdb #准备分区（如果目标是分区而不是硬盘需加选项fdisk t 8e）
pvcreate /dev/sda /dev/sdb #创建物理卷
vgcreate vg0 /dev/sda /dev/sdb #加入卷组
lvcreate -n lv_1 -L 15G vg0 #创建逻辑卷
mkfs.ext4 /dev/vg0/lv_1 #格式化逻辑卷
mount /dev/vg/lv_1 /mnt/lv_1 #挂载逻辑卷
```

扩展LVM：

```bash
vgdisplay #查看vg有无空闲空间	
lvextend -r -l +100%FREE /dev/vg0/lv_1 #扩展逻辑卷
resize2fs /dev/vg0/lv_1 #扩展文件系统（lvextend -r）
```

缩减LVM：

```bash
umount /mnt/lv_1
fsck -f /dev/vg0/lv_1
resize2fs /dev/vg0/lv_1 20G #缩减分区大小
lvreduce -L 20 /dev/vg0/lv_1 #缩减逻辑卷大小
mount /dev/vg0/lv_1 /mnt/lv_1
```

LVM快照管理：(当原逻辑卷的文件系统中存在修改过的文件时，快照才会对其进行相应的备份)

```bash
lvcreate -n lv_snap -s -p r -L 5G /dev/vg0/lv_1 #创建快照
mkdir /mnt/snap
mount -o nouuid,ro /dev/vg0/lv_snap /mnt/snap #挂载逻辑卷快照
#还原快照前将快照和对应逻辑卷取消挂载
umount /mnt/data
umount /mnt/snap
lvconvert --merge /dev/vg0/lv_data_snap #快照合并
```

### 软件包管理：

**`yum`** rpm包管理的前端工具

**`apt-get`** deb包管理的前端工具

**`zypper`** suse上的rpm前端管理工具

**`dnf`** Fedora 18+ rpm包管理前端工具

库文件：

查看二进制程序的库文件：**`ldd /PATH/TO/BINARY_FILE`**

管理及查看本机装载的库文件：**`ldconfig`** 加载配置文件中的执行的库文件

**`/sbin/ldconfig -p`** 显示本机已经缓存的所有可用库中文件名及文件路径的映射关系

配置文件：**/etc/ld.so.conf，/etc/ld.so.conf.d/*.conf**

缓存文件：**/etc/ld.co.cache**

rpm包管理：

CentOS系统上使用rpm命令管理程序包：

安装、卸载、升级、查询、校验、数据库维护

```bash
安装：rpm {-i|--install} [install-options] PACKAGE_FILE...
	-v：verbose
	-vv：
	-h：以#显示程序包管理执行进度
rpm -ivh PACKAGE_FILE …
	-q PACKAGE_FILE：查询软件包
	-e PACKAGE_FILE：卸载软件包
	[install-options]
	--test：测试安装，但不真正执行安装，鸡dry run模式
	--nodeps：忽略依赖关系
	--replacepkgs | replacefiles
	--nosignature：不检查来源合法性
	--root=/path：指定根目录
	--nodigest：不检查包完整性
	--noscripts：不执行程序包脚本
		%pre：安装前脚本 --nopre
		%post：安装后脚本 --nopost
		%preun：卸载前脚本 --nopreun
		%postun：卸载后脚本 --nopostun

	-U|--upgrade：升级程序包（旧程序存在升级则升级，旧程序不存在则执行安装旧程序）
	-F|--freshen：
	包查询：rpm {-q|--query} [select-options] [query-options]
	[select-options]
		-a：所有包
		-f：查看指定的文件由哪个程序包安装生成
		-p rmpfile：针对尚未安装的程序包文件做查询操作
		--whatprovides CAPABILITY：查询指定的CAPABILITY由哪个包所提供
		--whatrequires CAPABILITY：查询指定的CAPABILITY被哪个包所依赖
	rpm2cpio 包文件|cpio -itv 预览包内文件
	rpm2cpio 包文件|cpio -id "*.conf" 释放包内文件
		--changelog：查询rpm包的changelog
		-c：查询程序的配置文件
		-d：查询程序的文档
		-i：information
		-l：查看指定的程序包安装后生成的所有文件
		--scripts：程序包自带的脚本
		--provides：列出指定程序包所提供的的CAPABILITY
		-R：查询指定的程序包所依赖的CAPABILITY
	包校验：rpm {-V|--verify} [select-options] [verify-options]
		S file Size differs
		M mode differs (includes permissions and file type)
		5 digest (formerly MD5 sum) differs
		D Device major/minor number mismatch
		L readLink(2) path mismatch
		U User ownership differs
		G Group ownership differs
		T mTime differs
		P capabilities differ
```

yum ：rpm包管理前端工具

**/etc/yum.repos.d/**目录下存放yum服务器源信息

创建***.repo**后缀文件

主要内容：

```bash

	[base]
	name=
	baseurl=url://
	gpgcheck=0    #（设置默认不检查源，值为1时检查）
	gpgkey=url://
```

**`yum repolist`** 加载repo仓库

**`yum install/remove`** 安装/卸载

**`yum info PACKAGE_FILE`** 查看仓库中包的信息

**`yum list`** 列出所有仓库里的包

**`yum history`** 查看yum的历史操作

​	**`yum history undo/redo`** 撤销/重做历史操作（可用来卸载软件）

创建远程yum共享服务器：

1.  启用远程可访问的服务如：http/ftp等
2.  将资源放置到服务器的相关目录中
3.  修改客户机配置文件即可

##### 源码编译安装：

C语言源码编译安装三步骤：

1. ./configure**

    通过选项传递参数，指定启用特性、安装路径等；执行时会参考用户的指定以及**Makefile.in**文件生成**Makefile**

    检查依赖到的外部环境，如以来的软件包

    2. make** 根据**Makefile** 文件，构建应用程序
    3. make install** 复制文件到相应路径

开发工具：

**`autoconf`** 生成**configure**脚本

**`automake`** 生成**Makefile.in**

### Shell 脚本编程：

shell脚本：包含一些命令或声明，并符合一定合适的文本文件

格式要求：首行生命shebang机制

```bash
#!/bin/bash
#!/usr/bin/python
#!/usr/bin/perl
```

shell脚本的用途有：

1.  自动化常用命令
2.  执行系统管理和故障排除
3.  创建简单的应用程序
4.  处理文本或文件

脚本规范：

1.  第一行一般为调用使用的语言
2.  程序名，避免更改文件名为无法找到正确的文件
3.  版本号
4.  更改后的时间
5.  作者相关信息
6.  该程序的作用及注意事项
7.  最后是各版本的更新简要说明

bash检查脚本错误：

**`bash -n shell.sh`** 检查脚本语法错误

**`bash -x shell.sh`**  调试执行脚本

变量：命名的内存空间

​				数据存储方式：

​				字符：

​				数值：整型、浮点型

​			变量类型：

​				作用：

				1. 数据存储格式
   				2. 参与的运算
                        				3. 表示的数据范围

当局部变量定义成功后，使用**`export `** 可将局部变量转换为全局变量，如**`name=test;export name`** 或**`export name=test`** 或**`declare -x name=test`**，此时**name**则转换为全局变量

全局变量父进程可以传给各级附属子进程，但是子进程无法回传全局变量

执行**`export`** 或**`declare -x`** 或**`env`** 命令可查看当前系统的环境变量（全局变量）

**`set`** 命令可显示出当前系统中的所有变量包括局部变量和环境变量

**`unset name`** 删除变量

脚本中执行结束后应当使用**`unset`**删除变量释放内存

只读变量（常量）：

**`readonly name=test`** 设置只读变量

常量的生命有效期为整个程序运行的有效期

**`delcare -r`** 显示当前系统存在的常量（**`readonly -p`**）

shell中在括号中执行命令可将命令集中处理

shell中使用小括号内执行命令可开启子shell且不会影响当前的shell环境

shell中使用大括号内执行命令时相对于当前shell执行的操作

位置变量：在脚本代码中调用通过命令行传递给脚本的参数

```bash
$1,$2... #对应第1、第2等参数，shift[n]换位置
$0 #命令本身
$* #传递给脚本的所有参数，全部参数合为一个字符串
$@ #传递给脚本的所有参数，每个参数为独立字符串
$# #传递给脚本的参数的个数
$@ $* #只在被双引号包起来的时候才会有差异
set -- #清空所有位置变量
```

退出状态：

进程使用退出状态来报告称或失败

```bash
·0表示成功，1-255表示失败
·$?变量保存最近的命令退出状态
```

例如：**`ping -c1 -W1 hostdown &> /dev/null`**，**`echo $?`**

退出状态码：

**`exit 0`** 返回结果为0（**`exit 100`** 返回结果为100）

算术运算：

```bash
bash中的算术运算：help let
	+,-,*,/,%,**(乘方)
	实现算术运算：
	1.let var=算术表达式
	2.var=$[算术表达式]
	3.var=$((算术表达式))
	4.var=$(expr arg1 arg2 arg3...)
	5.delcare -i var=数值
	6.echo '算术表达式'|bc
乘法符号有些场景中需要转义，如*
bash由内建的随机数生成器：$RANDOM（0-32767）
	echo $[$RANDOM%50]：0-49之间随机数
```

逻辑运算：

```bash
逻辑运算：&与，|或，&&短路与，||短路或，^异或，!非
cmd1 && cmd2：如果cmd1为假，cmd2不需要执行；cmd1为真，则继续执行cmd2
cmd1 || cmd2：如果cmd1为真，cmd2不需要执行；cmd1为假，则继续执行cmd2
a^b=c，a^c=b，b^c=a
ab互换值：a=$[a^b];b=$[a^b];a=$[a^b]
```

bash的字符串测试：注意用于字符串比较是的用到的操作数都应该使用引号

```bash
	= 是否等于
	> ascii码是否大于ascii码
	< 是否小于
	!= 是否不等于
	=~ 左侧字符串是否内被右侧的PATTERN所匹配
	   注意：此表达式一般用于[[]]中；扩展的正则表达式
	-z "STRING" 字符串是否为空，空为真，不空为假
	-n "STRING" 字符串是否不空，不空为真，空为假
```

条件测试：注意：EXPRESSION前后必须要有空白字符

```bash
test EXPRESSION
[ EXPRESSION ]
[[ EXPRESSION ]]
```

---

## 其他

临时禁制ping命令：

如果想要临时允许的话只需要把下面的1换成0即可

**`echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all`**

永久禁止ping命令：

在**/etc/sysctl.conf**文件中新增加一行

**`net.ipv4.icmp_echo_ignore_all=1`** 修改完成后执行**`sysctl -p`** 使新的配置生效

防火墙禁制ping设置：

**`iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT`**

**`iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT`**

或者

**`iptables -A INPUT -p --icmp-type 8 -s 0/0 -j DROP`**



**`last`**命令获取用户登录信息：**`last |head -5 |tr -s " "`**

```bash
for user in `ls /home'; do echo -ne "$user\t"; last $user |wc -l; done #统计每个用户登录次数
```

脚本：

```bash
#!/bin/bash

echo -n "Logins since "
who /var/log/wtmp | head -1 | awk '{print $3}'
echo "======================="

for user in `ls /home`
do
  echo -ne "$user\t"
  last $user | wc -l
done
##################################################################

```

**`ac`** 命令统计每个用户登录时长：**`ac user`**

脚本：

```bash
#!/bin/bash

echo -n "hours online since "
who /var/log/wtmp | head -1 | awk '{print $3}'
echo "============================="

for user in `ls /home`
do
  ac $user | sed "s/^\t//" | sed "s/total/$user\t/"
done
```

bash脚本：

**`set -x -e -u -o pipefail`**

在写脚本时，在一开始（Shebang之后）加上下面这一句，或者它的缩略版，能避免很多问题，更重要的是能让很多隐藏的问题暴露出来：

**`set -xeuo pipefail`**

**-x**：在执行每一个命令之前把经过变量展开之后的命令打印出来

这个对于debug脚本，输出Log时非常有用，正式运行的脚本也可以不加

**-e**：遇到一个命令失败（返回码非零）时，立即退出

**-u**：试图使用未定义的变量，就立即退出

**-o pipefail**：只要管道中的一个子命令失败，整个管道命令就失败。



##### Httpd MPM：

**prefork**：进程模型，两级结构，主进程master负责生成子进程，每个子进程负载响应一个请求

**worker**：线程模型，三级结构，主进程master负责生成子进程，每个子进程负责生成多个线程

**event**：线程模型，三级结构，主进程master负责生成子进程，每个子进程负责响应多个请求



##### I/O：

网络IO：本质时socket读取

每次IO，都要经由两个阶段：

第一步：将数据从磁盘文件先加载到内核内存空间（缓冲区），等待数据准备完成，时间较长

第二部：将数据从内核缓冲区复制到用户空间的进程的内存中，时间较短

同步/异步：关注的是消息通信机制

​	同步：synchronous，调用者等待被调用者返回消息，才能继续执行

​	异步：asynchronous，被调用者通过状态、通知或回调机制主动通知调用者被调用者的运行状态

阻塞/非阻塞：关注调用者在等待结果返回之前所处的状态

​	阻塞：blocking，指IO操作需要彻底完成后才返回到用户空间，调用结果返回之前，调用者被挂起

​	非阻塞：noblocking，指IO操作被调用后立即返回给用户一个状态值，无需等到

IO操作彻底完成，最终的调用结果返回之前，调用者不会被挂起

I/O模型：

​	阻塞型、非阻塞型、复用型、信号驱动型、异步

I/O模型的具体实现：

​	select、poll、epoll



##### Nginx介绍：

特性：模块化设计，较好的扩展性，高可靠性

支持热部署：不停机更新配置文件，升级版本，更换日志文件

低内存消耗：10000个keep-alive连接模式下啊的非活动连接，仅需2.5M内存

event-driven，aio，mmap，sendfile

基本功能：

静态资源的web服务器

http协议反向代理服务器

pop3/imap4协议反向代理服务器

Fast CGI（LNMP），uWSGI（python）等协议

模块化（非DSO），如zip，ssl模块



web服务相关功能：

虚拟主机（server）

支持keep-alive和管道连接

访问日志（支持基于日志缓冲提高性能）

url rewrite

路径别名

基于IP及用户的访问控制

支持速率限制及并发数控制

重新配置和在线升级而无需中断

Memcached的GET接口



Nginx的程序架构：

master/worker结构

一个master进程：负责加载和分析配置文件，管理worker进程，平滑升级

一个或多个worker进程：处理并响应用户请求

缓存相关的进程：cache loader：载入缓存对象

​							   cache manager：管理缓存对象



Nginx 性能优化相关的配置：

```bash
1、worker_processes number | auto
    worker进程的数量；通常应该为当前主机的cpu的物理核心数
2、worker_cpu_affinity cpumsask …
    worker_cpu_affinity auto [cpumask] 提高缓存命中率
    CPU MASK：00000001：0号CPU
	        00000010：1号CPU
    worker_cpu_affinity 0001 0010 0100 1000；
    worker_cpu_affinity 0101 1010；
3、worker_priority number
    指定worker进程的nice值，设定worker进程优先级：[-20-10]
4、worker_rlimit_nofile number
    worker进程能过够打开的文件数量上限如65535

```



源码编译与二进制按照MySQL：首先检查环境

```bash
1.创建用户：useradd -r -s /sbin/nologin mysql -d /data/mysqldb
2.解压缩源码：tar -xvf mariadb_...tar.gz -C /usr/local/
   cd /usr/local
   ln -s mariadb.../ mysql
   chown -R root:root mysql/
3.准备环境变量：echo PATH=/usr/local/mysql/bin:$PATH > /etc/profile.d/mysql.sh 
   . /etc/profile.d/mysql.sh
4.mkdir -pv /data/mysqldb
  chown mysql.mysql /data/mysqldb
  chmod 770 /data/mysqldb
  cmake . \
  ........
  make -j 4 && make install
5.cd /usr/local/mysql
   scripts/mysql_install_db --datadir=/data/mysqldb --user=mysql
6.cd /usr/local/mysql
   cp support-files/my-huge.cnf /etc/my.cnf

vim /etc/my.cnf
[mysqld]
datadir=/data/mysqldb 加此行
7.准备启动脚本：cp /app/mysql/support-files/mysql.server /etc/init.d/mysqld
8.启动服务：chkconfig --add mysqld ;service mysqld start

```



yum安装包的基础上实现mysql多实例：

```bash
创建多实例数据库目录：mkdir /mysqldb/{3306,3307,3308}/{etc,socket,pid,log,data}
   		chown -R mysql.mysql /mysqldb/
mysql_install_db --datadir=/mysqldb/3306(78)/data --user=mysql --basedir=/usr
复制配置文件：cp /etc/my.cnf /mysqldb/3306(78)/etc/
修改配置文件内容，重点包括数据库目录等位置，注销掉“!includedir /etc/my.cnf.d”
配置启动脚本
```



LVS负载均衡：

**`ipvsadm`**

**`ipvsadm`**包构成：

程序包：**ipvsadm**

Unit File：**ipvsadm.service**

主程序：**/usr/sbin/ipvsadm**

规则保存工具：**/usr/sbin/ipvsadm-save**

规则重载工具：**/usr/sbin/ipvsadm-restore**

配置文件：**/etc/sysconfig/ipvsadm-config**



**`ipvsadm`** 命令：

核心功能：

​	集群服务管理：增删改

​	集群服务的RS管理：增删改

​	查看

```bash
ipvsadm -A|E -t|u|f service-address [-s scheduler] [-p [timout]] [-M netmask] [--pe persistence_engine] [-b sched-flags]
ipvsadm -D -t|u|f service-address 删除
ipvsadm -c 清空
ipvsadm -R 重载
ipvsadm -S [-n] 保存
ipvsadm -a|e -t|u|f service-address -r server-address [options]
ipvsadm -d -t|u|f service-address -r server-address
ipvsadm -L|l [options]
ipvsadm -Z [-t|u|f service-address]
管理集群服务：增删改
增、改：ipvsadm -A|E -t|u|f service-address [-s scheduler] [-p [time-out]]
删除：ipvsadm -D -t|u|f service-address
service-address:
	-t|u|f：
	        -t：TCP协议的端口，VIP：TCP_PORT
	        -u：UDP协议端口，VIP：UDP_PORT
	        -f：firewall MARK，标记，一个数字
[-s scheduler]：指定集群的调度算法，默认为wlc
管理集群上的RS：增、删、改
增、改：ipvsadm -a|e -t|u|f service-address -r server-address [-g|i|m] [-w weight]
删：ipvsadm -d -t|u|f service-address -r server-address
server-address:
	rip[:port] 如省略port，不做端口映射
选项：
	lvs类型：
	           -g：gateway，dr类型，默认
	           -i：ipip，tun类型
	           -m：masquerade，nat类型
	-w weight：权重
ipvsadm -Ln查看当前配置
ipvsadm-save保存配置（ipvsadm -Sn）

```

实现NAT模式的ipvsadm：

```bash
1 LVS
ip_forward=1
route add default gw 
ipvsadm -A -t vip -s wrr
ipvsadm -a -t vip -r rsip -m
2 router
ip_forward=1
route add default gw

```

实现单网络DR模型的ipvsadm：

```bash
1 LVS 
VIP：ip addr a 192.168.30.7/32 dev lo
DIP:  192.168.30.100/24 eth0
GATEWAY:  192.168.30.x

ipvsadm -A -t 192.168.30.7:80 -s rr
ipvsadm -a -t 192.168.30.7:80 -r 192.168.30.17 [-g]

2RS
echo 1 > /proc/sys/net/ipv4/conf/lo/arp_ignore
echo 1 > /proc/sys/net/ipv4/conf/all/arp_ignore
echo 2 > /proc/sys/net/ipv4/conf/all/arp_announce
echo 2 > /proc/sys/net/ipv4/conf/lo/arp_announce	
ip a a 192.168.30.7/32 dev lo

```



##### Linux 优化服务：

Linux分区：系统分区和数据分区分离原则，LVM是否需要，多分区原则（/、/boot、/var、/usr、/data）

服务器网络配置：

 1.    服务器IP地址配置：**/etc/sysconfig/network-scripts/ifcfg-eth/1/2...**

       重启网卡命令：**`service network restart`** 或者**`/etc/init.d/network restart`**

	2. 网关/主机名配置：**/etc/sysconfig/network**

	3. DNS配置：**/etc/resolv.conf**

	4. HOST配置：**/etc/hosts**

网络安全配置：

 1.    SeLinux配置（如何关闭selinux）

       查看selinux状态：**`cat /etc/selinux/config`**

       selinux的状态：enforcing开启状态，disabled禁用状态，permissive提醒的状态

       命令行关闭：**`setenforce 0`**

	2. iptables配置：**/etc/sysconfig/iptables**

	3. 授权用户与sudo设定：

    ​	**/etc/sudoers**文件

    ​	**`<user list> <host list> = <operator list> <tag list> <command list>`**

    ​	常见配置：**linux ALL=(ALL) NOPASSWD:ALL**

	4. ssh安全登录经验：

    备份：**`cp /etc/ssh/sshd_config sshd_config_bak`**（运维必备守则）

   `vim /etc/ssh/sshd_config`**

    ​	*#* 不适用DNS反查，可提高ssh连接速度

    ​	**UseDNS no**

    ​	*#* 关闭GSSAPI验证，可提高ssh连接速度

    ​	**GSSAPIAuthentication no*

    ​	*#* 禁制root账号登录

    ​	**PermitRootLogin no**

更新yum源以及软件版本：

 1.    常用的几个yum源：

       epel源：https://fedoraproject.org/wiki/EPEL

       repoforge源：http://repoforge.org/usr/

	2. 升级系统内核异界更新软件

    清空yum缓存：**`yum clean all`**

    生成缓存：**`yum makecache`**

    开始更新系统以及内核：**`yum upgrade`**

    必备软件：**`yum install ntpdate wget -y`**



调整服务器时间NTP设置

 1.    通过crontab设置时间同步

       推荐的时间服务器：ntp.sjtu.edu.cn

       `*/10 * * * * * /usr/sbin/ntpdate ntp.sjtu.edu.cn >> /var/log/ntp.log 2>&1; /sbin/hwclock -w`

	2. 架设ntp server

    关注两个文件：**/etc/ntp/ntpserver.conf、/etc/ntp.conf**



系统资源调优

 1.    关注ulimit命令

       ulimit -n （最大打开文件数）

       常见案例日志：java.net.SocketException:Too many open files

       相关配置文件：**/etc/security/limits.conf、/etc/security/limits.d/90-nproc.conf（centos6版本）**

       `* soft nofile 65536` 

       `* hard nofile 65536`

       ulimit -u （最大用户数）

       `* soft noproc 65536`

       root soft noproc unlimited

	2. 系统内核参数调优

    常见案例日志：kernel:ip_conntrack:table full,dropping packet

    ip_conntrack_max 参数

   /proc/sys/net/ipv4/netfiliter/ip_contrack_max**或者**/proc/sys/net/ipv4/ip_conntrack_max （centos5版本）**、**/etc/sys/net/netfiliter/nf_conntrack_max （centos6版本）**

    在**/etc/syscl.conf**加入

    `net.ipv4.netfilter.ip_conntrack_max = 655360（centos5）
    net.nf_conntrack_max = 1000000 （centos6）`

   `sysctl -p`**

    swappiness 参数

    表示使用swap的概率，此值越大，表示使用swap的概率越大，推荐配置如下：

    查看目前配置：**`cat /proc/sys/vm/swappiness`**

    添加如下内容到**/etc/sysctl.conf**

    `vm.swappiness=10`

    表示当内存使用率超过（100-10）90%时，才开始使用swap



精简系统服务和开机进程

 1.    线上服务器建议开启的服务：crond、network、syslog、sshd、iptables、udev-post、sysstat

       快捷开启方法：

       ```bash
       先关闭所有：for serv in `chkconfig ---list|grep 3:on|awk '{print $1}'`;do chkconfig --level 3 $serv off;done
       然后开启需要的服务：for serv in `crond network syslog sshd iptables udev-post sysstat`;do chkconfig --level 3 $serv on;done
       
       ```

	2. 可删除的系统用户和组

    ```bash
    # 删除不必要的用户
    userdel adm
    userdel Ip
    userdel sync
    userdel shutdown
    userdel halt
    userdel news
    userdel uucp
    userdel video
    userdel games
    userdel gopher
    userdel ftp
    # 删除不必要的群组
    groupdel adm
    groupdel Ip
    groupdel news
    groupdel uucp
    groupdel games
    groupdel dip
    
    ```

    

Linux故障排除思路

 1.    重视报错提示信息

 2.    日志文件

       系统日志：dmesg、/var/log/messages/、/var/log/secure

       应用日志：

       ​	Apache: $APACHE_BASE/logs/error_log $APACHE_BASE/logs/access_log
       ​	Nginx: $NGINX_BASE/logs/error_log $NGINX_BASE/logs/access_log
       ​	Tomcat: $TOMCAT_BASE/logs/catalina.out

	3. 综合分析过程，要以日志为导向，配合引用环境，根据报错信息，排除故障

	4. 网络故障排除思路

        	1. 网络硬件传输问题
            	2. 检查网卡是否能正常工作，可以从网卡是否正常加载、网卡IP设置是否正确
                	3. 检查DNS是否设置正确
                    	4. 服务是否正常打开
                        	5. 访问权限是否打开（iptables/selinux）
                            	6. 局域网主机之间联网是否正常



影响Linux性能的各种因素：

1.  系统硬件资源

    1.  CPU：如何判断多核CPU与超线程，消耗CPU的业务：动态web服务、mail服务
    2.  内存：物理内存与swap的取舍，选择64位的Linux操作系统。消耗内存的业务：内存数据库（redis/hbase/mongodb）
    3.  磁盘IO：RAID技术、SSD磁盘。消耗磁盘的业务：数据库服务器
    4.  网络带宽：网卡/交换机的选择，操作系统的双网卡绑定。消耗带宽的业务：hadoop平台、视频业务平台

2.  操作系统相关资源

    1.  系统安装优化：磁盘分区、RAID设置、swap设置

    2.  内核参数优化：ulimit -n（最大打开文件数、最大用户数）

    3.  文件系统优化：

        ext2：Linux下标准文件系统，无日志记录（inode）功能

        ext3：在ext2基础上增加了日志记录功能，及支持32000个目录

        ext4：ext3的后续版本，Linux2.6.28内核开始支持，无线子目录支持，快速fsck

        xfs：高性能文件系统，Linux3.10内核开始默认支持

        建议：

        ​	读操作频繁，同时小文件众多的应用，首选ext4文件系统，接下来依次时xfs、ext3

        ​	写操作频繁，首选是xfs，接下来依次是ext4和ext3

        ​	对性能要求不高，数据安全要求不高的业务，ext3时比较好的选择

3.  程序问题（开发人员相关）



Linux性能优化工具

1.  CPU性能评估工具：
    1.  vmstat（系统默认自带）：利用vmstat命令可以对操作系统的内存信息，进程状态、CPU活动等进行监控。常用方式：**`vmstat 2 3 `** （表示每3秒更新一次输出信息，统计5次后停止输出）
    2.  iostat（需要安装sysstat工具包）：iostat时I/O statistics（输入/输出统计）的缩写，主要功能时对系统的磁盘I/O操作进行监视。常用方式：**`iostat -c 3 5`**（其中，-c 表示显示CPU的使用情况，-d显示磁盘的使用情况）
    3.  uptime命令：主要用来统计系统当前的运行状况，输出的信息依次为：系统现在的时间，系统从上次开机到现在运行了多少时间，系统目前有多少登录用户，系统在一分钟内、五分钟内、十五分钟内的平均负载
2.  内存性能评估：
    1.  free命令：free命令是监控Linux内存使用情况最常用的命令。常见用法：**`free -m`**
    2.  sar/pidstat：这两个命令主要用户监控全部或指定进程占用系统资源的情况，如CPU、内存、设备IO。三个共同参数：-u（获取CPU状态）-r（获取内存状态）-d（获取磁盘）。常用组合：**`sar -r 3 `** 获取CPU3秒内的状态，**`pidstat -r -p 1 3`**获取内存3秒内的状态
3.  磁盘性能评估：
    1.  iostat -d组合，iostat -d 2 3
    2.  pidstat -d -p 31887 3
    3.  sar -d 2 3
4.  网络性能评估：
    1.  ping
    2.  netstat、netstat -i（查看路由情况）、netstat -r（查看网络接口状态）
    3.  mtr/traceroute命令：跟踪网络路由状态，推荐使用mtr，动态跟踪网络路由，用于排除网络问题



##### Ansible自动化运维

ansible的默认配置文件：

```bash
[default]
#inventory = /etc/ansible/hosts #主机列表配置文件
#blibrary = /usr/share/my_modules/ #库文件存放目录
#remote_tmp = $HOME/.ansible/tmp #临时py命令存放在远程主机目录
#local_tmp = $HOME/.ansible/tmp #本机的临时命令执行目录
#forks = 5 #默认并发数
#sudo_user = root #默认sudo用户
#ask_sudo_pass = True #每次执行ansible命令是否询问ssh密码
#ask_pass = True
#remote_port = 22
#host_key_checking = False #检查对应服务器的host_key，建议取消注释
#log_path = /var/log/ansible.log #日志文件，建议取消注释
```

ansible的使用语法：

```bash

ansible <host-pattern> [-m module_name] [-a args]
--version #显示版本
-m module #指定模块，默认为command
-v #详细过程 
-vv -vvv #更详细
--list-hosts #显示主机列表，可简写--list
-k，--ask-pass #提示输入ssh链接密码，默认Key验证
-K，--ask-become-pass #提示输入sudo时的口令
-C ，--check #检查，并不执行
-T，--timeout=TIMEOUT #执行命令的超时时间，默认10s
-u，--user=REMOTE_USER #执行远程执行的用户
-b，--become #代替旧版的sudo切换
```

ansible常用模块：

```bash
#Ping：检查主机活动状态
Command默认模块：在远程主机执行命令，可忽略-m选项
ansible srvs -m command -a 'service vsftpd start'
此模块不支持$varname<>|；&等，用shell模块实现
#Shell：与command相似，用shell执行命令
ansible srv -m shell -a 'echo user|passwd --stdin password'
调用bash执行命令，类似cat /tmp/stanley.md|awk -F '|' '{print $1,$2}' &> /tmp/example.txt这些复杂命令，即使使用shell也可能会失败，解决办法写到脚本时，copy到远程，执行，再把需要的结果拉回执行命令的机器
#Script：运行脚本
ansible websrvs -m script -a 'f1.sh'
#Copy：从服务器复制文件到客户端
ansible all -m copy -a 'src=/etc/shadow dest=/data/ mode=000 owner=user backup=yes'
如目标存在，默认覆盖
#Fetch：从客户端取文件到服务器端，copy相反，目录可先tar
ansible srv -m fetch -a 'src=/root/a.sh dest=/data/scripts'
#File：设置文件属性，新建或修改，删除
ansible srv -m file -a "path=/root/a.sh owner=wang mode=755"
ansible web -m file -a 'src=/app/testfile dest=/app/testfile-link state=link'
ansible all -m file -a 'name=/data/dir1 state=directory'
ansible all -m file -a 'name=/data/dir1 state=absent'
ansible all -m file -a 'name=/data/file1 state=touch'
#Hostname：管理主机名
ansible host -m hostname -a 'name=newhost'
#Cron：计划任务
支持时间：minute，hour，day，mouth，weekday
ansible srv -m cron -a "minute=*/5 job='/usr/sbin/ntpdate 172.16.0.1 &> /dev/null name=Synctime'" 创建任务
ansible srv -m cron -a 'minute=* weekday=1,3,5 job="/usr/bin/wall FBI Warning" name=warning'
ansible srv -m cron -a 'disabled=true job=/usr/bin/wall FBI Warning name=warning'
ansible src -m cron -a 'disabled=false job=/usr/bin/wall FBI Warning name=warning'（其中的ture和false也可以用yes与no替代）
ansible src -m cron -a 'job=/usr/bin/wall FBI Warning name=warning state=absent'
#Yum：管理包
ansible srv -m yum -a 'name=httpd state=present'
ansible srv -m yum -a 'name=httpd state=latest' 安装
ansible srv -m yum -a 'name=httpd state=removed'
ansible srv -m yum -a 'name=httpd,memcached,mariadb state=absent' 卸载
#Service：管理服务
ansible srv -m service -a 'name=httpd state=stopped'
ansible srv -m service -a 'name=httpd state=started enabled=true'
ansible srv -m service -a 'name=httpd state=reloaded/restarted'
#User：管理用户
ansible srv -m user -a 'name=user1 comment="test user" uid=2048 home=/app/user1 group=root groups=user'
ansible srv -m user -a 'name=sysuser1 shell=/sbin/nologin system=yes home=/app/sysuser1'
ansible srv -m user -a 'name=user1 state=absent remove=yes' 删除用户及家目录等数据
#Group：管理组
ansible srv -m group -a "name=testgroup system=yes"
ansible srv -m group -a "name=testgroup state=absent"

```



ansible-galaxy：

连接https://galaxy.ansible.com下载相应的roles

列出所有已安装的galaxy：**`ansible-galaxy list`**

安装galaxy：**`ansible-galaxy install geerlingguy.redis`**

删除galaxy：**`ansible-galaxy remove geerlinggue.redis`**



ansible-pull：推从命令至远程，可提升效率但对运维要求较高



ansible-playbook：

使用语法：**`ansible-playybook hello.yml`**

**`cat hello.yml`**

```yaml
#hello world yml file
	  - host: websrvs
	    remote_user: root
	    tasks:
	      - name: hello world
	         command: /usr/bin/wall hello world
	  ignore_errors: True #（忽略错误信息）
```



**`ansible-vault encrypt hello.yml`**：加密playbook
**`ansible-vault view hello.yml`**
**`ansible-vault rekey hello.yml`**
**`ansible-vault edit hello.yml`**

**`ansible-console`**：可执行交互式命令