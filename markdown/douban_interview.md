Date: 2015-4-5 09:17
Title: 豆瓣面试经过
Category: Tips
Summary: the interview in douban

====================================

### 面试前
在 v2ex 上看到豆瓣 ruby@douban.com 发招聘帖，然后发了份邮件。当天下午六点就收到 HR 电话，约了四月一号下午两点半面试。跟单位领导请假，不准，四月一号必须来公司完成任务。第二天真的没有能去面试。后来约四月二号下午面试， 结果四月二号去顺义，还是没有面成，真是太惭愧了。给 ruby@douban.com 发了份邮件表到了一下歉意。四月三号没去上班，上午抱着试试看的心态给 HR 打了个电话，可以下午面试。

- 面试两点开始
- 大概六点多结束
- 笔试，三个部门领导面试，HR面试

### 笔试
一个小时的答题时间，六道题

- 登录流程，表单项有用户名、密码、验证码。在提交后浏览器和服务器发生了什么。发送请求-处理-响应请求 的过程是怎样的
- Python 语言的特点是什么，相应的代价是什么
- 豆瓣用户uid从100000开始，前十亿用户中，可以被6、9整除的uid之和是多少
- 求一个自然数的最大质数
- 英文句子的单词反转，冠词+名词不反转，冠词+冠词反转

1. 流程
    - 浏览器将表单字段打包成HTTP报文----通过socket连接发给豆瓣服务器----豆瓣负载均衡服务器转发给Python后端
    - 解出body中三个字段----校验验证码----如果正确----校验用户名密码----如果正确----获取用户信息----如果存在用户----打包成HTTP报文
    - 发送报文----浏览器拿到报文----浏览器渲染CSS、HTML标签、执行js
    
2. 两个特点：缩进、包丰富  没有代价
3. code:

    #!/usr/bin/env python
    # utf8
    
    is_aliquot = lambda num: num % 6 == 0 or num %9 == 0
    get_total = lambda num_list: sum(filter(is_aliquot, num_list))
    
    if __name__ == "__main__":
        num_list = xrange(100000, 10 ** 9)
        print get_total(num_list)
        
4. code:

    #!/usr/bin/env python
    # utf8
    
    get_remainder = lambda prime, num=num: num % prime
    get_next_prime = lambda prime_list, num: prime_list if sum(map(get_remainder, prime_list)) else prime_list.append(num)
    get_prime_list = lambda num: reduce(get_next_prime, xrange(2, num), [])
    
    def get_biggest_prime(num):
        prime_list = get_prime_list(num)
        if not prime_list:
            return num
        for prime in prime_list[::-1]:
            if not get_remainder(prime, num):
                return prime
                
    if __name__ == "__main__":
        print get_biggest_prime(44444)
        
5. code:

    #!/usr/bin/env python
    # utf8
    
    ARTICLE_LIST = ['the', 'an', 'a']
    
    def correct_article(word_list):
        for index, word in enumerate(word_list[:-1]):
            if word in ARTICLE_LIST and word_list[index + 1] not in ARTICLE_LIST:
                word_list[index], word_list[index + 1] = word_list[index + 1], word_list[index]
                
    if __name__ == "__main__":
        string = "hello, welcome to the new world, a an"
        word_list = string.split(" ").reverse()
        print " ".join(correct_article(word_list))
        
### 豆瓣豆列负责人面试
因为中性笔出水不畅，所以用中号签字笔答题，乱，所以后来面试官都没有认真的看我的作答。

- context manager 异常机制
- 豆瓣使用的python框架是风车，database使用mysql
- try...except...else...finally except中return仍然会走finally
- 有人说python慢怎么会回复
- 类的复杂继承 __mor__

### 豆瓣广告和客服负责人面试

- 这块原有职工已经走的差不多了
- 单例模式 大资源如何不重复加载
- websocket 原理
- 自己平时做过的小项目
- WSGI　协议，自己写WEB服务器的难点在哪

### 豆瓣广告负责人面试

- 兴趣，豆瓣ID为什么会取“杨金丽”这个名字
- 薪资
- 如果来豆瓣，会先做面向豆瓣广告投放者的事情，然后再做广告投放
- 还面试了哪几家公司，知乎，如果两家选选哪一家，这个要看具体工作

### 豆瓣HR面试

- 平时的兴趣爱好
- 住在哪，方不方便来上班
- 现在公司情况，为什么考虑离职
