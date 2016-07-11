## 使用 *Router OS* 分流国内外流量的一些经验

### 前期准备
  - 一台国外服务器 或者一个VPN帐号
    - 我使用的是pptp 也可以使用gre ipip这些
    - 注意配置好服务器上面的路由
  - 国内IP列表
    - 目前使用的是高春辉整理的国内IP列表
    - 主流操作是使用ICANN的IP列表 筛选出国内IP
    - 高春辉的列表更加精简而且两个月一更新 但是是否有疏漏不得而知
  
### 操作步骤
  1. SSH登录Router OS
  2. 添加VPN接口

    > /interface pptp-client add name=vpn user=hello password=hello connect-to=1.2.3.4 default_route=no

  3. 添加策略路由 使标记为foreign的流量走VPN

    > /ip route add routing-mark=foreign gateway=vpn

  4. 整理国内IP为 address-list 标记为china 做成rsc脚本上传到ros 执行

    > /ip firewall address-list add address=1.0.1.0/24 name=china

  5. 打标签 把来自本地的 去往非国内流量非本地流量标记为 foreign

    > /ip mangle chain=prerouting src-address=192.168.88.0/24 dst-address-list=!china dst-addres-type=!local action=mark-routing new-routing-mark=foreign

  6. 路由器里面设置 VPN NAT

    > /ip firewall nat add src-address=192.168.88.0/24 chain=srcnat action=masquerade out-interface=vpn

  7. DNS设置为运营商分配的DNS 不用动
  8. 在layer7-protocol中标记DNS查询中包含敏感词的请求

    > /ip firewall layer7-protocol add comment="polute domain" name=polute regexp="polute-domain-regex"
    
  9. 在 prerouting 中标记流量

    > /ip firewall mangle add chain=prerouting action=mark-connection new-connection-mark=domain passthrough=yes protocol=udp layer7-protocol=polute dst-port=53
    
  10. nat 使DNS请求转向8.8.4.4查询

    > /ip firewall nat add chain=dstnat action=dst-nat to-address=8.8.4.4 connection-mark=domain
    > /ip firewall nat add chain=srcnat action=masquerade connection-mark=domain
  
  11. 过滤伪造的DNS响应

    > /ip firewall filter add chain=input action=drop protocol=udp src-address=8.8.4.4 src-port=53 dscp=0
    > /ip firewall filter add chain=input action=drop protocol=udp src-address=8.8.4.4 src-port=53 dscp=10

