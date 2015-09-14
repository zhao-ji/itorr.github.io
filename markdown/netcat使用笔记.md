Date: 2015-1-12 20:00
Title: netcat 使用笔记
Tag: Linux-Command NetWork
Category: NetWork
Summary: the Linux Command NetCat

======================

## netcat 三个例子

### 本地 client-server socket 模式
- 服务端：
    nc -l 666
- 客户端：
    nc localhost 666
        
### 用 nc 传送文件
- 服务端：
    nc -l 666 | tee new_file.txt
- 客户端：
    cat file.txt | nc localhost 666
    
### 永不断开的服务端
- 服务端：
    nc -k -l 666
- 客户端：
    nc localhost 666
    
### 端口扫描
- `nc -zv example.com 1-65536 2>&1| grep succee`

### 服务端启用执行 SHELL
- 服务端
    nc -l 666 -e /bin/sh
    
## netcat 参数详解

### 两端都适用的参数
- -u UDP连接
- -4 IPV4 -6 IPV6
- -d 不接受 stdin 的输入

### 服务端适用的参数
- -k 即使客户端断开，服务端也不断

### 客户端适用的参数
- -w 10 十秒接受不到内容就断开
- -n 不查询DNS
- -p 设置源端口
      
### netcat 蜜罐
- netcat -l -p 442 实时监听442端口

