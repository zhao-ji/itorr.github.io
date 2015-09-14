# 抓包工具 Scapy

---
## Content
    1. IP 包结构， ICMP 包结构， TCP 包结构， UDP 包结构
    2. BPF(Berkeley Packet Filter)，学习使用 tcpdump
    3. Scapy 安装、使用、小例子
    4. GFW 观察
----
## Limit
    1. 网络层之上
    2. 应用层之下
    2. IPv4
    3. No NAT
----
## 推荐书目
    1. TCP/IP 协议详解
    2. 超级安全工具集
----

### 网络层以上常用包结构

#### IP
    * 通常 20 个字节
    * 版本号 IPv4
    * IP 头部长度 以 **4字节** 为单位, 最小是*5*，最大是*15*
    * IP 报文全长
    * TTL time-to-live (Traceroute 就是在用这个)
    * 协议
        * 1 ICMP
        * 6 TCP
        * 17 UDP
        * 89 OSPF
    * checksum 经过每一跳路由都要经过重新计算，计算和校验步骤：
        * checksum 初始值设为零
        * 以两个字节为单位 相加
        * 溢出位拿出来 高位补零相加
        * 最后的和取反就是最终的 校验和
        * 接收端收到后 拆成两两字节 相加 和为0
    * 源地址和目的地址
![IP 包结构](http://7sbpck.com1.z0.glb.clouddn.com/ip.png)
    
#### ICMP
    * 头部有 4 个字节
    * Type 一个字节
    * Code 一个字节
    * CheckSum 两个字节 校验 ICMP Header 和 Body
![ICMP 包结构](http://7sbpck.com1.z0.glb.clouddn.com/icmp.png)
    
> ###### ICMP-ECHO
        * **捕捉实例**
        * ID
        * Sequence
        * Timestamp
        
#### UDP
    * 头部 8 个字节
    * 源端口 [0, 65535] 目的端口 [1, 65535] 分别两字节
    * Length UDP 包总长度
    * CheckSum UDP 包校验和 （pseudo-header）
![UDP 包结构](http://7sbpck.com1.z0.glb.clouddn.com/udp.png)
> ##### DNS
        * 无连接
        * 实际操作抓包
        * GFW 投毒、劫持
        * GFW 双向劫持观察
> ##### No TCP
        * 服务器间通信
        * 小包 数据少 频繁
        * Replace HTTP with Socket
        * Replace TCP with UDP or ICMP
        * 新浪微博
        * BitTorrent  [BEP 0029](http://bittorrent.org/beps/bep_0029.html)
        * [No TCP](http://notcp.io/)
        
#### TCP
    * 头部一般是 20 个字节 最多 60 字节
    * 源端口 目的端口 各 16 位
    * Sequence Acknowledgment 各 32 位
    * Header Length 4 bit [5, 15]
    * Fin Syn Rst Push Ack Urg
    * CheckSum
    * 建立连接 三次握手
    * 释放连接 四次挥手
    * 抓包观察 三次握手 flags and seq/ack
    * 抓包观察 四次挥手 flags and seq/ack
    * 抓包观察 数据传输 http-scapy 抓取 HTTP 报文
    * GFW 观察 TCP Reset
![TCP 包结构](http://7sbpck.com1.z0.glb.clouddn.com/tcp.png)
    
----
### BGP 学习 使用
    * type
        * host
        	> host chashuibiao.org
        	> host 23.226.226.196
        * net
        	> net 10.0.80
        	> net 10.0.80.154/24
        * port
        	> port 80
        * portrange
        	> protrange 100-200
    * dir
    	* src
    		> src host chashuibiao.org
    	* dst
    		> dst port 80
    * proto
    	* ip
    	* udp
    	* tcp
    	* icmp
    * len
    	* less than
    		> len <= length
    	* greater than
    		> len >= length
    * flags
    	* icmptype
    	* icmpcode
    	* tcpflags
    * logical operator
    	* and
    	* or
    	* not
----
### Scapy 安装 使用 帮助

#### 我们为什么要使用 Scapy
	* 能发包
	* 发包时能控制包的每一个细节
	* 能抓包
	* 抓完能看包的每一个细节 （多种图形化展示方式）
	* 能边抓边看 交互式发现、摸索
	* 放在脚本里面用
#### 安装
	* sudo apt-get install tcpdump graphviz imagemagick python-gnuplot python-crypto python-pyx
	* sudo pip install scapy scapy-http
#### 帮助
	ls()
	
	import __builtin__
	from pprint impor pprint
	pprint(filter(lambda f: f.islower(), dir(__builtin__)))
	
	ls(IP)
	ls(ICMP)
	ls(UDP)
	ls(DNS)
	ls(DNSQR)
	ls(TCP)
#### 魔法函数
	* from scapy_http import http
	* traceroute 
	* tshark wireshark
	* sniff
	* rdpcap wrpcap
	* .summary() .show()
	* send() sendp() sendpfast()
	* sr1() sr() 
	* promiscping() is_promisc()
#### 实际上手操作
	1. sniff use BPF and scapy_http
	2. Christmas-Scan (PFU) FIN-scan Null-scan
