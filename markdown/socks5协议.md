Date: 2015-1-13 12:16
Title: Socks5协议
Category: NetWork
Sumary: Socks5 Protocol

===========================

## socks5 协议

#### 特点
- 标准 RFC1928
- socks4 的改进版本
- 增加了用户名密码认证
- 增加了DNS域名查询

#### 握手经过

- 客户端发起

| field1 | field2 | field3 |
|:------:|:------:|:------:|
| 1 byte | 1 byte | 1 byte per method |
| 版本号 | 支持的认证方法数量 | 认证方式代码 |
| \x05   | \x00   | \x00 | 
    
- 服务端返回

| field1 | field2 |
|:------:|:------:|
| 1 bytes| 1 bytes|
| 版本号 | 认证方式代码 |
| \x05   | \x00   |
    
#### 传送数据

- 客户端请求

| 协议版本号 | 请求类别 | 保留位 | 地址类型 | 目的地址 | 端口号 |
|:------:|:-------:|:-------:|:---------:|:----------:|:----:|
| 1 byte | 1 byte | 1 byte|1 byte|dynamic| 2 byte |
| \x05 | \x01 | \x00 | \x01 | **4 bytes of IPv4** **16bytes of IPv6** **1 byte of name length and the name** | \x08\x00 |

- 服务端返回

| 版本号 | 状态 | 保留字段 | 地址类型 | 目的地址 | 端口号 |
|:---:|:---:|:---:|:---:|:---:|:---:|
|1 byte | 1 byte | 1 byte | 1 byte | 跟客户端请求一致 | 2 bytes |
| \x05 | \x00 | \x00 | \x01 | as the client | \x08\x00 |
    
