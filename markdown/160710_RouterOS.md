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

    > /interface pptp-client add user=hello password=hello default_route=no

  3. 添加策略路由 使标记为foreign的流量走VPN

    > /ip route add routing-mark=foreign gateway=vpn

  4. 整理国内IP为 address-list 标记为china 做成rsc脚本上传到ros 执行
    
    > /ip firewall address-list add address=1.0.1.0/24 name=china

  5. 打标签 把来自本地的 去往非国内流量非本地流量标记为 foreign
    
    > /ip mangle src-address=192.168.88.0/24 dst-address-list=!china dst-addres-type=!local action=marking-route new-routing-mark=foreign 

  6. 设置DHCP-SERVER 不使用运营商自带的DNS 用谷歌DNS
    
    > /ip dhcp-server set dns=8.8.8.8

  7. 添加路由 到谷歌DNS的包走VPN

    > /ip route add dst=8.8.8.8/32 gateway=VPN
    
  8. 路由器里面设置 VPN NAT
  
    > /ip firewall nat add src-address=192.168.88.0/24 chain=srcnat action=masquerade out-interface=vpn


### 踩过的坑
  - 默认使用运营商DNS 设置DHCP server 的DNS才解决
  - 现在默认使用国外DNS QQ空间和京东会上国外版

### 急需改进的地方
  - DNS必须默认使用运营商DNS 深度包检测敏感词然后打标记走8.8.4.4
