Date: 2014-6-1 17:30
Title: Linux命令概要
Category: Linux
Summary: Command Summary of Linux

====================================

#Linux命令概要

##帮助命令

* *whatis*
* *man*
* *info*
* which : 找出命令路径
* whereis : 找到命令路径

##用户

* finger someuser
* who
>who am I
* su
* sudo
* passwd

##shell

* history 显示当下最近输入的命令
* alias 显示所有的命令别称
* env 显示所有的环境变量
<pre>
    $export var=value
</pre>
将环境变量 var 设置为value

* expr 1+1 计算1+1

##文件系统

* du -sh somefile 以人类可见格式显示文件的摘要大小信息
* find 查找命令
* locate 寻找包含有字符串的路径
> $updatedb 更新数据库 获取最新locate信息

* pwd 显示当前路径
* cd *path* 跳转到path目录下

##文件操作

* touch
* rm
* cp
* ls
* mkdir
* rmdir
* chown
* chmod
* chgrp
* *file*
* od -c somefile 以二进制形式显示文件内容

##文件显示

* cat
* head
* tail
* more
* less
* diff
* sort 对文件中的行进行排序
* uniq 显示文件中不重复的行
* wc 统计字数

##文本

* echo

##时间与日期

* date
* sleep

##进程

* top
* ps
* kill
* time
* lsof
* dmesg

##硬件

* uname -a 显示系统信息
* df -lh
* mount 显示系统挂在情况
* pagesize
* free
* arch

##网络

* ifconfig
* iwconfig
* route
* netstat
* ping
* traceroute
* dhclient
* host
* wget

##SSH登录与文件传输

* ssh
* sftp
* scp

##压缩与归档

* gzip
* unzip
* zip
* gunzip
* tar

##打印

* lpt
* lpstat







