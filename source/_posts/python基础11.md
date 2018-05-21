#Lesson 11
___
##十四章
###【10】组合模式
我们前面学习了继承的概念，然后又学习了多继承，但是多继承里面有很多的坑，不到逼不得已是不会使用的。那么就有了组合模式来避免这样的问题。


案例如下，水池里面有水和乌龟

```python
class Turtle(object):
    def __init__(self,n):
        self.num = n

class Fish(object):
    def __init__(self,n):
        self.num = n

class Pool(object):
    def __init__(self,x,y):

         self.turtle = Turtle(x)
         self.fish = Fish(y)

    def echo(self):
        print('水池里面有%d只乌龟，%d只小鱼'%(self.turtle.num,self.fish.num))


pool = Pool(1,10)
pool.echo()


#水池里面有1只乌龟，10只小鱼
```
组合模式了就是在类里面调用其它的类，然后加以使用。

###【11】对象属性和类属性


```python


class Person(object):
    # 这里的属性实际上属于类属性(用类名来调用)
    name = "person"
    def __init__(self, name):
        pass
        #对象属性
        self.name = name


print(Person.name)
per = Person("tom")
#对象属性的优先级高于类属性
print(per.name)
#动态的给对象添加对象属性
per.age = 18#只针对于当前对象生效，对于类创建的其他对象没有作用
print(Person.name)
per2 = Person("lilei")
#print(per2.age)  #没有age属性


#删除对象中的name属性，在调用会使用到同名的类属性
del per.name
print(per.name)

#注意：以后千万不要讲对象属性与类属性重名，因为对象属性会屏蔽掉类属性。但是当删除对象属性后，在使用又能使用类属性了。



```

```python
class A(object):
    num = 0

a = A()
b = A()
c = A()

print(a.num,b.num,c.num)

a.num = 100

print(a.num,b.num,c.num)

A.num = 1000

print(a.num,b.num,c.num)

#0 0 0
#100 0 0
#100 1000 1000
```

这个例子能看出来，对实例对象a的num属性赋值后，就覆盖了原来类对象A的num属性了。

python中在类里面定义的属性是静态变量，相当于C、java、php等语言中的static关键字一样。类的属性是与类对象进行绑定的，并不会依赖任何它的实例对象。任何语言的对象都是这个样的。

###【12】什么是绑定

我们前面刚提到绑定，那是什么是绑定？

python严格按照要 类里面的方法 需要有实例才能被调用，这种限制其实就是python所谓的绑定概念。

我们看个例子：

```python

class A:
    def setXY(self,x,y):
        self.x = x
        self.y = y
    def echoXY(self):
        print(self.x,self.y)
a = A()
print(a.__dict__)

a.setXY(1,2)
print(a.__dict__)

del A  #删除类对象

a.echoXY()
#b = A()  #类对象删除了，不能再调用了

```

###【13】前方高能：插件方式

利用dict来扩展对象的方法

```python
class PlugIn(object):
    def __init__(self):
        self._exported_methods = []

    def plugin(self, owner):
        for f in self._exported_methods:
            owner.__dict__[f.__name__] = f

    def plugout(self, owner):
        for f in self._exported_methods:
            del owner.__dict__[f.__name__]


class AFeature(PlugIn):
    def __init__(self):
        super().__init__()
        self._exported_methods.append(self.get_a_value)

    def get_a_value(self):
        print('a feature.')


class BFeature(PlugIn):
    def __init__(self):
        super().__init__()
        self._exported_methods.append(self.get_b_value)

    def get_b_value(self):
        print('b feature.')


class Combine: pass


c = Combine()
AFeature().plugin(c)
BFeature().plugin(c)

c.get_a_value()
c.get_b_value()

```
###【14】相关的BIF

类和对象相关的内置函数

####1、issubclass(class,classinfo)

如果第一个参数(class)是第二个参数(classinfo)的子类,则返回True，否则返回False；

```python
1)第一个类被认定为子类
2）classinfo可以是对象组成的元祖，只要class是元祖中任何一个类的子类都返回True。
3）在其他情况下报错。
```

```python
class A:
    pass

class C:
    pass

class B(A):
    pass

tuple1 = (A,C)
print(issubclass(B,A))

#True
```

####2.isinstance(object,classinfo)

如果第一个参数(object)是第二个参数(classinfo)的实例对象，则返回True，否则返回False。

```python

1)如果objec是classinfo的子类一个实例，也符合条件
2)如果第一个参数不是对象，则永远返回False。
3)classinfo可以是类对象组成的元祖。
```

```python
class A:
    pass

class C:
    pass

class B(A):
    pass

tuple1 = (A,C)

b = B()
print(isinstance(b,tuple1))
print(isinstance('aas',str))

#True
#True
```

####3.hasattr(object,name)

attr即attribute的缩写，就是属性的意思，下面讲的几个函数都是和对象的属性有关的。

hasatt()的作用是测试一个对象里是否有指定的属性。

第一个参数(object)是对象，第二个参数(name)还属性名(属性的字符串名字)

```python
class C:
    def __init__(self,x = 0):
        self.x = x
c = C()
print(hasattr(c,'x'))

#True
```

####4、getattr(object,name[,default])

返回对象指定的属性值，如果指定的属性不存在，则返回default(可选参数)的值；若没有设置default参数，则抛出AttributeError异常。

存在则返回0

```python
class C:
    def __init__(self,x = 0):
        self.x = x
c = C()
print(getattr(c,'x'))
print(getattr(c,'y','你访问的属性不存在'))

#0
#你访问的属性不存在
```

####5、setattr(object,name,value)
与getattr()相对应，但是setattr()可以设置对象中指定属性的值，如果指定的属性不存在，则会新建属性并赋值。

```python
class C:
    def __init__(self,x = 0):
        self.x = x
c = C()

setattr(c,'x',1)
print(c.x)

#1
```

####6、delattr(object,name)
与setattr()相反，delattr()用于删除对象中指定的属性，如果属性不存在则抛出AttributeError异常。

```python
class C:
    def __init__(self,x = 0):
        self.x = x
c = C()

print(delattr(c,'x'))

#None
```

####7、property(fget=None,fset=None,fdel=None,doc=None)


```python
class C:
    def __init__(self,x = 0):
        self.x = x
    def getVar(self):
        return self.x
    def setVar(self,value):
        self.x = value
    def delVar(self):
        del self.x
    r = property(getVar,setVar,delVar)

c = C(100)

print(c.r)

c.r = 2000

print(c.r)

del c.r
```
property()函数的作用就是可以设置属性的属性，就是给一个属性指定3个方法。

等学完了魔术方法就知道它是怎么运行的了。


##魔术方法(魔法方法)

我们在前面的内容里面已经接触过魔术方法了，比如`__init__`,`__del__`,`__dict__`.

那么什么是魔术方法了？

```python
1)总是被下划线包围
2)魔术方法是加强python的面向对象的
3)它在适当的时候总是能被调用
```

###【1】`__slots__`‘属性’

`__slots__`它的作用就是限制类中可以动态添加指定的属性名和方法名。

使用了`__slots__`后`__dict__`就不能再使用了，因为`__dict__`也可以给动态添加类中的属性值。

```python

class A:
    age = '1'
    __slots__ = ['func','name']

a = A()

a.name = 1

def func():
    return 123

a.func = func

print(a.func())

#a.sex = 'male'

```

###【2】`__new__(cls[, ...])`

`__new__()`才是在一个对象实例化的时候第一个调用的方法。它和其它的魔术方法不同，他的第一个参数不是self(本对象），而是这个类本生(cls)，而其它的参数会直接传递给`__init__()`方法的。

`__new__()`方法需要返回一个实例对象，通常是cls这个类实例化的对象，当然你也可以返回其它对象。

`__new__`方法平时很少去重写它，一般让python用默认的方案去执行它就可以了。一般`__new__`在整个继承链中有一个就可以了，一种情况下需要重写这个魔术方法，就是集成了一个不可变类型的时候。

如果子类中没有定义new()方法，那么会自动调用其父类的new()方法来制造实例。

而如果新式类中重写了new()方法，那么你可以自由选择任意一个的其他的新式类（必定要是 新式类，只有新式类必定都有new()，因为所有新式类都是object的后代，而经典类则没有new() 方法）的new()方法来制造实例，包括这个新式类的所有前代类和后代类，只要它们不会造成递归死 循环。具体看以下代码解释：

```python

class A(str):
    def __new__(cls,string):
        print('new')
        str1 = string.upper()
        return str.__new__(cls,str1)

    def __init__(self,string):
        print('ok')

a = A("hello shanghai ")
print(a)

#new
#ok
#HELLO SHANGHAI 
```

<font color='red'>注意：千万不要用自己笨类去调用`__new__`，这样会死造成循环。</font>

###【3】@property

在绑定属性时，如果我们直接把属性暴露出去，虽然写起来很简单，但是，没办法检查参数，导致可以把类属性随便改；

那么我们就会想到私有属性的定义，私有属性在调用和修改的时候需要加太长的调用规则`_类名__属性`，这样一来也挺麻烦的，所以我们给每个私有属性定义两个方法

```python

class myCls:

    def __init__(self):
        self.__name = 'tom'

    def getName(self):
        return self.__name

    def setName(self,val):
        self.__name = val

m = myCls()
print(m.getName())
m.setName('jack')
print(m.getName())

```

还有一种更加简单的方法就是@property

还记得装饰器（decorator）可以给函数动态加上功能吗？对于类的方法，装饰器一样起作用。Python内置的@property装饰器就是负责把一个方法变成属性调用的：

```python
class myCls:

    def __init__(self):
        self.__name = 'tom'

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self,val):
        self.__name = val

m = myCls()
print(m.name)
m.name = 'jack'
print(m.name)

```
注意到这个神奇的@property，我们在对实例属性操作的时候，就知道该属性很可能不是直接暴露的，而是通过getter和setter方法来实现的。

还可以定义只读属性，只定义getter方法，不定义setter方法就是一个只读属性：

@property的实现比较复杂，我们先考察如何使用。把一个getter方法变成属性，只需要加上@property就可以了，此时，@property本身又创建了另一个装饰器@score.setter，负责把一个setter方法变成属性赋值，于是，我们就拥有一个可控的属性操作：

###【4】工厂函数

现在有一个新的名词需要大家记住：工厂函数，大家现在可能没听过，但是我们早就接触到了，知识那个时候我们还没有学习过类和对象，那个时候说了也白说。

python2.2以后，对类和类型进行了统一，做法就是将int()、float()、str()、list()这些转换为工厂函数。

我们看个例子：

```python
print(type(len))
print(type(dir))
print(type(list))
print(type(int))


#<class 'builtin_function_or_method'>
#<class 'builtin_function_or_method'>
#<class 'type'>
#<class 'type'>
```

普通的BIF应该是<class 'builtin_function_or_method'>，而工厂函数是<class 'type'>，大家有没有很眼熟，在哪里见过。

```python

class A:
    pass

print(type(A))

#<class 'type'>
```

它也是type类型，也就是类对象，也就是所谓的工厂函数，那么工厂函数就是一个类对象，当调用类对象的时候，它返回的是一个实例对象：

```python
a = int('123')
b = int('345')
print(a+b)

#468
```
当在求a + b等于多少的时候，事实上python就是讲两个对象进行相加操作。

现在是不是豁然开朗，原来实例对象是可以进行运算的！其实早该发现这个问题了，python中无处不对象。

###【5】算术运算符

python的魔术方法还提供了自定义对象的数值处理，通过对下面这些魔术方法的重写，可以自定义任何对象的算术运算。

 ![算术](images\算术.png)

```python

#不同的类型用加法会有不同的解释
class _int(object):
    def __init__(self, num):
        self.num = num
    #运算符重载
    def __add__(self, other):
        return _int(self.num + other.num)
    def __str__(self):
        return "num = " + str(self.num)
per1 = _int(1)
per2 = _int(2)
print(per1 + per2)#per1 + per2 ==== per1.__add__(per2)
#print(per1.__add__(per2))
print(per1)
print(per2)

#num = 3
#num = 1
#num = 2
```
<font color='red'>注意下面的例子：</font>

```python
class _int(int):
    def __add__(self, other):
        return self + other

a = _int(1)
b = _int(2)
print(a+b)

#RecursionError: maximum recursion depth exceeded while calling a Python object
```
看这个例子，变成了无限递归，为什么？注意add里面，写的是 `return self + other`，self代表这个类，每次都会调用`__add__`方法，这样就变成死递归了。怎么解决？

```python
class _int(int):
    def __add__(self, other):
        return int(self) + other

a = _int(1)
b = _int(4)
print(a+b)

#5
```
###【7】短信接口

```python

#接口类型 秒嘀科技 短信验证码
#账户注册 http://www.miaodiyun.com
#注意事项：
#（1）调用期间要在 秒嘀的控制台 添加好短信模板
#（2）ACCOUNT SID和AUTH TOKEN 在 控制台->用户中心->账户管理->开发者中心查看
#（3）该代码仅供接入秒嘀科技验证码短信接口参考使用，如若接入其它公司短信产品要按照该产品规定；

"""
格式拼接

accountSid = a14f6bfd43ce44c9b019de57f4e2de4b & smsContent =【秒嘀科技】您的验证码是345678，30
分钟输入有效。
& to = 13896543210 & timestamp = 20150821100312 & sig = a14f6bfd43ue44c9b019du57f4e2ee4r & respDataType = JSON

"""


from http import client
from urllib import request,parse
from random import randint
import hashlib
import time

class sendSMs:


    def __init__(self,to = str(17621044208)):
        self.accountSid = '43ca172021e8420fbbda5741d097c37d'
        self.authToken  = '97c65cbf25ee4602806edf8eb01771e6'
        self.verificationCode = randint(999,10000)
        self.smsContent = '【仁雨科技】尊敬的用户，您正在进行登陆验证，您的验证码为：{%d},有效时间为3分钟。为了您的信息安全，请妥善保管好您的验证码。'%self.verificationCode
        self.to = to
        self.timestamp = time.strftime("%Y%m%d%H%M%S", time.localtime())

    def encryption(self):

        self.sig = self.accountSid + self.authToken +self.timestamp
        md5 = hashlib.md5()
        md5.update(self.sig.encode('utf-8'))  # 注意转码
        self.sig = md5.hexdigest()
        self.respDataType  = 'JSON'
        del self.verificationCode,self.authToken  #这两个就没有用了
        sDict = self.__dict__
        params = parse.urlencode(sDict)
        return params

    def sendMsg(self):
        host = 'api.miaodiyun.com'
        postUrl = '/20150822/industrySMS/sendSMS'
        headers = {"Content-type": "application/x-www-form-urlencoded;charset:utf-8;", "Accept": "text/plain"}
        connect = client.HTTPConnection(host,port = 80,timeout=30)
        params = self.encryption()
        a=connect.request("POST", postUrl, params, headers)
        response = connect.getresponse()
        response_str = response.read()
        connect.close()
        return response_str

s = sendSMs(18626070896)
print(s.sendMsg())


```

###【8】发送邮件

```python
import smtplib

from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

class SendMail:
    def __init__(self, message = '用户', title = '仁雨科技', to = ['this_my_email@126.com']):
        # SMTP服务器
        self.SMTPServer = "smtp.126.com"
        # 发邮件的地址
        self.sender = "this_my_email@126.com"
        # 发送者邮箱的密码
        self.passwd = "rd911123"
        #指定的信息(某某用户)
        self.message = message
        #邮件的标题
        self.title = title
        #发送给谁
        if isinstance(to,list):
            self.to = to
        else:
            return '请输入list类型'

    def _html(self):
        message = '''
            <!DOCTYPE html>
            <html lang="zh-CN">
              <head>
                <meta charset="utf-8">
                <meta http-equiv="X-UA-Compatible" content="IE=edge">
                <meta name="viewport" content="width=device-width, initial-scale=1">
                <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！-->
                <title>Bootstrap 101 Template</title>
            
                <!-- Bootstrap -->
                <!--<link href="http://www.mantoman.cn/static/bootstrap/css/bootstrap.min.css" rel="stylesheet">-->
            
                <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
                <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
                <!--[if lt IE 9]>
                  <script src="https://cdn.bootcss.com/html5shiv/3.7.3/html5shiv.min.js"></script>
                  <script src="https://cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
                <![endif]-->
              </head>
              <body>
                <div style="padding-left:100px;padding-top:48px;padding-bottom:48px;margin-bottom: 30px;color: inherit;background-color: #eee;box-sizing: border-box;display: block;font-size: 14px;line-height: 1.42857143;">
                    <div class="container">
            
                        <h1>仁雨科技邮箱验证!</h1>
                        <h3>尊敬的%s，感谢您在仁雨科技注册帐户！激活帐户需要点击下面的链接!</h3>
                        <p><a class="btn btn-primary btn-lg" role="button" href="http://www.baidu.com" style='padding: 10px 16px;font-size: 18px;line-height: 1.3333333;border-radius: 6px;color: #fff;background-color: #337ab7;border-color: #2e6da4;display: inline-block;margin-bottom: 0;text-align: center;white-space: nowrap;touch-action: manipulation;cursor: pointer;vertical-align: middle;user-select: none;background-image: none;border: 1px solid transparent;text-decoration: none;box-sizing: border-box;-webkit-tap-highlight-color: rgba(0,0,0,0);box-sizing: border-box;'>
                         百度</a>
                        </p>
                        <br />
                        <h3>Python改变世界！</h3>
                    </div>
                </div>
              </body>
                <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
                <script src="https://cdn.bootcss.com/jquery/1.12.4/jquery.min.js"></script>
                <!-- Include all compiled plugins (below), or include individual files as needed -->
                <script src="js/bootstrap.min.js"></script>
            </html>
        '''%self.message

        return message

    def sendmail(self):
        msg = self._html()
        #转换成邮件文本
        msg = MIMEText(msg,'html','utf-8')
        #邮件的标题
        msg["Subject"] = self.title
        #发送者信息
        msg['From'] = self.sender
        # 创建SMTP服务器
        mailServer = smtplib.SMTP(self.SMTPServer, 25)
        # 登陆邮箱
        mailServer.login(self.sender, self.passwd)
        # 发送邮件
        mailServer.sendmail(self.sender, self.to, msg.as_string())
        # 退出邮箱
        mailServer.quit()

s = SendMail()
s.sendmail()
```