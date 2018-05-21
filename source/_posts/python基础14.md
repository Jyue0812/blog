#Lesson 17
___
##第十六章
###网络爬虫

网络爬虫（又被称为网页蜘蛛，网络机器人，在FOAF社区中间，更经常的称为网页追逐者），是一种按照一定的规则，自动地抓取万维网信息的程序或者脚本。另外一些不常使用的名字还有蚂蚁、自动索引、模拟程序或者蠕虫。

####【1】urllib爬取网页

```python
import urllib.request

# 向指定的url地址发起请求，并返回服务器响应的数据(文件的对象)
response = urllib.request.urlopen("http://www.baidu.com")

#返回状态码

if response.getcode() == 200 or response.getcode() == 304:
    pass
else:
    print(response.getcode())
    exit()


#print(response)
# 读取问文件的全部内容，会把读取到的数据赋值给一个字符串变量
data = response.read()
# 读取一行
# data = response.readline()

#读取文件的全部内容，会把读取到的数据赋值给一个列表变量
# data = response.readlines()
#
# print(data)
# print(type(data))
# print(len(data))
# print(type(data[100].decode("utf-8")))




#将爬取到的网页写入文件
with open(r"file1.html", "wb") as f:
    f.write(data)


#response 属性
#返回当前环境的有关信息
# print(response.info())



#返回当前正在爬取的URL地址
# print(response.geturl())


#

# url = r"https://www.baidu.com/s?ie=utf-8&f=3&rsv_bp=0&rsv_idx=1&tn=baidu&wd=%E5%87%AF%E5%93%A5%E5%AD%A6%E5%A0%82&rsv_pq=96b2af980000cb00&rsv_t=ed0aZ%2FMEmvroTfrwq5E%2FJFwohlrfGzQfpCwXWirqpFgzTvJwE9WdPgDp4Jk&rqlang=cn&rsv_enter=1&rsv_sug3=3&rsv_sug1=2&rsv_sug7=100&rsv_sug2=1&prefixsug=%25E5%2587%25AF%25E5%2593%25A5&rsp=0&inputT=4668&rsv_sug4=5958"
# print(url)
# #解码
# newUrl = urllib.request.unquote(url)
# print(newUrl)
# #编码
# newUrl2 = urllib.request.quote(newUrl)
# print(newUrl2)

```

####【2】直接写入文件

```python
import urllib.request

#retrieve是检索的意思，它的作用是把它直接写到指定的文件中
urllib.request.urlretrieve("http://www.baidu.com", "file2.html")

#urlretrieve在执行的过程当中，会生成一些缓存
#清除缓存
urllib.request.urlcleanup()
```
####【3】模仿浏览器

```python
import urllib.request,gzip
import random
import chardet


url = "http://www.baidu.com"


#模拟请求头
headers = {
    "Accept" : "application/json, text/javascript, */*; q=0.01",
    "X-Requested-With" : "XMLHttpRequest",
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36",
    "Content-Type" : "application/x-www-form-urlencoded; charset=UTF-8"
}
#设置一个请求体
req = urllib.request.Request(url,headers=headers)
#发起请求
response = urllib.request.urlopen(req)
#chardet.detect检查爬取下来的字符集编码，如果encoding是none的话那么他就是一个gzip压缩格式，那么我们需要解压
#print(chardet.detect(response.read()))
#我们要先解压然后才能获取
gziper = gzip.GzipFile(fileobj=response)
data = gziper.read()


print(data)


# agentsList = [
#     "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Maxthon/4.4.3.4000 Chrome/30.0.1599.101 Safari/537.36",
#     "Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36",
#     "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.84 Safari/535.11 SE 2.X MetaSr 1.0"
# ]
# agentStr = random.choice(agentsList)
# req = urllib.request.Request(url)
#向请求体里添加了User-Agent
# req.add_header("User-Agent", agentStr)
# response = urllib.request.urlopen(req)
# print(response.read().decode("utf-8"))

```
####【4】设置超时

```python

import urllib.request


#如果网页长时间未响应，系统判断超时，无法爬取
for i in range(1, 100):
    try:
    #0.5秒后请求超时，开始下一个
        response = urllib.request.urlopen("http://www.baidu.com", timeout=0.5)
        print(len(response.read()))
    except:
        print("请求超时，继续下一个爬取")
        
```

####【5】http协议

超文本传输协议（HTTP，HyperText Transfer Protocol)是互联网上应用最为广泛的一种网络协议。所有的WWW文件都必须遵守这个标准。设计HTTP最初的目的是为了提供一种发布和接收HTML页面的方法。1960年美国人Ted Nelson构思了一种通过计算机处理文本信息的方法，并称之为超文本（hypertext）,这成为了HTTP超文本传输协议标准架构的发展根基。Ted Nelson组织协调万维网协会（World Wide Web Consortium）和互联网工程工作小组（Internet Engineering Task Force ）共同合作研究，最终发布了一系列的RFC，其中著名的RFC 2616定义了HTTP 1.1。

```python

使用场景：进行客户端与服务端之间的消息传递时使用

GET: 通过URL网址传递信息，可以直接在URL网址上添加要传递的信息
POST: 可以向服务器提交数据，是一种比较流行的比较安全的数据传递方式
PUT: 请求服务器存储一个资源，通常要指定存储的位置
DELETE: 请求服务器删除一个资源
HEAD: 请求获取对应的HTTP报头信息
OPTIONS:可以获取当前UTL所支持的请求类型

```
```python
1xx：指示信息--表示请求已接收，继续处理
2xx：成功--表示请求已被成功接收、理解、接受
200 表示成功了
3xx：重定向--要完成请求必须进行更进一步的操作
304 表示已经缓存了过
4xx：客户端错误--请求有语法错误或请求无法实现
403 服务器收到请求，但是拒绝提供服务
404 没有这个地址
5xx：服务器端错误--服务器未能实现合法的请求
500 服务器内部发生不可预期的错误
503 服务器当前不能处理客户端的请求，一段时间后可能恢复正常

```
<image src='images/http响应状态V1.png'/>
<image src='images/http响应状态V2.png'/>
<image src='images/http响应状态V3.png'/>

####【6】get请求

主要是用来获取数据而使用的协议，但是它有长度限制，理论上是2048个字节，但是实际上不止（不同的浏览器不一样）。get请求是通过url传递值得。
get得到的数据会被浏览器缓存下来。

```python

'''
特点：把数据拼接到请求路径的后面传递给服务器

有点：速度快

缺点：承载的数据量小，不安全
'''

import urllib.request
url = "http://www.baidu.com?name=tom&age=18"
response = urllib.request.urlopen(url)
data = response.read().decode("utf-8")
print(data)
print(type(data))

```

####【7】json数据解析

json是一种轻量的网络传输格式，相对于xml它比较的简洁，但是xml可以有字段约束，可读性更加高。

首先我们要引用json库，

它和pickle非常的相像，pickle.load(),pickle.dump()

```python
'''
概念：一种保存数据的格式
作用：可以保存本地的json文件，页可以将json串进行传输，通常将json称为轻量级的传输方式

json文件组成
{}     代表对象(字典)
[]     代表列表
:      代表键值对
,     分隔两个部分
'''
import json

jsonStr = '{"name":"tom", "age":18, "hobby":["money","power","english"], "parames":{"a":1,"b":2}}'
#将json格式的字符串转为python数据类型的对象
jsonData = json.loads(jsonStr,encoding='utf-8')
print(jsonData)
print(type(jsonData))
print(jsonData["hobby"])

#将python数据类型的对象转为json格式的字符串
jsonData2 = {"name":"tom", "age":18, "hobby":["money","power","english"], "parames":{"a":1,"b":2}}
jsonStr2 = json.dumps(jsonData2)
print(jsonStr2)
print(type(jsonStr2))


#读取本地的json文件
path1 = r"caidanJson.json"
with open(path1, "rb") as f:
    data = json.load(f)
    print(data)
    #字典类型
    print(type(data))

#写本地json
path2 = r"test.json"
jsonData3 = {"name":"tom", "age":18, "hobby":["money","power","english"], "parames":{"a":1,"b":2}}
with open(path2, "w") as f:
    json.dump(jsonData3, f)

```
####【8】post请求

post请求是以包的形式提交过去的，相对get请求来说要安全一些，而且可以提交海量数据，它在提交的时候是将数据保存在request body中的。但是它不能被浏览器缓存。

```python
'''
特点：把参数进行打包，单独传输

优点：数量大，安全(当对服务器数据进行修改时建议使用post)

缺点：速度慢
'''
import urllib.request
import urllib.parse

url = "http://www.baidu.com"
#将要发送的数据合成一个字典
#字典的键取网址里找，一般为input标签的name属性的值
data = {
    "name":"tomr",
    "age":18
}
#对要发送的数据进行打包,记住编码
postData = urllib.parse.urlencode(data).encode("utf-8")
#请求体
req = urllib.request.Request(url, postData)
#请求
req.add_header("User-Agent", "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Maxthon/4.4.3.4000 Chrome/30.0.1599.101 Safari/537.36")
response = urllib.request.urlopen(req)
print(response.read().decode("utf-8"))

```

####【9】ajax请求

ajax是js里面最常用的一种异步请求方法。

```python

import urllib.request
import ssl
import json

def ajaxCrawler(url):
    headers = {
        "User-Agent":"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Maxthon/4.4.3.4000 Chrome/30.0.1599.101 Safari/537.36"
    }
    req = urllib.request.Request(url, headers=headers)

    #使用ssl创建未验证的上下文
    context = ssl._create_unverified_context()
    response = urllib.request.urlopen(req,context=context)

    jsonStr = response.read().decode("utf-8")
    jsonData = json.loads(jsonStr)

    return jsonData

url = "https://movie.douban.com/j/chart/top_list?type=11&interval_id=100%3A90&action=&start=20&limit=20"
info = ajaxCrawler(url)
print(info)

# for i in (1,3):
#     url = "https://movie.douban.com/j/chart/top_list?type=11&interval_id=100%3A90&action=&start="+ str(i * 20)+"&limit=20"
#     info = ajaxCrawler(url)
#     print(info)
```

####【10】抓取糗事百科

```python
import urllib.request
import re,ssl

def jokeCrawler(url):
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Maxthon/4.4.3.4000 Chrome/30.0.1599.101 Safari/537.36"
    }
    req = urllib.request.Request(url,headers=headers)
    context = ssl._create_unverified_context()
    response = urllib.request.urlopen(req,timeout=10,context=context)
    HTMl = response.read().decode("utf-8")

    regularStr = r'<div class="author clearfix">(.*?)<span class="stats-vote"><i class="number">'
    re_joke = re.compile(regularStr, re.S)
    divsList = re_joke.findall(HTMl)
    # print(divsList)
    dic = {}
    for div in divsList:
        # 用户名
        re_u = re.compile(r"<h2>(.*?)</h2>", re.S)
        username = re_u.findall(div)
        username = username[0]
        # 段子
        re_d = re.compile(r'<div class="content">\n<span>(.*?)</span>', re.S)
        duanzi = re_d.findall(div)
        duanzi = duanzi[0]

        dic[username] = duanzi

    return dic

url = 'https://www.qiushibaike.com/text/page/1/'
info = jokeCrawler(url)
for k, v in info.items():
    print(k + "的段子：\n" + v)
```