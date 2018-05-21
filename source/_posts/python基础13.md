#Lesson 16
___
##第十六章

###【1】正则表达式

我们在网上扒取html的时候会有很多的标签，那么怎么把一些有规律的标签内容给获取出来了，总不能一个一个的用str.find()来一个一个找吧。

但是正则表达式很难学，但是却非常的有用。

我们想判断手机号合不合法：

```python
def checkPhone(str):
    if len(str) != 11:
        return False
    elif str[0] != "1":
        return False
    elif str[1:3] != "39" and str[1:3] != "31":
        return False

    for i in range(3, 11):
        if str[i] < "0" or str[i] > "9":
            return False
    return True
print('13912341234')
```
这样写是不是太麻烦了。

用正则试一下

```python
import re
def checkPhone2(str):
    #13912345678
    pat = r"^1(([3578]\d)|(47))\d{8}$"
    res = re.match(pat, str)
    return res


print(checkPhone2("14712345678"))
print(checkPhone2("13412345678"))
print(checkPhone2("1391234a678"))
print(checkPhone2("23912345678"))
print(checkPhone2("19012345678"))

#<_sre.SRE_Match object; span=(0, 11), match='14712345678'>
#<_sre.SRE_Match object; span=(0, 11), match='13412345678'>
#None
#None
#None
```
####【1】re模块


不同的语言均有使用正则表达式，但是各不相同。python是通过re模块来实现的

#####re.search()

search(pattern, string, flags=0)

```python
参数：
patter: 匹配的正则表达式
string: 要匹配的字符串
flags:标志位，用于控制正则表达式的匹配方式
功能：扫描整个字符串，并返回第一个成功的匹配
```

我们看例子：

```python
import re

_str = 'I Love ShangHai And BeiJing'

res = re.search(r'ShangHai', _str)
print(res)

#<_sre.SRE_Match object; span=(7, 15), match='ShangHai'>
```
search()方法用于在字符串中搜索正则表达式模式第一次出现的位置，这里找到，匹配的位置是（7，12）。

<font color='red'>注意两点：</font>

```python
（1）第一个参数是正则表达式模式，也就是你要描述的搜索规则，需要使用原始字符串来写，因为这样可以避免很多不必要的麻烦。

（2）找到后返回的范围是以下标0开始的，这跟字符串一样。如果找不到，他就返回None。
```

#####re.match()

match(pattern, string, flags=0)

```python
patter: 匹配的正则表达式
string: 要匹配的字符串
flags:标志位，用于控制正则表达式的匹配方式,值如下
	re.I    忽略大小写
	re.L    做本地户识别
	re.M    多行匹配，影响^和$
	re.S    是.匹配包括换行符在内的所有字符
	re.U    根据Unicode字符集解析字符，影响\w  \W  \b   \B
	re.X    使我们以更灵活的格式理解正则表达式
参数：
功能：尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，返回None
```

看下面的例子：

```python

import re
print(re.match("www", "www.baiwwwdu.com").span())
print(re.match("www", "ww.baidu.com"))
print(re.match("www", "baidu.wwwcom"))
print(re.match("www", "www.baidu.com").group())
print(re.match("www", "wwW.baidu.com", flags=re.I))

```

<font color='red'>注：match和search一旦匹配成功，就是一个match object对象，而match object对象有以下方法：</font>


```python
group() 返回被 RE 匹配的字符串
start() 返回匹配开始的位置
end() 返回匹配结束的位置
span() 返回一个元组包含匹配 (开始,结束) 的位置
group() 返回re整体匹配的字符串，可以一次输入多个组号，对应组号匹配的字符串。
a. group（）返回re整体匹配的字符串，
b. group (n,m) 返回组号为n，m所匹配的字符串，如果组号不存在，则返回indexError异常
c.groups（）,groups() 方法返回一个包含正则表达式中所有小组字符串的元组，从 1 到所含的小组号，通常groups()不需要参数，返回一个元组，元组中的元就是正则表达式中定义的组。 
```
group()例子：

```python

import re
a = "123abc456"
print(re.search("([0-9]*)([a-z]*)([0-9]*)",a).group(0))   #123abc456,返回整体
print(re.search("([0-9]*)([a-z]*)([0-9]*)",a).group(1))   #123
print(re.search("([0-9]*)([a-z]*)([0-9]*)",a).group(2))   #abc
print(re.search("([0-9]*)([a-z]*)([0-9]*)",a).group(3))   #456
```

#####re.findall()

findall(pattern, string, flags=0)

```python

patter: 匹配的正则表达式
string: 要匹配的字符串
flags:标志位，用于控制正则表达式的匹配方式
功能：扫描整个字符串，并返回结果列表
```

例子：

```python
import re
print(re.findall("ShangHai", "Love shanghai!Shanghai", flags=re.I))

#['shanghai', 'Shanghai']
```

#####re.compile()
编译正则表达式模式，返回一个对象的模式。（可以把那些常用的正则表达式编译成正则表达式对象，这样可以提高一点效率。）

re.compile(pattern,flags=0)

```python
pattern: 编译时用的表达式字符串。

flags 编译标志位，用于修改正则表达式的匹配方式，如：是否区分大小写，多行匹配等。常用的
```
结合findall()使用：

```python
import re
tt = "Shanghai ShangHai  shanghai shangHai"
rr = re.compile(r'\w*an\w*')
print(rr,type(rr))
print(rr.findall(tt))   #查找所有包含'oo'的单词

#re.compile('\\w*an\\w*') <class '_sre.SRE_Pattern'>
#['Shanghai', 'ShangHai', 'shanghai', 'shangHai']
```

####【2】通配符

例如:

```python
_str = 'I Love ShangHai And BeiJing'

print(_str.find('ShangHai'))

#7
```，
但是find()也有找不到的，那怎么办？

通配符，可能有些人会熟悉一些，比如我们在linux下面找一个word类型的文件时，我们就find `*.docx`。这里的*就代表所有的意思。

正则表达式也有通配符，就是一个英文点号`.`来表示，它可以匹配除了换行符以外的任何字符。

```python
import re

_str = 'I Love ShangHai And BeiJing'

res = re.search(r'ShangHai', _str)
res1 = re.search(r'(.)', _str)

print(res)
print(res1)

#<_sre.SRE_Match object; span=(7, 15), match='ShangHai'>
#<_sre.SRE_Match object; span=(0, 1), match='I'>
```
一个点只代表一个字符。

####【3】正则表达式中常用的字符含义

#####1、普通字符和10个元字符：

| 元字符  | 用法 | 写法（以abc为例子）| 以abc为例子(可以匹配的类型)|
|    --- | --- |     ---         |        ---              |
|普通字符 |匹配自身|     abc        |            abc         |
|.      |匹配任意除换行符"\n"外的字符(在DOTALL模式中也能匹配换行符|a.c|abc|
|\\|转义字符，使后一个字符改变原来的意思|a\.c;a\\c|a.c;a\c|
|\*|匹配前一个字符0或多次|abc*|abccc|
|+|匹配前一个字符1次或无限次|abc+|abccc|
|?|匹配一个字符0次或1次|abc?|ab;abc|
|^|匹配字符串开头。在多行模式[]中匹配每一行的开头	|^abc|abc|
|\||或。匹配\|左右表达式任意一个，从左到右匹配，如果\|没有包括在()中，则它的范围是整个正则表达式|abc\|def|abc,def|
|{}	|{m}匹配前一个字符m次，{m,n}匹配前一个字符m至n次，若省略n，则匹配m至无限次|ab{1,2}c|abbc|
|[]|字符集。对应的位置可以是字符集中任意字符。字符集中的字符可以逐个列出，也可以给出范围，如[abc]或[a-c]。[^abc]表示取反，即非abc。所有特殊字符在字符集中都失去其原有的特殊含义。用\反斜杠转义恢复特殊字符的特殊含义。|a[bcd]e|abe,ace,ade|
|()|被括起来的表达式将作为分组，从表达式左边开始没遇到一个分组的左括号“（”，编号+1.分组表达式作为一个整体，可以后接数量词。表达式中的、|仅在该组中有效。|(abc){2}，a(123\|456)c，abcabc，a456c|

___
这里需要强调一下反斜杠\的作用：

	1)反斜杠后边跟元字符去除特殊功能；（即将特殊字符转义成普通字符）
	2)反斜杠后边跟普通字符实现特殊功能；（即预定义字符）
	3)引用序号对应的字组所匹配的字符串。

```python
import re
a=re.search(r'(tina)(fei)haha\2','tinafeihahafei tinafeihahatina').group()
print(a)
#tinafeihahafei
#\2代表第二个（）中的‘fei
```

####2、预定义字符集（可以写在字符集[...]中） 

| 预定义字符集  |    用法      | 写法（以abc为例子）| 以abc为例子(可以匹配的类型)|
|    ---      |    ---      |     ---          |          ---           |
|      \d     |  数字:[0-9]	  |  a\dc           |            a1c         |
|      \D     | 非数字:[^\d] |   a\Dc           |           abc          |
|      \s     |匹配任何空白字符:[<空格>\t\r\n\f\v]|   a\sc  |     a c       |
|     \S      |非空白字符:[^\s]	|      a\Sc      |       abc              |
|     \w      |匹配包括下划线在内的任何字字符:[A-Za-z0-9_] |   a\wc   |  abc |
|     \W     |匹配非字母字符，即匹配特殊字符	 |   a\Wc |    a c              |
|     \A     |仅匹配字符串开头,同^	|       \Aabc    |     abc             |
|     \Z     |仅匹配字符串结尾，同`$`	|    abc\Z       |        abc          |
|     \b     |匹配\w和\W之间，即匹配单词边界匹配一个单词边界，也就是指单词和空格间的位置。例如， 'er\b' 可以匹配"never" 中的 'er'，但不能匹配 "verb" 中的 'er'。| \babc,\ba,\b!bc|空格abc空格,a!bc|
|    \B      |   匹配非单词边界	|    a\\Bbc    |     abc   |

|

结合上面的表格看个例子：

匹配单个字符与数字：

```python
import re

print("----------匹配单个字符与数字---------")

'''
[0123456789]     []是字符集合，表示匹配方括号中所包含的任意一个字符
[sunck]          匹配's','u','n','c','k'中任意一个字符
[a-z]            匹配任意小写字母
[A-Z]            匹配任意大写字母
[0-9]            匹配任意数字，类似[0123456789]
[0-9a-zA-Z]      匹配任意的数字和字母
[0-9a-zA-Z_]     匹配任意的数字、字母和下划线
[^ ShangHai]         匹配除了ShangHai这几个字母以外的所有字符，中括号里的^称为脱字符，表示不匹配集合中的字符
[^0-9]           匹配所有的非数字字符
'''

print(re.findall("[ShangHai]", "ShangHai so666 beautiful"))

```


锚字符(边界字符)：

```python

import re
print("--------------锚字符(边界字符)-------------")

'''
^     行首匹配，和在[]里的^不是一个意思
$     行尾匹配

\A    匹配字符串开始，它和^的区别是,\A只匹配整个字符串的开头，即使在re.M模式下也不会匹配它行的行首
\Z    匹配字符串结束，它和$的区别是,\Z只匹配整个字符串的结束，即使在re.M模式下也不会匹配它行的行尾


\b    匹配一个单词的边界，也就是值单词和空格间的位置
      'er\b'可以匹配never,不能匹配nerve
\B    匹配非单词边界

'''

#不区分大小写，搜索以Shanghai开头的
print(re.search("^ShangHai", "shanghai is  good",re.I))
#不区分大小写，搜索Good结尾的
print(re.search("Good$", "ShangHai is  good",re.I))
#多行模式，扫描整个字符串，以shanghai开头，并返回结果列表
print(re.findall("^shanghai", "shanghai is  good\nshanghai so beautiful", re.M))
print(re.findall("\Ashanghai", "shanghai is  good\nshanghai so beautiful", re.M))
	#多行模式，扫描整个字符串，以beautiful结尾，并返回结果列表
print(re.findall("beautiful$", "shanghai is  good\nshanghai so beautiful", re.M))
print(re.findall("beautiful\Z", "shanghai is  good\nshanghai so beautiful", re.M))
	#搜索以er为边界符
print(re.search(r"er\b", "never"))
print(re.search(r"er\b", "nerve"))
	#搜索er为非边界符
print(re.search(r"er\B", "never"))
print(re.search(r"er\B", "nerve"))

```
匹配多个字符

```python
import re
print("-------------------匹配多个字符------------------------")
'''
说明：下方的x、y、z均为假设的普通字符,n、m（非负整数），不是正则表达式的元字符
(xyz)    匹配小括号内的xyz(作为一个整体去匹配)
x?       匹配0个或者1个x
x*       匹配0个或者任意多个x（.* 表示匹配0个或者任意多个字符(换行符除外)）
x+       匹配至少一个x
x{n}     匹配确定的n个x（n是一个非负整数）
x{n,}    匹配至少n个x
x{n,m}   匹配至少n个最多m个x。注意：n <= m
x|y      |表示或，匹配的是x或y
'''
print(re.findall(r"a?", "aaabaa"))#非贪婪匹配(尽可能少的匹配)
print(re.findall(r"a*", "aaabaa"))#贪婪匹配(尽可能多的匹配)
print(re.findall(r"a+", "aaabaaaaaa"))#贪婪匹配(尽可能多的匹配)
print(re.findall(r"a{3}", "aaabaa"))
print(re.findall(r"a{3,}", "aaaaabaaa"))#贪婪匹配(尽可能多的匹配)
print(re.findall(r"a{3,6}", "aaaaaaaabaaa"))
print(re.findall(r"((s|S)hangHai)", "ShangHai--shanghai"))
```

特殊：

```python
import re
#需求，提取shanghai……ok,
str = "ShangHai is good ok!shanghai so beautiful ok"
print(re.findall(r"shanghai.*?ok", str,re.I))



print("---------------特殊-------------------")
'''
*?   +?   x?  最小匹配，通常都是尽可能多的匹配，可以使用这种解决贪婪匹配

(?:x)        类似(xyz),但不表示一个组

'''
#注释：  /*  part1  */  /*   part2  */
s =r'/* part 1 */ code /* part 2 */'
print(re.findall( r'/\*.*\*/', s ))
print(re.findall( r'/\*.*?\*/', s ))
print(re.findall(r'(/.*?/)',s))
print(re.findall(r'(.*)',s))
print(re.findall(r'(.*?)',s))
print(re.findall(r'(?:/\*(.*?)\*/)',s))

```

####【4】加深re模块学习

#####re.split()
通过正则表达式将字符串分离。如果用括号将正则表达式括起来，那么匹配的字符串也会被列入到list中返回。maxsplit是分离的次数，maxsplit=1分离一次，默认为0，不限制次数。

```python

import re
str1 = "ShangHai    is a good place"
print(str1.split(" "))
print(re.split(r" +", str1))

#['ShangHai', '', '', '', 'is', 'a', 'good', 'place']
#['ShangHai', 'is', 'a', 'good', 'place']
```
#####re.finditer()


finditer(pattern, string, flags=0)
参数：

```python
patter: 匹配的正则表达式
string: 要匹配的字符串
flags:标志位，用于控制正则表达式的匹配方式
功能：与findall类似，扫描整个字符串，返回的是一个迭代器
```

```python

import re

str3 = "ShangHai is good ok!shanghai so beautiful ok"
d = re.finditer(r"(shanghai)", str3,re.I)

for i in d:
    print(i.group())


#ShangHai
#shanghai
```

#####sub()\subn()
re.sub(pattern, repl, string, count=0, flags=0)

找到 RE 匹配的所有子串，并将其用一个不同的字符串替换。可选参数 count 是模式匹配後替换的最大次数；count 必须是非负整数。缺省值是 0 表示替换所有的匹配。如果无匹配，字符串将会无改变地返回。


re.subn(pattern, repl, string, count=0, flags=0)

与re.sub方法作用一样，但返回的是包含新字符串和替换执行次数的两元组。

参数：

```python
pattern:  正则表达式(规则)
repl:     指定的用来替换的字符串
string:   目标字符串
count:    最多替换次数
功能：在目标字符串中以正则表达式的规则匹配字符串，再把他们替换成指定的字符串。可以指定替换的次数,如果不指定，替换所有的匹配字符串

区别：前者返回一个被替换的字符串，后者返回一个元组，第一个元素被替换的字符串，第二个元素表示被替换的次数
```

```python
import re

sstr = "shanghai is b b   good place"
# print(re.sub(r"(b)", "a", sstr))
# print(type(re.sub(r"(b)", "a", sstr)))
print(re.subn(r"(b)", "a", sstr))
print(type(re.subn(r"(b)", "a", sstr)))
```

#####?P<name>

?P<name>是段落的表示，那么表示可以自己取个名称。

```python
import re

str6 = "021-56173036"
m = re.match(r"(?P<first>\d{3})-(?P<last>\d{8})", str6)
#使用序号获取对应组的信息，group(0)一直代表的原始字符串
print(m.group())
print(m.group(1))
print(m.group("first"))
print(m.group(2))
print(m.group("last"))
#查看匹配的各组的情况
print(m.groups())
```

###【2】urllib模块

python中的urllib模块中的方法
urllib是基于http的高层库，它有以下三个主要功能：

（1）request处理客户端的请求

（2）response处理服务端的响应

（3）parse会解析url

下面讨论的是request

urllib.request模块定义了一些打开URLs（一般是HTTP协议）复杂操作像是basic 和摘要模式认证，重定向，cookies等的方法和类。这个模块式模拟文件模块实现的，将本地的文件路径改为远程的url。因此函数返回的是类文件对象（file-like object）

urllib.request.urlopen(url, data=None, [timeout, ]*, cafile=None, capath=None, cadefault=False, context=None)

url可以是一个字符串形式或者Request对象

如果data参数有值就是用post方式响应否则默认为GET 方式

urllib.request 模块使用HTTP/1.1 的无连接的状态协议

urllib.request 模块使用HTTP/1.1 的无连接的状态协议

urlopen()函数返回类文件对象，提供以下内建方法：

-      read() , readline() ,readlines() , fileno() , close() ：这些方法的使用方式与文件对象完全一样

-      info()：返回一个httplib.HTTPMessage对象，表示远程服务器返回的头信息

-      getcode()：返回Http状态码。（详情参考https://tools.ietf.org/html/rfc7231#section-6）
