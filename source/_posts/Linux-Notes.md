---
title: Linux Notes
date: 2020-02-14 13:00:54
tags: [笔记, Linux]
---

# 一、初识

## 1、Linux用途

免费的，开源的，主要用于服务器领域，性能稳定，安全。大多数企业使用的都是Linux系统。

Linux一般用来做服务器端的操作系统。

<!-- more -->

[siki学院资料](http://www.sikiedu.com/course/345/material/29127/download)

[siki学院视频](https://www.bilibili.com/video/av71383568)

## 2、什么是操作系统

操作系统=我们开机之后进入的操作环境就是Windows操作系统 

电脑 = 硬件 + 操作系统（软件） 

硬件=鼠标 键盘 显示屏 耳机 CPU 主板 内存卡 声卡，等肉眼可以看见，手可以摸得到的东西

**操作系统是我们玩电脑的时候的中介。 我们用硬件 鼠标键盘 显示器 操作系统负责收集你在键盘和鼠标上做的什么事情，然后显示给显示器，或者保存到硬盘上。**

**操作系统分类**

桌面、服务器、手机、嵌入式 

桌面操作系统：给大众使用的 Windows MacOS Linux Windows xp windows 7 windows10

服务器操作系统：其实服务器就是我们平时使用的电脑主机

Linux

 Windows Server 2008 2010 2018 

Mac OS Server

手机（iPad）操作系统 （基于Linux）Android iOS
嵌入式操作系统（手机、游戏机，汽车、MP3、MP4、智能家具、人工智能软件...） Linux

操作系统不止Windows这一种，还有MacOS、Linux 手机上也是硬件和操作系统的结合 Android iOS 我们使用的软件（QQ 浏览器 播放器 等）的运行环境就是操作系统。我们使用编程语言开发的软
件，就是运行在操作系统上的，Windows和MacOS一般家用，我们可以叫做客户端，客户端操作系统。 Linux一般运行在服务器端，所以Linux可以叫做服务器端操作系统

## 3、GNU/Linux 的历史

自由软件之父 Richard M. Stallman 1984 GNU Copyleft OpenSource Free GPL

Linux 之父 Linus Torvalds林纳斯.托瓦兹 1991
[www.kernel.org](http://www.kernel.org)
 Linus之父 2017.6.19 来中国了，Linux基金会宣布在华建立正式分支机构

Linux 发行版介绍 RHEL/Centos/Ubuntu/Suse/Debian

Linux 相关认证介绍RHCE/RHCA

[Linux发展历史](https://blog.csdn.net/zengxiantao1994/article/details/53141747)

## 4、学习方向

怎么创建文件夹，怎么创建文件，怎么保存文件，怎么控制文件权限，怎么运行程序，怎么安装程 序.... 那我们学习Linux也是学习怎么在Linux操作系统上做上述事情，不过Linux上没有可视化的操作界
面，不能使用鼠标，所以我们要学习怎么使用命令来完成我们平时在windows电脑上很常见的操作。

## 5、Linux版本与虚拟机

**Linux版本**

​			内核版本：操作系统心脏，处理跟各种硬件打交道的工作。 

​								硬件管理，内存管理，文件系统，线程管理..... 

​								稳定版本 开发版本
​			发行版本 

​								内核版本+各种应用软件（办公 媒体播放 浏览器 数据库 .... ） 

​								Ubuntu Redhat CentOS ...

**虚拟机**

​	 虚拟的计算机，一台电脑上只能同时运行一个操作系统。有了虚拟机，我们可以现有计算机的基础上，安装多个其他的操作系统（包括Linux Windows），可以很方便通过虚拟机对操作系统进行安装、卸载，这样方便我们学习别的操作系统。 虚拟机其实就是一个软件，虚拟的计算机，它用来模拟一个真实存在的计算机，我们可以安装操作系统在这个模拟的计算机环境上。

[VMWare安装](https://blog.csdn.net/weixin_43925504/article/details/89099541)

[Ubuntu](https://cn.ubuntu.com/download)

**Linux文件系统（目录和文件） **

Windows下有盘符

Linux没有盘符的概念，只有一个根目录

不同的目录有哪些作用： 

/home/用户名 存储一些用户相关的文档 

/usr 安装的应用程序 

[Linux各个目录以及每个目录的作用介绍](http://www.cnblogs.com/duanji/p/yueding2.html)

# 二、Linux终端命令

## 1、目录相关

**ls**（list查看所有内容）

+ ls -l以列表形式展示（缩写**ll**）

+ ls -a显示全部文件，包含隐藏文件(**.开头的文件都是隐藏文件，创建时加“.即可隐藏”** )

  第一个表示当前目录，第二个表示上级目录，表明文件之间的层级关系。

  ![Linux-1](https://github.com/ZephXu07/IMG/raw/master/Linux-1.png)

+ 以上两个可组合ls -l -a

+ ls -l -h以列显示，大小单位为K，没有的话单位为字节（Byte）

+ ls -lh，ls -lha简写，顺序可变

+ ls通配符（[更加详细介绍](https://www.cnblogs.com/0zcl/p/6821213.html)）

  ![Linux-2](https://github.com/ZephXu07/IMG/raw/master/Linux-2.png)

**pwd**（print work directory查看所在路径）

**cd**（change directory打开目 录）

+ cd .：切回当前目录

+ cd .. ：切回上一级
+ cd ../..：切回上一级的再上一级
+ cd ~：回到home目录）
+ cd -切换最近的两个目录来回切换 （在当前目录和上一个目录 来回切换）
+ 相对路径：相对于当前目录
+ 绝对路径：从根路径开始完整的路径（从\和~开始的路径都是绝对路径）

**tab** 自动补全），可以补全文件 目录（***当且仅当只有唯一一个符合前几个字母的文件，多个时按一次没有效果，按两次会显示所有相关目录***）

**方向键** 上下 上一个命令 下一个命令

## 2、文件相关

**文件\文件夹的**：创建、删除、移动（剪切、重命名）、复制

+ touch（创建文件）
+ + 创建隐藏文件 touch .test.txt
+ mkdir（创建文件夹）
+ rm（移除）
+ + rm xx （文件）
  + rm -d xx  （空文件夹）
  + rm -r xx （有内容文件夹）
+ mv（移动） mv 文件 目录   可使用相对路径或绝对路径
+ + mv 125.odt .    提示是同一个文件
  + mv 125.odt ./126.odt     重命名
+ cp（复制） 
+ + 文件    cp 123.odt bb  复制123.odt到相对当前目录的bb目录下
+ + 目录   cp -r bb/aa .    复制bb目录下的aa文件夹到当前目录

## 3、Linux命令的格式

**cmd -option parameter **

cmd是命令，就是一个操作 

parameter一般是要要做的对象 

option一般是用来修改parameter的，就是这个是一个什么样的对象 

杀一个男人 杀是命令 人是参数 男是修饰

**命令 --help**：查找帮助手册

**man 命令**：详细手册

## 4、which查看命令所在位置

每个命令（ls touch mkdir mv cd）执行的时候，都会去执行一个程序，这个程序文件里面保存了当我们 执行某个命令的时候需要做哪些事情，来完成这个命令，并输出结果。 

**which cd 为空，cd是shell内置的命令**

/bin 	binary，二进制文件，普通命令
/sbin 	system binary,系统二进制文件,需要有系统权 

/usr/bin	 用户安装的应用程序
/usr/sbin	 超管安装的应用程序

 带s和不带s的区别，带usr和不带usr的区别

## 5、文件搜索

### a、ls通配符：仅限于当前目录下的模糊查找

### b、find 搜索范围 搜索条件 

示例一：find /home -name 123.odt //精确搜索

示例二：find /home -name 123* //模糊搜索 其他用法：*123* 123？？ 

示例三：find /home -iname abc //选项-i 不区分大小写

示例四：find / -size +204800	//根据文件大小搜索，1数据块=512字节Byte=0.5KB

-204800 204800 // 100MB 100*1024KB 100*1024*2*数据块

示例五：find /home -user siki	//文件所属人

示例六：find /home -mmin -5 	文件内容上次被修改时间在5分钟以内 

+ mmin上次文件内容被修改时间 

+ amin 上次文件被访问时间 

+ cmin 上次文件属性（文件的权限）

+ 被修改时间 

+ + -5 5分钟以内

+ + +5超过5分钟

示例七：find /home -type f 

+ -type文件类型 f文件 d目录（文件夹）l软链接文件（Link）

**-a and同时满足 -o or或者，满足其中一个即可 **

示例八：find /home -name 123 -a -size +5

示例九：ls -i **显示每个文件各自的id（不重复）**

find /home -inum 3434	通过id搜索

### c、locate

locate搜索比较快，因为它搜索的是自己的索引库 

+ 优点：查找快

+ 缺点：最新文件找不到（需要时间更新索引库）

  locate 123.odt	会搜索包含'123.odt'在内的所有文件，若是搜索目录，即目录下所有文件将会被搜索到
+ sudo updatedb	命令前面加sudo表示通过管理员方式运行

## 6、文件内容

### a、查看文件内容：cat、more

+ cat xx.txt 显示所有文件内容 
+ cat -b xx.txt 显示行号 去除空行 
+ cat -n xx.txt 显示行号 包含空行 
+ more xx.txt 分页显示文件内容 下一页（空格） 上一页（b） 下一行（Enter）

### b、搜索文件内容：grep

+ grep xx xxx.txt   显示包含内容行
+ grep -n xx xx.txt 显示包含内容行的行号 
+ grep -v xx xx.txt 去掉包含内容的行，显示其他所有内容 
+ + grep -v '#' xx.txt 去掉带#的行（去掉带注释的行） '#' 
+ + grep -v ^'#' xx.txt 去掉以#开头的行
+ + grep -v \$'#' xx.ttxt	去掉以\$开头的行
+ grep -i xx xx.txt 忽略大小写搜索 

### c、多个文件的编辑

***linux中文件的后缀可以加可不加，加上方便识别，在linux中很多文本是没有任何后缀的。***

+ echo xxx 

+ echo xxx > xxx.txt 写入（覆盖） 

+ echo xxx >> xxx.txt 追加（末尾）

+ + ls > xx.txt 

+ + ls >> xx.txt 

+ + ls -lh > xx.txt
  + 将ls得到的写入

***任何有结果的命令均可使用">"或“>>”输出到某个文件中，文件不存在则创建。***

### d、管道

把一个命令的输出 通过管道连接 作为另一个命令的输入

输出就是命令的结果，输入一般是一个命令的参数（cat xxx.txt 这个txt就是cat的输入）

管道连接通过 ==|== 建立。

**ls -lh | grep 125**

### e、文件软链接：ln 文件/文件夹 软链接

# 三、用户管理、用户组管理 和权限

Linux是多用户的， 服务器是多个人管理（运维人员是多个）。

## 1、root用户

超管和普通用户的提示符的区别，为什么？

安装系统的时候不是默认启用一个root用户，而是创建一个普通用户来使用呢？

 root具有所有权限，能力越大，责任越大，越容易闯祸。 日常维护工作使用普通用户完成，除非遇到系统管理的工作，使用root来完成！

## 2、普通用户添加

用户添加 

+ 第一步：添加用户名 

+ + sudo useradd xx （-m：创建家目录 和 -g：指定所在的组 选项） 

+ 第二步：设置密码(不设置用户名的用户是不能使用的)（注意是passwd不是password） 

+ + sudo passwd xx （sudo passwd xx）
  + 直接passwd是设置当前用户的密码

==关于sudo命令== 

***是允许系统管理员让普通用户执行一些或者全部的root命令的一个工具，如useradd，halt，reboot，su 等等。这样不仅减少了root用户的登录 和管理时间，同样也提高了安全性。 用户使用sudo的时候，会验证当前用户的密码，然后又5分钟的有效期，有效期内执行sudo不需要在再输 入密码！ 切换到root就不需要sudo命令了。***

[相关百科](https://baike.baidu.com/item/sudo/7337623?fr=aladdin)

## 3、用户组

每个用户都有一个初始组，可以有零个或者多个附加组。用户组的作用，是为了方便权限控制。（附加组 就是为了给用户附加别的权限） 当创建用户的时候，系统会创建一个跟用户名同名的组。 

文件属性：所属用户、所属用户组

## 4、用户切换

+ su xx	用户切换
+ su - xx  	用户切换，并回到家目录

+ exit （ctrl+D）退出当前用户，返回上一个用户（从哪个用户切换过来的）如果没有上一个用户，直接退出终端
  

## 5、用户删除

userdel xx 

userdel -r xx 删除家目录 

userdel -f xx 强制删除，即使用户正在登陆系统

## 6、用户组管理

groupadd xx	添加 

+ cat /etc/group 确认组是否被添加成功

goupmod -n xx newxx 改名 
groupdel xx   删除

## 7、Linux中的ID

文件id uid gid

+ ls -i 	查看文件id

+ id	查看当前用户的uid和gid
+ id xx 	查看xx用户的uid和gid

## 8、关于配置文件

### a、/etc/group

配置当前系统有哪些用户组 1，组名 2，组密码标志 3，GID 4，组中附加用户

### b、/etc/passwd

配置当前系统有哪些用户，以及用户的密码（密码在影子文件里面，passwd的影子文 件）

![Linux-3](https://github.com/ZephXu07/IMG/raw/master/Linux-3.png)

1用户名 2密码标志 3UID 4GID 5用户全名 6家目录 7使用的shell

### c、什么是shell?（命令 cd ls ...）

shell是用来解析命令的，它接收用户命令，然后调用相应的程序执行。 

shell相当于一个翻译，翻译我们的命令，让机器听懂。 

+ 第一种shell：/bin/bash	翻译一号	
+ 第二种shell：/usr/sbin/nologin   翻译二号
+ 第三种shell：/bin/sh   翻译二号（我们创建用户的时候的shell）

![Linux-4](https://github.com/ZephXu07/IMG/raw/master/Linux-4.png)

查看所有shell： cat /etc/shells

修改shell：chsh

### d、影子文件

/etc/shadow

/etc/gshadow

存放密码，root影子文件中密码为加密，组影子文件中密码未设置显示为“!”。

### e、命令执行顺序

![Linux-5](https://github.com/ZephXu07/IMG/raw/master/Linux-5.png)

### f、which cd显示空白？

+ 1，为什么没有命令文件
+ + 因为cd这个命令是放在shell（bash里面的）
+  2，什么是内置命令（cd dirs ls）
+  +  内置命令在系统启动时就调入内存，是常驻内存的，所以执行效率高。 而外部命令是系统的软件功能，用户需要时才从硬盘中读入内存。 大部分内置命令都是内置在shell中的，也有一些内置命令有自己单独的文件。 系统启动，会把shell中的内置命令，其他其他不在shell中的内置命令加载到内存中。

+ (Linux内置命令和外置命令)[https://www.cnblogs.com/pingzhe/p/7077685.html]

### g、查看用户信息

+ id 当前登录用户详细信息

+ whoami  当前登录用户名

+ who 当前所有登录用户罗列出来

### h、修改用户信息（usermod）（某些需要重新登录生效）

+ usermod -g group user	修改初始组（基本不去修改）

+ usermod -G group,group xxuser    修改附加组（多个使用“,”）
+ usermod -s /bin/bash xxuser     修改shell

# 四、用户权限

**文件对用户来说的权限，用户操作文件或者文件夹的权限**

## 1、什么是可执行文件 

windows下的是exe（批处理命令或者说批处理脚本），一般用来启动某个应用程序的 linux下的shell脚本（或者类型的脚本），一般用来启动某个应用程序或者服务程序

## 2、权限

​	==- --- --- ---==

​       u   g    o

user  group   other

第一个==-==表示文件类型，==-==表二进制文件（包括不限于文本文件）==d==目录（文件夹）

第一个==---==表user，所有者

第二个==---==表group，所属组

第三个==---==表other，其他用户

==r==-->可读

==w==-->可写

==x==-->可执行

![Linux-6](https://github.com/ZephXu07/IMG/raw/master/Linux-6.png)

**一个文件（文件夹）改名、删除的权限是由它所在目录的权限控制的，而不是自身的权限控制。因为它自 身的权限只控制它自身的内容。**

## 3、文件权限修改

chmod change the permissions mode of file

只有文件所有者和超管可以修改文件的权限。

### a、

chmod \[ugo\]\[+-=\]\[rwx\] 文件或者目录

==+==添加，==-==减少，==\===设置为

+ chmod u+w,g+x xx.txt

### b、

用数字表示权限 r=4 w=2 x=1

r--rw-rwx	467

rw-r-x--x  	651

u	g	o

chmod 651 xxfile

chmod -R 777 xxfile 修改文件包括文件的所有子文件

### c、

rwx	--->	对应二进制 

r-- 		--->	100

-w-	---> 	010

--x	---> 	001

类似如此。

## 4、其他

### a、chown(change owner)修改拥有者（所属者）

chown newuser 文件/文件夹 修改文件或者文件夹的拥有者

### b、chgrp(change group)修改拥有组（所属组）

chgrp newgroupname 文件/文件夹 修改文件或者文件夹的所属组

### c、文件是所属者和所属组发生改变，用户对文件的权限也发生改变。

### d、-R 递归修改所有子文件