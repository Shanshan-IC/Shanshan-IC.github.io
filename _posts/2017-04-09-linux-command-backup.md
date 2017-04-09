---
layout:     post
title:      "Linux Command Backup"
category:   Linux
tags:		Linux
---

* content
{:toc}

## User

* create an account

```
useradd shanshan
```

* delete an account

```
userdel shanshan
```

* Get the errors

creating mailbox fiel:file exists, you should :

```
userdel -r shanshan
sudo useradd -d /shanshan/test -m shan
```

* update password

```
sudo passwd shan
```

* check users

```
w
who
```

* shift user

```
su shan
```

* errors: shans is not in the sudoers file

check the sudoers location

```
whereis sudoers
chmod u+w /etc/sudoers
```

在root ALL=(ALL)ALL行下添加
shan ALL=(ALL)ALL

还原权限

```
chmod u-w /etc/sudoers
```

* swift the user

```
exit
```

## Structure

/bin：

bin是Binary的缩写, 这个目录存放着最经常使用的命令。

/boot：

这里存放的是启动Linux时使用的一些核心文件，包括一些连接文件以及镜像文件。

/dev ：

dev是Device(设备)的缩写, 该目录下存放的是Linux的外部设备，在Linux中访问设备的方式和访问文件的方式是相同的。

/etc：

这个目录用来存放所有的系统管理所需要的配置文件和子目录。

/home：

用户的主目录，在Linux中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。

/lib：

这个目录里存放着系统最基本的动态连接共享库，其作用类似于Windows里的DLL文件。几乎所有的应用程序都需要用到这些共享库。

/lost+found：

这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。

/media：

linux系统会自动识别一些设备，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目录下。

/mnt：

系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。

/opt：

 这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。

/proc：

这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。

这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件，比如可以通过下面的命令来屏蔽主机的ping命令，使别人无法ping你的机器：

echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all

/root：

该目录为系统管理员，也称作超级权限者的用户主目录。

/sbin：

s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序。

/selinux：

 这个目录是Redhat/CentOS所特有的目录，Selinux是一个安全机制，类似于windows的防火墙，但是这套机制比较复杂，这个目录就是存放selinux相关的文件的。

/srv：

 该目录存放一些服务启动之后需要提取的数据。

/sys：

这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统 sysfs 。

sysfs文件系统集成了下面3种文件系统的信息：针对进程信息的proc文件系统、针对设备的devfs文件系统以及针对伪终端的devpts文件系统。

该文件系统是内核设备树的一个直观反映。

当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。

/tmp：

这个目录是用来存放一些临时文件的。

/usr：

这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似与windows下的program files目录。

/usr/bin：

系统用户使用的应用程序。

/usr/sbin：

超级用户使用的比较高级的管理程序和系统守护程序。

/usr/src：

内核源代码默认的放置目录。

/var：

这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。

## linux command review

`ls`

```
ls -a
ls -all
# all files and directory
ls -l -R 
# 当前目录下t开头的内容
ls -l t**
# 当前目录的所有文件的绝对路径，目录不递归
find $PWD -maxdepth 1 | xargs ls -ld
#当前目录的所有文件的绝对路径，目录递归
find $PWD | xargs ls -ld 
```

`cd`

```
cd data/workspace
cd -
```

`mkdir`

```
# 递归生成多个文件夹
mkdir -p test/test
# 赋予777权限生成文件夹
mkdir -m 777 test2
#777：rwxrwxrwx
```

`rm`

```
rm -r -f test.c
```

`rmdir` 删除非空目录

```
rmdir test
rmdir -p test
# 如果删除后它变成了非空目录，那么也递归一并删除
```

`mv` 改名和移动文件

```
mv test.c test2.c
mv test2.c test2
# 所有文件移动到上级目录
mv * ..
```

`cp` 复制文件或目录

```
# 文件
cp test2.c test2
# 整个文件夹下的东西
cp test2 test
```

`touch`

```
# 新建一个文件
touch test3.c
# 修改时间戳相等
touch test2.c test3.c
ll
```

`cat`

```
cat test2.c
# 文件添加到后面
cat -n test2.c test3.c
```

`nl` 显示行号

```
nl test2.c
```

`more`命令，功能类似`cat`，`cat`命令是整个文件的内容从上到下显示在屏幕上。 more会以一页一页的显示方便使用者逐页阅读，而最基本的指令就是按空白键（`space`）就往下一页显示，按`b`键就会往回（`back`）一页显示，而且还有搜寻字串的功能 。

```
more test2.c
# 每屏显示2行代码
more -2 test2.c
```

less和more功能一样，但更强大


`head`和`tail`

```
# 显示前两行和后两行
head -n 2 test2.c
tail -n 2 test2.c
# 前两个字节
head -c 2 test2.c
```

`which` 找到可执行文件的位置

```
which ls
which cd 
#找不到cd命令，因为cd是bash内置的命令
```

`whereis`命令只能用于程序名的搜索，而且只搜索二进制文件（参数-b）、man说明文件（参数-m）和源代码文件（参数-s）。如果省略参数，则返回所有信息。
和find相比，whereis查找的速度非常快，这是因为linux系统会将 系统内的所有文件都记录在一个数据库文件中，当使用whereis和下面即将介绍的`locate`时，会从数据库中查找数据，而不是像`find`命令那样，通过遍历硬盘来查找，效率自然会很高。
但是该数据库文件并不是实时更新，默认情况下时一星期更新一次，因此，我们在用`whereis`和`locate`查找文件时，有时会找到已经被删除的数据，或者刚刚建立文件，却无法查找到，原因就是因为数据库文件没有被更新。 


`find` 目录下查找

```
find -atime -1
# 1天内修改过的文件
find . -name "*.c"
```

`chmod`命令

权限范围：

* u ：目录或者文件的当前的用户

* g ：目录或者文件的当前的群组

* o ：除了目录或者文件的当前用户或群组之外的用户或者群组

* a ：所有的用户及群组

权限代号：

* r ：读权限，用数字4表示

* w ：写权限，用数字2表示

* x ：执行权限，用数字1表示

* - ：删除权限，用数字0表示

* s ：特殊权限 

```
# 新增可执行权限
chmod u+x test2.c
# 同时修改权限
chmod ug+w,o-x log2012.log
chmod 751 test2.c
# 给file的属主分配读、写、执行(7)的权限，给file的所在组分配读、执行(5)的权限，给其他用户分配执行(1)的权限
```

`tar` 打包

仅打包，不压缩！ 

```
tar -cvf test2.tar test2.c
# 打包后，以 gzip 压缩 
tar -zcvf test2.gz test2.c
# 打包后，以 bzip2 压缩 
tar -zcvf test2.bz2 test2.c
```

`chgrp`	改变群组

`chown`  确定群组

`gzip`	压缩和解压

```
# 文件夹下所有文件都压缩
gzip *
# 解压所有
gzip -dv *
# 递归得压缩目录
gzip -rv test6
```

`df` 查看磁盘使用情况

```
df
```

`du`	查看所占用的空间

```
du
du test2.c
du test2
```

`ln` 建立超链接

`ln`是linux中又一个非常重要命令，它的功能是为某一个文件在另外一个位置建立一个同步的链接.

```
# 软连接
ln -s test2.c linktest
# 硬链接
ln test2.c linktest
```

`diff` 比较文件

```
diff test2.c test3.c
# 上下文的格式输出
diff test2.c test3.c -c
# 比较文件夹
diff test2 test
```

`date` 命令

```
date
date '+%c'
date '+%D'
date '+%x'
date '+%T'
date '+%X'
```

`cal` 日历

```
cal
cal -y 2013
```

`grep`	正则表达式

`grep`命令是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹 配的行打印出来。

```
# 文件中查找关键词
grep 'linux' test.txt
# 多个文件中查看关键词
grep 'linux' test.txt test2.txt
# u开头的内容
cat test.txt |grep ^u
# hat结尾的内容
cat test.txt |grep hat$
```

`wc` Word Count 命令的功能为统计指定文件中的字节数、字数、行数，并将统计结果显示输出。

-c 统计字节数。

-l 统计行数。

-m 统计字符数。这个标志不能与 -c 标志一起使用。

-w 统计字数。一个字被定义为由空白、跳格或换行字符分隔的字符串。

-L 打印最长行的长度。

-help 显示帮助信息

--version 显示版本信息

```
wc test.txt
```

`ps` Process Status的缩写。ps命令用来列出系统中当前运行的那些进程。

```
ps -A
# 指定用户进程
ps -u root
# ps 与grep 常用组合用法，查找特定进程
ps -ef|grep ssh

`kill`

```
# 列出所有信号
kill -l
# 找到名字后，kill
kill -l name
# 或者用ps找到
kill 3268
#彻底杀死
kill -9 3268


`killall`

```
# kill同名进程
killall vi
```

`top`命令是Linux下常用的性能分析工具，能够实时显示系统中各个进程的资源占用状况，类似于Windows的任务管理器。

```
top
```

`free`命令可以显示Linux系统中空闲的、已用的物理内存及swap内存,及被内核使用的buffer。

```
free
```

`watch`可以帮你监测一个命令的运行结果，省得你一遍遍的手动运行

```
# 每隔一秒高亮显示网络链接数的变化情况
watch -n 1 -d netstat -ant
```

`lsof`（list open files）是一个列出当前系统打开文件的工具。在linux环境下，任何事物都以文件的形式存在，通过文件不仅仅可以访问常规数据，还可以访问网络连接和硬件。

`ifconfig`

许多windows非常熟悉ipconfig命令行工具，它被用来获取网络接口配置信息并对此进行修改。Linux系统拥有一个类似的工具，也就是ifconfig(interfaces config)。

```
ifconfig
# 启动关闭制定网卡
ifconfig eth0 up
ifconfig eth0 down
# 关闭网卡并修改MAC地址
ifconfig eth0 hw ether 00:50:56:BF:26:20
# 配置IP地址
ifconfig eth0 192.168.120.56 
```

`route` 显示和操作IP路由表

```
# 显示当前路由器
route 
# 添加网关
route add -net 224.0.0.0 netmask 240.0.0.0 dev eth0
# 删除网关
route del -net 224.0.0.0 netmask 240.0.0.0
```

`ping`	测试与目标主机的连通性

```
ping 192.168.120.205
```

`traceroute`	知道信息从你的计算机到互联网另一端的主机是走的什么路径

```
traceroute hostname
traceroute www.baidu.com
```

`xshell` 文件传输

```
rz # 上传
sz test.c
# 下载到本地
```

`ss`	`ss`是Socket Statistics的缩写。顾名思义，`ss`命令可以用来获取socket统计信息，它可以显示和netstat类似的内容。但`ss`的优势在于它能够显示更多更详细的有关TCP和连接状态的信息，而且比netstat更快速更高效。

```
# 显示TCP连接
ss -t -a
# socket 摘要
ss -s
# 列出所有打开的网络连接端口
ss -l
# 显示所有UDP Sockets
ss -u -a
```

`telnet`	远程登录

```
telnet 192.168.120.209
talnet www.baidu.com
```

`rcp`	remote file copy

`scp`	secure copy

用于在Linux下进行远程拷贝文件的命令，和它类似的命令有cp，不过cp只是在本机进行拷贝不能跨服务器，而且scp传输是加密的。

`wget`	下载