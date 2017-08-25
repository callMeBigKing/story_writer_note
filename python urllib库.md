---
title: python urllib库
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---

### 从http协议开始思考
浏览器发送一个简单的request请求
request的消息结构如下图
![enter description here][1]

第一行中的Method表示请求方法,比如"POST","GET",  Path-to-resoure表示请求的资源， Http/version-number 表示HTTP协议的版本号

当使用的是"GET" 方法的时候， body是为空的

比如我们打开博客园首页的request 如下
![enter description here][2]

那么urllib打开一个网页需要确定几个关键的地方

 1. 连接类型是get还是post
 2. 地址
 3. header header中包括cookie
 4. body中内容，仅仅针对post方法
 
 正对上面的四个点，来展开urllib中的一些方法和对象
 
 

``` python
#encoding:UTF-8
import urllib
 
url = "http://www.baidu.com"
data = urllib.request.urlopen(url)  # return <class 'http.client.HTTPResponse'>
data=data.open()
data = data.decode('UTF-8')
print(data)
```
**urllib.request.urlopen(url, data=None, [timeout, ]*, cafile=None, capath=None, cadefault=False, context=None)**

 - url:  需要打开的网址
 - data：Post提交的数据
 - timeout：设置网站的访问超时时间

==urllib.request.urlopen()== 返回一个 ==http.client.HTTPResponse==
**对象主要提供方法和属性**

 - read(),readline() ,readlines() , fileno() , close() ：对HTTPResponse类型数据进行操作
 - info()：返回HTTPMessage对象，表示远程服务器返回的头信息
 - getcode()：返回Http状态码。如果是http请求，200请求成功完成;404网址未找到
 - geturl()：返回请求的url
 ## 使用request
 **urllib.request.Request(url, data=None, headers={}, method=None)**
 使用request（）来包装请求，再通过urlopen（）获取页面。
 

``` stylus
url = r'http://www.lagou.com/zhaopin/Python/?labelWords=label'
headers = {
    'User-Agent': r'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) '
                  r'Chrome/45.0.2454.85 Safari/537.36 115Browser/6.0.3',
    'Referer': r'http://www.lagou.com/zhaopin/Python/?labelWords=label',
    'Connection': 'keep-alive'
}
req = request.Request(url, headers=headers)
page = request.urlopen(req).read()
page = page.decode('utf-8')
```

## Post数据
**urllib.request.urlopen(url, data=None, [timeout, ]*, cafile=None, capath=None, cadefault=False, context=None)**

urlopen（）的data参数默认为None，当data参数不为空的时候，urlopen（）提交方式为Post。

``` stylus
from urllib import request, parse
url = r'http://www.lagou.com/jobs/positionAjax.json?'
headers = {
    'User-Agent': r'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) '
                  r'Chrome/45.0.2454.85 Safari/537.36 115Browser/6.0.3',
    'Referer': r'http://www.lagou.com/zhaopin/Python/?labelWords=label',
    'Connection': 'keep-alive'
}
data = {
    'first': 'true',
    'pn': 1,
    'kd': 'Python'
}
data = parse.urlencode(data).encode('utf-8')
req = request.Request(url, headers=headers, data=data)
page = request.urlopen(req).read()
page = page.decode('utf-8')
```

**urllib.parse.urlencode(query, doseq=False, safe='', encoding=None, errors=None)**
## 添加header的两种方法
第一种就和上面添加header一样简单的写成dict就可以了
**第二种**使用build_opener 这个方法, 用来自定义 opener, 这种方法的好处是可以方便的拓展功能, 例如下面的代码就拓展了自动处理 Cookies 的功能.

``` stylus
import urllib.request
import http.cookiejar
 
# head: dict of header
def makeMyOpener(head = {
    'Connection': 'Keep-Alive',
    'Accept': 'text/html, application/xhtml+xml, */*',
    'Accept-Language': 'en-US,en;q=0.8,zh-Hans-CN;q=0.5,zh-Hans;q=0.3',
    'User-Agent': 'Mozilla/5.0 (Windows NT 6.3; WOW64; Trident/7.0; rv:11.0) like Gecko'
}):
    cj = http.cookiejar.CookieJar()
    pro = urllib.request.HTTPCookieProcessor(cj)
    opener = urllib.request.build_opener(pro)
    header = []
    for key, value in head.items():
        elem = (key, value)
        header.append(elem)
    opener.addheaders = header
    return opener
 
oper = makeMyOpener()
uop = oper.open('http://www.baidu.com/', timeout = 1000)
data = uop.read()
print(data.decode())
```




  [1]: ./images/1501504683052.jpg
  [2]: ./images/1501504760821.jpg