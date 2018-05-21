#Lesson 7
___
##第十章
###【3】装饰器和生成器
####生成器
我们知道通过列表生成式，我们可以直接创建列表。但是了会受到内存的限制，列表容量肯定是受限制的。而且，创建一个包含100元个元素的列表，不仅占用内存空间，如果我们仅仅需要访问前面几个元素，那后面绝大多素元素占用的空间白白浪费了。

所以，如果列表元素可以按照某种算法推算出来的话，那我们是否可以在循环的过程中不断推算出后续的元素呢？这样就不必创建完整的list，从而节约大量的空间。在python中，这一种一边循环一边计算的的机制，称为生成器（generator）。


第一类：生成器函数：还是使用 def 定义函数，但是，使用yield而不是return语句返回结果。yield语句一次返回一个结果，在每个结果中间，挂起函数的状态，以便下次从它离开的地方继续执行。

如下案例加以说明：

```python
# 使用next()生成斐波那契数列
def Fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return '亲！没有数据了...'
# 调用方法，生成出10个数来
f=Fib(10)
# 使用一个循环捕获最后return 返回的值，保存在异常StopIteration的value中
list1 = []
while  True:
    try:
        x = next(f)
        list1.append(x)
    except StopIteration as e:
        print("生成器最后的返回值是：",e.value)
        break

print(list1)
```

第二类：生成器表达式：类似于列表推导，只不过是把一对大括号[]变换为一对小括号()。但是，生成器表达式是按需产生一个生成器结果对象，要想拿到每一个元素，就需要循环遍历。

如下案例加以说明：

```python
generator1 = [ i*i for i in range(10)]
generator2 = ( i*i for i in range(10))
print(generator1)
print(generator2)

for i in generator2:
	print(i)

#[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
#<generator object <genexpr> at 0x10452a0a0>
```


####装饰器
内衣可以遮羞，但是到了寒冷的季节它无法抵御严寒，于是聪明的人类发明了棉衣棉裤，给我们提供了保暖的功效，装饰器就像棉衣棉裤一样，在不影响内衣的作用下，还能给我们提供另一种功效.

概念：是一个闭包，把一个函数当做参数,返回一个替代版的函数，本质上就是一个返回函数的函数

简单的装饰器

```python
#简单的装饰器
def func1():
    print("上海好啊！！！")

def outer(func):
    def inner():
        print("*******************")
        func()
    return inner
#f是函数func1的加强版本
f = outer(func1)()
```

复杂一点的装饰器

```python

def outer(func):
    def inner(age):
        if age < 0:
            age = 0
        func(age)
    return inner

#使用@符号将装饰器应用到函数
#@python2.4支持使用@符号
@outer   #相当于say = outer(say)
def say(age):
    print("he is %d years old" % (age))


say(-10)
```

通用一点的装饰器

```python

def outer(func):
    def inner(*args, **kwargs):
        #添加修改的功能
        print("&&&&&&&&&&&&&")
        return func(*args, **kwargs)
    return inner



@outer #say = outer(say)
def say(name, age): #函数的参数力理论上是无限制的，但实际上最好不要超过6、7个
    print("my name is %s, I am %d years old" % (name, age))
    return "aaaa"


say("tom", 18)
```
###偏函数
functools，用于高阶函数：指那些作用于函数或者返回其它函数的函数，通常只要是可以被当做函数调用的对象就是这个模块的目标。

在Python 2.7 中具备如下方法，

```python
cmp_to_key，将一个比较函数转换关键字函数；

partial，针对函数起作用，并且是部分的；

reduce，与python内置的reduce函数功能一样；

total_ordering，在类装饰器中按照缺失顺序，填充方法；

update_wrapper，更新一个包裹（wrapper）函数，使其看起来更像被包裹（wrapped）的函数；

wraps，可用作一个装饰器，简化调用update_wrapper的过程；
```

偏函数的实现：

```python
import functools

print(int("1010", base = 2)) #设置成2进制

def int2(str, base = 2):
    return int(str, base)
print(int2("1011"))


#partial把一个参数固定住，形成一个新的函数
int3 = functools.partial(int, base = 2)
print(int3("111"))

#那么现在int3默认就是返回2进制的
```

##第十一章
___
###【1】你不可能总是对的

我们是人，不是神，所以我们经常会犯错，就算你是个经验丰富的程序员，也不能保证你写的代码百分之百的没有问题。

另外作为一个合格的程序员，再编程的时候你要记住一点，就是永远都不要相信你的用户。要把他们想象成熊孩子，把他们想象成黑客，这样你才能写出安全稳定的程序。

我们看例子：

```python
var = float(input('请输入一个数字:'))
print(var)

#请输入一个数字:q
#ValueError: could not convert string to float: 'q'
```
上面这个例子就报错了ValueError异常，那么python会抛出那些异常了

<image src='images/错误代码1.png' width='500' >
<image src='images/错误代码2.png' width='500' >
<image src='images/错误代码3.png' width='500' >

####1、AssertionError:断言语句(assert)失败

assert 关键字 在前面的章节里面讲过了，在测试程序的时候使用

它在条件不成立的情况下抛出 AssertionError

```python
var = float(input('请输入一个数字'))
assert var<0
print(var)

#请输入一个数字100
#AssertionError
```
####2、AttributeError:尝试访问位置的对象属性

当试图访问的对象属性不存在时抛出异常：

```python
list1 = []
list1.shanghai

#AttributeError: 'list' object has no attribute 'china'
```

####3、IndexError:索引超出范围

```python
list1 = [1,2,3]
list1[3]

#IndexError: list index out of range
```
####4、KeyError:字典中没有这个键

```python
list1 = {1:2,3:4}
list1[6]

#KeyError: 6
```

####5、TypeError:不同类型间的无效操作

```python

1 + '1'

#TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

####ZeroDivsionError:除数为零

```python

5 / 0

ZeroDivisionError: division by zero
```
###【2】try-except语句

格式如下：

```python
try:
	检测范围
except Exception [as reason]:
	出现异常的代码
	
```

举个例子：

```python



try:
    var = int(input('请输入一个数字：'))
    print(var)
except ValueError:
    print('输入错误')
    
#请输入一个数字：q
#输入错误   
    
    
#当然也可以这样写，错误信息会更加准确    
#except ValueError as reason:
#    print('输入错误,错误原因:'+ str(reason))

```

####针对不同的异常设置多个except

```python

try:
    var = int(input('请输入一个数字：'))
    rel = var + '1'
    print(rel)
except ValueError as reason:
    print('输入错误,错误原因:'+ str(reason))
except TypeError as reason:
    print('输入错误,错误原因:' + str(reason))
    
    
#请输入一个数字：1
#输入错误,错误原因:unsupported operand type(s) for +: 'int' and 'str'    
```
####捕获所有异常

```python

try:
    var = int(input('请输入一个数字：'))
    rel = var + '1'
    print(rel)
except:
    print('报错了')
    
#请输入一个数字：q
#报错了

```

###【3】try-finally语句

这里我们使用打开文件作为例子，因为文件打开了不管报不报错都需要关闭。

文件操作在后续内容会讲到

```python
try:
    f = open('我是一个不存在的文件.txt') #打开文件
    print(f.read())
except:
    print('出错了')  #在没有finally的时候报错了就会被终止
finally:
    #f.close()   #关闭文件,这里给大家看的，注释去掉会报错
    print('关闭文件成功')  
```
在try没有报错的情况下，会跳到finally里面执行代码。

try报错了，会执行except，在执行finally。

finally就是确保无论如何都要被执行的。

###【4】raise语句

它的作用是随时随地抛出一个异常，可以带参数。

```python
raise ZeroDivisionError

#raise TypeError('类型错误')

```

###【5】丰富的else语句

这里的else说的不是if-else那个玩意。

不过if-else也可以抛出异常,我们已经玩过了，比如说是不是大于某个数。

例子：

```python
try:
    int('abc')
except ValueError as reason:
    print('出错了，错误原因是：' + str(reason))
else:
    print('没有问题')

#出错了，错误原因是：invalid literal for int() with base 10: 'abc'
```
上面的这个例子else中代码没有执行，因为else是在try中没有问题的情况下执行的。

###【6】简洁的with语句
我们上面讲过了finally，在文件读取的时候可以用它来关闭文件，想想又要打开又要关闭，太烦人，那么我们的`with`就可以上场了，在你忘记关闭文件的时候它会自动帮你关上。

```python

try:
    with open('我是一个不存在的文件.txt') as f:
        print(f.read())
except OSError as reason:
    print('挂啦！原因是:' + str(reason))
    
```

这样写是不是方便多了，也不怕忘记关闭文件。


##第十二章
___
###【1】文件恒久远，一个永流传
大多数的程序都是遵循，输入->处理->输出的模型，首先接受输入数据，然后按照要求进行处理，最后输出结果。可能以后你的需求就不止这些了，你可能需要你的程序可以去自动的分析系统的日志，然后分析结果在保存作为一个新的日志，这时候就需要用到文件了。

或者说你在IDLE中写程序，突然一个不对劲，电脑蓝屏了，在开机，你的代码都没了，但是在pycharm中为什么就不会了，因为必须要新建一个文件，然后你写的时候自动存储在文件里，文件是写在硬盘上的。

在你编写代码的时候，操作系统为了更快的做出响应，会把当前的数据全部保存在内存中，因为内存和CPU之间的数据传输是最快的，比硬盘和CPU快多了。但是内存的不足就是一断电就玩完了。

文件的格式我们也见过很多，windows 的.exe .txt还有我们python 的.py等等，这些都是文件。


####字符串类型和字节类型

字符串类型向字节类型转化称之为编码  encode

字节类型向字符串类型转化称之为解码  decode

<font color='red'>注意编解码格式一定要保持一致，如果是程序会报错，如果是编辑器查看，直接乱码</font>

常用的字符集都是什么意思

```python
ascii  
	这玩意就是美国搞的一套标准，用的是一个字节，用了其中的0-127表示了所有的老外用的东西
ansi 
	这玩意用两个字节，叫做扩展的ascii码，128-0xffff
gbk  
	扩展的国标，在gb2312的基础上又多了好多的繁体字xxx，兼容gb2312 
gb2312 
	这玩意是中国搞了一套自己编解码（韩国搞了一套自己的、日本也搞了一套自己的）
	对应的中国的ansi 
utf-8   
	互联网兴起了，迫切需要统一的编码，utf-8就在unicode的基础上规定了存储和读取的方式，他存储的时候是变化的，如果存储英文字母，其使用的是1个字节，如果用来存储汉字，占用3个字节
unicode
	是一套国际标准，称之为万国码，也是两个字节
	并没有真正的执行起来，而且也没有规定怎么存储和读取

```
<font color='red'>注意：以后你要用的话，应该都是utf-8无bom的格式，如果碰到了gbk，你要自己会转化相应的格式</font>

###【2】打开文件

在python中，使用open()这个函数来打开文件返回文件对象：

open(file,mode = 'r',buffering = -1,encoding = None,errors = None,newline = None,closefd = True,opener = None)

open()这个函数有很多参数，但作为初学者来说，只需要知道第一个和第二个参数就可以了。

```python
file：              要打开的文件名，需加路径(除非是在当前目录)。唯一强制参数
mode：              文件打开的模式
buffering：         设置buffer（取值为0,1,>1）
encoding：          返回数据的编码（一般为UTF8或GBK）
errors：            报错级别（一般为strict，ignore）
newline：           用于区分换行符(只对文本模式有效，可以取的值有None,'\n','\r','','\r\n')
closefd：           传入的file参数类型（缺省为True）
```

mode对照表：

| 打开模式 | 执行操作                                     |
| ---- | ---------------------------------------- |
| r    | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。         |
| rb   | 以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。   |
| r+   | 打开一个文件用于读写。文件指针将会放在文件的开头。                |
| rb+  | 以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。          |
| w    | 打开一个文件只用于写入。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。 |
| wb   | 以二进制格式打开一个文件只用于写入。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。 |
| w+   | 打开一个文件用于读写。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。 |
| wb+  | 以二进制格式打开一个文件用于读写。如果该文件已存在则将其覆盖。如果该文件不存在，创建新文件。 |
| a    | 打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
| ab   | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
| a+   | 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。 |
| ab+  | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。 |


例子：

```python
path = r"C:\Users\xlg\Desktop\Python-1704\day07\5-文件读写\file1.txt"
#ignore  忽略错误
#f = open(path, "r", encoding="utf-8", errors="ignore")
f = open(path, "r", encoding="utf-8")

```

###【3】文件对象的方法

打开文件并获取文件对象以后，就可以利用文件对象的一些方法对文件进行读取或修改等操作。

| 文件对象方法            | 执行操作                                     |
| ----------------- | ---------------------------------------- |
| close()           | 关闭文件                                     |
| read(size =-1)    | 从文件读取size个字符，当未给定或者给定负值的时候，读取剩余的所有的字符，然后作为字符返回 |
| reading()         | 从文件中读取一整行字符                              |
| write()           | 将字符串str写入文件                              |
| writelines(seq)   | 向文件写入字符串序列seq，seq应该是一个返回字符串的可迭代对象        |
| seek(offset,from) | 在文件中移入文件指针，从from(0代表文件起始位置，1代表当前位置，2代表文件末尾)偏移offset个字节 |
| tell()            | 返回当前在文件中的位置                              |

###【4】文件的关闭

close()方法用于关闭文件。如果是C语言的话，我在这里一定会强调一万次关闭的，如果你不关闭的话，别人想要读写就会无法完成 。不关闭文件会导致（other）无法再次已写的方式打开，以前是连只读的方式都不行。而python拥有垃圾回收机制，会在文件对象的引用此计数降至零的时候自动关闭文件。

但是并不代表可以不关闭文件，如果你对文件进行写入操作的话，那么应该在完成写入之后关闭文件。因为python可能会缓存你写入的数据，如果中途发生类似断电之类的事故，那些缓存的数据根本就不会写入到文件中。所以，为了安全起见，要养成使用完文件后立即关闭的好习惯。




###【5】文件的读取和定位

文件的读取方法很多，可以使用文件对象read()和readline()方法，也可以直接list(f)或者直接使用迭代来读取。

read()方法是按字节来的去，如果不设置字节数，那么会全部读取。tell()方法会告诉你当前文件的指针位置。


```python

f = open(r'/Users/ruidong/PycharmProjects/project/demo.txt')
print(f.read())
print(f.tell())
f.close()
```
刚刚提到文件指针是个什么玩意？你可以认为它是一个书签，起到定位的作用。使用seek()方法可以调整文件指针的位置。seek（offset，from）方法有两个参数。

也就是文件读取了多少以后，会生成指针，只能向后读，不能再读取已度去过的，除非使用seek()重新调整指针。

```python

from  表示从(0代表当前文件起始位置，1代表当前位置，2代表文件末尾)偏移 offset字节。
```
因此，将文件指针设置到文件起始位置，使用seek(0,0)即可：

```python

f = open(r'/Users/ruidong/PycharmProjects/project/demo.txt')
print(f.read())
print(f.tell())
f.seek(0,0)
print('\n********************\n')
print(f.read())
f.close()
```

readline()方法用于在文件中读取一整行，就是从文件指针的位置向后读取，直到遇到换行符(\n)结束。

```python
f = open(r'/Users/ruidong/PycharmProjects/project/demo.txt')
print(f.readline())
print(f.readline())
f.close()
```

此前介绍过列表强大，说什么都可以往里面放，这不，也可以把整个文件的内容放到列表中：

```python

f = open(r'/Users/ruidong/PycharmProjects/project/demo.txt')
lines = list(f)
for each_line in lines:
    print(each_line)
f.close()
```

这样写是没有问题的，但是了感觉像是非要用酒精烧开水，水能烧的开，但是效率不高。文件本来就是可以迭代的。

```python

f = open(r'/Users/ruidong/PycharmProjects/project/demo.txt')
for each_line in f:
    print(each_line)
f.close()
```
###【6】文件的写入

如果需要写入文件，请确保之前的打开模式有‘w’或者‘a’或者多带上‘+’，否者在写入的时候回出错：

open 没有 ‘w’那些可写入的操作符或报错：

```python
import os
os.system('touch wdemo.txt')  #在当前文件夹下新建一个wdemo.txt文件
f = open(r'/Users/ruidong/PycharmProjects/project/wdemo.txt')
f.write('这是一个神奇的地方')
f.close()

#io.UnsupportedOperation: not writable

```
使用‘r+’读写模式，但是要注意‘r+’或者是‘w’会把原来的文件内容给删除。

```python
f = open(r'/Users/ruidong/PycharmProjects/project/wdemo.txt','r+')
f.write('这是一个神奇的地方')
f.close()

```

如果是追加的话，要不然会造成血淋淋的教训，那就要使用‘a’操作符打开：

```python

f = open(r'/Users/ruidong/PycharmProjects/project/wdemo.txt','a+')
f.write('\n这是一个美丽的地方')
f.close()

```

将序列单行写入

writelines() 方法用于向文件中写入一序列的字符串。
这一序列字符串可以是由迭代对象产生的，如一个字符串列表。
换行需要制定换行符 \n。

```python
f = open("wdemo.txt", "w")

seq = ['千锋教育\n','python']
f.writelines(seq)

```
####刷新缓冲区域

文件在写入的时候斌没有直接写入，而是在内存中，只有我们执行f.close()关闭文件以后，它才会写入。

如果想不关闭文件直接写入，那么使用f.flush(),它的作用是立即将内存上的数据写入硬盘。

```python
f = open('wdemo.txt','w')
f.write('niahoa')
f.flush()

```

###【7】一个文件案例

下面我们做个案例对record.txt文件进行分割，规则如下：

（1）将千锋吴彦祖的对话单独保存为boy_*.txt的文件(去掉‘千锋吴彦祖’)

（2）将千锋客服的对话单独保存为girl_*.txt的文件(去掉‘千锋吴彦祖’)

（3）文件中总共有三段对话，分别保存为boy_1（2、3）.txt、girl_1（2、3）.txt

```python
#record.txt

千锋客服:吴彦祖，今天有客户问你有没有女朋友？
千锋吴彦祖:咦？？
千锋客服:我跟她说你有女朋友了！
千锋吴彦祖:。。。。。。
千锋客服:她让你分手后考虑下她！然后我说:"您要买个优盘，我就帮您留意下~"
千锋吴彦祖:然后呢？
千锋客服:她买了两个，说发一个货就好~
千锋吴彦祖:呃。。。。。。你真牛！
千锋客服:那是，谁让我是千锋最可爱的客服嘛~
千锋吴彦祖:下次有人想调戏你我不阻止~
千锋客服:滚！！！
================================================================================
千锋客服:千锋吴彦祖，有个好评很好笑哈。
千锋吴彦祖:哦？
千锋客服:"有了吴彦祖，以后妈妈再也不用担心我的学习了~"
千锋吴彦祖:哈哈哈，我看到丫，我还发微博了呢~
千锋客服:嗯嗯，我看了你的微博丫~
千锋吴彦祖:哟西~
千锋客服:那个有条回复“左手拿著彦祖，右手拿著打火機，哪裡不會點哪裡，so easy ^_^”
千锋吴彦祖:T_T
================================================================================
千锋客服:千锋吴彦祖，今天一个会员想找你
千锋吴彦祖:哦？什么事？
千锋客服:他说你一个学生月薪已经超过12k了！！
千锋吴彦祖:哪里的？
千锋客服:上海的
千锋吴彦祖:那正常，哪家公司？
千锋客服:他没说呀。
千锋吴彦祖:哦
千锋客服:老大，为什么我工资那么低啊？？是时候涨涨工资了！！
千锋吴彦祖:啊，你说什么？我在外边呢，这里好吵吖。。。。。。
千锋客服:滚！！！
```

代码如下：

```python

#思路：
#我们首先知道我们要把三段对话分别分成boy_1、2、3和girl_1、2、3，一共是6个文件
#我没知道每段对话都是以'==='组成的
#我们列表的的写入需要用到writeline()
#我们的文件用完以后需要关闭

def save_file(boy,girl,count):
    file_name_boy = 'boy' + str(count) + '.txt'
    file_name_girl = 'girl' + str(count) + '.txt'
    boy_file = open(file_name_boy,'w')
    girl_file = open(file_name_girl,'w')
    boy_file.writelines(boy)
    girl_file.writelines(girl)
    boy_file.close()
    girl_file.close()

def split_file():
    boy = []
    girl = []
    count = 1
    f = open(r'/Users/ruidong/PycharmProjects/project/record.txt')
    for eachLine in f:
        if not eachLine.startswith('='):
            (role,line_spoken) = eachLine.split(':',1)
            if role == "千锋吴彦祖":
                boy.append(line_spoken)

            if role == "千锋客服":
                girl.append(line_spoken)
        else:
            save_file(boy,girl,count)
            boy = []
            girl = []
            count += 1
    save_file(boy, girl, count)
    f.close()

split_file()

```


