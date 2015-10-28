##OpenResty：一种后端新玩法

----------------------------
###特点

- 在NginX中嵌入Lua 适合逻辑简单但性能要求高的应用
- 取代部分复杂晦涩的nginx配置语法 用简单明了的Lua来管理请求跳转

- 模块都是特殊打造的 但是相对缺乏
- NginX错误日志无法定制
- 各种错误处理 流程啰嗦

-----------------------------

###我用它来干什么

- 取代nginx的配置指令和正则表达式 (rewrite set_header proxy_pass)
- 规整请求
    - 旧的API传递的参数或者格式有缺陷 让OpenResty整理后再传给Python
    - 可以处理 query-parameter xml json headers (规整微信请求，格式化后传给后端)
- 小而精的需求 用 OpenResty 来处理
    - 反代
    - 短链接
    - 特定 IP User-Agent 请求频次限制
    
--------------------------------
###准备知识
- NginX upstream http server location
- Lua 基本语法
    - 《Programming In Lua》
    - 面向过程的语言 没有面向对象
    - 从1开始记数
    - 只有 nil 和 false 为假 0为真
    - 列表和字典统一起来了 Lua表
    - 局部变量 用local声明 而不是 全局变量用 global 没有Python 优雅
    - 不用了解太多，语法相当简单 OpenResty 里面用到的更是少得可怜
    
-----------------------------------
### OpenResty需要了解的几个部分
- 执行阶段
    - set_by_lua set_by_lua_file 变量初始化
    - rewrite_by_lua rewrite_by_lua_file 转发 重定向 缓存
    - access_by_lua access_by_lua_file  准入 权限相关
    - content_by_lua content_by_lua_file 内容生成
    - header_filter_by_lua header_filter_by_lua_file 应答HEADER过滤处理
    - body_filter_by_lua body_filter_by_lua_file 应答BODY过滤处理
    - log_by_lua log_by_lua_file 日志记录


- 获取请求信息
    - ngx.arg.arg_ARGS 取query parameter
    - ngx.var.VARIABLE  nginx变量  由set_by_lua/set定义
    - ngx.header.HEADERS 请求头
    - ngx.req.get_method  请求方法
    - ngx.req.get_uri_args  所有query parameter放进表里面
    - ngx.req.get_post_args  所有表单元素放进表里面
    - ngx.req.get_body 解析HTTP body
    - ngx.req.get_body_file ngx.req.get_body_data 拿到 HTTP body 不解析

- 特别的容器
    - ngx.shared.dict 
    	- 开辟一块内存空间 所有worker共享 
    	- 不能当队列用
    - ngx.ctx 上下文容器 同一个location里面 不同运行阶段可以共享
    
- 内置常量
    - method
    - status
    - log level
    - ngx.null
    
- 单元测试
    - lua-resty-test 可惜几个项目都没有写单元测试
    
---------------------------------------
### 实践环节
- 逻辑简单响应快速 短链接
- 内部跳转外部跳转 推特发送机

### 插图
    
![执行阶段](https://moonbingbing.gitbooks.io/openresty-best-practices/content/ngx_lua/step.png)
