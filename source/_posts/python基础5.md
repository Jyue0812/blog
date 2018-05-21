#Lesson_5
——————
##第九章

###【1】元祖(牢笼中的的列表)
元祖 tuple

我们这里说的元祖不是那个赫赫有名的元祖零食、元祖蛋糕。

能力越大的人都有可能滥用权力，反而导致自身万劫不复。

同样，因为列表过于强大，python的作者发明了它的表亲---元祖。

元祖和列表的最大区别就是，元祖里面的数据是不可动的。

####访问和创建一个元祖

元祖和列表，除了不可变这个特征意外，那就是list用的中括号，tuple用的是小括号

```python

tuple1 = ()

tuple2 = (1,) #只有一个元素的时候一定要在结尾加上一个逗号，不加上逗号就是number

tuple3 = (1,2,3)

print('tuple1:',tuple1,type(tuple1))
print('tuple2:',tuple2,type(tuple2))
print('tuple3:',tuple3,type(tuple3))

#tuple1: () <class 'tuple'>
#tuple2: (1,) <class 'tuple'>
#tuple3: (1, 2, 3) <class 'tuple'>

```

另类定义：

```python

tuple1 = 1,  #number加上逗号就是tuple，不加就是数字

tuple2 = 1,2,3


print('tuple1:',tuple1,type(tuple1))
print('tuple2:',tuple2,type(tuple2))

#tuple1: (1,) <class 'tuple'>
#tuple2: (1, 2, 3) <class 'tuple'>
```

我们尝试一下不带逗号会怎么样：

```python
tuple1 = (1)

tuple2 = (1,)

print(tuple1 * 3)
print(tuple2 * 3)

#3
#(1, 1, 1)
```

访问tuple的索引和list是一样的：

```python
tuple1 = ((1,2,3),4,(5,6,7),[1,2,3])
#二维的元祖，可以嵌套多类型的数据

print(tuple1[0][0])
print(tuple1[1])
print(tuple1[3][2])

#1
#4
#3
```
tuple也是可以切片的：

```python
tuple1 = 1,2,3,4,5,6,7,8,9

print(tuple1[:5])  #从0开始取列表中钱5个元素
print(tuple1[-1])  #查找最后一个元素
print(tuple1[::2]) #隔2个查一次
print(tuple1[::-1]) #返回翻转的结果

#(1, 2, 3, 4, 5)
#9
#(1, 3, 5, 7, 9)
#(9, 8, 7, 6, 5, 4, 3, 2, 1)
```

tuple的元素是不可变的：

修改：

```python

tuple1 = 1,2,3,4,5,6,7,8,9

tuple1[0] = 0

print(tuple1)

#TypeError: 'tuple' object does not support item assignment
```

删除：

```python

tuple1 = 1,2,3,4,5,6,7,8,9

del tuple1[-1]

print(tuple1)

#TypeError: 'tuple' object does not support item assignment
```

####更新和删除元祖


#####修改

前面说过了，元祖的元素具有不可变性，那么有没有其它办法了？

我们可以通过合并的方式向元祖的尾部或者头部插入数据

```python

tuple1 = '成龙','李连杰','李小龙'

name1 = '梁小龙',  

name2 = '元彪','洪金宝'

tuple1 = tuple1 + name1 #通过拼接在重新赋值给 tuple1

tuple1 = name2 + tuple1

print(tuple1)


#('元彪', '洪金宝', '成龙', '李连杰', '李小龙', '梁小龙')

#注意：拼接只能是同类型之间拼接
```

得到结论，元祖要修改就必须要重新赋值。

#####删除元祖

删除元祖的元素我们在上面的内容已经尝试过了，是不可实现的。

元祖的删除和修改差不多，要删就全删。

```python

tuple1 = '成龙','李连杰','李小龙'

del tuple1

```


####返回指定值得下标

```python

tuple1 = '成龙','李连杰','李小龙'


print(tuple1.index('成龙'))

#0
```

####返回元祖的个数


```python

tuple1 = '成龙','李连杰','李小龙'

print(len(tuple1))

#3
```

####返回元祖中的最大值和最小值

```python

tuple1 = 1,2,3,4,5,6,7


print(max(tuple1))
print(min(tuple1))

#7
#1
```

####返回数组的和


```python

tuple1 = 1,2,3,4,5,6,7

tuple1 = 1,2,3,4,5,6,7

print(sum(tuple1))


#28
```

####将元祖转成列表

```python

tuple1 = 1,2,3,4,5,6,7

print(list(tuple1))

#[1, 2, 3, 4, 5, 6, 7]
```

####将其它类型转成tuple

```python

list1 = [1,2,3,4,5,6,7]

string = '123344'

print(tuple(list1))
print(tuple(string))

#(1, 2, 3, 4, 5, 6, 7)
#('1', '2', '3', '3', '4', '4')

#number 和 bool 类型的值是不可迭代的，所以不能转换
```

####元祖的遍历

```python

tuple1 = [1,2,3,4,5,6,7]

for i in tuple1:
    print(i)
```

###【2】string补充

字符串我们在前面的内容里面已经学过不少了，想必大家消化的差不多了，
我们今天再来一波新的用法。


####splitlines([keepends]) 多行分割

默认keepends = false的，表示不保留换行符

```python
str40 = '''sunck is a good man!
sunck is a nice man!
sunck is handsome man!
'''
print(str40.splitlines(True))

#['sunck is a good man!\n', 'sunck is a nice man!\n', 'sunck is handsome man!\n']

```

####max()、min()

max()、min(）可以判断字符串大小值

```python

str1 = "abcdefg!"
print(max(str1))
print(min(str1))

#g
#!
```

<image src='images/timg.jpeg'/>

####创建字符映射的转换表

str.maketrans(intab, outtab) 方法用于创建字符映射的转换表，对于接受两个参数的最简单的调用方式，第一个参数是字符串，表示需要转换的字符，第二个参数也是字符串表示转换的目标。

```python
str1 = str.maketrans("ac", "65")

print(str1)

#{97: 54, 99: 53}
```


####过滤字符映射

translate() 方法根据参数table给出的表(包含 256 个字符)转换字符串的字符,要过滤掉的字符放到 deletechars 参数中。

str.translate(table, deletechars) 

```python
table -- 翻译表，翻译表是通过 maketrans() 方法转换而来。
deletechars -- 字符串中要过滤的字符列表。

```
例如：

```python

intab = "aeiou"
outtab = "12345"
trantab = str.maketrans(intab, outtab)  # 制作翻译表

str = "this is string example....wow!!!"
print(str.translate(trantab))

#th3s 3s str3ng 2x1mpl2....w4w!!!

```

####编码

encode() 方法以 encoding 指定的编码格式编码字符串。errors参数可以指定不同的错误处理方案。

```python
encoding -- 要使用的编码，如"UTF-8"。

errors -- 设置不同错误的处理方案。默认为 'strict',意为编码错误引起一个UnicodeError。 其他可能得值有 'ignore', 'replace', 'xmlcharrefreplace', 'backslashreplace' 以及通过 codecs.register_error() 注册的任何值。
```
看个例子：

```python

str1 = "这是一个字符串"
#ignore忽略错误
data2 = str1.encode("utf-8", "ignore")
print(data2)
print(type(data2))

#解码  注意：要与编码时的编码格式一致
str3 = data2.decode("gbk", "ignore")
print(str3)


#b'\xe8\xbf\x99\xe6\x98\xaf\xe4\xb8\x80\xe4\xb8\xaa\xe5\xad\x97\xe7\xac\xa6\xe4\xb8\xb2'
#<class 'bytes'>
#杩欐槸涓涓瀛楃︿覆

```

####字符判断

#####isalpha()
如果字符串中至少有一个字符且所有的字符都是字母返回True,否则返回False

```python
str1 = "abcde"
print(str1.isalpha())

>>>True
```

#####isalnum()
如果字符串中至少有一个字符且所有的字符都是字母或数字返回True,否则返回False

```python

str1 = "1a2b3"
print(str1.isalnum())

>>>True
```

#####isspace()

如果字符中只包含空格则返回True,否则返回False

```python

print(" ".isspace())
print("      ".isspace())
print("\t".isspace())
print("\n".isspace())
print("\r".isspace())

```

###【3】字典(dict)

我们在翻开《新华字典》的时候想查一个字的时候，比如“万“，我们不会从‘a’到‘z’开始逐个查找，而是直接从‘w’开始，接着找wan这个发音，最终找个”万“字。

python中的字典类型会把‘wan’看着是 键（key）,”万“字看着是值（value），另外python中的 dict在有些地方称为哈希（hash），有些地方称为 关系数组，也和javascript 的轻量数据交换格式（json）是一样的。

用键-值(key-value)存储，具有极快的查找速度

<font color='red'>注意：字典是映射关系,字典不能被切片</font>

key的特性：

```python
1、字典中的key必须唯一
2、key必须是不可变对象
3、字符串、整数等都是不可变的，可以作为key
4、list是可变的，不能作为key
```

```python
字典是Python语言中唯一的映射类型。
映射类型对象里哈希值（键，key）和指向的对象（值，value）是一对多的的关系，通常被认为是可变的哈希表。
字典对象是可变的，它是一个容器类型，能存储任意个数的Python对象，其中也可包括其他容器类型。
字典类型与序列类型的区别：
1.存取和访问数据的方式不同。
2.序列类型只用数字类型的键（从序列的开始按数值顺序索引）；
3.映射类型可以用其他对象类型作键（如：数字、字符串、元祖，一般用字符串作键），和序列类型的键不同，映射类型的键直接或间接地和存储数据值相关联。
4.映射类型中的数据是无序排列的。这和序列类型是不一样的，序列类型是以数值序排列的。
5.映射类型用键直接“映射”到值。
字典是Python中最强大的数据类型之一。
```

#### 创建和访问dict

#####创建dict

字典在创建的时候必须是{'key':'value'}

```python

dict1 = {}
dict2 = {'name':'tom','sex':'male','age':25}
dict3 = dict()
print(dict1,type(dict1))
print(dict2,type(dict2))
print(dict3,type(dict3))

#{} <class 'dict'>
#{'name': 'tom', 'sex': 'male', 'age': 25} <class 'dict'>
#{} <class 'dict'>
```

#####访问dict

访问dict必须要指定它的`key`

```python

dict1 = {'name':'tom','sex':'male','age':25}

print(dict1['name'])

#tom
```

#####添加一个新的值

```python

dict1 = {'name':'tom','sex':'male','age':25}
dict1['height'] = '175cm'
print(dict1)

#{'name': 'tom', 'sex': 'male', 'age': 25, 'height': '175cm'}

```

#####修改指定的值

```python

dict1 = {'name':'tom','sex':'male','age':25}
dict1['age'] = '30'
print(dict1)

#{'name': 'tom', 'sex': 'male', 'age': '30'}
```

#####删除指定的值

```python

dict1 = {'name':'tom','sex':'male','age':25}

dict2 = dict1.copy()

dict3 = dict1.copy()

del dict1['age']        #直接删除

print(dict2.pop('sex')) #弹出一个指定的键，并返回被弹出的值

print(dict3.popitem())  #弹出最后一项，并返回被弹出的值

print(dict1)
print(dict2)
print(dict3)

#male
#('age', 25)
#{'name': 'tom', 'sex': 'male'}
#{'name': 'tom', 'age': 25}
#{'name': 'tom', 'sex': 'male'}
```
#####深度拷贝dict

```python

dict1 = {'name':'tom','sex':'male','age':25}

dict2 = dict1.copy()  

dict3 = dict1

dict1.pop('age')

print(id(dict1),dict1)
print(id(dict2),dict2)
print(id(dict3),dict3)

#4303185888 {'name': 'tom', 'sex': 'male'}
#4303185960 {'name': 'tom', 'sex': 'male', 'age': 25}
#4303185888 {'name': 'tom', 'sex': 'male'}
```

#####清除dict

dict.clear()

不管是list还是dict，清除都建议使用clear(),为什么了？举个例子

```python
dict1 = {'name':'tom','sex':'male','age':25}

dict2 = dict1

dict1 = {}

print(id(dict1),id(dict2))
print(dict1,dict2)

#4301088808 4301088736
#{} {'name': 'tom', 'sex': 'male', 'age': 25}
```

上面的例子中 dict1 = {} 并没有把内存中的值给去除， 而是从新定义了一个 空dict，把指针指向了另一个地址.

dict2是浅拷贝dict1的，那么原来的值还在内存中。这样做的弊端就是浪费内存的使用空间。

使用clear()试一下

```python
dict1 = {'name':'tom','sex':'male','age':25}

dict2 = dict1

print(id(dict1),id(dict2))  #这是清理之前的内存地址

dict1.clear()

print(id(dict1),id(dict2))

print(dict1,dict2)


#4301088736 4301088736
##4301088736 4301088736
{} {}
```

使用clear()以后两个被一起清理了，而且是在原内存空间上做清理的。

所以不论是list、dict都建议使用.clear()

#####修改dict

```python

dict1 = {'name':'tom','sex':'male','age':25}

dict1['age'] = 26

dict1.update(sex = 'female')

dict1['cname'] = '汤姆'       #指定key可以修改也可以添加

dict1.update(height = '170')  #height并不存在

print(dict1)

#{'name': 'tom', 'sex': 'female', 'age': 26, 'cname': '汤姆', 'height': '170'}

```

上面的例子我们能看出来.update()和指定key的效果是一样的，如果指定的 键值对 已经存在 则修改，不存在 则添加

<font color='red'>注意：update(key = ‘value’)中key是不带引号的，而value是带引号的，除非它是整数</font>

#####宽松访问

get()方法提供了更加合适的访问方式。

```python

dict1 = {'name':'tom','sex':'male','age':25}

print(dict1.get('age'))

print(dict1.get('height'))

print(dict1.get('height','not find'))

#25            找到对应的key则返回value
#None          没有找到key返回None
#not find      如果设置第二个参数，找到key返回对应的value，没有找到返回设定的默认值

```

相同的，可以用 in 和 not in 判断是否在dict里面，但是只能用key作为查找条件


```python
dict1 = {'name':'tom','sex':'male','age':25}

print('name' in dict1)

#True
```

#####其它方式创建dict

fromkeys()用于创建一个新的字典，它有两个参数，第一个参数是字典的 键 ，第二个参数是可选的，是传入键的对应值，第二个参数不写的话，值默认是None。

<font color='red'>注意：第一个参数必须是可迭代的序列，在我们python中可迭代的序列中有三种，str，list，tuple。而且它是返回一个新的字典，并不会改变原来的值</font>

```python

dict1 = {}
print(dict1.fromkeys('12','str'))
print(dict1.fromkeys([2,3],(1,2,3)))
print(dict1.fromkeys((5,6)))

#{'1': 'str', '2': 'str'}
#{2: (1, 2, 3), 3: (1, 2, 3)}
#{5: None, 6: None}
```

上面的例子告诉我们做事不能想当然，在第二个print()中并不会将(1,2,3)拆开，而是将他们当着一个值。

#####keys(),values(),items()

访问字典的方法还有keys(),values(),items()

keys()是返回字典中的所有键，values()是返回字典中的值，那么items()就是返回字典中的键值对。items()返回的是一个list，每个元素都是tuple。

```python

dict1 = {'name':'tom','sex':'male','age':25}

print(dict1.keys())
print(dict1.values())
print(dict1.items())

#dict_keys(['name', 'sex', 'age'])
#dict_values(['tom', 'male', 25])
#dict_items([('name', 'tom'), ('sex', 'male'), ('age', 25)])

```


课堂小作业：

list1 = [('name', 'tom'), ('sex', 'male'), ('age', 25)]

我们将list转换成dict，不使用dict()。

```python

list1 = [('name', 'tom'), ('sex', 'male'), ('age', 25)]

dict1 = {}

for each in list1:
    dict1[each[0]] = each[1]
print(dict1)

#{'name': 'tom', 'sex': 'male', 'age': 25}
```




###课后作业：

####dict支不支持一件多值？
####dict对key和value有没有类型限制了？
####目测dict1的运行结果是什么？
```python
>>> dict1.fromkeys((1, 2, 3), ('one', 'two', 'three')) 
>>> dict1.fromkeys((1, 3), '数字')
```
####尝试写一个用户登录的小程序














