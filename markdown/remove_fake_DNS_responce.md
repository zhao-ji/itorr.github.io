## 现象陈述
* 在国内请求谷歌DNS，GFW会返回虚假DNS应答包，俗称 DNS劫持
* 有时是一个，但目前大多时候是两个
* 返回的 fake DNS responce 有一些特征
* fake responce 返回的IP是随机的
* 返回的 TTL 是完全随机的
* 返回的 ToS 字段固定的是 0x00 0x10

## 过滤手段
* 根据 ToS 字段过滤掉 8.8.8.8 fake responce
* sudo iptables -A INPUT -s 8.8.8.8 -p udp --sport 53 -m tos --tos 0x0 -j DROP
* sudo iptables -A INPUT -s 8.8.8.8 -p udp --sport 53 -m tos --tos 0x10 -j DROP
* 根据 flags DF 位过滤掉 208.67.222.222(OpenDNS) fake responce
* sudo iptables -A INPUT -s 208.67.222.222 -p udp --sport 53 -m u32 --u32 "0x3&0x40>>0x6=0x0" -j DROP


## 过滤特点
* 能拿到正确的DNS解析结果
* 可能有时效性 过段时间就不行了
* 被广泛传播后 可能会被封锁
* 不能拿到最优的DNS解析结果
* 想要拿到最优的解析结果还得从运营商或者国内 DNS 查询
* 关于 DNS 分流现在只是有个初步的想法 还不成熟
