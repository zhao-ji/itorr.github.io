Title: 一月点滴收集
Category: Tips
Date: 2015-1-13 16:30
Summary: Tips in Jan

=======================

## Python Tips

#### Python 暴力字典生成（brute 算法）

> 可重复全排列

        def brute(choices, length):
            return (
                ''.join(candidate) for candidate in
                chain.from_iterable(
                    product(
                        choices,
                        repeat = i,
                    ) for i in range(1, length + 1),
                )
            )

<br>

#### isinstance 用法

> isinstance(...)
>    isinstance(object, class-or-type-or-tuple) -> bool
>   
>    Return whether an object is an instance of a class or of a subclass thereof.
>    With a type as second argument, return whether that is the objects type.
>    The form using a tuple, isinstance(x, (A, B, ...)), is a shortcut for
>    isinstance(x, A) or isinstance(x, B) or ... (etc.).
>
>> In [9]: isinstance("hello", str)
>> Out[9]: True
>
>
>> In [10]: isinstance(1, (str, int))
>> Out[10]: True
>
>> In [4]: class A:
>>    ...:     pass
>>    ...: 
>> In [5]: a = A()
>> In [6]: isinstance(a, A)
>> Out[6]: True

**isinstance 的第二个参数可以是 类型、类、包含类型或类的元祖。**

<br>

#### How to flatten arbitrarily nested lists in Python?

        nested_list = [1, 2, [3, 4, [5],['hi']], [6, [[[7, 'hello']]]]]
        
        def flatten(nested):
        	for item in nested:
            	if isinstance(item, list) or isinstance(item, tuple):
                	for element in flatten(item):
                    	yield element
                else:
                	yield item
                    
        print list(flatten(nested_list))
        
        > [1, 2, 3, 4, 5, 'hi', 6, 7, 'hello']

<br>

#### map 传参数可以设置默认参数，和使用*方法

> In [1]: sum_5 = lambda x, y=5: x+y
> 
> In [2]: sum_5(4)
> Out[2]: 9
> 
> In [3]: sum_5(4, 3)
> Out[3]: 7

> In [6]: sum_new = lambda *args: sum(args)
> 
> In [7]: sum_new(1,2,3,4)
> Out[7]: 10


<br>

#### bisect 模块二分查找，作用对象：字符串、列表

> In [1]: from bisect import bisect, insort
> 
> In [2]: a = [1,2,3,4,5,7,8,9]
> 
> In [3]: insort(a, 6)
> 
> In [4]: a
> Out[4]: [1, 2, 3, 4, 5, 6, 7, 8, 9]
> 
> In [5]: bisect(a, 6)
> Out[5]: 6

<br>

#### unidecode 将汉字转为拼音

> In [8]: from unidecode import unidecode
> 
> In [9]: unidecode(u'你好')
> Out[9]: 'Ni Hao '

<br>

#### iter(func(), value) : make the iterator of func() until func()==value

<br>

#### 条件判断

> In [1]: a = 3
> 
> In [2]: if 1< a< 4:
>    ...:     print 4
>    ...:     
>         4
> 
> In [3]: if not (1 < a < 4):
>    ...:     print 4
>    ...:     
> 
> In [4]: if not 4<a<5:
>    ...:     print 4
>    ...:     
>         4

<br>
<br>

## VIM Tips

<br>

#### 以普通用户身份打开的文件需要以sudo身份保存
> :w !sudo tee %

<br>

#### 插入模式 自动补全
> CTRL + N

<br>

#### 打开文件自动回到上次编辑位置
> au BufReadPost * if line("'\"") > 0|if line("'\"") <= line("$")|exe("norm '\"")|else|exe "norm $"|endif|endif

<br>

#### 代码折叠
> V模式选择文本，可以使用%快速匹配括号, zf 折叠
> zo 打开折叠
> zc 关闭折叠

<br>

### HML 分别将光标移至屏幕最上、正中、最下

<br>

### IrA 列选择后分别在前面、当下、后面修改或添加

<br>

### 将光标所在行移至屏幕正中: z.

<br>

### 编辑远程文件
> vim scp://root@baidu.com:12345//etc/nginx/nginx.conf

<br>

### 书签使用
#### 命令模式
> marks 显示所有书签
>
> marks a 显示A书签的详细信息

#### 普通模式
> ma 在当前位置设置A书签, 大写字母为全局书签，小写字母为局部书签
>
> `a 回到A书签所在行所在列
>
> 'a 回到A书签所在行
>
> `. 回到上次编辑位置所在行所在列
>
> '. 回到上次编辑位置所在行

<br>
<br>

## Shell Tips

#### 查看当前目录文件夹大小
>    du -h --max-depth=1 ./

<br>

#### 修改系统默认编辑器
>    sudo update-alternatives --config editor

<br>

#### redis 开启远端访问
> remove the "bind 127.0.0.1" 
> set password after "requirepass" 
> in redis.conf 

<br>

#### mongo 修改字段名
> db.collection.update({}, {$rename: {old_name: new_name}})

<br>

#### unalias 删除alias后的命令， 'ls' 和 \ls 能强制调用原始ls命令

<br>

#### 禁用ubuntu内部错误报告

> sudo service apport stop
>
> vim /etc/default/apport enabled=0

<br>

#### 设置服务器不回应PING

> echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all
>
> 回应则设为0

#### 用户管理

> useradd -d /home/nightwish -g root nightwish
> 添加用户 nightwish, home目录为 /home/nightwish 用户组为 root

> userdel -r nigthwish 
> 连同HOME目录一同删除

> usermod -g hello nightwish
> 修改用户

<br>
<br>

## 前端 Tips

<br>

#### 移动端设置 viewport 使网页自适应

> <code><meta name="viewport" content="width=device-width, initial-scale=1" /><code>
> [网页自适应--软一峰](http://www.ruanyifeng.com/blog/2012/05/responsive_web_design.html)
