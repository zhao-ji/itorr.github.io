Date: 2014-8-10 20:30
Title: 正则表达式
Category: Re
Summary: a summary of Regular Expression

================

#正则表达式

##元字符

- *()*  *[]*  *{}*     捕获器 选择器  次数
- *\** *+* *?*  零和任意多次  一次和任意多次  零次和一次
- *^* *$* 匹配开始 匹配结束
- *\\* 转义
- *|* 或
- *.* 匹配任意字符  非换行符

##匹配案例

###类型
- *\\d* 匹配数字 
- *\\D* 匹配非数字
- *\\s* 匹配空白字符
- *\\S* 匹配非空白字符
- *\\w* 匹配字母和数字
- *\\W* 匹配非字母和数字

###次数
- *{0,}* *
- *{1,}* +
- *{0,1}* ?

###消歧义
- raw \\不用转义

##Python Re 模块用法
- Re 方法： search  match findall finditer
- RegexObject 方法 ： group start end span
- compile 选项 ： 
> - DOTALL S .代表一切字符 包括换行符
> - IGNORECASE I 忽略大小写、
> - LOCALE L 本地化字符设置
> - MULTILINE M 多行匹配 改变^$的行为
> - VERBOSE V 分行写RE语句  并可以添加注释

 


