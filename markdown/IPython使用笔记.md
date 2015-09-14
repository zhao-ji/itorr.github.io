Date: 2015-3-12 16:30
Title: IPython 使用笔记
Category: Python
Summary: Ipython 文档大致理解和一些使用体验

====================================

#### 主要功能

- IPython 结合了shell的方便特性和输入输出的历史记录机制
- 进入标准python帮助系统，help()进入，quit退出
- 魔法命令: %magic 可查看魔法子系统
- 系统命令别名: %alias 查看
- 对象帮助: 
    - ?word or word? 对象信息
    - ??word or word?? 对象详细信息
    - %pdoc object 显示对象doc-string
- 自动补全： TAB 或者 Ctrl+p/Ctrl+n 或者 Ctrl+r 或者 %hist
- 跨会话永久命令历史
- 工作记录保存和恢复
- module deep-reload
- 彩色输出
- 获得输入历史 _i _ii _iii
- 获得输出历史 _ __ ___
- 括号引号自动补全

## Tips
