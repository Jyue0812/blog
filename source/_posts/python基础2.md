#Lesson 2
___

##第三章
___
###【1】注释
每个语言中都有注释，包括我们小时候学的语文课中有很多的文言文它们都有注释；那么我们可以得出结论，python的注释就是把代码描述出来，让其他人更快的去理解。

前面我们提到过注释，被注释的内容就是不被程序解析的文本域。

```python
#井号代表单行注释


'''
三个单引号表示多行注释
三个单引号表示多行注释
三个单引号表示多行注释
'''


"""
三个双引号表示多行注释
三个双引号表示多行注释
三个双引号表示多行注释
"""
```
###【2】舒克和贝塔（ print和input ） 
print和input一个是输出一个是输入，这两个函数难舍难分。

```python
#print()的作用就是向屏幕上打印输出内容

print('hello 1000phone')

print('hello 1000phone','hello 1000phone')

print(12)

print(13,14)
```
print的参数’end‘，我们上面的print输出完以后每次都会换行，这就是end导致的，end的默认参数是’\n‘就是回车的意思。

```python
print('hello word',end=' ')#表示以空格拼接
print('hello shanghai'，end=' =>') #表示以=>（箭头）拼接

>>>hello word hello shanghai =>

```

input就是接受我们输入的信息的,例如在我们输入账号和密码的时候，在输入我们的手机号的时候。

```python
name = input('随便输入一段话：')

>>>随便输入一段话：你好python
>>>你好python

```

###【3】标识符
1、什么是标识符？标识符就是一段字符`提示：字符串未必是标识符`。

2、标识符的规则

```
1、只能由字母、数字、下划线组成，且不能以数字开头。
2、不能是python的关键字
	import keyword
	print(keyword.kwlist)
可以在python脚本中引入keyword查看
3、区分大小写，见名知意，比如声明一个（用户账号）的变量 ：username
```
3、标识符的作用就是给变量、函数、类等等命名的。

```python
提示：在python3中非 ASCII 标识符也是允许的
```

###【4】闲聊数据类型
计算机顾名思义就是做数学计算使用的，因此计算机理所当然可以处理各种数值。但是计算机远不止能处理数值，还可以处理文本、图形、音频、视频等其它数据，不同的数据就需要不同的类型。

我们python的中的变量是没有数据类型的，python中的变量更加像是标签想贴哪儿就贴哪儿，通过这个标签，就可以找到变量在内存中对应的存放位置。

```python
python的数据类型有
	number(数字)：int（整形或者说正整数和负整数）、float（浮点型或者说小数）、complex(复数)
	string(字符串)
	boolean(布尔值)
	none(空值)
	list(列表)
	tuple(元祖)
	dict(字典)
	set(集合)
```

##第四章
___
在成为高手之前我们我们必须要知道的一些基础知识

###【1】变量和常量

当你把一个赋值给一个名字时，它会储存在内存中，把这块内存空间成为变量，在大多数语言中，都把这种行为称为’给变量赋值‘或’或把值存在变量中‘。

不过，python不同于其它语言，python并不是把值存在变量中，而是把名字’贴‘在’值‘上面。所以有些python的程序员会说python没有变量，自由名字，但是变量本来就是一个名字，可以找到我们想要的东西。

常量就是恒久不变的变量，它在.py文件执行过程中就会自动加载到内存的静态区中，遗憾的是，python中没有常量的定义。

看个例子：

```python
name = '李连杰'
print(name)

>>>李连杰

name = '吴京'
print(name)

>>>吴京
#name是变量 等于号 后面的是值
```

为什么叫变量不叫衡量？因为它是可变的！再看一个例子：

```python
x = 3
x = 5
y = 8
z = x + y
print(z)

>>>13
#我先给x赋值了一个3，然后又给它赋值了一个5（这个时候3就被5替换了），接下来创建一个y，给它初始化并赋值一个8，最后创建一个变量z，它的值是变量和y的和。
```
同样运用到字符串中：

```python
name1 = '梁山伯'
name2 = '祝英台'
name3 = name1 + name2
print(name3)

>>> 梁山伯祝英台
#再次提示这种字符串相加叫拼接，不是拼爹
```
<font color= 'red'>需要注意的地方：</font>

```python
1、在使用之前，需要对它赋值。
2、变量名可以包括字母、数字下划线，但变量名不能以数字开头。
3、等号（=）地赋值的意思，左边是名字，右边是值，不可写反了。
4、变量的名字理论上可以取任何合法的名字，但作为一个优秀的程序员，请尽量给变量一个专业一点的名字。
```

变量是指向内存分配给 值 得空间的，那么我们怎么知道这个值存储的位置了？

使用BIF  `id()` 它的作用是查找 值在内存中的地址，看下面的例子：

```python
num1 = 3
num2 = 3

print(id(num1),id(num2))


>>>4297636960 4297636960

#我们可以发现num1，和num2 的结果是一样，那么我们可以得到一个结论，num1和num2指向内存中的同一个地址。
```


####关于类型的信息

虽然我们的变量是没有类型的，但是我们的 值 是有类型区分的，怎么查看值得类型了？

使用BIF  `type()` 作用是获取值得类型：

```python

str = 'abcd' 

sn  = None

int = 123

flt = 1.22

com = 234j

boo = True

print(str,sn,int,flt,com,boo)
print(type(str),type(sn),type(int),type(flt),type(com),type(boo))

>>>abcd None 123 1.22 234j True
>>><class 'str'> <class 'None'> <class 'int'> <class 'float'> <class 'complex'> <class 'bool'>

```

通过上面的例子可以看出python的数据类型有

`数字(number)、字符型(string)、布尔型(boolean)、None(空值)`

我们后面还要学：

`列表(list)、tuple(元祖)、dict(字典)、set(集合)`

这是我们python的8种数据类型


还可以使用 isinstance(）

```python
stri = '123'

print(isinstance(stri,int))
print(isinstance(stri,str))

>>>False
>>>True
#第一个参数是我们要分辨的变量，第二个参数是我们需要判断的类型，它只会返回True和False
```


###【2】Number（数字）

我们在前面提到过我们的number类型分为 `整形、浮点型、复数`

整形说白了就是整数，python3的整形已经与长整型进行了无缝结合，现在的python3的整形类似于Java的BigInteger类型，它的长度不受限制，如果非要有个限制，那就只限于计算机的虚拟内存总数了。所以python3很容易进行大数计算。

```python

num1 = 10
num2 = num1
print(id(num2))
# 连续定义多个变量
num3 = num4 = num5 = 1
print(num3, num4, num5)
#交互式赋值定义变量
num6, num7 = 6, 7
print(num6, num7)

```

###【3】float(浮点数)

浮点数就是平时说的小数，例如圆周率就是浮点型，python中的整形和浮点型的唯一区分方式就是看有没有小数点。

谈到了浮点型，不得不说下E记法。也就是我们平时说的科学计数法，用于表示特别大和特别小的书：

```python

num = 0.000025
print(num)

>>>2.5e-05

num = 25000
print(format(num,'.1e'))

>>>2.5e+04

#python3在正整数输出的时候默认会原样输出，所以使用format()函数转换成科学计数法。
format(num,'.1e')第二个参数是'.1e'表示保留小数点后面的1个小数部分。
format(num,'e')如果是”e“会默认保留多个小数部分。
```

###【4】复数（了解）

一个实数和一个虚数的组合构成一个复数。一个复数是一对有序浮点数(x, y)。表示为x + yj，其中x是实数部分，y是虚数部分。渐渐的复数在日常运算,机械,电子等行业获得了广泛的应用。由于一些研究人员不断的重复制造用于复数运算的工具，在很久以前的Python1.4 版本里，复数终于成为一个真正的Python 数据类型。 

下面是 Python 语言中有关复数的几个概念：

```python
虚数不能单独存在，它们总是和一个值为 0.0 的实数部分一起来构成一个复数。
复数由实数部分和虚数部分构成
表示虚数的语法： real+imagj
实数部分和虚数部分都是浮点数
虚数部分必须有后缀j或J。
```
复数的内建属性 
复数对象拥有数据属性，分别为该复数的实部和虚部。复数还拥有conjugate 方法，调用它可以返回该复数的共轭复数对象。

复数属性：

```python
属性                   描述 
num.real             该复数的实部 
num num.imag         该复数的虚部 
num.conjugate()      返回该复数的共轭复数
```

```python

c=2.3+2.5j
print(c.real)
print(c.imag)
print(c.conjugate())

>>>2.3
>>>2.5
>(2.3-2.5j)
```

###【5】类型的转换

接下来介绍几个跟数据类型紧密相关的函数：int()、float()、str()

####int()：

`int()`的作用是将一个字符串或者一个浮点数转换成一个整数

```python
a = '123'

b = 3.1415926

c = 5.9

print(int(a),end=',')
print(int(b),end=',')
print(int(c))


>>>123,3,5

#通过结果可以发现int在转换浮点型的时候，python会采取’截断‘处理，就是把小数点后面的数据直接砍掉，而不是四舍五入；
```


<font color='red'>注意：</font>

```python
a = '4a'
print(int(a))

#如果这个字符串里面不是纯数字字符那么就会报错。



>>>Traceback (most recent call last):
  File "/Users/ruidong/PycharmProjects/project/demo.py", line 7, in <module>
    print(int(a),end=',')
ValueError: invalid literal for int() with base 10: 'q'
```


####float():

`float()` 的作用是把一个字符串或整数转换成浮点数。

```python
a = 520

b = '520'

c = '980'

print(float(a))
print(float(b + c))

>>>520.0
>>>520980.0

#python进行浮点型转换的时候默认在后面加了一个’.0‘
```

####str():
`str()`的作用是将一个数或任何类型转换成一个字符串

```python
a = str(3.4)

b = str(89)

c = 5e15

print(a,b,str(c))

>>>3.4 89 5000000000000000.0

#在被转类型的两边加上了引号
```

###【6】数学功能

python3的数学功能是强大的，但是在强大的功能也要去熟悉它的用法和操作。

首先我们要在python的编译器中输入

```python
import math    #引入数学库

print(math)

#没有报错就表示引入正常
```

####abs()绝对值

```python
a1 = -10
a2 = abs(a1)
print(a2)

>>>10
```
####比较两个数的大小

```python
a3 = 100
a4 = 9
print((a3>a4)-(a3<a4))

>>>1
```

####max()返回一个最大的值

```python

print(max(1,2,3,4,5,6,7,8))

>>>8
```

####min()返回一个最小的值

```python

print(min(1,2,3,4,5,6,7,8))

>>>1
```

####pow(x,y)求x的y次方

```python
print(pow(2, 5))

>>>32
```

####round(x,y)四舍五入 x表示数字  y表示保留几位小数

```python

print(round(3.456))
print(round(3.556))
print(round(3.456, 2))
print(round(3.546, 1))


>>>3
>>>4
>>>3.46
>>>3.5

```

####math.ceil()向上取整

```python

print(math.ceil(18.1))
print(math.ceil(18.9))

>>>19
>>>19
```

####math.floor()向下取整

```python

print(math.floor(18.1))
print(math.floor(18.9))

>>>18
>>>18
```

####math.modf()返回整数部分与小数部分

```python

print(math.modf(22.3))

>>>(0.3000000000000007, 22.0)
```

####math.sqrt()开放 返回浮点类型

```python

print(math.sqrt(16))

>>>4.0
```

###【7】随机数

随机数在我们日常的生活中也是比较常见的，比如说我们手机的验证码等。

####random.choise() 从序列的元素中随机挑选一个元素

```python

print(random.choice([1,3,5,7,9]))
print(random.choice(range(5)))#range(5) == [0,1,2,3,4]
print(random.choice("sunck"))#"sunck"  == ["s","u","n","c","k"]
print(random.choice(range(10)) + 1)
```

####random.randrange() 从指定范围内，按指定的基数递增的集合中选取一个随机数

```python

#random.randrange([start,] stop[, step])
#start--指定范围的开始值，包含在范围内，默认是0
#stop--指定范围的结束之，不包含在范围内
#step--指定的递增基数，默认是1
print(random.randrange(1, 100, 2))
#从0-99选取一个随机数
print(random.randrange(100))
```

####random.random() 随机生产[0,1)之间的数(浮点数)

```python

print(random.random())

```

####random.shuffle()将序列的所有元素随机排序

```python
list = [1,2,3,4,5]
random.shuffle(list)
print(list)
```
####random.uniform(x,y)随机生产一个实数，他在[x,y]范围

```python

print(random.uniform(3,9))

```

###【8】三角函数(了解)

我们为什么不把三角函数放在 数学功能里面讲了，因为在商业开发中很少会用到三角函数。

<image src='images/三角.jpg' width="500"/>

正弦：在Rt△ABC中，∠C=90°，我们把锐角A的对边与斜边的比叫做∠A的正弦（sine），记作sinA，即`sinA=∠A的对边/斜边=a/c`

```python

sin(A) #返回A的正玄值

```


余弦：我们把∠A的邻边与斜边的比叫做∠A的余弦（cosine），记作cosA，即`cosA=∠A的邻边/斜边=b/c`

```python

cos(A) #返回A的余玄值

```

cosA=∠A的邻边/斜边=b/c

正切：把∠A的对边与邻边的比叫做∠A的正切（tangent），记作tanA，即

      tanA=∠A的对边/∠A的邻边=a/b

      对于tanA还有一个公式

      tanA=sinA/cosA
      
```python

tan(A)  #返回A的正切值

```


##第五章
___

###【1】算数操作符

和大多数语言一样，python的算数操作符绝大部分能被我们所理解，注意不是全部。

```python

+   -   *   /     %      **           //

加  减  乘   除   取模    求幂          取整
               （取余） （math.pow）
```
前面四个应该不用多说了，大名鼎鼎的四则运算。

```python

num1 = 5
num2 = 3
print(num1 + num2)
print(num1 - num2)
print(num1 * num2)
print(num1 / num2)
print(num1 % num2)
print(num1 ** num2)#5^3  pow(5, 3)
print(num1 // num2)



>>>8
>>>2
>>>15
>>>1.6666666666666667
>>>2
>>>125
>>>1
```
###【2】赋值运算符和赋值运算表达式


赋值运算符  =

赋值运算表达式
格式：变量 = 表达式
功能：计算了等号右侧“表达式”的值，并赋值给等号左侧的变量
值：赋值结束后变量的


```python

num3 = 10
num4 = num3 + 20

print(num3,num4)

>>>10 30

```

###【3】复合运算符

```python

复合运算符
+=   a += b     a = a + b
-=   a -= b     a = a - b
*=   a *= b     a = a * b
/=   a /= b     a = a / b
%=   a %= b     a = a % b
**=   a **= b     a = a ** b
//=   a //= b     a = a // b

```

###【4】优先级问题

当一个表达式存在多个运算符的时候，就可能发生不知道先运行谁的情况；

比如小学数学规定，先括号在乘除，加减是最低，这就是优先级。

例如：

```python

-3 * 2 + 5 / -2 -4

相当于：

(-3) * 2 + 5 / (-2) -4 

#这个大家很容易理解
```
python有一个特殊的乘法，双星号（**）幂运算，

例如：

```python
3 ** 2

星号左侧是底数，星号右侧是指数，这叫做3的2次幂，或者3的2次方

```


因为幂运算操作符和一元操作符的优先级关系比较特别，幂运算操作符比期左侧的一元操作符优先级高，比其右侧的医院操作符优先级低。

```python
-3 ** 2

>>>9

3 ** -2

>>>0.1111111111111111
```


##思考

###以下哪个变量名不正确的是？为什么

```python
A)MM_520
B)_MM520_
C)520_MM
D)_520_MM

```
###熟记标识符规则
###把数字和随机数库练习三遍



<!---->