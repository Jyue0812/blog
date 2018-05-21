#Lesson 3
___
##第五章

###【5】位运算符

位运算符：按位运算符是把数字看做二进制数来进行计算

####& 按位与运算符

相应的位数都为1，则该位的结果是1，否则为0

```python
print（5 & 7）
'''
5 ->10
7 ->111


101
111
————
101

101->5
'''
>>>5

```
####|  按位或运算符

两个二进制位有一个位1时，结果为1

```python

print(5 | 7)

'''
101
111
---
111
'''

>>>7
```

####^  按位异或运算符

二进制的两位相异时，结果为1

```python

print(5 ^ 7)

'''
101
111
---
010
'''
>>>2
```

#### ~  按位翻转运算符

将二进制数+1之后乘以-1

```python

print(~5)
'''
~101
___
(101+1) * -1
___
(111) * -1
__——
-111
'''

>>>-6
```


####<<  左移动运算符

各二进制位全部左移动若干位，由<<右侧的数字决定，高位丢弃，低位补0

方法:    X<<N 将一个数字X所对应的二进制数向左移动N位.

```pyhon
print(2 << 2)

'''
0000 0010
___
0000 1000
'''

>>>8
```

####>>  右移动运算符

各二进制位全部右移动若干位，由>>右侧的数字决定

方法:    X>>N 将一个数字X所对应的二进制数向右移动N位.

```pyhon
print(8 << 2)

'''
0000 1000
___
0000 0010

'''

>>>2
```

###【6】比较运算符

比较运算符根据表达式值得真假返回布尔值。

格式：  表达式1   关系运算符   表达式2

`==     !=     >       <      >=      <=`

python在布尔值处理上有些不同，True等于整数1，False等于整数0

```python

#全等于，包括数据类型,布尔型的
print(1 == 2)      >>>False
print(1 == '1')    >>>False
print(1 == True)   >>>True
#不等于
print(1 != 2)      >>>True
print(0 != False)  >>>False
print(1 != '1')    >>>True
#大于
print(1 > 2)       >>>False
print(True > False) >>>True
#小于
print(3 < 8)       >>>True
print(True < False) >>>False
#大于等于
print(True >= False) >>>True
print(1 >= True)  >>>True
#小于等于
print(3.14 <= 3.14)  >>>Ture
print(math.ceil(math.pi) <= math.floor(math.pi)) >>>True
```

####逻辑运算符

逻辑操作符包括`and`、`or`、`not`

逻辑与：and操作符左边的操作符为真，右边也为真，那么结果为真。

and执行的是一个串联的短路原则，一个地方坏了都换了（悲观原则）

```python

a = 0
b = 1
print(a==0 and b==1)
print(a==0 and b==2)

>>>True
>>>False
```


逻辑与：or操作符只需要左边或右边有一个为真，那么结果为真。

or是一个并联的原则，其它的短路了我这里依然是好的，只要一个是好的那就是好的（乐观原则）

```python

a = 0
b = 1
print(a==2 and b==12)
print(a==0 or b==2)

>>>False
>>>True
```

逻辑非：not操作符是一个一元操作符，它的作用是得到一个和操作符相反的布尔类型。

```python

a = 0

print(not a==1)
print(not a==0)

#这里相当于 !=

>>>True
>>>False
```
###【7】成员运算符

成员运算符包括`in`、`not in`,从字义上可以看，他是判断在什么里面和不在什么里面，返回一个布尔值。

格式： x in y        x not in y

```python
a = 'qwert'

print('e' in a)
print('e' not in a)

>>>True
>>>False
```
###【8】身份运算符

身份运算符包括`is`、`is not`，判断标识符是不是引用同一个对象。

格式： x is y        x is not  y

```python
a = None
b = 333
c = 233
print(a is None)
print(b is not None)
print(c is 233)


>>>True
>>>True
>>>True
```

##第六章

###【1】字符串

到目前为止，我们所认知的在字符串就是引号内的一切东西，我们把字符串叫做文本，文本和数字是截然不同。

python创建字符串的时候，必须要加上引号，单引号也可以双引号也可以，python一点也不挑，但是你不能一边用单引号，一边用双引号，这样语法就会报错了。

```python

print('python")

>>>SyntaxError: EOL while scanning string literal
```

我们以前提到过拼接，两个数字叫相加，两个字符串相加叫拼接。

```python

print('5' + '8')

>>>58
```

那如果在字符串内容中需要用到单引号怎么办了？

```python

print('Let's go')


>>>SyntaxError: invalid syntax
```

有一种方法，只要用上不同的引号，python就不会误解你的意思了

```python

print("Let's go")

>>>Let's go
```

###【2】原始字符串

反斜杠是一个好东西，但是我们试一试C:\now

```python

print('C:\now')

>>>C:
>>>ow

#因为 \n  在计算机里是 回车键
```

那如何才能正常的去打印？

```python

print('C:\\now')

>>>C:\now

# 反斜杠(\)代表转义的意思
```

但是如果一个路径里面有很多的\那我么一个一个的输入就不乐意了,这时候我们就可以使用 原始字符串 了，只需要在字符串前面加一个英文字母r即可：


```python

string = r'C:\now\start'

print(string)

>>>C:\now\start
```

<font color='red'>使用字符串的时候需要注意一点：无论是否是原始字符串，都不能以反斜杠结尾。（反斜杠放在字母的结尾表示还没有结束，换行继续的意思）</font>

如果你继续操作就会报错：

```python

string = r'C:\now\start\'
print(string)

>>>SyntaxError: EOL while scanning string literal
```
###【3】长字符串

如果你希望得到一个跨多行的字符串，例如：

```python

从明天起, 做一个幸福的人 
喂马, 劈柴, 周游世界 
从明天起, 关心粮食和蔬菜 
我有一所房子, 面朝大海, 春暖花开  
从明天起, 和每一个亲人通信 
告诉他们我的幸福 
那幸福的闪电告诉我的 
我将告诉每一个人 
给每一条河每一座山取一个温暖的名字 
陌生人, 我也为你祝福 
愿你有一个灿烂的前程 
愿你有情人终成眷属 
愿你在尘世获得幸福 
而我只愿面朝大海, 春暖花开
```

这是一首好诗，但是如果要打印出来，那就需要用到很多的换行符：

```python
print("从明天起, 做一个幸福的人\n喂马, 劈柴, 周游世界\n从明天起, 关心粮食和蔬菜\n我有一所房子, 面朝大海, 春暖花开\n\n从明天起, 和每一个亲人通信\n告诉他们我的幸福\n那幸福的闪电告诉我的\n我将告诉每一个人\n\n给每一条河每一座山取一个温暖的名字\n陌生人, 我也为你祝福\n愿你有一个灿烂的前程\n愿你有情人终成眷属\n愿你在尘世获得幸福\n而我只愿面朝大海, 春暖花开")

```
这样会给我们带来很多困扰，好在python里面有长字符串，只需要三个引号包裹起来，不管是三个单引号韩式双引号。

```python

print('''
从明天起, 做一个幸福的人 
喂马, 劈柴, 周游世界 
从明天起, 关心粮食和蔬菜 
我有一所房子, 面朝大海, 春暖花开  
从明天起, 和每一个亲人通信 
告诉他们我的幸福 
那幸福的闪电告诉我的 
我将告诉每一个人 
给每一条河每一座山取一个温暖的名字 
陌生人, 我也为你祝福 
愿你有一个灿烂的前程 
愿你有情人终成眷属 
愿你在尘世获得幸福 
而我只愿面朝大海, 春暖花开
''')

```
###【4】字符串运算

####字符串拼接

```python

str1 = '你好'
str2 = '世界'
str3 = str1 + str2

print(str3)

>>>你好世界
```

####重复字符串

```python

str1 = '你好'
str2 = '世界'
str3 = str1 + str2

print(str3 * 3 )

>>>你好世界
>>>你好世界
>>>你好世界
```

####访问字符串中的某一个字符

通过索引下标查找字符，索引从0开始

```python
str1 = 'hello word,hello shanghai'
print(str1[1])
print(str1[-1])

>>>e
>>>i
```

####字符串的不可变性质

```python
str1 = 'hello word,hello shanghai'
str1[1] = 'a'
print(str1)

>>>TypeError: 'str' object does not support item assignment

```

####返回截取字符串中的一部分

语法 str[start:length:skip]

start表示从下表几开始，length表示截取长度，skip表示隔几位截取一次

```python
str1 = 'hello word,hello shanghai'
print(str1[0:7])     #从0开始取7个
print(str1[0::2])    #从0开始取全部，隔2个取一次
print(str1[::3])     #默认从0开始，隔3个取一次
print(str1[-10::2])  #从倒数第10个开始，隔2个取一次，如果是倒取得话，不能取指定长度


>>>hello w
>>>hlowr,el hnhi
>>>hlwdeohgi
>>>osaga
```
####返回翻转字符串结果

```python
str1 = 'hello word,hello shanghai'

print(str1[::-1])

>>>iahgnahs olleh,drow olleh

#翻转以后不影响原来的str1内存中的值，而是使用一次以后就被回收了
```

####返回去除的空格结果

```python

str1 = ' aleX '
print(str1.lstrip()) #left strip  去除左边的空格
print(str1.rstrip()) #right strip  去除右边的空格
print(str1.strip())  #strip 去除两边的空格


```
####判断是不是以什么开头

```python

str1 = 'abcde'

print(str1.startswith('ab')) #结果正确返回布尔值

>>>True
```

####判断以什么结尾

```python

str1 = 'abcde'

print(str1.endswith('de')) #结果正确返回布尔值

>>>True


>>>True
```

####返回替换字符

语法：str. replace(i,j,k)

i代表被替换字符，j代表准备替换的字符，k代表替换的次数，替换的方向是自左向右去查找

```python

str1 = 'abcdeabcd'

print(str1.replace('a','A'))
print(str1)

>>>AbcdeAbcd
>>>abcdeabcd

#默认替换所有的
```

```python

str1 = 'abcdeabcd'

print(str1.replace('a','A'，1))
print(str1)

>>>Abcdeabcd
>>>abcdeabcd

#替换了一次
```


####返回分割字符

语法：str.split(i,k)

i代以什么为分割符的，k代表分割次数，分割自左向右运行,返回一个`列表（类型）`后面会学习到,被设定为分隔符的字符不会出出现在列表中。

```python

str1 = 'abcdeabcd'

print(str1.split('d'))

>>>['abc', 'eabc', '']

#默认全部分割
```


```python

str1 = 'abcdeabcd'

print(str1.split('d'，1))

>>>['abc', 'eabcd']

#添加第二个参数，分割一次
```

####返回全大写

```python

str1 = 'abcdeabcd'

print(str1.upper())

>>>ABCDEABCD
```
####返回全小写


```python

str1 = 'ABCDEABCD'

print(str1.lower())

>>> abcdeabcd
```

####返回首字母大写

```python

str1 = 'abcdabcd'

print(str1.capitalize())

>>>Abcdabcd
```

```python

str1 = 'ABCDABCD'

print(str1.title())

>>> Abcdabcd
```

```python
str1 = 'abcdabcd'

print(str1[0].upper()+str1[1:])

>>> Abcdabcd

```

####返回首字母小写

```python

str1 = 'ABCDABCD'

print(str1[0].lower()+str1[1:])

>>>aBCDABCD
```

####判断是否是全大写

返回布尔值,如果是空字符串返回False

```python
str1 = 'ABCDABCD'

print(str1.isupper())

>>>Ture
```

####判断是否是全小写

返回布尔值,如果是空字符串返回False

```python
str1 = 'abcdabcd'

print(str1.islower())

>>>Ture
```

####判断首字母大写

返回布尔值,如果是空字符串返回False

但是python没有给我们提供iscapitalize()的方法

```python
str1 = 'Abcdabcd'

print(str1.istitle())

>>>Ture

```

####返回以什么分割的字符

语法：'i'.jion(j)

i代表分割的符号，j代表被分割的字符

```python
str1 = 'abcdabcd'

print(','.join(str1))

>>>a,b,c,d,a,b,c,d

#以逗号分割
```

###【5】占位符

为什么需要占位符，因为变量在引号里面会被看成一个字符串，那么python就不会解析。

语法格式：

```python

'字符串 %s' % 变量或'字符'

'字符串%s %d %f'%(变量1，变量2，变量3)

```


python的占位符包括：

```python

%s   #代表str

%d   #代表int

$f   #代表float

```

####打印字符串

```python
num = 'Tom'
print ("His name is %s"%num)

>>>His name is Tom

#如果变量里面是个数字那么使用了%s也会解析成字符
```

####打印整数

```python
num = 2
print ("1 +1 = %d"%num)

>>>1 +1 = 2

#如果变量里面是个字符串那么使用了%d会 报类型错
```
####打印浮点数

```python
num = 2.5
print ("1.5 +1 = %f"%num)

>>>1.5 +1 = 2.500000

#如果变量里面是个字符串那么使用了%f会 报类型错,如果是整数会自动转换成浮点数
```

####打印浮点数（指定保留小数点位数）

语法：'字符串 %1.1f' % 变量

```python
num = 2.5
num1 = 16.5
print ("1.5 +1 = %.1f"%num)
print ("15.5 +1 = %0.2f"%num1)

>>>1.5 +1 = 2.5
>>>15.5 +1 = 16.50

#如果是整数相加，并且使用%.0f，那么会四舍五入
#双进度的不会影响整数部分
```

<font color='red'>注意：</font>

python 在四舍五入的时候会出现奇怪的问题,0.5问题，整数部分为偶数，0.5则被舍去，整数部分为奇数，0.5则进1，这只是单精度的浮点数问题。


```python
num1 = 1.5
num2 = 2.5
num3 = 3.5
num4 = 4.5

print ("0.5 +1 = %.0f"%num1)
print ("1.5 +1 = %.0f"%num2)
print ("2.5 +1 = %.0f"%num3)
print ("3.5 +1 = %.0f"%num3)

>>>0.5 +1 = 2
>>>1.5 +1 = 2
>>>2.5 +1 = 4
>>>3.5 +1 = 4
```
####双进度的浮点数问题(了解)

双进度的浮点问题和但进度不一样

python的 BigDecimal.ROUND_HALF_UP与ROUND_HALF_DOWN机制(了解)

```python
由于 python3 包括python2.7 以后的round策略使用的是decimal.ROUND_HALF_EVEN 
即Round to nearest with ties going to nearest even integer. 也就是只有在整数部分是奇数的时候， 小数部分才逢5进1； 偶数时逢5舍去。 这有利于更好地保证数据的精确性， 并在实验数据处理中广为使用。

但如果一定要decimal.ROUND_05UP 即Round away from zero if last digit after rounding towards zero would have been 0 or 5; otherwise round towards zero. 也就是逢5必进1需要设置float为decimal.Decimal, 然后修改decimal的上下文
```


```python

import decimal
context=decimal.getcontext() # 获取decimal现在的上下文
context.rounding = decimal.ROUND_05UP

print(round(decimal.Decimal(2.55), 1)) # 2.6
print(format(decimal.Decimal(2.55), '.1f')) #'2.6'
print ("3.5 +1 = %.0f"%decimal.Decimal(2.55)) #3

```
####指定占位符宽度

```python

print ("Name:%10s Age:%8d Height:%8.2f"%("Aviad",25,1.83))

```


####指定占位符宽度（左对齐）

左对齐就是在%后面加-

```python

print ("Name:%-10s Age:%-8d Height:%-8.2f"%("Aviad",25,1.83))

```

####指定占位符（只能用0当占位符）

如果坚持用其它的字符或数字作占位符，那么输出的时候为空

```python

print ("Name:%-10s Age:%08d Height:%08.2f"%("Aviad",25,1.83))

```

####科学计数法(以前提过)

```python

format(0.0015,'.2e')

```

##条件分支

大家在前面的学习已经接触过if-else了，它就是一个条件分支。

比如在网络游戏中，打在在NPC领取任务，在领取任务的时候都会给你几个选择或者是退出，那它是怎么实现的了，就是通过`条件分支`

我们先来个小游戏

规则：给你一个随机数字，你猜到就夸你一句，你猜错了讽刺就你一句；

```python

#首先我们引入随机库
from random import randint

ran = randint(1,100)  

guess =  int(input("你猜猜我有几根手指："))   #用户输入的数字传递进来以后默认是字符串，所以要转成int

if guess == ran:
    print("Y*^_^*Y 哇你猜对了 给你一个😘")
else:
    print("你可真笨👎")

```

##while循环

循环对于一般人是很难理解的。比如游戏，超级玛丽，当你挂了，游戏会重新开始，而且规定了你有几次从新开始的机会，这就是while循环。

但是这次你要是猜不对就要一直猜

但是我们要给点提醒

while结合if-else小案例

```python

res = 1234567

guess = int(input('猜一下中奖号码：'))

while guess != res:

    guess = int(input('不对不对，再猜,再猜：'))

    if guess == res:
        print("Y*^_^*Y 哇你猜对了 ")
        print('不过毛都没有！')
        exit()
    else:
        print('在用两块钱试试')

print("(*@ο@*) 哇～这么厉害一次就猜对了！！！")

```
不过else还可以和while配合使用：

```python

count = 0
while count < 5:
   print(count, " 小于5")
   count = count + 1
else:
   print (count, " 不小于5 ")
   
#在条件不满足时触发else
```

###str = r'C:\Program Files\FishC\Good\'
如果非要在原始字符串结尾输入反斜杠，如何可以灵活处理？

```python

str1 = r'C:\Program Files\FishC\Good'"\\"
print(str1)

```

##作业：
###使用while循环实现输出2-3+4-5+6.....+100的和
###当天代码敲一遍
###熟练掌握今天的内容
###判断输入的数字是不是回文


