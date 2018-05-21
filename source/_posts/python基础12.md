#Lesson 12
___
##第十四章
###【9】描述符(property的原理)
此前提到过property()函数，现在我们来剖析一下它是怎么实现的。

描述符(descriptor)，用一句话来解释，描述符就是将某种特殊类型的类的实例指派给一个类的属性，那什么是特殊类型的类了？就是至少要在这个类中定义了`__get__()`、`__set__()`、`__delete__()`三个特殊方法中的任意一个。

|魔术方法                      |含义                               |
|-----------------------------|----------------------------------|
|__get__(self,instance,owner) |     用于访问它的属性，它返回属性的值  |
|__set__(self, instance,value)| 将在属性分配操作中调用，不返回任何内容 |
|__delete__(self,instance)    |       控制删除操作，不返回任何内容    |

instance表示实例对象，owner是所有者的类。

descriptor的实例自己访问自己是不会触发__get__，而会触发__call__，只有descriptor作为其它类的属性才有意义。

举个例子：

```python
class MyDescriptor:
    def __get__(self, instance, owner):
        return '__get'
    def __set__(self,instance,value):
        return '__set__'
    def __delete__(self, instance):
        return '__delete__'

class Test:
    x = MyDescriptor()

test = Test()

print(test.x)

#__get
```

上面的例子MyDescriptor实现了方法`__get__()`、`__set__()`、`__delete__()`，并且将它的类实例指派给Test类的属性里面，所以MyDescriptor就是所谓的描述符类。

在调用x属性的时候，它会自动调用`__get__()`属性，那么在从新赋值和删除都是一样的了。

那我们封装自己的property方法。

```python
class MyProperty:
    def __init__(self, fget=None, fset=None, fdel=None):
        self.fget = fget
        self.fset = fset
        self.fdel = fdel

    def __get__(self, instance, owner):
        return self.fget(instance)

    def __set__(self, instance, value):
        self.fset(instance, value)

    def __delete__(self, instance):
        self.fdel(instance)



class Test:
    def __init__(self):
        self._x = None

    def getX(self):
        return self._x

    def setX(self, value):
        self._x = value

    def delX(self):
        del self._x

    x = MyProperty(getX, setX, delX)

test = Test()
#获取
print(test._x)
#设置
test.x = 'tom'
print(test._x)
#删除成功
del test._x

#None
#tom
```

###【10】网上银行系统

见网上银行系统文件夹。

模拟网上银行系统，由于现在我们没有任何的数据库和缓存系统，我们所有的记录都要保存在文件中。



#第十五章
##高阶函数的使用
###【1】reduce()函数

reduce函数和我们之前学习的map函数类似。

reduce也是接受两个参数，一个函数f，一个list，但行为不同，reduce()传入的函数 f 必须接收两个参数，reduce()对list的每个元素反复调用函数f，并返回最终结果值。

例如，编写一个f函数，接收x和y，返回x和y的和：

```python
from functools import reduce
def f(x, y):
    return x + y
reduce(f, [1, 3, 5, 7, 9])
```
调用 reduce(f, [1, 3, 5, 7, 9])时，reduce函数将做如下计算

```python
先计算头两个元素：f(1, 3)，结果为4；
再把结果和第3个元素计算：f(4, 5)，结果为9；
再把结果和第4个元素计算：f(9, 7)，结果为16；
再把结果和第5个元素计算：f(16, 9)，结果为25；
由于没有更多的元素了，计算结束，返回结果25。
```

上述计算实际上是对 list 的所有元素求和。虽然Python内置了求和函数sum()，但是，利用reduce()求和也很简单。

reduce()还可以接收第3个可选参数，作为计算的初始值。如果把初始值设为100，计算：

```python
reduce(f, [1, 3, 5, 7, 9], 100)
```

结果将变为125，因为第一轮计算是：

计算初始值和第一个元素：f(100, 1)，结果为101。

###【2】sorted()函数

sorted函数是python的内置函数，和sort差不多，只不过sort是list的方法而已。

```python

#普通排序
list1 = [4,7,2,6,3]
list2 = sorted(list1)#默认升序排序
print(list1)
print(list2)

#按绝对值大小排序
list3 = [4,-7,2,6,-3]
#key接受函数来实现自定义排序规则
list4 = sorted(list3, key=abs)
print(list3)
print(list4)

#降序
list5 = [4,7,2,6,3]
list6 = sorted(list5, reverse=True)#默认升序排序
print(list5)
print(list6)

#函数可以自己写
#按照字符的长短排序
def myLen(str):
    return len(str)
list7 = ['b333','a1111111','c22','d5554']
list8 = sorted(list7,key=myLen)#默认升序排序
print(list7)
print(list8)

```

###【3】冒泡排序

```python
array = [1,2,3,6,5,4]
num = 0
for i in range(len(array)):
    for j in range(i):
        num += 1
        if array[j] > array[j + 1]:
            array[j], array[j + 1] = array[j + 1], array[j]
print(array,num)

# 0.0
#
# 0.0
# 0.1
#
# 0.0
# 0.1
# 0.2
#
# 0.0
# 0.1
# 0.2
# 0.4
#
# 0.0
# 0.1
# 0.2
# 0.4
# 0.5

#[1, 2, 3, 5, 4, 6] 15
```

while循环的：

```python

array = [1, -2, 4, 7, 6, 3, 2, 3]
tmp = ''
start = 0

if len(array) == 0 and len(array) == 1:
    print(array)
    exit()

for i in range(len(array)-1):
    while array[i+1] < array[i]:
        tmp = array[i+1]
        del array[i+1]
        array.insert(i,tmp)

print(array)

#[-2, 1, 4, 6, 3, 2, 3, 7]
```


###单元测试

####【4】函数的单元测试

unittest是一个python的单元测试框架。那么它是做什么的了？

作用：用来对一个函数、一个类或者一个模块来进行正确性校验工作

1、单元测试通过了，说明我们测试的函数是正常的

2、单元测试不通过，说明函数功能有BUG，要么测试条件输入有误

看下面的例子

```python


import unittest
from demo import mySum
from demo import mySub

#unittest是一个继承包
#继承unittest包的TestCase类
class Test(unittest.TestCase):
    def setUp(self):
        print("开始测试时自动调用")
    def tearDown(self):
        print("结束测试时自动调用")

    #为了测试mySum
    def test_mySum(self):
    #这是一个断言，继承testcase得到的第一个是调用的函数，第二个是值
        self.assertEqual(mySum(1,2), 3, "加法有误")
    def test_mySub(self):
        self.assertEqual(mySub(2,1), 1, "减法有误")


if __name__ == "__main__":
    unittest.main()
```

```python
#demo.py

def mySum(x, y):
    return x + y

def mySub(x, y):
    return x - y

print(mySum(1,2))
```

这是一个成功的案例那么我们让它失败：

```python
#demo.py

#我们在后面加上一个+1，这样结果就不相同了
def mySum(x, y):
    return x + y + 1

def mySub(x, y):
    return x - y

print(mySum(1,2))
```

再次运行

会报错，应为4 != 3 

```python
#Traceback (most recent call last):
#  File "/Users/ruidong/PycharmProjects/project/demo.py", line #15, in test_mySum
#    self.assertEqual(mySum(1,2), 3, "加法有误")
#AssertionError: 4 != 3 : 加法有误
```

<image src='images/TestCase.png'>

```python
一个TestCase的实例就是一个测试用例。什么是测试用例呢？就是一个完整的测试流程，包括测试前准备环境的搭建(setUp)，执行测试代码(run)，以及测试后环境的还原(tearDown)。元测试(unit test)的本质也就在这里，一个测试用例是一个完整的测试单元，通过运行这个测试单元，可以对某一个问题进行验证。

而多个测试用例集合在一起，就是TestSuite，而且TestSuite也可以嵌套TestSuite。

TestLoader是用来加载TestCase到TestSuite中的，其中有几个loadTestsFrom__()方法，就是从各个地方寻找TestCase，创建它们的实例，然后add到TestSuite中，再返回一个TestSuite实例。

TextTestRunner是来执行测试用例的，其中的run(test)会执行TestSuite/TestCase中的run(result)方法。

测试的结果会保存到TextTestResult实例中，包括运行了多少测试用例，成功了多少，失败了多少等信息。
```

###【5】对类进行单元测试

```python
import unittest
from person import Person

class Test(unittest.TestCase):
    def test_init(self):
        p = Person("hanmeimei", 20)
        self.assertEqual(p.name, "hanmeimei", "属性赋值有误")
    def test_getAge(self):
        p = Person("hanmeimei", 22)
        self.assertEqual(p.getAge(), p.age, "getAge函数有误")

if __name__ == "__main__":
    unittest.main()
```

```python
#person.py

class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.age  = age

    def getAge(self):
        return self.age
```

###【6】文档测试

检查是否

```python
import doctest
#doctest模块可以提取注释中的的代码执行
#doctest严格按照Python交互模式的输入提取
def mySum(x, y):
    '''
    get The Sum from x and Y
    :param x: firstNum
    :param y: SecondNum
    :return: sum
    注意有空格
    example:
    >>> print(mySum(1,2))
    3

    '''
    return x + y


print(mySum(2, 2))

#进行文档测试
doctest.testmod()
```