##OpenResty 开发者大会

###概况

- 在360大厦举行 人很满 中午在旁边小饭馆吃的饭
- openresty现在用的最多的是CDN厂商，有一些电商也在用，比如京东的商品详情页和阿里的Tengine
- 整体质量高，有个阿里的姚来强缺席找了个同事顶替干货不怎么多，有个adobe的代码没有跑起来。除了这两个都很好

###章亦春《浅谈OpenResty未来发展》
- openresty的过去
    - 起源 想用新技术做个人博客
    - 发展 雅虎搜索 需求功能琐碎 机器配置差劲 Perl+c openresty雏形 性能不好
    - 开始 淘宝量子统计
        - 当时面临的业务形势：业务逻辑复杂、数据量大、性能要求高
        - 在这一阶段完成了现在openresty
        - 成果 代码量减少90% 性能提升一个数量级（并发 延迟）
        - 自己搞了个小编译器，把针对业务的小语言编译成lua
`
技巧就是我经常鼓吹的一种玩法：设计一种针对业务的小语言，或者说DSL
`
`
我觉得很多时候不用纠结到底使用什么编程语言，更多的应该考虑来表达我们的业务。比如团队里面产品经理用犀利的语言把业务描述的很精确，那么他写的这个文档， 已经是这个业务系统本身了。我们写个编译机让它跑起来就行了。大家可以去想一思路。
`
    - 成熟 福州隐居 好多高级功能都是在这完成的
    - 加入cloudflare openresty在CDN行业取得成功
- openresty的现在
    - 三个应用场景
        - API Server
        - HTTP Proxy
        - Web Application
    - 设计目标
        - 简单 不需要的东西一定不能存在
        - 小巧 能够完全控制整个代码机
        - 快速 互联网环境拥挤 机器不尽如人意
        - 灵活 不要有太多的语言限制
        - 实用主义 高效 健壮 优美
        - 有趣 要让乐趣变成我们工作的主旋律 不要让工作变成一种负担
- openresty的未来
    - 教材 《OpenResty最佳实践》
    - 包管理器
    - 命令行工具 iresty 
    - 模块命名 github-ID/module-name 防止抢坑 鼓励fork
    - 命令行文档 标准模块 安装模块的格式化文档
    - 命令行解释器
    - LuaRocks 没有考虑Openresty的阻塞和非阻塞问题
    - 更多官方的二进制发布包
    - NginX成为一个TCP-Server UDP-Server
    - 新的模板 同一份模板服务端和客户端都可以用
    - Streaming Regex, lua-resty-pegex
    - semaphore
    - 基于list的共享内存
    - init_by_lua 支持 cosockets
    - cosockets连接池
    - ngx.connection 注册到nginx时间循环里的文件描述符
    - balencer_by_lua 刚刚开源的负载均衡器
    - ssl_certificate_by_lua 用lua严格控制下游SSL握手过程