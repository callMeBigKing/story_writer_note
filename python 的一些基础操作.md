---
title: python 的一些基础操作
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---


###　三元运算
一般的是
![enter description here][1]
如result=5>3?1:0
而python是
![enter description here][2]
如
flag=1 if 5>3 else 0

### 
defaultdict
``` python
from collections import defaultdict
senDict = defaultdict()
    for s in senList:
        senDict[s.split(' ')[0]] = s.split(' ')[1]
```


  [1]: ./images/1498291211731.jpg
  [2]: ./images/1498291256533.jpg