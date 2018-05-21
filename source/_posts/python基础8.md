#第十二章
___
##【8】对序列的文件操作:泡菜（pickle）

文件的写入只能写入普通的字符，对于list、tuple、dict、set这些类型无法写入，所以只能使用二进制写入，但是‘wb’使用了以后一直在报错`TypeError: write() argument must be str, not tuple`

那怎么办：

python给我们提供了pickle模块,它几乎可以把所有python的对象转化为二进制的形式存放，这个过程称为picking，那么二进制转换为对象就是unpicking.

python的pickle模块实现了基本的数据序列和反序列化。通过pickle模块的序列化操作我们能够将程序中运行的对象信息保存到文件中去，永久存储；通过pickle模块的反序列化操作，我们能够从文件中创建上一次程序保存的对象。

基本接口：

pickle.dump(obj, file, [,protocol])

注解：将对象obj保存到文件file中去。　　　　　

protocol为序列化使用的协议版本，0：ASCII协议，所序列化的对象使用可打印的ASCII码表示；1：老式的二进制协议；2：2.3版本引入的新二进制协议，较以前的更高效。其中协议0和1兼容老版本的python。protocol默认值为0。

file：对象保存到的类文件对象。file必须有write()接口， file可以是一个以'w'方式打开的文件或者一个StringIO对象或者其他任何实现write()接口的对象。如果protocol>=1，文件对象需要是二进制模式打开的。

pickle.load(file)

注解：从file中读取一个字符串，并将它重构为原来的python对象。

file:类文件对象，有read()和readline()接口。

```python

import pickle   #引入数据持久性模块

myList = (1,2,3,4,5,"sunck is a good man")
path = r"C:\Users\xlg\Desktop\Python-1704\day08\1-文件读写\file6.txt"
f = open(path, "wb")
pickle.dump(myList, f)
f.close()


#读取
f1 = open(path, "rb")
tempList= pickle.load(f1)
print(tempList)
f1.close()
```

###【9】编码和解码

如果中文字符在写入文件的时候没有设置`utf-8`或者`gbk`、`gb2312`等中文字符集，那么读取的时候就是2进制的。
```python
path = 'wdemo.txt'

with open(path, "wb") as f1:
    str = "你好上海，你好千锋"
    f1.write(str.encode("utf-8")) 

with open(path, "rb") as f2:
    data = f2.read()
    print(data)
    print(type(data))
    newData = data.decode("utf-8")
    print(newData)
    print(type(newData))
```

###【10】文件系统（os模块）

接下来我们讲一个Python里面十分有用的模块，什么是模块？其实我们每一个.py的文件都是一个模块。python自身带有非常多使用的模块，在日常编程中，如果能够熟练地掌握它们，将事半功倍。

首先要介绍的高大上的OS模块，OS就是Operating System的缩写，意思是操作系统。很多的文件系统的访问都是通过OS模块来实现的。我们所知道的windows、Mac OS、UNIX、Linux等,对于这些系统的底层实现起来也是不一样的，因此你就需要考虑用到哪个模块了。

但是python是跨平台的语言，也就是说，同样的源码在不同的操作系统不需要修改同样可以实现。有了OS模块，不需要关心什么操作系统下使用什么模块，OS会帮你选择正确的模块并调用。

|函数名                    |                       使用方法                            |
|-------------------------|---------------------------------------------------------|
|os.getcwd()              |                       获得当前工作目录                     |
|os.curdir                |                   返回当前目录（'.')                       |
|os.environ               |                     获取当前环境变量                       |
|os.environ.get(path)     |                    获取指定的环境变量                       |
|os.listdir(path)：       |                 列出dirname下的目录和文件                   |
|os.mkdir(path):          |             创建单层目录，如果目录已经存在抛出异常             |
|os.makedirs(.path)       |递归创建多级目录，如果目录已经存在抛出异常（E:\a\b和E:\a\c不会冲突)|
|os.remove(path)          |                       删除文件                            |
|os.rmdir(path)           |        删除单层目录，如果目录非空则抛出异常                    |
|os.removedirs(path)      | 递归删除目录，从子目录到父目录逐个删除，遇到目录非空则抛出异常     |
|os.rename(new,old)       |                  将文件的old重命名为new                    |
|os.system(command)       |                  运行系统的shell命令                       |
|以下是：                  |        支持路径操作中常用到的一些定义支持所有平台               |
|os.curdir                |                   指代当前目录（'.'）                      |
|os.pardir                |                  指代上一级目录('..')                      |
|os.sep                   |  输出操作系统特定的路径分隔符（windons下是\，linux下是/）       |
|os.linesp                | 当前平台使用的终止符（（windons下是\r\n，linux下是\n）         |
|os.name                  | 指定当前的操作系统（包括'posix','nt','mac','os2','ce','java')|

####1.getcwd()
得当前工作目录  

```python
import os
print(os.getcwd())

#C:\\Python36
```

####2.chdir()
改变工作目录

```python
import os
os.chdir('C:\\Python27')
print(os.getcwd())

#C:\\Python27
```

####3、system()
运行系统命令

```python

import os
os.system('clear')  #清理命令行屏幕上的所有过去输入的信息

```

####4、walk()
非常有用的函数，可以用来指定遍历指定路径下的所有子目录，并返回一个三元祖的结果：

```python

import os

for i in os.walk('/Users/ruidong/www'):
    print(i)

```


####5.os.path模块
这是另一个强大的模块，它可以完成一些路径操作。


|函数名                                   |                           使用方法                       |
|----------------------------------------|---------------------------------------------------------|
|os.path.abspath(path)                   |#返回绝对路径                                              |
|os.path.basename(path)                  |#返回文件名                                                |
|os.path.dirname(path)                   |#返回文件路径                                              | 
|os.path.join(path1[, path2[, ...]])     |#把目录和文件名合成一个路径                                   |
|os.path.split(path)                     |#把路径分割成dirname和basename，返回一个元组                  |
|os.path.splitext(path)                  |#分割路径，返回路径名和文件扩展名的元组                         |
|os.path.getsize(path)                   |#返回文件大小，如果文件不存在就返回错误                         |
|os.path.getatime(path)                  |#返回最后一次访问的时间。                                     |
|os.path.getctime(path)                  |#返回文件的创建时间                                          |
|os.path.getmtime(path)                  |#返回在此path下最后一次修改的时间。                            |
|以下函数返回的是                           |True或False                                               |
|os.path.exists(path)                    |#路径存在则返回True,否则回False                              |
|os.path.samefile(path1, path2)          | #判断两个变量是不是指向同一个文件                             |
|os.path.isabs(path)                     |#判断指定路径是否是绝对路径                                   |
|os.path.isdir(path)                     | #判断指定路径是否存在且是个目录                               |
|os.path.isfile(path)                    |#判断指定路径是否存在且是个文件                                |
|os.path.islink(path)                    |#判断指定路径是否存在且是一个符号链接                           |
|os.path.ismount(path)                   |#判断指定目录是否存在且是个挂载点                              |
 


#####os.path.join（）

这里的join和BIF里面的join不是一回事，它是将路径名和文件名组合成一个完整的路径。

```python
import os

_path = r'/Users/ruidong/www'

_file = r'demo.txt'

final_path = os.path.join(_path,_file)

print(final_path)


#/Users/ruidong/www/demo.txt
```

####split()和splitext()
split()和splitext()函数都用于分割路劲，split()函数分割路径和文件名，而splitext()用于分割文件名和后缀名。

```python
import os

_path = r'/Users/ruidong/www/demo.txt'

print(os.path.split(_path))
print(os.path.splitext(_path))

#('/Users/ruidong/www', 'demo.txt')
#('/Users/ruidong/www/demo', '.txt')
```



###【11】栈和队列

collections是Python内建的一个集合模块，提供了许多有用的集合类。

使用list存储数据时，按索引访问元素很快，但是插入和删除元素就很慢了，因为list是线性存储，数据量大的时候，插入和删除效率很低。

deque是为了高效实现插入和删除操作的双向列表，适合用于队列和栈：
####栈


栈（stack）又名堆栈，它是一种运算受限的线性表。其限制是仅允许在表的一端进行插入和删除运算。这一端被称为栈顶，相对地，把另一端称为栈底。向一个栈插入新元素又称作进栈、入栈或压栈，它是把新元素放到栈顶元素的上面，使之成为新的栈顶元素；从一个栈删除元素又称作出栈或退栈，它是把栈顶元素删除掉，使其相邻的元素成为新的栈顶元素。

栈的原则就是先进后出

<image src='images/stack.jpg' />

我们用一个列表来模拟压栈：

我们列表的最后一个元素就是栈顶

第一个元素就是栈底

```python
#用队列集合模拟栈运行
import collections
#创建一个队列 ,用于模拟栈的运行
queue = collections.deque()
print(queue)

#进栈(存数据)
queue.append("A")
print(queue)
queue.append("B")
print(queue)
queue.append("C")
print(queue)


#出栈(取数据)
res1 = queue.pop()
print("res1 =", res1)
print(queue)
res2 = queue.pop()
print("res2 =", res2)
print(queue)
res3 = queue.pop()
print("res3 =", res3)
print(queue)
```

####队列

队列是一种特殊的线性表，特殊之处在于它只允许在表的前端（front）进行删除操作，而在表的后端（rear）进行插入操作，和栈一样，队列是一种操作受限制的线性表。进行插入操作的端称为队尾，进行删除操作的端称为队头。

它的原则是先进先出

<image src='images/deque.png' />

```python


import collections

#创建一个队列
queue = collections.deque()
print(queue)

#进队(存数据)
queue.append("A")
print(queue)
queue.append("B")
print(queue)
queue.append("C")
print(queue)


#出队(取数据)
res1 = queue.popleft()
print("res1 =", res1)
print(queue)
res2 = queue.popleft()
print("res2 =", res2)
print(queue)
res3 = queue.popleft()
print("res3 =", res3)
print(queue)

```

我们的栈和队列了其实就是学习一种思想，包裹之前的递归都是一中程序的思想

####课堂小案例，结合文件

遍历目录

```python

import os

def getALlDir(path,sp = '  '):
    filesList = os.listdir(path)
    sp += '  '
    for fileName in filesList:
        filesAbsPath = os.path.join(path, fileName)
        if os.path.isdir(filesAbsPath):
            print(sp + '目录：',fileName)
            getALlDir(filesAbsPath,sp)
        else:
            print(sp + '文件：',fileName)

getALlDir(r'/Users/ruidong/PycharmProjects')

```

##第十三章
###【1】时间可以改变一切：time模块
___

在我们平常的代码中，经常需要和时间打交道。在Python中，与时间处理相关的模块有：time、datetime以及calendar。学会计算时间，对程序的调优非常重要，可以在程序中狂打时间戳，来具体判断程序中哪一块耗时最多，从而找到程序调优的重心处。这里先来讲一个time模块。 
在开始前，先说明几点：

```python
1、在Python中，通常有这几种方式表示时间：时间戳、格式化的时间字符串、元组（struct_time 共九种元素）。由于Python的time模块主要是调用C库实现的，所以在不同的平台可能会有所不同。
2、时间戳（timestamp）的方式：时间戳表示是从1970年1月1号 00:00:00开始到现在按秒计算的偏移量。查看一下type(time.time())的返回值类型，可以看出是float类型。返回时间戳的函数主要有time()、clock()等。
3、UTC（世界协调时），就是格林威治天文时间，也是世界标准时间。在中国为UTC+8。DST(夏令时)：是一种节约能源而人为规定时间制度，在夏季调快1个小时。
4、元组方式：struct_time元组共有9个元素，返回struct_time的函数主要有gmtime()，localtime()，strptime()。
```

使用该模块中的函数时，必须先引入该模块（import time） 

####1、时间戳
python中的时间戳是以秒为单位的，它是一个浮点类型的数据。

```python

import time

#时间戳
print(time.time())
#毫秒时间戳，
print(time.time() * 1000)
#毫秒时间戳取整
print(int(time.time() * 1000))

#1510884320.13084
#1510884320130.936
#1510884320130
```

####2、struct_time元祖结构格式
time.localtime(secs) 
将一个时间戳转换为当前时区的struct_time，即时间数组格式的时间

如果secs参数未提供，则以当前时间为准（即会默认调用time.time()）。 

```python
#没有传入参数

import time
print(time.localtime())

#time.struct_time(tm_year=2017, tm_mon=11, tm_mday=17, tm_hour=10, tm_min=14, tm_sec=2, tm_wday=4, tm_yday=321, tm_isdst=0)
``` 

```python
#传入参数的
import time

out_time = time.time() - (60 * 60 * 24 * 365 *2)
print(int(out_time))
print(time.localtime(1447812614))

#1447812789
#time.struct_time(tm_year=2015, tm_mon=11, tm_mday=18, tm_hour=10, tm_min=10, tm_sec=14, tm_wday=2, tm_yday=322, tm_isdst=0)

```

####3、将一个时间戳转换为UTC时区的struct_time 

time.gmtime([secs]) 

time.gmtime() 函数将一个时间戳转换为UTC时区（0时区）的struct_time，可选的参数sec表示从1970-1-1 00:00:00以来的秒数。其默认值为time.time()，函数返回time.struct_time类型的对象。（struct_time是在time模块中定义的表示时间的对象）。 
如果secs参数未提供，则以当前时间为准。 

sec – 转换为time.struct_time类型的对象的秒数


```python
#注意它是0时区，就是说比我们的时间少了8个小时
import time

print(time.gmtime())

#time.struct_time(tm_year=2017, tm_mon=11, tm_mday=17, tm_hour=2, tm_min=18, tm_sec=12, tm_wday=4, tm_yday=321, tm_isdst=0)
```

####4、time.mktime(t)：将一个struct_time转化为时间戳 

time.mktime(t) 函数执行与gmtime(), localtime()相反的操作，它接收struct_time对象作为参数,返回用秒数表示时间的浮点数。 
如果输入的值不是一个合法的时间，将触发 OverflowError 或 ValueError。 
参数：

t – 结构化的时间或者完整的9位元组元素

```python
import time

print(time.mktime(time.localtime()))

#1510885313.0
```

####5、让程序睡一会

time.sleep(secs)：线程推迟指定的时间运行 
线程睡眠指定时间，单位为妙。


secs：为数值类型的整数或浮点数。

```python

import time

for i in range(1,6):
    print(i)
    time.sleep(1)


#5秒以后触发
print("节日快乐")

```

####6、time.clock() 
这个函数， 函数以浮点数计算的秒数返回当前的CPU时间。用来衡量不同程序的耗时，比time.time()更有用。在不同的系统上含义不同。在NUix系统上，它返回的是“进程时间”，它是用妙表示的浮点数（时间戳）。而在Windows中，第一次调用，返回的是进程运行时实际时间。而第二次之后的调用是自第一次调用以后到现在的运行时间。 
返回值 
该函数有两个功能：

（1）在第一次调用的时候，返回的是程序运行的实际时间；
（2）第二次之后的调用，返回的是自第一次调用后,到这次调用的时间间隔在win32系统下，这个函数返回的是真实时间（wall time），而在Unix/Linux下返回的是CPU时间。


```python
import time

print(time.clock())
print(time.clock())

#0.066535
#0.0666

```
####7、time.asctime( [t] ) 
把一个表示时间的元组或者struct_time表示为 ‘Sun Aug 23 14:31:59 2015’ 这种形式。如果没有给参数，会将time.localtime()作为参数传入。 
参数：

t – 9个元素的元组或者通过函数 gmtime() 或 localtime() 返回的时间值

```python

import time

local = time.localtime()
asc = time.asctime(local)

print(asc)

Fri Nov 17 10:41:46 2017
```


####8、time.ctime([secs]) 
把一个时间戳（按秒计算的浮点数）转化为time.asctime()的形式。如果未指定参数，将会默认使用time.time()作为参数。它的作用相当于time.asctime(time.localtime(secs)) 
参数：

secs – 要转换为字符串时间的秒数

```python
import time

print(time.ctime())

#Fri Nov 17 10:44:43 2017
```

####9、格式化时间
time.strftime( format [, t] ) 

返回字符串表示的当地时间。 

把一个代表时间的元组或者struct_time（如由time.localtime()和time.gmtime()返回）转化为格式化的时间字符串，格式由参数format决定。如果未指定，将传入time.localtime()。如果元组中任何一个元素越界，就会抛出ValueError的异常。函数返回的是一个可读表示的本地时间的字符串。 
参数：

format：格式化字符串

t ：可选的参数是一个struct_time对象

```python

%a  本地星期名称的简写（如星期四为Thu）      
%A  本地星期名称的全称（如星期四为Thursday）      
%b  本地月份名称的简写（如八月份为agu）    
%B  本地月份名称的全称（如八月份为august）       
%c  本地相应的日期和时间的字符串表示（如：15/08/27 10:20:06）       
%d  一个月中的第几天（01 - 31）  
%f  微秒（范围0.999999）    
%H  一天中的第几个小时（24小时制，00 - 23）       
%I  第几个小时（12小时制，0 - 11）       
%j  一年中的第几天（001 - 366）     
%m  月份（01 - 12）    
%M  分钟数（00 - 59）       
%p  本地am或者pm的相应符      
%S  秒（00 - 61）    
%U  一年中的星期数。（00 - 53星期天是一个星期的开始。）第一个星期天之    前的所有天数都放在第0周。     
%w  一个星期中的第几天（0 - 6，0是星期天）    
%W  和%U基本相同，不同的是%W以星期一为一个星期的开始。    
%x  本地相应日期字符串（如15/08/01）     
%X  本地相应时间字符串（如08:08:10）     
%y  去掉世纪的年份（00 - 99）两个数字表示的年份       
%Y  完整的年份（4个数字表示年份）
%z  与UTC时间的间隔（如果是本地时间，返回空字符串）
%Z  时区的名字（如果是本地时间，返回空字符串）       
%%  ‘%’字符  

```

```python

import time

local_time = time.localtime()

format_time = time.strftime('%Y年%m月%d日 %H：%M：%S',local_time)

print(format_time)
#注意月份是小m（%m），分钟是大M（%M）。年是大写

#2017年11月17日 10：51：10

```

你也可以玩拼接

```python

import time

local_time = time.localtime()

print(str(local_time.tm_year) + "年" + str(local_time.tm_mon) + "月" + str(local_time.tm_mday) + "日")

#2017年11月17日
```

获取当前时间的时分秒

```python
import time

local_time = time.localtime()

print(time.strftime('%H:%M:%S',local_time))

#10:55:44
```
获取当前时间的格式化时间

```python
import time

t = time.localtime()

print(time.strftime('%F %T',t)) #简写
print(time.strftime('%Y-%m-%d %H:%M:%S %p',t)) # am 还是 pm

#2017-11-17 11:23:57
#2017-11-17 11:23:57 AM
```

####10、将格式字符串转化成struct_time.

time.strptime(string[,format]) 

该函数是time.strftime()函数的逆操作。time strptime() 函数根据指定的格式把一个时间字符串解析为时间元组。所以函数返回的是struct_time对象。 
参数：

string ：时间字符串
format：格式化字符串

```python

import time,datetime

#创建一个时间字符串变量stime
stime = "2015-08-24 13:01:30"

formattime = time.strptime(stime,"%Y-%m-%d %H:%M:%S")

print(formattime)


#遍历返回的时间元组序列
for i in formattime :
    print(i,end=' ')

#time.struct_time(tm_year=2015, tm_mon=8, tm_mday=24, tm_hour=13, tm_min=1, tm_sec=30, tm_wday=0, tm_yday=236, tm_isdst=-1)
#2015 8 24 13 1 30 0 236 -1 
```

<font color='red'>注意:在使用strptime()函数将一个指定格式的时间字符串转化成元组时，参数format的格式必须和string的格式保持一致，如果string中日期间使用“-”分隔，format中也必须使用“-”分隔，时间中使用冒号“:”分隔，后面也必须使用冒号分隔，否则会报格式不匹配的错误。</font>

###【2】学会操控时间：datetime模块
___

 Python提供了多个内置模块用于操作日期时间，像calendar，time，datetime。time模块我在之前的文章已经有所介绍，它提供 的接口与C标准库time.h基本一致。相比于time模块，datetime模块的接口则更直观、更容易调用。今天就来讲讲datetime模块。
 
 datetime模块定义了两个常量：datetime.MINYEAR和datetime.MAXYEAR，分别表示datetime所能表示的最 小、最大年份。其中，MINYEAR = 1，MAXYEAR = 9999。（对于偶等玩家，这个范围已经足够用矣~~）

datetime模块定义了下面这几个类：

```python
datetime.date：表示日期的类。常用的属性有year, month, day；
datetime.time：表示时间的类。常用的属性有hour, minute, second, microsecond；
datetime.datetime：表示日期时间。
datetime.timedelta：表示时间间隔，即两个时间点之间的长度。
datetime.tzinfo：与时区有关的相关信息。（这里不详细充分讨论该类，感兴趣的童鞋可以参考python手册）
```
今天我们讲讲datetime的基本的几种方法：

####1. 获取当前datetime

```python
import datetime
print(datetime.datetime.now())

#2017-11-17 14:42:01.175940
```
####2. 获取当天date

```python
import datetime
print(datetime.date.today())

#2017-11-17
```

####3. 获取明天/前N天 /或者昨天
```python
import datetime
print(datetime.date.today())
print(datetime.date.today() + datetime.timedelta(days=1))
print(datetime.date.today() + datetime.timedelta(days=-1))
print(datetime.date.today() - datetime.timedelta(days=1))

#2017-11-17
#2017-11-18
#2017-11-16
```
####4、获取当天开始和结束时间(00:00:00 23:59:59)
datetime.combine(date, time)：根据date和time，创建一个datetime对象；

```python
import datetime

print(datetime.datetime.combine(datetime.date.today(), datetime.time.min))
print(datetime.datetime.combine(datetime.date.today(), datetime.time.max))
print((str(datetime.datetime.combine(datetime.date.today(), datetime.time.max)).split('.'))[0])  #转换成str类型的舍去毫秒值


#2017-11-17 00:00:00
#2017-11-17 23:59:59.999999
#2017-11-17 23:59:59
```

####5. 获取两个datetime的时间差

total_seconds()把两时间集转换成总秒数

```python
print((datetime.datetime(2018,1,13,12,0,0) - datetime.datetime.now()).total_seconds())

#4912373.883664
```
####6.关系转换 

#####datetime => string 

```python
import datetime

date_to_str = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

print(date_to_str,type(date_to_str))

#22014-12-31 18:20:10 <class 'datetime.datetime'>
```

#####string => datetime

```python
import datetime

str_to_date = datetime.datetime.strptime("2014-12-31 18:20:10", "%Y-%m-%d %H:%M:%S")

print(str_to_date,type(str_to_date))

#2014-12-31 18:20:10 <class 'datetime.datetime'>
```

#####datetime => timetuple (time.struct_time格式)

```python

import datetime

date_to_timetuple = datetime.datetime.now().timetuple()

print(date_to_timetuple,type(date_to_timetuple))

#time.struct_time(tm_year=2017, tm_mon=11, tm_mday=17, tm_hour=16, tm_min=31, tm_sec=2, tm_wday=4, tm_yday=321, tm_isdst=-1) <class 'time.struct_time'>
```

#####timetuple  => datetime

```python

import datetime,time
now = time.localtime() #struct_time类型
print(now)
now = time.strftime("%F %T",ls)  #先转成timestamp时间格式,转成字符串
print(now,type(now))
now = datetime.datetime.strptime(now, "%Y-%m-%d %H:%M:%S")
print(now,type(now))

```

#####datetime => timestamp 

```python

import datetime,time

now = datetime.datetime.now()
timestamp = time.mktime(now.timetuple())
print(timestamp,type(timestamp))

#1510908711.0 <class 'float'>
```

#####timestamp => datetime

```python

import datetime

datetime = datetime.datetime.fromtimestamp(1421077403.0)
print(datetime,type(datetime))

#2015-01-12 23:43:23 <class 'datetime.datetime'>
```

####7. 获取本周/本月/上月最后一天 和第一天

本周

date.weekday()：返回weekday，如果是星期一，返回0；如果是星期2，返回1，以此类推；

```python
import datetime

today = datetime.date.today()
print(today)

one = today - datetime.timedelta(today.weekday())
print(one)  #本周第一天

two = today + datetime.timedelta(6-today.weekday())
print(two)  #本周最后一天


#2017-11-17
#2017-11-13
#2017-11-19
```

本月

cale是python的日历模块

calendar.monthrange(year,month) 

返回两个整数。第一个是该月的星期几的日期码，第二个是该月的日期码。日从0（星期一）到6（星期日）;月从1到12。

```python

import calendar,datetime
today = datetime.date.today()
_,last_day_num = calendar.monthrange(today.year,today.month)
print(last_day_num)
last_day = datetime.date(today.year, today.month,last_day_num)
print(last_day)




#_,取可迭代序列的最后一个值，但是不能取中间的，舍弃如果是三个那么就是_,_,
#30
#2017-11-30


```

获取上个月的最后一天

```python

import datetime

today = datetime.date.today()
print(today)
first = datetime.date(day=1, month=today.month, year=today.year)
print(first)
lastMonth = first - datetime.timedelta(days=1)
print(lastMonth)

#2017-11-17
#2017-11-01
#2017-10-31
```

上个月的最好一天（跨年）


```python

import datetime,time

today = datetime.datetime.strptime('2017-01-01',"%Y-%m-%d")
print(today)
first = datetime.date(day=1, month=today.month, year=today.year)
print(first)
lastMonth = first - datetime.timedelta(days=1)
print(lastMonth)

#2017-01-01 00:00:00
#2017-01-01
#2016-12-31
```

###【3】时间的书籍：calendar（日历模块）
——————
####1、日历
ccalendar(year,w=2,l=1,c=6) 
返回一个多行字符串格式的year年年历，3个月一行，间隔距离为c。 每日宽度间隔为w字符。每行长度为21* W+18+2* C。l是每星期行数。

```python
import calendar
print(calendar.calendar(2017))
```

####2、获取每周的开始值
firstweekday() 
返回当前每周起始日期的设置。默认情况下，首次载入caendar模块时返回0，即星期一。

```python
import calendar
print(calendar.firstweekday())

#0
```

####3、判断是否是润年
calendar.isleap(year) 
是闰年返回True，否则为false。

<font color='red'>注意：只能是整数，否则会报错</font>

```python

import calendar
print(calendar.isleap(2020))


#True
```

####4、返回在两个年数时间轴之间的闰年总数。
calendar.leapdays(y1,y2) 
返回在Y1，Y2两年之间的闰年总数。

```python

import calendar
print(calendar.leapdays(-1000,2017))

#732
```

####5、返回指定月的日历

calendar.month(year,month,w=2,l=1) 

返回一个多行字符串格式的year年month月日历，两行标题，一周一行。每日宽度间隔为w字符。每行的长度为7* w+6。l是每星期的行数。

```python
import calendar
print(calendar.month(2017,11))

```

####6、返回指定月的瑞列表

calendar.monthcalendar(year,month) 

返回一个整数的单层嵌套列表。每个子列表装载代表一个星期的整数。Year年month月外的日期都设为0;范围内的日子都由该月第几日表示，从1开始。

```python

import calendar
print(calendar.monthcalendar(2017,11) )

#[[0, 0, 1, 2, 3, 4, 5], [6, 7, 8, 9, 10, 11, 12], [13, 14, 15, 16, 17, 18, 19], [20, 21, 22, 23, 24, 25, 26], [27, 28, 29, 30, 0, 0, 0]]
```

####7、返回指定月的最后一天的星期码和日期码

calendar.monthrange(year,month) 

返回一个元祖。第一个是该月的星期几的日期码，第二个是该月的最后一天日期码。日从0（星期一）到6（星期日）;月从1到12。

```python

import calendar
time1 = calendar.monthrange(2017,11)
print(time1,type(time1))

#(2, 30) <class 'tuple'>
```

####8、返回指定日期的星期码

calendar.weekday(year,month,day) 

返回给定日期的日期码。0（星期一）到6（星期日）。月份为 1（一月） 到 12（12月）。


```python
import calendar
print(calendar.weekday(2017,11,17))

#4
```

####9、设置一周里那一天作为第一天

calendar.setfirstweekday(weekday) 

设置每周的起始日期码。0（星期一）到6（星期日）。

```python
import calendar
print(calendar.firstweekday())
calendar.setfirstweekday(calendar.SUNDAY)
print(calendar.firstweekday())

#0
#6
```



####10、将tupletime转成时间戳

calendar.timegm(tupletime) 

和time.gmtime相反：接受一个时间元组形式，返回该时刻的时间辍（1970纪元后经过的浮点秒数）。

```python


import calendar,time

now = time.localtime()
date = calendar.timegm(now)
print(date)

#1510940959
```