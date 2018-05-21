#Lesson 9
___
#排序算法

##快速排序

```python

#通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，法然后再按此方对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。


def qkSort(_list,start,end):

    if start < end:
        i,j = start,end
        #设置基数
        base = _list[i]

        while i < j:
            #如果列表后边的数,比基准数大或相等,则前移一位直到有比基准数小的数出现
            while (i < j) and (_list[j] >= base):
                j = j - 1

            #如找到,则把第j个元素赋值给第个元素i,此时表中i,j个元素相等
            _list[i] = _list[j]

            #同样的方式比较前半区
            while (i < j) and (_list[i] <= base):
                i = i + 1
            _list[j] = _list[i]
        #做完第一轮比较之后,列表被分成了两个半区,并且i=j,需要将这个数设置回base
        _list[i] = base

        #递归前后半区
        qkSort(_list, start, i - 1)

        qkSort(_list, j + 1, end)
    return _list


_list = [49,38,65,97,76,13,27,49]

qkSort(_list,0,len(_list)-1)

print(_list)

```

##插入排序

```python

#插入排序的基本操作就是将一个数据插入到已经排好序的有序数据中，从而得到一个新的、个数加一的有序数据，算法适用于少量数据的排序，时间复杂度为O(n^2)。是稳定的排序方法。插入算法把要排序的数组分成两部分：第一部分包含了这个数组的所有元素，但将最后一个元素除外（让数组多一个空间才有插入的位置），而第二部分就只包含这一个元素（即待插入元素）。在第一部分排序完成后，再将这个最后元素插入到已排好序的第一部分中。

def insert_sort(lists):
    # 插入排序
    count = len(lists)
    print(count)
    for i in range(1, count):
        key = lists[i]
        #key  = 38
        #key  = 65
        #key =  97
        #key = 76
        j = i - 1
        while j >= 0:
            if lists[j] > key:
                lists[j + 1] = lists[j]
                lists[j] = key
                #[38,49,65,97,76,13,27,49]
                #[38,49,65,76,97,13,27,49]
            j -= 1
    return lists

_list = [49,38,65,97,76,13,27,49]

insert_sort(_list)

print(_list)

```


```python

#基本思想：第1趟，在待排序记录r1 ~ r[n]中选出最小的记录，将它与r1交换；第2趟，在待排序记录r2 ~ r[n]中选出最小的记录，将它与r2交换；以此类推，第i趟在待排序记录r[i] ~ r[n]中选出最小的记录，将它与r[i]交换，使有序序列不断增长直到全部排序完毕。

def select_sort(lists):
    # 选择排序
    count = len(lists)

    for i in range(0, count):

        min = i

        for j in range(i + 1, count):

            if lists[min] > lists[j]:

                min = j

        lists[min], lists[i] = lists[i], lists[min]

    return lists

_list = [49,38,65,97,76,13,27,49]

select_sort(_list)

print(_list)
```
---
##做个有趣的事情(开心一会儿)

###1.windows扩展库

如果同学们打过魔兽争霸的话就知道`按键精灵了`，它是通过调用Windows的键盘号来改变的，那我们python也可以。

不仅如此，python通过pywin32还可以控制我们桌面上的窗口。

那什么是pywin32了？它是一个python调用windows的一个集合包。直接对应python的版本安装就可以了。

但是在安装之前，在安装之前可以最好安装过vc库，比如java在windows底下需要安装vc2013，php7需要的是vc2012和vc2015，我们python了需要vc2015就可以了，不过最好使用驱动精灵检查安装，它会告诉你，你的电脑缺什么。

###2.控制窗口

在我们toos文件夹里面有个Spy.exe，它的瞄准窗口可以获取任何的程序运行信息。

<image src='images/spy.png'>

这里面我们只需要知道标题和类名就可以了。

我们来个小例子：

```python
import win32con #引入windows的常量定义库
import win32gui #引入windows界面对象

#我们使用上面QQ的窗口信息
QQWin = win32gui.FindWindow("TXGuiFoundation", "QQ")
#第一个参数是类名，第二个是标题，找出这个对象在内存中的位置
#隐藏窗口
win32gui.ShowWindow(QQwin,win32con.SW_HIDE)

#显示窗口
win32gui.ShowWindow(QQwin,win32con.SW_SHOW)

```
我们做个整蛊的小程序：
我们在程序以后，只要他一开QQ就让他闪的没完没了。

```python
import win32con
import win32gui
import time

while True:
    QQWin = win32gui.FindWindow("TXGuiFoundation", "QQ")
    win32gui.ShowWindow(QQWin, win32con.SW_HIDE)
    time.sleep(2)
    win32gui.ShowWindow(QQWin, win32con.SW_SHOW)
    time.sleep(2)
```
###内存的管理

这就是一个例子，但是内存地址是随便找的

```python

import win32process  #进程模块  需要安装 pywin32 包  
import win32con      #系统定义  
import win32api      #调用系统模块  
import ctypes        #C语言类型  
import win32gui      #界面  
  
PROCESS_ALL_ACCESS=(0x000F0000|0x00100000|0xFFF)    #一个常量，标识最高权限打开一个程序  
window=win32gui.FindWindow('MainWindow','植物大战僵尸中文版')  #查找窗体  
hid,pid=win32process.GetWindowThreadProcessId(window)      #根据窗体抓取进程编号  
phand=win32api.OpenProcess(PROCESS_ALL_ACCESS,False,pid)   #用最高权限打开进程线程  
date=ctypes.c_long()     #C语言的整数类型，读取数据  
mydll=ctypes.windll.LoadLibrary('C:\\Windows\\System32\\kernel32.dll')   #加载内核模块  
mydll.ReadProcessMemory(int(phand),405455088,ctypes.byref(date),4,None)  #读取内存（内存地址是:405455088）  
print(date.value)  
newdata=ctypes.c_long(10010)    #修改内存数据为10010  
mydll.WriteProcessMemory(int(phand),405455088,ctypes.byref(newdata),4,None)   #修改内存地址

```

3、语音合成

在这个之前，我们要打开  控制面板->轻松访问->语音识别里面启动语音识别


循环读取指定的字

```python
import time
import win32com.client

#获取win32的语音接口
dehua = win32com.client.Dispatch("SAPI.SPVOICE")

while 1:
    dehua.Speak(“我不管，我最帅，我是你们的小可爱")
    time.sleep(1)

```


##模块化
___
###1.模块概述


概述：
目前代码比较少，写在一个文件中还体现不出什么缺点，但是随着代码量越来越多，代码就越来越难以维护。

为了解决难以维护的问题，我们把很多相似功能的函数分组，分别放到不同的文件中取。这样每个文件所包含的内容相对较少，而且对于每一个文件的大致功能可用用文件名来体现。很多编程语言都是这么来组织代码结构。一个.py文件就是一个模块

为什么需要模块化：

```python
1、提高代码的可维护性
2、提高了代码的复用度，当一个模块完毕，可以被多个地方引用
3、引用其他的模块(内置模块和三方模块和自定义模块)
4、避免函数名和变量名的冲突
```
###2、导入模块

我们引入模块一般都会直接使用 import XXXX

其实还是有很多种引入方法的。

```python
# 我们可以分开引入各个模块
# import 模块名
# import os
# import sys

#也可以用（file.class）的方式去做，多个模块用逗号隔开
# import 模块名.函数或属性 ， 模块名
# import os.path,sys


#从什么模块引入什么类
# from 模块名 improt 函数或属性
# from os import path


```
我们python中有标准模块，也就是自己自带的模块，比如：

```python

math   数学模块
time   时间模块
os     文件系统模块
sys    系统指令模块

```

这些模块是远远不足以满足我们日后的开发需求的，所以在开源社区中，很多的python支持者和官方也提供了第三方模块：

```python

pymysql    mysql数据库模块
redis      redis缓存模块
pymongo    mongoDB文件存储模块
pywin32    windows模块库总名称

```

###3、自己定义一个模块

我们现在已经知道一个模块就是一个文件，那么我们自己可以定义一个试一试

####我们定义一个shanghai的模块：

```python
#shanghai.py
#一个.py文件就是一个模块

def BaoShan():
    print("Baoshan District is a wonderful place")

def Hongkou():
    print("Hongkou District is a wonderful place")

def YangPu():
    print("YangPu District is a wonderful place")

HuangPu =  'YangPu District is a wonderful place'


```

####我们在另一个文件里面引入它：

```python

import shanghai

shanghai.BaoShan()

shanghai.Hongkou()

shanghai.YangPu()

print(shanghai.HuangPu)

#HuangPu是一个普通的变量，在这里叫属性，所以必须print

#Baoshan District is a wonderful place
#Hongkou District is a wonderful place
#YangPu District is a wonderful place
#YangPu District is a wonderful place
```


####我们使用指定引入：

```python

#指定引入的话我们只能使用BaoShan这个方法，不能使用其它的方法

#as的作用是起别名。不能使用原来的函数名或者方法名。

from shanghai import BaoShan as BS

BS()

#Baoshan District is a wonderful place

```

####我们使用指定全引入：

这种方法最好不要使用，如果两个模块的方法名一样，那么后引入的会覆盖前面的。

```python
#星号(*)代表所有，用了星号，就不能用as

from shanghai import * 

BaoShan()

Hongkou()

#Baoshan District is a wonderful place
#Hongkou District is a wonderful place
```

####`__name__`的使用

```python

每一个模块都有一个__name__属性，当其值等于"__main__"时，表明该模块自身在执行。否则被引入其他文件

当前文件如果为程序的入口文件，则__name__属性的值为__main__
```
看下面的例子：

```python
#shanghai.py

if __name__ == "__main__":
    print("这是shanghai.py")
else:
    print(__name__)
    def BaoShan():
        print("Baoshan District is a wonderful place")

    def Hongkou():
        print("Hongkou District is a wonderful place")

    def YangPu():
        print("YangPu District is a wonderful place")

#:我在shanghai.py中运行得到一下结果

#这是shanghai.py
```

我在其他文件中引入并且调用：

```python
import shanghai

shanghai.BaoShan()


#shanghai
#Baoshan District is a wonderful place
```

换一种方法来写：

```python
#shanghai.pu

def  main():
    print('我是main')

def BaoShan():
    print("Baoshan District is a wonderful place")


def Hongkou():
    print("Hongkou District is a wonderful place")


def YangPu():
    print("YangPu District is a wonderful place")



if __name__ == "__main__":
    main()


#这样的话在本程序内部里面运行的话，自动调用main(),而且main()也可以被外部程序引入调用，因为if在下面执行。

```

###4、“包”的理解

思考：如果不同的人编写的模块同名怎么办？

解决：为了解决模块命名的冲突，引入了按目录来组织模块的方法，称为包

特点：引入了包以后，只要顶层的包不与其他人发生冲突，那么模块都不会与别人的发生冲突

注意：目录只有包含一个叫做`__init__.py`的文件才被认作是一个包，主要是为了避免一些滥竽充数的名字，目前这个文件中基本上什么也不用写.


比如我们定义两个名字一样的模块，都叫loadpath，但是功能有一点差异，那么一起引入到一个.py文件中会出现问题。这个时候我们建立一个文件夹，一个叫‘a’，一个‘b’，每个文件夹里面都建立以`__init__.py`,这样‘a’和‘b’都是一个包了，看下面的例子：

a文件下的loadpath模块

```python
def Loadpath(a):
    print("这是%s包的范围"%a)


if __name__ == "__main__":
    Loadpath('a')
else:
    Loadpath('A')
```
b文件下的loadpath模块

```python
def Loadpath(b):
    print("这是%s包的范围"%b)


if __name__ == "__main__":
    Loadpath('b')
else:
    Loadpath('B')
```
在其它文件中调用：

```python
import a.loadpath,b.loadpath

a.loadpath
b.loadpath

#这是A包的范围
#这是B包的范围

```

####4、安装第三方模块

什么是第三方模块了，就是别人活官方提供的，在python安装的时候它们不在安装包内部，需要我们自己去下载安装。

python的模块安装也是分系统的，比如mac，linux，windows。
常用的三种安装方法，有pip，easy_install，和python 手动安装

windows在安装python的时候可以勾选环境变量和pip，而mac和linuc需要自己去用brew和yum安装pip。如果电脑中包含了python2版本，和python3版本的的活，指定的python版本安装的时候要给pip加上版本号,比如`pip3 install pymysql`,这样的话`pymysql`这个第三方模块就安装到puthon3中去了，如果在执行`pip install pymysql`的话，那么pip就不会去官网去寻找了，而是现在本地寻找，会直接去python2的扩展库里面去copy一份过去。
当执行完毕后，可以使用`pip list`来查看第三方扩展库在不在，

easy_install 是setuptoos 这个包里面的命令，所以要安装setuptoos这个扩展才能使用。它和pip相似。`easy_install pyPdf`,安装好以后同样可以使用`pip list`来查看。如果这里先前就有了python2版本的话那么一样，python3 可以直接使用`pip3 install pyPdf`，这样就可以直接从python2的库里面copy一份过去了。

手动安装以 windows 安装 setuptoos为例子，在python官网下载了setuptoos的安装包以后，记住它的存放路径。启动cmd，把路径切换到setuptoos文件夹里面，输入`dir`可以看见`setup.py`，然后执行`python setup.py install`就可以了。每个第三方的安装包里面都有`setup.py`文件，安装的步骤相同。

####5、命名空间

什么是命名空间？命名空间(Namespace)表示标识符的可见范围。一个标识符可在多个命名空间定义，他在不同的空间中的含义是互不干扰的。

比如两个模块中的变量和函数，可能函数名一样，但是作用不一样。

在python中每个模块都会维护一个独立的命名空间，我们应该加上模块名，才能够正常的使用模块中的函数。

####6、搜索路径

有一个问题，写好的模块应该放在那里？

可以放在标准模块的文件夹里，但是为了区分不可能全部放进去，这样不便于管理。那我想通过自己创建的文件夹更好的组织我的代码。

但是在此之前我们必须要理解搜索路劲这个概念。

python模块的导入需要一个路径搜索的过程。就是说，你导入一个叫lib的模块，那么python会在定义好的搜索路径中寻找一个叫hello.py的模块文件--如果有，那么久导入，没有久导入失败。而这个搜索路径，就是一组目录。

我们可以通过sys.path显示出来(mac OS下的路径，每个系统都不一样)

```python
['/Users/ruidong/PycharmProjects/project', 
 '/Users/ruidong/PycharmProjects/project',
 '/Library/Frameworks/Python.framework/Versions/3.6/lib/python36.zip', 
 '/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6', 
 '/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/lib-dynload', 
 '/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages',
 '/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages/easygui-0.98.1-py3.6.egg']
```

列出这些路径都是python在导入模块操作时去搜索的，尽管这些模块都可以使用，但/python3.6/site-packages目录是最好的选择，因为它就是用来做这些事情。

我们按照刚才的逻辑来说只需要告诉python你的模块文件在哪里找，python在导入模块的时候就能正确找到它：

我在`/Library/Frameworks/Python.framework/Versions/3.6`下创建了`demo`文件夹，然后创建了`lib.py`。

```python
#lib.py

lib = 1000
```

我们在另一个.py文件中去引入它：

```python
import lib

#ModuleNotFoundError: No module named 'lib'
```
直接导入会出错，因为找不到包含模块路径的位置
那么我们把模块的位置添加到搜索路径中去

```python
import sys

pa = sys.path

nPath = '/Library/Frameworks/Python.framework/Versions/3.6/demo'

print(pa,type(pa))  #sys.path搜索路径是list类型的

pa.append(nPath)


# ...，'/Library/Frameworks/Python.framework/Versions/3.6/demo']
```

在打印的时候出现在结尾了。我们在试一试导入lib模块

```python
import sys

pa = sys.path

nPath = '/Library/Frameworks/Python.framework/Versions/3.6/demo'

print(pa,type(pa))  #sys.path搜索路径是list类型的

pa.append(nPath)

print(pa)

import lib

print(lib.lib)


#1000
```