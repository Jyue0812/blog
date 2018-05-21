#Lesson_06
___
##第九章
###【4】集合（set）

在我的世界里你就是唯一，集合是个专一的类型

那么什么是集合了，集合就是没有key的dict，我们看个例子：

```python

dict1 = {1,2,3,4,5,4,3,2,1}

print(dict1,type(dict1))

#{1, 2, 3, 4, 5} <class 'set'>
```
上面提到了，set是很专一的，它会把重复的类型给去除掉。

那么set不像dict那样是映射关系，那么我们怎么去找它的索引了。

```python
dict1 = {1,2,3,4,5,4,3,2,1}

print(dict1[1])

#TypeError: 'set' object does not support indexing
```

上面的例子中出现了错误，为什么了，因为set是无序的,也就是它的索引会变动，所以要取出set中的值要把它转成其它类型,才能访问索引。


####创建set

```python
set1 = {'nihao',2,3,'hello'}

set2 = set()

set3 = set([1,2,3,4,5])

print(set1,type(set1))
print(set2,type(set2))
print(set3,type(set3))

#{'nihao', 2, 3, 'hello'} <class 'set'>
#set() <class 'set'>
#{1, 2, 3, 4, 5} <class 'set'>
```

课堂小练习：

去除list中的重复值

```python

list1 = [1,2,3,4,5,4,3,2,1]

print(list(set(list1)))

#[1, 2, 3, 4, 5]
```

####访问集合

由于集合是无序的，所以了不能用下标的方法进行访问，我们可以用迭代的方法：

```python

set1 = [1,2,3,4,5,6,7]

for v in set1:
    print(v,end=' ')
    
#1 2 3 4 5 6 7    
```
当然也可以使用 in  和 not in 判断值在不在set中：

```python

set1 = [1,2,3,4,5,6,7]

print(2 not in set1)
print(1 in set1)


#False
#True
```

也可以使用add()和remove()去添加和删除元素

```python
set1 = {1,2,3,4,5,6,7}

set1.add(8)
set1.remove(1)

print(set1)

{2, 3, 4, 5, 6, 7, 8}
```

###【5】不可变集合

有的时候我们也希望集合更具有稳定性，也就是像元祖那样不能随意的增加或删除集合中的元素。那么我们定义不可变的集合，这里使用的是frozenset（）函数，没错，就是把元素frozen(冰冻)。

```python
set1 = frozenset({1,2,3,4,5,6,7})

set1.add(8)

print(set1)

#AttributeError: 'frozenset' object has no attribute 'add'
```

```python

s8 = set([1,2,3])
s9 = set([2,3,4])
#交集
a1 = s8 & s9
print(a1)
print(type(a1))
#并集
a2 = s8 | s9
print(a2)
print(type(a2))
#差集
a3 = s9 ^ s8
print(a3)
print(type(type(a3)))

#{2, 3}
#<class 'set'>
#{1, 2, 3, 4}
#<class 'set'>
#{1, 4}
#<class 'type'>
```

###【5】再回首，类型转换

以前我们学习了int、float、str、bool等类型的转换，
现在我们学习set、dict、tuple、list的类型转换。

```python

#list-->set
l1 = [1,2,3,4,5,3,4,5]
s1 = set(l1)
print(s1)

#tuple-->set
t2 = (1,2,3,4,3,2)
s2 = set(t2)
print(s2)

#set-->list
s3 = {1,2,3,4}
l3 = list(s3)
print(l3)

#set-->tuple
s4 = {2,3,4,5}
t4 = tuple(s4)
print(t4)

```

#####来一个有趣的练习：

使用zip(key,value)函数

使用zip函数的是把两个list或者tuple合拼成一个（（key,value），key,value））格式

```python

val = (1,2,3,4,5)
key = ['one','two','three','foul','five']
dict1 = dict(zip(key,val))
print(dict1)


#{'one': 1, 'two': 2, 'three': 3, 'foul': 4, 'five': 5}

```

二维矩阵变换（矩阵的行列互换）

比如我们有一个由列表描述的二维矩阵

zip([seql, ...])接受一系列可迭代对象作为参数，将对象中对应的元素打包成一个个tuple（元组），然后返回由这些tuples组成的list（列表）。若传入参数的长度不等，则返回list的长度和参数中长度最短的对象相同。

```python

a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(list(zip(*a)))

#[(1, 4, 7), (2, 5, 8), (3, 6, 9)]
```

#####另一种生成方式,生成器生成列表

```python

print(list(x for x in range(10)))
print(tuple(x for x in range(10)))
print(set(x for x in range(10)))

#[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
#(0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
#{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
```

###【6】迭代器


####可迭代对象

可迭代对象：可以直接作用于for循环的对象统称为可迭代对象(Iterable)。可以用isinstance()去判断一个对象是否是Iterable对象

可以直接作用于for的数据类型一般分两种

```python
1、集合数据类型，如list、tuple、dict、set、string
2、是generator，包括生成器和带yield的generator function
```
```python
from  collections import Iterable

#首先引入collections文件Iterable的类
```

```python
from  collections import Iterable

print(isinstance([], Iterable))
print(isinstance((), Iterable))
print(isinstance({}, Iterable))
print(isinstance("", Iterable))
print(isinstance((x for x in range(10)), Iterable))
print(isinstance(1, Iterable))

#True
#True
#True
#True
#True
#False
```

####迭代器

迭代器：不但可以作用于for循环，还可以被next()函数不断调用并返回下一个值，直到最后跑出一个StopIteration错误表示无法继续返回下一个值

可以被next()函数调用并不断返回下一个值的对象称为迭代器(Iterator对象)

可以使用isinstance()函数判断一个对象是否是Iterator对象

```python

from  collections import Iterator

```

```python
from  collections import Iterator

print(isinstance([], Iterator))
print(isinstance((), Iterator))
print(isinstance({}, Iterator))
print(isinstance("", Iterator))
print(isinstance((x for x in range(10)), Iterator))


#False
#False
#False
#False
#True
```

####可迭代对象指针下移

```python

l = (x for x in [23,4,5,64,3435])
print(next(l))
print(next(l))
print(next(l))
print(next(l))
print(next(l))
# print(next(l))

#23
#4
#5
#64
#3435
##如果后面已经没有值了，指针继续下移会报错
```

####转成Iterator对象

```python
from  collections import Iterator

a = iter([1,2,3,4,5])
print(next(a))
print(next(a))

print(isinstance(iter([]), Iterator))
print(isinstance(iter(()), Iterator))
print(isinstance(iter({}), Iterator))
print(isinstance(iter(''), Iterator))

#1
#2
#True
#True
#True
#True
```

##第十章
###【1】函数

```python
认识函数：在一个完整的项目中，某些功能会反复的使用。那么会将功能封装成函数，当我们要使用功能的时候直接调用函数即可

本质：函数就是对功能的封装

优点
1、简化代码结构，增加了代码的复用度(重复使用的程度)
2、如果想修改某些功能或者调试某个BUG，还需要修改对应的函数即可
```

#### 一、python的‘’积木“

```python
函数就像是积木一样通过创意和想想可以自由的组合，从而使我们的代码，变的更加的简单易懂,节约开发时间，不需要去理解底层的运行，把复杂的事情变的简单有乐趣。
```
```python
在学习这一章节之前了，其实我们就已经接触过BIF了，例如print()、range()这些都是python自己封装的函数提供给我们使用的
```

##### 1、创建和调用函数
​	函数的定义:	

```python
'''
关键字 def 函数名():
			函数体
			return 返回表达式
调用  函数名()
		
'''
#函数名可以以使用大小写字母、下划线开头，不能以数字开头
def mydef():#关键字def 函数名()：
    print('这是我的第一个函数')
    print('我表示非常的激动...')
    print('在这里感谢我的父母，感谢千锋，你们成就了我')
mydef()
#注意：在函数名后面一定要加上小括号，小括号的作用是用来保存参数的
#函数的运行机制：mydef()发生调用操作时，python会自动往上去寻找 def mydef（）：定义的过程，然后依次执行该代码块内所包含的所用代码部分。
```

调用代码三次：

```python
def mydef():
    print('这是我的第一个函数')
    print('我表示非常的激动...')
    print('在这里感谢我的父母，感谢千锋，你们成就了我')
for i in range(3):     #使用循环反复的调用
	mydef()
'''
result:
这是我的第一个函数
我表示非常的激动...
在这里感谢我的父母，感谢千锋，你们成就了我
这是我的第一个函数
我表示非常的激动...
在这里感谢我的父母，感谢千锋，你们成就了我
这是我的第一个函数
我表示非常的激动...
在这里感谢我的父母，感谢千锋，你们成就了我
'''
```

##### 2、函数的参数

```函数的参数就是放在括号里的东西，参数可以实现鸟枪换大炮的功能，总之就是是函数可以个性化```

```python
def mydef(name):      #从某种意义上来说括号中的参数就是个变量
    print(name + '是帅锅')

mydef('刘德华')
mydef('郭富城')
mydef('张学友')
mydef(
```

##### 3、函数的返回值

```有些时候，我们需要函数给我返回一些数据来报告执行的结果，而不是想上面的代码块那样直接去输出打印结果。其实非常的简单，只需要在函数中使关键字return，后面跟上的就是制定要返回的值。```

```python
def add(num1,num2):
    return num1 + num2
print(add(1,2)) 
#注意：当函数内部使用的是return的时候，调用的时候没有print()的话，是不会打印输出的
#如果函数没有了参数，那么函数就变的非常的单一，一个函数就只能完成一个功能
```

#### 二、灵活强大的用法

```有时候我们评价一种编程语言是否优秀，往往我们看的是它够不够灵活。灵活并非意味它无所不能。犹如我们上述的参数一样，函数没有了参数就会变的非常的死板，只能完成单一的功能```

##### 1、形参和实参

```参数从调用的角度来说，分为形式参数和实际参数。python和绝大数语言一样，形参指的是函数创建和定义过程中的小括号里面的参数（可以理解卫一个新的变量）而实参指的是函数在调用的时候传递进来的参数或值```

```python
def mydef(name): #小括号里面的name就是形参
    return name
myname = '成龙'
print(mydef(myname)) #调用时候的myname就是实参
#在这个代码段中把 myname 中的值（成龙）赋值给了 name
#相当于 name = myname
#可以理解为结婚以后夫妻的财产是共有的，没有为什么，法律规定的，这里也一样，语法规定的
#不论是形参还是实参都只是一个概念和名词，只需要去记住他，不需要去纠结为什么
```

##### 2、函数的文档

```给函数写文档是为了让别人更好的去理解你的函数的，所以这是一个好习惯。特别是在大型的项目开发中，就需要阅读别人的文档，因此适当的文档非常的重要。```

```python
def mydef(params):
    #引号中的部分就是我们书写文档的地方   并且文档部分应该写在函数的开头
    ''' 
    这是我们第一个文档
    :param params:
    :return:
    '''
    return params
#print(mydef.__doc__)     #显示文档的内容  函数名（不带小括号）.__doc__
help(mydef)               
#当函数不知道怎么去使用的时候可以用help()去查看文档，当然使用方法需要自己去写
```

##### 3、关键字参数

```普通的参数叫位置参数，通常在调用的时候，粗心的程序员很容易弄错参数的顺序，导致函数达不到预期的效果。我们看一下例子：```

```python
def mydef(name,age):
    print(name,'他的年龄是',age,'岁')
mydef(21,'hal')

#应为参数顺序错误导致结果不正确
#result：21 他的年龄是 hal 岁
```

```因此，有了关键字参数。使用关键子参数可以有效的避免这种情况的发生。```

```python
def mydef(name,age):
    print(name,'他的年纪是',age,'岁')
mydef(age=23,name='小米')

#使用了关键字参数以后顺序错了，但是结果依然正确，所谓的关键字就是指定的形参
#result:小米 他的年纪是 23 岁
```
##### 4、默认参数

```初学者很容易把关键字参数和默认参数搞混，默认参数是在设定形参的时候给形参赋的值```

```python
def mydef(name='千锋',action='是最好的IT教育机构'):
    print(name,action)
    
mydef()
#在参数没有传递值的时候也不会报错，因为有了默认的值
#result:千锋 是最好的IT教育机构

mydef(name='中国',action='是最伟大的国家')
#在参数传递的过程中，替换了默认的值
#result:中国 是最伟大的国家

```

```通过上面的例子可以看出来关键字参数是在调用函数的时候使用的，而默认参数是在定义函数的时候使用的```

##### 5、收集参数（可变参数）

```这个名字听起来比较的新鲜。发明这种机制的人就是不知道在特定的情况下会用到多少的参数...听起来您认不解，但是确实有这种情况，这时候需要在参数前面加上（*）星号就可以了```

```python
def test(* params):
    print('params 有%d个参数'%len(params))
    print('最后一个参数是：',params[-1])
    print(type(params))
    print(params)
test(1,3,5,7,9)

'''
result:
params 有5个参数
最后一个参数是： 9
<class 'tuple'>
(1, 3, 5, 7, 9)
'''

#调用的时候传递多个参数，python会把多个收集参数打包成tuple(元祖)
#所以在查找第几个参数的时候可以使用元祖的查找方法
```

```星号（*）既可以是打包，又可以是解包，举个例子，如果我现在实参是一个list是那么便会变成嵌套，此时在调用的实参前面加沙个一个星号（*）进行解包就就可以了```

```python
def test(* params):
    print('有%d个参数' % len(params))
    print(params[-1])
    print(type(params))
    print(type(params[-1]))  #list是被嵌套在tuple里面的
    print(params)
list = [1,3,5,7,9]
test( list)

'''
result:
有1个参数
[1, 3, 5, 7, 9]
<class 'tuple'>
<class 'list'>
([1, 3, 5, 7, 9],)
'''
```

```为了是用起来更加的方便我们试一试解包```

```python
def test(* params):
    print('有%d个参数' % len(params))
    print(params[-1])
    print(type(params))  
    print(type(params[-1]))
    print(params)
list = [1,3,5,7,9]
test(* list)  #解包以后的list是逐个传递的

'''
result:
有5个参数
9
<class 'tuple'>
<class 'int'>
(1, 3, 5, 7, 9)
'''
```
#### 三、函数的地盘
##### 1、函数的过程
很多编程语言中，函数和过程其实是区分开的。一般认为函数(function)是返回值的，而过程(procedure)是简单、特殊并且没有返回值的。

也就是说，函数是干完事儿必须写报告的“苦逼”，而过程是完事后拍拍屁股一走了之的“小混蛋”。

python严格来说只有函数，没有过程！但是通过上面的例子看过去，没有return之前，python的function也是没有返回值？我们看看下面的例子

```python
def mydef():
    print(123)
print(mydef())

#123
#None

#没有return默认返回一个None
```
##### 2、谈谈返回值

python可以利用序列打包多种类型的一次性返回值。

```python

def mydef():
    return 1,2,3,4
print(mydef())

#(1, 2, 3, 4)
```

##### 3、函数变量的作用域

变量的作用域也就是平时所说的变量可见性

```python
def discounts(price,rate):
    final_price= price * rate
    return final_price

old_price = 80
rate = 0.5
new_price = discounts(old_price,rate)
print(new_price)
print(final_price)

#40.0
#NameError: name 'final_price' is not defined
```
错误的原因是final_price没有被定义过，因为他是discounts函数里面的内容，再有在函数体内部才有效，出了这个范围就不是它的地盘了。

总结一下：在函数里面定义的参数以及变量，都称谓局部变量，出了函数外，它们都是无效的。事实上，python在运行函数的时候，是利用内存中的‘栈（stack）’区域进行储存的，当执行完函数以后，函数中的所有内容都要被自动删去，所以在函数体外是找不到的。

和局部变量相对应的就是全局变量，全局变量拥有更加庞大的作用域

```python
def discounts(price,rate):
    final_price= price * rate
    print(old_price)
    return final_price

old_price = 80
rate = 0.5
new_price = discounts(old_price,rate)
print(new_price)

#80     #old_price在函数内部输出
#40.0
```

看起来全局变量更加霸道，但是我们看看下面的例子：

```python
def discounts(price,rate):
    old_price = 100
    final_price= price * rate
    print('这是里面的old_price',old_price)
    return final_price

old_price = 80
rate = 0.5
new_price = discounts(old_price,rate)
print('这是外面的old_price',old_price)
print(new_price)

#这是里面的old_price 100
#这是外面的old_price 80
#40.0

```
这样的话就已经出现奇怪的问题。

其实函数里面的old_price是python自己创建的新的局部变量，但是全局的old_price纹丝不动。

####四、内嵌函数和闭包

##### 1、global关键字
刚刚我们在上一个例子中看到了Python中对于全局变量的保护，也就是在函数内部重新复制的话，python会创建一个变量名一样的局部变量，但是在不经意中会出现衡多的bug，代码的维护也会变得困难。

衡多编程语言为了避免这一个情况，都会使用`global`关键字，也就是说我们上面的那种方法就不要在用了。例子如下：

```python
count = 5
def myfun():
    global count
    count = 10
    return count
print(myfun())
print(count)

#10
#10  
```
看上面的例子内部的count重新复制，外层的count也随之改变
##### 2、内嵌函数

什么是内嵌函数，就是允许在函数内部创建另外一个函数。

```python
def myfun():
    print('fun1')
    def myfun2():
        return 'fun2'
    return myfun2()
print(myfun())


#fun1
#fun2
```
这个函数虽小，但五脏俱全，不过看起来好像没什么用。

<font color='red'>注意：myfun2是myfun1的内部函数，所以它的作用域也在myfun1的函数体内。如果要在外部调用就会报错。</font>

##### 3、闭包（closure）
闭包是函数重要的组成结构，函数编程是一种编程范式。著名的函数编程语言LISP，这个大家可能知道，主要用于绘图和人工智能，一直被认为是天才使用的语言。

那么语言不同，那么闭包的的实现方式也就不同。

python中的闭包定义：一个内部函数里，对外部的作用域（而不是全局作用域）的变量进行引用，那么内部函数就被认为是闭包。看例子：

```python
def funx(x):
    def funy(y):
        return x * y
    return funy  #这里是不带括号的


#两种调用格式
i = funx(8)
print(i(5))
print(funx(10)(5))

#40
#50
```
<font color='red'>注意：它和闭包是一个意思，所以不能直接去调用funy()，否则会报错。</font>

#####闭包中的变量关系对应

在闭包中外面一层函数中定义的变量是不能再内层函数中直接修改的，只能访问，相当于全局变量和局部变量的关系，看例子：

```python
def funx():
    x = 5
    def funy():
        x *= x
        return x
    return funy  #这里是不带括号的

print(funx()())

#UnboundLocalError: local variable 'x' referenced before assignment
```
这个报错信息和全局变量是一样的，python认为内部函数的x是局部变量，外部的函数x被屏蔽了起来。所以

#### 五、lambda表达式（匿名函数）
python允许使用 lambda 关键字来创建匿名函数，我们提到一个新的关键字`匿名函数`。那是一个什么函数了？匿名函数和普通的函数在使用上又有什么不同了，使用匿名函数又有哪些优势了？


看看比较，这是平常的定义：

```python
def de(x):
    return 2 * x+1
print(de(2))
```

zai看看lambda：

```python

a = lambda x: 2 * x + 1
print(a(2))

```

我们可以看到lambda的语法风格非常的简洁

lambda 关键字 冒号左边是参数，多个参数可以用逗号隔开；冒号右边是表达式，lambda返回的是函数表达式，所以要把它赋给一个变量，那么变量就相当于一个函数名

演示一个多参数的lambda：

```python

f = lambda x,y: x + y
print(f(3,4))

#7
```

看上去好像是没用，因为我们现在遇不到使用它的场景：

```python
1、python在编写一些执行脚本的时候可以使用lambda，这样可以接受定义函数的过程，比如写一个简单的脚本管理服务器。
2、对于一些比较抽象，并且整个程序执行下来只需要调用一两次的，有时候给函数起名实在想不出来的。
3、简化代码的可读性。

```

##### 1、filter()
它是一个内建函数过滤器，就是一个BIF

第一个参数是一个函数也可以是一个None，如果是None的话会把值为True的选取出来；如果是函数的话，就把第二个参数传递进去计算，第二个参数应该是一个可迭代的序列；

我们可以用help()来查看它

```python
print(help(filter))

#Help on class filter in module builtins:

```
看看我们使用的例子：

```python
temp = filter(None,[2,0,False,True])
print(list(temp)

#[1, 2, True]
```
```python
def odd(x):
    return x % 2
temp = filter(odd,range(10))
print(list(temp))

#[1, 3, 5, 7, 9]
```
```python
print(set(filter(lambda x: x % 2,range(10))))

#{1, 3, 5, 7, 9}
```
##### 2、map()

map()了在这里不是地图的意思，在编程领域，map一般作“映射”来解释。map()这个内置数也有两个参数，和filter()相似，但是它的第一个参数只能是函数：

```python
print(help(map))

#Help on class map in module builtins:
```

看下面例子：

```python
print(list(map(lambda x: x * 2 , range(10))))

#[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

### 【2】递归
#### 1、驾驭递归
优秀的程序员是伯乐，那么递归就是千里马、万里马。普通的程序员用迭代，‘天才的程序员’用递归。

递归的这个概念，是算法的范畴，不是属于python的东西，但是当你掌握了递归的技巧和思路后，你会发现这是一个非常棒的编程思路。

那么递归在我们日常生活中有那些例子？

谢尔宾斯基三角形：
<image src='images/timg-2.jpeg' width='500'>

其实它就是一个树形的结构：
<image src='images/timg.jpeg' width='500'>


说了这么多，递归的概念就是自身调用自身。

```python
def mydef(x):
    return mydef(x+1)
print(mydef(1))

#RecursionError: maximum recursion depth exceeded
```
尝试这个例子，很多人都会出现这个错误，从理论上来说，这个程序会永远的执行下去，一直耗尽内存资源。但是python3出于保护机制，默认的递归深度是100次，所以你的代码才会停下来。不过你写写网络爬虫等其它工具，可能会爬的很深，那么可以自己设置递归的深度，如下：

```python
import sys
sys.setrecursionlimit(10000)

#设置最大深度为一万层
```
####2、写一个求阶乘的函数
整数阶乘是指10 * 9 * 8 * 7.....* 1:

我们用迭代函数写一个：

```python
def mydef(n):
    res = n
    for i in range(1,n):
        res *= i
    return res
print(mydef(5))

#120
```
用递归写一个：

```python
def myrecursion(n):
    if n ==1:
        return 1;
    else:
        return n * myrecursion(n-1)
print(myrecursion(5))

#120
```
这个例子递归满足了两个条件：
(1）调用函数本身
(2)设置了正确的返回值


```python

myrecursion(5) = 5 * myrecursion(4)
	myrecursion(4) = 4 * myrecursion(3)
		myrecursion(3) = 5 * myrecursion(2)
			myrecursion(2) = 5 * myrecursion(1)
				myrecursion(1) = 1
				
```
最后郑重的说一下，不是说会使用递归，把所用可以迭代的东西用递归来替代，真的这样作就是乌龟程序员了。为什么这么说，递归是自己调用自己，每次函数调用都需要进行压栈、弹栈、保存和恢复寄存器的栈操作，所以非常的耗费时间和空间。

另外，如果递归一旦忘记了返回，或者错误的设置了返回条件，那么执行这样的递归代码，就会是一个无底洞：只进不出！，所以递归，有来有回。
#### 3、斐波那契数列
斐波那契数列（Fibonacci sequence），又称黄金分割数列、因数学家列昂纳多·斐波那契（Leonardoda Fibonacci）以兔子繁殖为例子而引入，故又称为“兔子数列”，指的是这样一个数列：1、1、2、3、5、8、13、21、34、……在数学上，斐波纳契数列以如下被以递归的方法定义：F(0)=0，F(1)=1, F(n)=F(n-1)+F(n-2)（n>=2，n∈N*）在现代物理、准晶体结构、化学等领域，斐波纳契数列都有直接的应用，为此，美国数学会从1963起出版了以《斐波纳契数列季刊》为名的一份数学杂志，用于专门刊载这方面的研究成果。

下面是他讲过的故事，如果兔子在出生两个月后就有繁殖能力，在拥有繁殖能力后，这对兔子每个月能生出一对兔子来，假设所有兔子都不会死去，那么一年后能有多少对兔子？


| 所有经过的月数  | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10| 11| 12| 
| ------------- |---|---|---|---|---|---|---|---|---|---|---|---|
| 兔子的总对数    | 1 | 1 | 2 | 3 | 5 | 8 | 13| 21| 34| 55| 89|144|

数学中的定义：

```python
		|  1,               当 n = 1 时
F(n) =  |  1,               当 n = 2 时
		|  F(n-1)+F(n-2)    当 n > 2 时
```
假设现在我们经历了20个月，现在有多少对：

迭代实现：

```python
def fab(n): #n代表月数
    a1 = 1  #代表这个月现有对数
    a2 = 1  #代表下个月要出生的对数
    a3 = 1  #代表这个月总对数
    if n <1:
        print('输入有误')
        return -1
    while (n - 2) > 0:
        a3 = a1 + a2
        a1 = a2
        a2 = a3
        n -= 1
    return a3

result = fab(20)
if result != -1:
    print('总共有 % d对小兔崽子诞生！' % result)
    
#总共有  6765对小兔崽子诞生！
```

```python
def fab(n):
    if n < 1:
        print('输入有误！')
        return -1
    if n ==1 or n ==2:
        return 1
    else:
        return fab(n-1) + fab(n-2)
result = fab(20)
if result != -1:
    print('总共有 % d对小兔崽子诞生！' % result)
    
#总共有  6765对小兔崽子诞生！
```
上面的例子看，递归实现起来要简单一些，但是说过了递归消耗内存，消耗cpu，效率低，我们试试35个月的递归和迭代。

如果你想测试你的电脑牛不牛逼，不妨用递归试试。
递归实现。
#### 4、汉诺塔（课堂小练习）
汉诺塔：汉诺塔（又称河内塔）问题是源于印度一个古老传说的益智玩具。大梵天创造世界的时候做了三根金刚石柱子，在一根柱子上从下往上按照大小顺序摞着64片黄金圆盘。大梵天命令婆罗门把圆盘从下面开始按大小顺序重新摆放在另一根柱子上。并且规定，在小圆盘上不能放大圆盘，在三根柱子之间一次只能移动一个圆盘。

汉罗塔游戏：
<image src='images/timg-3.jpeg' width='500'>

 	
	三根柱子分别是： X                  Y                Z

对于游戏的玩法:

```python
(1)将前63个盘子从X移动到Y上，确保大盘在小盘下。
(2)将最底下的第64个盘子从X移动到Z。
(3)将Y上的63个盘子移动到Z上。
```
思路如下：
最底下的盘子我们给它编号第64个，最上面的给编号第1个。

```python
def hanoi(n,x,y,z):
    if n == 1:
        print(x,'-->',z) #如果只有一层就直接x移动到z
    else:
        hanoi(n-1,x,z,y) #将n-1的盘子从x移动到y上
        print(x,'-->',z) #将最底下的第64个盘子从x移动到z
        hanoi(n-1,y,x,z) #将Y上的63个盘子移动到z上
hanoi(64,'X','Y','Z')
```
这就是递归的魔力


##作业

####封装函数，输入一个数字判断它是不是闰年
闰年的条件是 能被4整除 且不能被100整除

