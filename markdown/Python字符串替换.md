## 字符串替换

    def replace_words(text, word_dic): 
        yo = re.compile('|'.join(map(re.escape, word_dic))) 
        def translate(mat): 
            return word_dic[mat.group(0)] 
        return yo.sub(translate, text) 

链接： [请教：Python字符串替换的一个问题](http://segmentfault.com/q/1010000002474308)
