##OpenResty：一种后端新玩法

----------------------------
###特点

- 在NginX中嵌入Lua 适合逻辑简单但性能要求高的应用
- 取代复杂晦涩的nginx配置语法 用简单明了的Lua来管理请求跳转
- 经过淘宝、CloudFlare的大规模生产实践 相对成熟 国内360和去哪儿也在用
- Lua过程式语言 没有面向对象

- 模块都是特殊打造的 但是相对缺乏
- NginX错误日志无法定制
- 调试困难 处理流程啰嗦

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
    - 没有mail
    - 新出socket模块，正式版出来后可以把shadowsocks迁移到NginX上面来
- Lua 基本语法
    - 《Programming In Lua》
    - 不用了解太多，语法相当简单
    - OpenResty 里面用到的更是少得可怜
    
-----------------------------------
### OpenResty需要了解的几个部分
- 执行阶段
    - init_by_lua init_by_lua_file 
    - init_worker_by_lua init_by_lua_file
    - set_by_lua set_by_lua_file
    - content_by_lua content_by_lua_file
    - rewrite_by_lua rewrite_by_lua_file
    - access_by_lua access_by_lua_file
    - header_filter_by_lua header_filter_by_lua_file
    - body_filter_by_lua body_filter_by_lua_file
    - log_by_lua log_by_lua_file
- 获取请求信息
    - ngx.arg.arg_ARGS
    - ngx.var.VARIABLE
    - ngx.header.HEADERS
    - ngx.req.get_method
    - ngx.req.get_uri_args
    - ngx.req.get_post_args
    - ngx.req.get_body ngx.req.get_body_file ngx.req.get_body_data
- 特别的数据结构
    - ngx.shared.dict
    - ngx.ctx
- 内置常量
    - method
    - status
    - log level
    - ngx.null
    
---------------------------------------
### 实践环节
- 逻辑简单响应快速 短链接
- 内部跳转外部跳转 推特发送机
