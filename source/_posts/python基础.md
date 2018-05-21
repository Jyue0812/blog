#Lesson 1
___
##简述
___
###【1】python是什么类型的语言
python是脚本语言

```python
脚本语言是计算机编程语言，因此也能让开发者编写出让电脑听命行事的程序。以简单的方式完成默写复杂的事情通常是创造脚本语言的重要原则，基于这项原则，使得脚本语言通常比C语言、C++语言活着java之类的系统编程语言要简单容易。
```
python是强类型语言

```python
什么是强类型，比如c或者java这些语言在声明变量之前是需要定义变量是int还是str类型的。
php是弱类型的语言，它不会区分变量的类型，你给它什么它就是什么。
那很多人就会奇怪了，python在声明变量的时候也没有给类型啊，python的变量是引用内存地址的，如果给一个其它类型的变量，它会把指针直线另一个地方。
```
###【2】.pyc文件
python的文件都是以.py结尾的，那么.pyc的文件是什么了，
```python
pyc是一种二进制文件，是由py文件经过编译后，生成的文件，是一种byte code，py文件变成pyc文件后，加载的速度有所提高，而且pyc是一种跨平台的字节码，是由python的虚拟机来执行的，这个是类似于JAVA或者.NET的虚拟机的概念。pyc的内容，是跟python的版本相关的，不同版本编译后的pyc文件是不同的，2.5编译的pyc文件，2.4版本的 python是无法执行的。
```
为什么需要pyc文件了
```python
这个需求太明显了，因为py文件是可以直接看到源码的，如果你是开发商业软件的话，不可能把源码也泄漏出去吧？所以就需要编译为pyc后，再发布出去。当然，pyc文件也是可以反编译的，不同版本编译后的pyc文件是不同的，根据python源码中提供的opcode，可以根据pyc文件反编译出 py文件源码，网上可以找到一个反编译python2.3版本的pyc文件的工具，不过该工具从python2.4开始就要收费了，如果需要反编译出新版本的pyc文件的话，就需要自己动手了（俺暂时还没这能力^--^）,不过你可以自己修改python的源代码中的opcode文件，重新编译 python，从而防止不法分子的破解。
```
怎么生成pyc文件了
```python
我们吧编写好的python文件的记录下来
在cmd中运行：

python -m 你的文件名.py

或者在IDLE中运行：
import py_compile
py_compile.compile(r'H:\game\test.py')

如果是批量生产pyc文件可以直接指定一个目录
```
查看pyc文件
```
找到pyc文件的目录
当你生成pyc文件成功以后默认有一个名为‘__pycache__’的文件夹
进入文件夹输入

hexdump -C test.cpython-36.pyc 

```
___
##第一章
___
###【1】从IDLE启动python
```
首先我们打开cmd 输入python

import sys
print(sys.path) #打印出python的安装路径
```
我们在python的安抓过包里面可以看见`idle.exe`把它发送到桌面的快捷方式上去，它可以直接打开python自带的编译工具，而不需要从cmd进入

`IDLE是什么：

```
IDLE是python shell，shell的意识就是‘外壳’，就是通过输入文本与程序交互的途径。就像是我们windows的cmd窗口，linux那个黑乎乎的命令窗口那样的东西，利用它们就可以给系统下达命令。

同样的利用IDLE就可以给python下达命令
```

###【2】尝试第一次失败

我们安装的是python3

那么默认的就是的输出打印就是：
print(‘I love 1000phone’)

```python
>>> print("I love 1000phone")
I love 1000phone
```

如果我们输入python2的语法
print "I love 1000phone"

```python
>>> print "I love 1000phone"
SyntaxError: Missing parentheses in call to 'print'
```
这样的话就会报语法错误

如果我们输入c语言的语法
printf(‘I love 1000phone’)；

```
>>> printf(‘I love 1000phone’)；
SyntaxError: invalid character in identifier
```
这样的话就会报 名字错误 ，没有定义过

所以了python3是个很专一的语言
如果在代码前面加上了井号（#），那么后面的文字就不会被输出，井号是python中的注释，后面的内容不会被当着是代码运行。

###【3】玩点新花样
我们输入`print(5+3)`
那么python会直接计算出结果，没发现它还会加法！这不奇怪，计算机嘴开始的时候就是用来做计算的，而且任何语言都有计算的能力，我们看看python在计算方面有何神奇的。
```
输入print(1234567890987654321 * 9876543210123456789)
python可以直接得出结果

```python

>>> print(1234567890987654321 * 9876543210123456789)
12193263121170553265523548251112635269

```
如果是c语言的话需要大费周章地利用数组做大运算，而python轻而易举地就可以完成了！
```
我们在输入一下`print('罗密欧' + '朱丽叶')`

```
print('罗密欧' + '朱丽叶')
罗密欧朱丽叶
```
可以看到他们两个人在一起了，非常幸福！

###【4】奇怪的语法

我们输入

```python
>>> print('I love 1001phone\n' * 3)#在这里`\n`代表的是换行的意思
I love 1001phone
I love 1001phone
I love 1001phone
```

我们发现乘法可以使结果重复，我们在试一试加法

```python
>>> print("I love 1000phone\n" + 3)
Traceback (most recent call last):
  File "<pyshell#2>", line 1, in <module>
    print("I love 1000phone\n" + 3)
TypeError: must be str, not int
```
失败了！因为在python里 加号 的作用是用来作数学运算和字符串链接的

___
##第二章
___
###【1】第一个小游戏
目前对于我们所掌握的基础貌似只有`print()`这个BIF,哦，BIF的概念甚至还没讲解...不过不影响我们今天上课的节奏！
先看看下面的代码，并试图猜测一下每条语句的作用：

```python
"""---第一个小游戏---"""
temp = input("猜一猜我心里想的是那一个数字：")
guess = int(temp)
num = 8
if guess == num:
    print("你是我肚子里的蛔虫嘛？")
    print("不过你猜中了也没有奖励！")
else:
    print("猜错了，我想的是$d"%num)
print('game over  (^_^!) ')

```
这里需要大家动动手亲手输入这些代码，你们需要做的事打开`pycharm`然后新建一个python文件按照我上面的格式输入一遍代码，记的`Ctrl+S`,然后右键-->‘Run’

```python
猜一猜我心里想的是那一个数字：8
你是我肚子里的蛔虫嘛？
不过你猜中了也没有奖励！
game over  (^_^!) 
```

```提示
Tab按键的作用
（1）缩进。
（2）IDLE会提供联想，比如你输入 pr 按Tab键 会提供可能使用的命令供你选择参考。
```
我们看到程序成功的运行起来了，坦白的说，这玩意配叫游戏吗？以后我们在去慢慢的改进，我们说下语法

```
一切语法类似于c语言的编程语言都叫c-like语言
有c-like编程基础的人都会受不了python的IDLE的执行过程，没有声明变量类型，怎么就直接给变量定义了？没有基础的可能还不知道什么是变量
，变量我们后面会学到的，后面我们还会发现python根本就没有大括号来界定作用域，好多语言都是用大括号来表示作用域的，在python中只需要用适当的缩进(Tab)来表示。
```
###【2】缩进
缩进是python的灵魂，缩进的严格要求，使得python的代码显得非常的精简并且要层次感。

但是，在python中对待代码的缩进要万分的小心，因为你如果没有正确的使用缩进，代码所做的事情可能和你预期相差甚远（好比时其它语言的大括号打错了位子）

```
n = True
if  n == True:
    print('结果是true打印是这里')
else:
    print('这里我特意少打了一个Tab，结果就发生了变化 ')
print('结果是false打印是这里')
```

###【3】BIF
接下来我们学习一个新的名词：BIF。
BIF就是	`built-in Functions`，内置函数的意思。什么是内置函数？为了程序员快速的编写程序而把代码打包起来的形成的方法体。（说了你也不懂）

例如`print()`就是一个内置函数，它就是一个BIF，还有刚才的小游戏中的`input()`也是一个BIF

```python
在IDLE中输入dir(__builttins__)可以看到python中的内置函数列表。
```
```python
#help()这个BIF用于现实BIF的功能描述：


>>> help(print)
Help on built-in function print in module builtins:

print(...)
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    
    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.

>>> 
>>> 
```
###【4】我们今天学习的两个BIF
```python
input() #让用户输入的函数括号里面可以填写提示符
print() #打印和输出括号里的值
```

###【5】编码规范
pep8 官网规范地址
`https://www.python.org/dev/peps/pep-0008/`
变量和函数命名：下划线分割，小驼峰
切片里面的冒号：冒号两边都不加空格
字典里面的冒号：冒号前面不加空格，后面加空格
lambda中的冒号：冒号前面不加空格，后面加空格
定义变量=号两边加空格
函数中形参=号两边不加空格
关键字参数调用函数不加空格

优先级高的运算符不建议有空格:

```python
i = i + 1
submitted += 1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)
模块名：使用下划线分割
```
包名：直接全部小写，不推荐使用下划线


##思考题：(不懂的去百度)
###IDLE是什么？
###print()的作用是什么？
###python中表示乘法的符号是什么？
###什么是pyc文件？
###数一数python3提供了多少的内置函数
###今天的课程中出现了‘=’和‘==’，他们有不同的区别，那么区别在哪里？
###你听过‘拼接’这个词吗？

##动手题：
###编写程序hello.py,要求用户自己输入姓名，并打印‘你好，姓名’。
###在IDLE中计算答应一年有多少秒？
###在IDLE中输入‘hello word’与print(‘hello word’)有什么不同？
