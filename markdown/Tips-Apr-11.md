## Shell Tips

#### 安装新字体

- 将字体文件夹拷贝到 /usr/share/fonts 目录下
- 更改权限　644
- 进入字体文件夹
- command:
    sudo mkfontscale
    sudo mkfontdir
    sudo fc-cache -fv
    
#### 无密码登录VPS前的密钥传递
- ssh-copy-id -p 80 username@host

#### shell 去空行
- cat hello | tr -s '\n'

#### shell 去重
- uniq

#### shell 排序
- sort

#### zip文件解压乱码
- unzip -O GBK xxxx.zip

## Python Tips

#### 自然数生成器

    class Num:
        '''output the nature number'''
        num = 0
        
        def gen(self):
            while True:
                yield self.num
                self.num += 1
                
#### yield

- only yield: frozen the status
- yield someone: frozen the status and return the someone
- somebody = yield: frozen the status and send the somebody to function
- somebody = yield someone: frozen the status and send the somebody to the generator and return someone and 

#### 用字典实现switch功能 (router)

## Vim Tips

#### 读取内容到正在编辑的文件中
- :r hey.txt
- :r !ls

#### 执行shell命令
- Ctrl+z 回到命令行 fg 回到Vim
- :shell 回到命令行 exit 回到Vim

#### rot13 加密混淆当前文本
- :'<,'> !rot13
