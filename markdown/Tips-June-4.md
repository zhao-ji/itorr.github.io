## Vim Tips

- Vim 中空格代替 制表符配置
    1. set expandtab # replace the tab with space
    2. set tabstop=4 # 4 space
    3. set shiftwigth=4 # auto shift width 4 space
 
- 交换当前行和下一行： ddp

- i internal a outer : cis cip cas cap

- 保存sudo权限的文件 :w !sudo tee %

- Tab页切换 gt

- 刷新页面使 syntax 生效 :e

## Linux Tips

- locate updatedb

- find ~ -type f -name "*.pyc" -size -1M -delete

- cat -Ans file 显示行号、空行压缩、不可打印字符

- sort -k 2.3brn,2 -t ';'

- cut -f 2,3 -c 4,5

- paste file1 file2

- 去掉系统错误提示 /etc/default/apport 设为0

- command line 里用一个横线的option 方便书写, scripts 里面用两个横线的option 易于维护

- cut 残废在对多空格分隔符的处理上，用 tr -s " " | cut -d " " -f 4 代替

- dot = soruce, chmod 755

- 用户script存放在 ~/bin/ 下，脚本自制脚本放入/usr/local/bin和/usr/local/sbin下

- sh 不支持 delare, bash 支持

- bash 引用执行结果  $(ls)

- bash 引用计算结果  $((4+5))

- bash 字符串长度 ${#aaaaa}

- bash 拼接执行结果  aaaa${b}cccc

- bash 进制转换 $((16#fffff))

- bash 上条命令执行状态码 $?


## Git Tips

- 撤销修改 git checkout -- somefile.txt

- 撤销add git reset HEAD somefile.py

- 撤销commit git commit -m 'add: hey' | git add somefile.py | git commit --amend 

- 查看config git config --list

- 设置默认编辑器  git config --global core.editor vim

> 为什么要写好的 commit log? 为了自己review方便 为了后人维护方便 方便写文档
> 注意点： fix/add/change issue/feature号开头，放上issue链接
> 开头综述干了什么，隔空行后放上链接
> 接下来分条讲清楚为什么要做改动、是什么问题让自己不得不改动代码，自己是怎么解决这个问题的，问题解决后会不会有副作用、会不会留下什么坑


## algorithm

- 正则执行原理

- LRU cache 设计注意点
