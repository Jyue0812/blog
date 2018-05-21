#Lesson 10
___
##第十四章
###给大家介绍“对象”

现代的编程语言里面无处不提到对象的，然而初学者并不知道什么是对象，那我们下面一点一点的剖析：

我们之前所学习的编程方式都属于面向过程，什么是面向过程了？

```python
1)自上而下顺序执行，逐步求精；
2)其程序结构是按功能划分为若干个基本模块，这些模块形成一个树状结构；
3)各模块之间的关系尽可能简单，在功能上相对独立；
4)每一模块内部均是由顺序、选择和循环三种基本结构组成；
5)其模块化实现的具体方法是使用子程序。
6)程序流程在写程序时就已决定。
```

那么面向对象是什么样的了？

```python

1)把数据及对数据的操作方法放在一起，作为一个相互依存的整体——对象。
2)对同类对象抽象出其共性，形成类。
3)类中的大多数数据，只能用本类的方法进行处理。
4)类通过一个简单的外部接口与外界发生关系，对象与对象之间通过消息进行通信。
5)程序流程由用户在使用中决定。

```

理解面向对象：

```python

1)面向对象是相对面向过程而言
2)面向对象和面向过程都是一种思想
3)面向过程
	强调的是功能行为
	关注的是解决问题需要哪些步骤 
4)面向对象
	将功能封装进对象，强调具备了功能的对象
	关注的是解决问题需要哪些对象 
5)面向对象是基于面向过程的。

```

我们说把大象塞进冰箱：

 ![理解](images\理解.png)


在我们显示生活中我们如何运用面向对象的了？

比如说打电话：

我们会想到手机：手机有品牌，下面有型号，还要分配制，手机的最大功能是打电话......

比如说驾驶

我们会想到汽车: 汽车一样有品牌，系列，配制。汽车的主要功能就是行驶......

面向对象的特点：

```python
1)是一种符合人们思考习惯的思想
2)可以将复杂的事情简单化
3)将程序员从执行者转换成了指挥者

4)完成需求时：
	先要去找具有所需的功能的对象来用。
	如果该对象不存在，那么创建一个具有所需功能的对象。

```

 ![比较](images\比较.png)


我们讲到面向对象了，就离不开类，函数把普通的代码块打包，而现在又出现了一个类，它可以把函数打包。

类和对象的关系怎么理解，我们说的“汽车”，这个范围很大，它就是类，因为它们是一类的东西。比如说 宝马 5系 528 它就是对象，因为对象是实际存在的东西。

####类的定义

```python
1）生活中描述事物无非就是描述事物的名称/属性和行为。
	如：人有身高，体重等属性，有说话，打架等行为。
2）Python中用类来描述事物也是如此
	属性：对应类中的成员变量。
	行为：对应类中的成员方法。
3）定义类其实在定义类中的成员(成员变量和成员方法)
 	拥有相同（或者类似）属性和行为的对象都可以抽像出一个类
```

####类的设计

```python
只关心3样东西
	事物名称（类名）：人（Person）
	属性：身高（height）、年龄（age）
	行为（功能）：跑（run）、打架（fight）
```

###【1】类：对象=属性 + 方法

我们命名方法：

在类里面的变量改口叫属性，函数叫方法。

```python
类名：见名之意，首字母大写，其他遵循驼峰原则
属性：见名之意，其他遵循驼峰原则
行为(方法/功能)：见名之意，其他遵循驼峰原则
```

我们定义第一个类,一个人的类：

```python

#  object:基类，超类，所有类的父类，一般没有合适的父类就写object
class Peroson(object):
    # 定义属性(定义变量)
    name = "tom"
    age = 25
    height = 175
    sex = 'male'

    # 定义方法(定义函数)
    # 注意：方法的参数必须以self当第一个参数
    # self代表类的实例(某个对象)，默认是自己(当前类)
    def run(self):
        print("run")

    def eat(self, food):
        print("eat" + food)

P = Peroson();  #创造一个人 对象
print(P)
P.run()
print(P.name)

#<__main__.Peroson object at 0x103b1f908>
#run
#tom
```
以上代码就是一个'人'的类，定义了它的属性`name,age,height,sex`,它的行为`run()，eat()`。

有了类就可以创造对象，`P = Peroson()`就是创建一个对象，这个对象就是这个这个类的实例，也叫实例对象。


###【2】实例化多个对象

我们刚才在上面只实例化了一次，我们再实例化一个看看

```python

 #            object:基类，超类，所有类的父类，一般没有合适的父类就写object
class Peroson(object):
    # 定义属性(定义变量)
    name = ""
    age = 0
    height = 0
    weight = 0

    # 定义方法(定义函数)
    # 注意：方法的参数必须以self当第一个参数
    # self代表类的实例(某个对象)
    def run(self):
        print("run")

    def eat(self, food):
        print("eat" + food)

P1 = Peroson()
print(id(P1))
P2 = Peroson()
print(id(P2))

#4363254136
#4363254192
```

我们看上面的例子可以发现实例化两次，两个存储的id不一样，这个就好比是，P1 = 1，P2 = 2一样，每次实例一次都是一个新的对象，就是新的‘人’，这个当然你可以通过想象，两个人不可能一样。


###【3】访问对象的属性和方法

访问属性

```python
语法： 对象名.属性名

赋值： 对象名.属性名 = 新值
```

我们看下面这个例子：

```python
class Person(object):
    name = ''
    age = 0
    height = 0
    sex = ''
    def openDoor(self):
        print("我已经打开了冰箱门")

    def fillEle(self):
        print("我已经把大象装进冰箱了")

    def closeDoor(self):
        print("我已经关闭了冰箱门")

    def myinfo(self):
        print(self.__dict__)


P = Person()
#给这个人添加一些属性
P.name = 'tom'  
P.age  = 25
P.height = 175
P.sex = 'male'
print(P.name,P.age,P.height,P.sex)  #普通的访问
print(P.__dict__)  #对象.__dict__， 以dict的形式返回这个对象的属性

#tom 25 175 male
#{'name': 'tom', 'age': 25, 'height': 175, 'sex': 'male'}
```

调用方法

```python
语法： 对象名.属性名(参数列表)
```

看下面例子：

```python
class Person(object):
    name = ''
    age = 0
    height = 0
    sex = ''
    def openDoor(self,name):
        print("%s已经打开了冰箱门"%name)

    def fillEle(self,name):
        print("%s已经把大象装进冰箱了"%name)

    def closeDoor(self,name):
        print("%s已经关闭了冰箱门"%name)



P = Person()
P.name = 'tom'
P.age  = 25
P.height = 175
P.sex = 'male'
P.openDoor(P.name)
P.fillEle(P.name)
P.closeDoor(P.name)

#tom已经打开了冰箱门
#tom已经把大象装进冰箱了
#tom已经关闭了冰箱门
```

###【4】构造函数

目前来看我们所有创建的person的属性是一样的，这样有点不符合我们日常的逻辑。比如有些人有一些特质，我们可以把这个特质当做是他的一个属性，没有这个特质的人视为没有这个属性。

那我们用原来的知识点事是没有办法完成的，所以我们用构造函数来解决这个问题。

```python
构造函数：__init__(), 在创建类的时候回自动调用这个魔术方法
```
<font color='red'> 注意：类里面如果不写构造函数的话，会默认添加一个空的构造函数。</font>

空的构造函数:

```python
class Person(object):
    name = ''
    age = 0
    height = 0
    sex = ''
    def openDoor(self,name):
        print("%s已经打开了冰箱门"%name)

    def fillEle(self,name):
        print("%s已经把大象装进冰箱了"%name)

    def closeDoor(self,name):
        print("%s已经关闭了冰箱门"%name)
    def __init__(self):
        pass

P = Person()
```
那我们用`__init__()`结合dict动态创建属性

`__dict__`是以字典的形式返回当前对象的所有属性和值。

```python
class Person(object):

    def openDoor(self,name):
        print("%s已经打开了冰箱门"%name)

    def fillEle(self,name):
        print("%s已经把大象装进冰箱了"%name)

    def closeDoor(self,name):
        print("%s已经关闭了冰箱门"%name)

    def __init__(self, **params):  #收集参数过来的是一个dict
        for key,val in params.items():
            self.__dict__[key]=val

P = Person(name = 'tom',age = 25)
print(P.__dict__)

#{'name': 'tom', 'age': 25}
```
这种方法就是玩，在实际开发中熟悉都是定义好的。

####【5】self是什么

我们发现每个方法里都有一个self，其实很多语言都有类似self的用法，python的`self`相当C++的this指针。

self代表当前实例，谁调用它，他就是谁。也就是那个对象。它自能在类里面使用。

`self.__class__`代表本类名。

```python

class Person(object):
    '''这是一个人的类'''
    def __init__(self, **params):  #收集参数过来的是一个dict
        for key,val in params.items():
            self.__dict__[key] = val

    def openDoor(self,name):
        print("%s已经打开了冰箱门"%name)

    def fillEle(self,name):
        print("%s已经把大象装进冰箱了"%name)

    def closeDoor(self,name):
        print("%s已经关闭了冰箱门"%name)


    def printVar(self):
        print(self.name)
        print(self.__class__)
        print(self.__doc__)

P = Person(name = 'tom',age = 25)
P.printVar()

P1 = Person(name = 'jack',sex = 'male')
P1.printVar()

#tom
#class '__main__.Person'>
#这是一个人的类
#jack
#<class '__main__.Person'>
#这是一个人的类
```

self 它不是关键字，但是在指定对象使用self的准确性确实很棒。

###【6】析构函数

析构函数`__del__()`  释放对象的时候自动调用的

理论上我们内存堆区的内存需要去手动的去开辟，手动的去释放的。但是python自己有垃圾回收机制，比如说那个对象不用了，python会自己把它释放掉，这是引用记录器的原理。

当程序执行结束了会自动释放。

我们看下面的例子：

```python

class Person(object):
    '''这是一个人的类'''
    def __init__(self, **params):  #收集参数过来的是一个dict
        for key,val in params.items():
            self.__dict__[key] = val

    def openDoor(self,name):
        print("%s已经打开了冰箱门"%name)

    def fillEle(self,name):
        print("%s已经把大象装进冰箱了"%name)

    def closeDoor(self,name):
        print("%s已经关闭了冰箱门"%name)
	
	def __del__(self):
        print(self.name,'释放')

P1 = Person(name= 'P1', age= 25)

#del P1

#在函数里定义的对象，会在函数结束时自动释放，这样可以用来减少内存空间的浪费
def func():
    P2 = Person(name= 'P2',sex= 'male')

func()

#while是死循环，这样的话程序没有结束，内存不会释放
while 1:
    pass

```

###【7】`__repr__`和`__str__`函数

这两个信息是将类的信息重写的魔术方法或者说魔法方法。

```python
重写：将函数重写定义写一遍

__str__():在调用print打印对象时自动调用，是给用户用的，是一个描述对象的方法。
__repr__()：是给机器用的，在Python解释器里面直接敲对象名在回车后调用的方法
注意：在没有str时，且有repr,str = repr

```

我们一般在打印一个类的时候，只能得到一个类信息，我们修改一下用上面的那个例子：

```python

class Person(object):
    '''这是一个人的类'''
    def __init__(self, **params):  #收集参数过来的是一个dict
        for key,val in params.items():
            self.__dict__[key] = val

    def openDoor(self,name):
        print("%s已经打开了冰箱门"%name)

    def fillEle(self,name):
        print("%s已经把大象装进冰箱了"%name)

    def closeDoor(self,name):
        print("%s已经关闭了冰箱门"%name)


P = Person(name= 'P', age= 25)

print(P)

#<__main__.Person object at 0x103d1f828>
```
现在我们str来重写它：

```python
#我们现在的需求是打印类名就可以得到属性值

class Person(object):
    '''这是一个人的类'''
    def __init__(self, **params):  #收集参数过来的是一个dict
        for key,val in params.items():
            self.__dict__[key] = val

    def openDoor(self,name):
        print("%s已经打开了冰箱门"%name)

    def fillEle(self,name):
        print("%s已经把大象装进冰箱了"%name)

    def closeDoor(self,name):
        print("%s已经关闭了冰箱门"%name)

    def __str__(self):
        return '这是一个构造人的类'


P = Person(name= 'tom', age= '25',sex= 'male')

print(P)

#这是一个构造人的类
```

<font color='red'>注意：返回的类型只能是字符类型的，是其它类型的就报错</font>

###【8】访问限制

访问限制就是不让变量在外部被访问，也就是私有属性。

一般编程语言都有public(公共的)和private(私有的)和protected(受保护的)关键字，但是python没有类似的关键字来进行修饰。

为了实现类似的私有变量的特性，python内部采用了name mangling(名字改遍)的技术，只用在变量或者函数的名字前加上了“__“两个下划线，那么函数和变量就变成了私有的,在外部是找不到的。

```python
class Person(object):
    def __init__(self,name):
        self.__name= name

    def getName(self):
        print(self.__name)

P = Person('tom')
#P.getName()   #这是在内部访问的
print(P.__name)

#AttributeError: 'Person' object has no attribute '__name'
```
私有的变量只能在本类里面使用。但是python是 名字改编，就是对变量名动一下手脚而已，实际上在外部你使用”_类名__变量名“就可以访问到私有的变量了：

```python
class Person(object):
    def __init__(self,name):
        self.__name= name

    def __getName(self):
        print(self.__name)

P = Person('tom')
print(P._Person__name)
P._Person__getName()

#tom
#tom
```
注意：Python目前的私有机制是伪私有，Python的类没有权限这么一说，所有的方法和属性都可以被外部调用。

###【8】继承

我们发现每个`class 类名（object）`的小括号里面都有一个object，它是什么了？

直接继承object类的类在某种程度上可以理解为是顶级类。这个小括号可以不带，object也可以不写，它会默认该类是顶级类。那么这个object就是父类或者是基类或超类。

那什么是继承了？比如说你可以继承你父母的财产，那么类也可以，它是拟人化的，它也可以有父类，但是没有母类这一说法，这比较像西方的文化。



```python
class Person:
    Walk = 1
    
    def __init__(self):
        print('我是一个人')        

    def __str__(self):
        print('我是人类')

    def eat(self):
        return '我会吃东西'

    def createHuman(self):
        return '创造了一个人类'

    def walkAbout(self):
        return '我走动了%d步'%self.Walk



class Student(Person):
    def __init__(self):
        print(self.eat(),self.walkAbout())


S = Student()
print(Student)

#我会吃东西 我走动了1步
#<class '__main__.Student'>
```
通过上面的例子发现父类的`__init__`和`__str__`没有被自动调用,因为自己有一个`__init__`和`__str__`,所以父类的构造函数是不能自己调用的。那怎么调用了？

如果你想调用的话也是可以的，自己手动去调用。

但是，你不能使用`self.__init__`,这样会报错的。使用一个新的函数`super()`：

```python
class Person:
    Walk = 1
    def __init__(self):
        print('我是一个人')

    def __str__(self):
        return '我是人类'

    def eat(self):
        return '我会吃东西'

    def createHuman(self):
        return '创造了一个人类'

    def walkAbout(self):
        return '我走动了%d步'%self.Walk



class Student(Person):
    def __init__(self):
        print(self.eat(),self.walkAbout())
        super().__init__()

    def __str__(self):
        return super().__str__()


S = Student()
print(S)

#我会吃东西 我走动了1步
#我是一个人
#我是人类

```

super()函数能够自动去寻找父类的方法，而且还为我们传入父类的self参数，这样就不需要做这些事情了。


这样看可能更加直观：

```python
class Person(object):
    Walk = 1

    def __init__(self):
        print('我是一个人')

    def __str__(self):
        return '我是人类'

    def eat(self):
        return '我会吃东西'

    def createHuman(self):
        return '创造了一个人类'

    def walkAbout(self):
        return '我走动了%d步'%self.Walk

    def secret(self):
        print("it's a secret")


class Father(Person):

    def __init__(self):
        print('我是你的父亲')

    def __str__(self):
        return '我是你爸爸'

    def eat(self):
        return '我喜欢吃排骨'

    def createHuman(self):
        return '创了你'

    def walkAbout(self):
        return '我走动了%d步'%self.Walk

    def secret(self):
        print("我只是藏了私房钱")


class Student(Father):
    def __init__(self):
        print( super().eat(),super().walkAbout())
        super().__init__()
        super().secret()     

    def __str__(self):
        return '我是学生'

    def eat(self):
        return '我喜欢吃辣条'

    def createHuman(self):
        return '我还小'

    def walkAbout(self):
        return '我走动了%d步' % self.Walk

    def secret(self):
        print("我上课偷偷玩手机")


S = Student()
print(S)

#我喜欢吃排骨 我走动了1步
#我是你的父亲
#我只是藏了私房钱
#我是学生
```

上面这个例子可以看出，Student使用super()，只调用了父类属性和方法。

那么不喜欢父类的属性和方法，我就是要调用爷爷或者在往上的层级，那怎么用了？

调用父级以上的层级

```python
语法  父类名.调用方法(self)
```

```python

class Person(object):
    Walk = 1

    def __init__(self):
        print('我是一个人')

    def __str__(self):
        return '我是人类'

    def eat(self):
        return '我会吃东西'

    def createHuman(self):
        return '创造了一个人类'

    def walkAbout(self):
        return '我走动了%d步'%self.Walk

    def secret(self):
        print("it's a secret")


class Father(Person):

    def __init__(self):
        print('我是你的父亲')

    def __str__(self):
        return '我是你爸爸'

    def eat(self):
        return '我喜欢吃排骨'

    def createHuman(self):
        return '创了你'

    def walkAbout(self):
        return '我走动了%d步'%self.Walk

    def secret(self):
        print("我只是藏了私房钱")


class Student(Father):
    def __init__(self):
        print( Person.eat(self),Person.walkAbout(self))
        Person.__init__(self)
        Person.secret(self)      #调用指定的层级

    def __str__(self):
        return '我是学生'

    def eat(self):
        return '我喜欢吃辣条'

    def createHuman(self):
        return '我还小'

    def walkAbout(self):
        return '我走动了%d步' % self.Walk

    def secret(self):
        print("我上课偷偷玩手机")


S = Student()
print(S)

#我会吃东西 我走动了1步
#我是一个人
#it's a secret
#我是学生
```
那么用`Person().eat()`可以吗？

也可以但是这样算是实例化在调用了，每次实例化都会调用一次`__init__`这样会达不到预期的效果。

###【9】多继承

很多的语言都是不支持多继承的，比如php、java、C，它们都只能模拟多继承，通过interface（接口）来模拟，但是python直接就可以多继承。

这里你继承你老爸和你老叔的房子为例：

```python


class Father(object):
    F_house = 2

class Uncle(object):
    U_house = 3

class MeMe(Father,Uncle):
    def __init__(self):
        print(self.F_house + self.U_house)
MeMe()

#5    
```
但是有个问题，如果两个父类方法的属性名重复，方法名重复会怎么办样


```python

class Father(object):
    house = 2

class Uncle(object):
    house = 3

class MeMe(Father,Uncle):
    def __init__(self):
        print(self.house + super().house)
MeMe()

#4
```

不管是继承下来的，还是父类找到的都是`Father`这个类的属性，不是名字的关系，是优先选择排在小括号`MeMe(Father,Uncle)`前面的那个类。

解决方案，直接使用类名：

```python

class Father(object):
    house = 2
    def money(self):
        return 10000000

class Uncle(object):
    house = 3
    def money(self):
        return 10000000

class MeMe(Father,Uncle):
    def __init__(self):
        print(Father.house + Uncle.house)
        print(Father.money(self) + Uncle.money(self))
MeMe()

#5
#20000000
```
<font color='red'>注意：多继承有个菱形继承陷阱，看下面例子：</font>

D的两个父类(B,C)都继承了A类，这样的话就形成了代码的冗余，继承等于在内存的堆区里面把父类的所有东西都拷贝一份然后在保存在另外一个堆区。

```python

class A():
    def __init__(self):
        print("进入A…")
        print("离开A…")


class B(A):
    def __init__(self):
        print("进入B…")
        A.__init__(self)
        print("离开B…")


class C(A):
    def __init__(self):
        print("进入C…")
        A.__init__(self)
        print("离开C…")


class D(B, C):
    def __init__(self):
        print("进入D…")
        B.__init__(self)
        C.__init__(self)
        print("离开D…")

D()
```



 ![菱形](images\菱形.png)

多重继承容易导致钻石继承的问题，上面代码实例化D类后我们发现A被前后进入了两次，有的人会说无所谓，我女朋友都不止了......

这有什么危害了，比如说A类有个`time.sleep(60)`，每次都进去是不是运行的非常慢，而且还非常的耗费效率。

你可以使用python的 方法解析顺序(MRO),这个使用C3算法，反正很复杂，就是说在避免一个类被多次调用的前提下，使用广度优先和从左到右的原则去寻找需要的属性和方法。


不管怎么样`object`都是金字塔的顶层

```python
print(D.__mro__)

(<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)
```

我们可以只取一个类的`__init__`，或者说使用super(),它会默认取小括号前面一个类的内容：

```python

class A():
    def __init__(self):
        print("进入A…")
        print("离开A…")


class B(A):
    def __init__(self):
        print("进入B…")
        super().__init__()
        print("离开B…")


class C(A):
    def __init__(self):
        print("进入C…")
        super().__init__()
        print("离开C…")


class D(B, C):
    def __init__(self):
        print("进入D…")
        super().__init__()
        print("离开D…")
D()
```

<font color='red'>所以使用多继承要小心！！！</font>


##作业人开枪射击子弹

三个条件，人，枪，弹夹
