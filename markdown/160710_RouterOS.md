## 使用 *Router OS* 分流国内外流量的一些经验

### 前期准备
  - 一台国外服务器 或者一个VPN帐号
    - 我使用的是pptp 也可以使用gre ipip这些
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
    
