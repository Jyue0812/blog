#Lesson_4
___
##第七章

###【1】布尔值

布尔类型是特殊的整形，尽管布尔类型用True和False来表示‘真’和‘假’，但是布尔型可以当做整数来对待，这个型内容我们在前面已经体现过了，True相当于整形值1，False相当于整形值0：

```python
print(True + True)  #2
print(True * False) #0
```

###【2】空值

空值`None`，它是python里的一个特殊的值。None不能理解为0，因为0是有意思的，而None是一个特殊值。

```python

n = None
print(n)


>>>None
```

###【3】list(列表)

有的时候需要把一堆东西暂时储存起来，因为它们的某种直接或间接的关系，需要把他们放在一组或者一个集合中，因为将来可能用的上。很多接触过程序的人都知道`数组`，数组是把一大堆同种类型的数据挨个放一块儿，然后通过下标去寻找。由于python的变量没有数据类型，也就是说python是没有数组的，所以python加入了更加强大的列表。

python列表有多强大了？如果说数组比作是集装箱，那么python的列表就是仓库。

先看一个例子：

```python

age1 = 18
age2 = 19
age3 = 20
age4 = 21
age5 = 22
print((age1 + age2 + age3 + age4 + age5) / 5)   #20.0
```

这样一次就声明了5个变量，写起来还非常的麻烦，那么我们用列表来试试：

```python

list2 = [18, 19, 20, 21, 22]
print(sum(list2)/len(list2))   #20.0

```

使用列表以后代码变得非常的简洁.


####创建列表


创建列表和创建普通变量一样，只是把数据用中括号括起来就可以了，数据之间用逗号隔开。

先创建一个空的列表；

```python
list1 =[]

print(list1,'----------',type(list1))

```

再创建一个带有元素的列表：


```python

list2 = [18, 19, 20, 21, 22]

print(list2)

```

####访问列表中的元素

我们访问元素中的单个值，可以通过元素的索引值（index）

<font color='red'>注意，列表的索引值是从零开始的：</font>

```python
name = ['鸡蛋','鸭蛋','鹅蛋','傻蛋']

print(name[0])
print(name[3])


>>>鸡蛋
>>>傻蛋
```

我们看到上面的列表一面一共只有4个元素，那么索引值就是0、1、2、3，
如果输入name[4]的话，那就超出范围了，会报错：

```python
name = ['鸡蛋','鸭蛋','鹅蛋','傻蛋']

print(name[4])

>>>IndexError: list index out of range
```

有的时候，list可能会非常的长，我们不可能去数它，在计算索引值啊，那怎么办了？

```python
现在我要找这个列表中间的元素

name = ['鸡蛋','鸭蛋','鹅蛋','傻蛋','李狗蛋']

print(name[int(len(name)/2)])

>>> 鹅蛋
```

####列表的组合

列表的组合其实和字符串拼接是一样的，都是使用+号相连接。

```python
name = ['鸡蛋','鸭蛋','鹅蛋','傻蛋','鱼蛋']

nameto = ['鸵鸟蛋','恐龙蛋','鳄鱼蛋','王八蛋','李狗蛋']

print(nameto + name )

>>>['鸵鸟蛋', '恐龙蛋', '鳄鱼蛋', '王八蛋', '李狗蛋', '鸡蛋', '鸭蛋', '鹅蛋', '傻蛋', '鱼蛋']


#合并的时候那个数组在前面，那个数组的索引的值就偏小
```
####列表的重复

列表的重复和字符串是一样的，使用 * 

```python

name = ['鸡蛋','鸭蛋','鹅蛋','傻蛋','鱼蛋']
print(name * 3 )

>>>['鸡蛋', '鸭蛋', '鹅蛋', '傻蛋', '鱼蛋', '鸡蛋', '鸭蛋', '鹅蛋', '傻蛋', '鱼蛋', '鸡蛋', '鸭蛋', '鹅蛋', '傻蛋', '鱼蛋']

```

####判断元素是不是这个列表中的

我们学过in 和 not in ，返回布尔值

```python

name = ['鸡蛋','鸭蛋','鹅蛋','傻蛋','鱼蛋']

print('驴蛋' in name)
print('驴蛋' not in name)

>>>False
>>>True
```

####列表的分片

依然和字符串一样

```python

name = ['鸡蛋','鸭蛋','鹅蛋','傻蛋','鱼蛋']

print(name[:2])   #从0开始取2个
print(name[::2])  #从0开始，每两个取一次
print(name[::-1])  #返回翻转


>>>['鸡蛋', '鸭蛋']
>>>['鸡蛋', '鹅蛋', '鱼蛋']
>>>['鱼蛋', '傻蛋', '鹅蛋', '鸭蛋', '鸡蛋']
```

####二维列表

什么是二维列表，就是列表的元素也是列表

```python

list1 = [[1,2,3],[4,5,6],[7,8,9]]
print(list1)

[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

二维列表获取元素是一样的：

```python

list1 = [[1,2,3],[4,5,6],[7,8,9]]
print(list1[1][2])  #6
print(list1[0][1])  #2
print(list1[2][0])  #7

```

####在列表中末尾添加新的元素

```python
list1 = [1,2,3,4,5]
list1.append(6)
list1.append([7,8,9])
print(list1)

#添加的是列表，那么这个元素也是列表

>>>[1, 2, 3, 4, 5, 6, [7, 8, 9]]
```

####在末尾一次性追加另一个列表中的多个值

```python

list1 = [1,2,3,4,5]
list1.extend([6,7,8])
print(list1)

>>>[1, 2, 3, 4, 5, 6, 7, 8]

#extend()插入的只能是list类型的
```

####在指定下标处添加一个元素，不覆盖原数据，原数据向后顺延

```python
list1 = [1,2,3,4,5]
list1.insert(2, 100)
list1.insert(2, [200,300])
print(list1)

>>>[1, 2, [200, 300], 100, 3, 4, 5]

```

####弹出(移除)列表中指定下标处的元素（默认移除最后一个元素）,并返回删除的数据

```python

list1 = [1,2,3,4,5]
list1.pop()  #不写索引的话默认弹出最后一个元素
#写就是等于是list1.pop(-1)
list1.pop(2)
print(list1.pop(1))
print(list1)


>>>2
>>>[1, 4]
```

####修改指定的值

修改list只需要通过索引重新复制就可以了

```python

list1 = [1,2,3,4,5]
list1[0] = 0
list1[-1] = [1,2,3]
print(list1)


#[0, 2, 3, 4, [1, 2, 3]]
```
#### 移除列表中的某个元素第一个匹配的结果

remove()在不知道值的下表情况下使用。

```python
list1 = [1,2,3,4,5,4,5,4]
list1.remove(4) #删除第一个4
print(list1)

>>>[1, 2, 3, 5, 4, 5, 4]
```
删除所有指定的重复值

```python
list1 = [1,2,3,4,5,4,5,4]

while 4 in list1:
    list1.remove(4)
print(list1)

>>>[1, 2, 3, 5, 5]
```

####获取列表值得下标(索引)

index() 函数用于从列表中找出某个值第一个匹配项的索引位置。

该方法返回查找对象的索引位置，如果没有找到对象则抛出异常。

```python
list1 = [1,2,3,4,5,4,5,4]
print(list1.index(3))

>>>2   #返回3的索引是2
```

index还有两个参数：

index(需要查找的值,start,stop)

```python
list1 = [1,2,3,4,5,4,5,4]

one = list1.index(4)   #这是第一个四的位置

end = len(list1)    #这是list1的含有元素长度,代表结束的位置，list1里面没有下表为8的地方那么默认不会去查找

start_two = one + 1        #第一个4的下表为'3'，那么+1以后就不会从下表为3的位置开始找

two = list1.index(4,start_two,end) #获取第二个two的下标值，把值赋给变量two

start_three = two + 1   #代表第三次查找的开始位置

three = list1.index(4,start_three,end)

print(one,two,three)


>>>3 5 7
```



####语句删除del

注意del 不是list的一个方法，所以后面不用加小括号，它的删除方式和pop有些类似，不过del 必须指定下标,如果不加索引，那就是删除整个列表。

```python
list1 = [1,2,3,4,5,4,5,4]
del list1[0]
del list1[-1]
print(list1)

>>>[2, 3, 4, 5, 4, 5]
```

####清楚列表中的所有数据

del list

```python
list1 = [1,2,3,4,5,4,5,4]
del list1

print(list1)
>>>[]
```

clear()

```python
list1 = [1,2,3,4,5,4,5,4]
list1.clear()

print(list1)

>>>[]
```

####计算指定值在列表中出现的次数

```python
list1 = [1,2,3,4,5,4,5,4]

print(list1.count(4))

>>>3
```
####获取列表中元素的个数

```python
list1 = [1,2,3,4,5,4,5,4]

print(len(list1))

>>>8
```
####列表的的最大值、最小值、列表中数字的总和

```python

list1 = [1,2,3,4,5,4,5,4]

print(max(list1),min(list1))
print(sum(list1))

>>>5 1
>>>28
```

####翻转列表

我们原来说过list[：：-1]的方法可以返回翻转列表的结果，但是默认是不影响列表的原来的值。

```python
list1 = [1,2,3,4,5,4,5,4]

print(list1[::-1])

print(list1)


#[4, 5, 4, 5, 4, 3, 2, 1]
#[1, 2, 3, 4, 5, 4, 5, 4]  并没有被影响
```

list.reverse(),它也是翻转列表，但是它影响原来的结果：

```python
list1 = [1,2,3,4,5,4,5,4]

list1.reverse()

print(list1)

#[4, 5, 4, 5, 4, 3, 2, 1]
```

####列表的排序

list.sort(func,key,reverse)

func和key参数用于设置排序得到方法和关键字，默认使用的是归并排序，reverse的默认值是False，也就是正序排列。

正序：

```python
list1 = [1,2,3,4,5,4,5,4]

list1.sort()  #没有写默认是从小到大

print(list1)

>>>[1, 2, 3, 4, 4, 4, 5, 5]
```

倒序：

```python
list1 = [1,2,3,4,5,4,5,4]

list1.sort(reverse=True)  #指定了reverse=True就是倒叙排列

print(list1)

>>>[5, 5, 4, 4, 4, 3, 2, 1]
```

模拟倒序：

```python

list1 = [1,2,3,4,5,4,5,4]

list1.sort()

list1.reverse()

print(list1)

>>>[5, 5, 4, 4, 4, 3, 2, 1]
```

####关于分片“拷贝”概念  深拷贝和浅拷贝

```python

list1 = [1,3,2,9,7,8]

list2 = list1[:]  #分片拷贝的并没有受到影响，深拷贝，它在内存中的地址与list1不一样

list3 = list1     #浅拷贝

list4 = list1.copy()  #深拷贝，它在内存中的地址与list1不一样，深拷贝也不会受到影响

list1.sort()

print('list1：',list1,id(list1))
print('list2：',list2,id(list2))
print('list3：',list3,id(list3))
print('list4：',list4,id(list4))

#list1： [1, 2, 3, 7, 8, 9] 4323685000
#list2： [1, 3, 2, 9, 7, 8] 4323686152
#list3： [1, 2, 3, 7, 8, 9] 4323685000
#list4： [1, 3, 2, 9, 7, 8] 4323686536
```
分片拷贝了就是把原先的list表的值复制到一个新的地址上，所以原来的list发生改变都不会影响到。

<image src='images/copy.jpg' width="500"/>


####将其它类型转换成list

```python

tu = (1,2,3)

list1 = list(tu)

print(tu,type(tu))
print(list1,type(list1))


#(1, 2, 3) <class 'tuple'>
#[1, 2, 3] <class 'list'>
```

##第八章
###【1】条件控制语句
___
####if-elif-else

我们在没有学习这一章节之前只有if-else，那么这样可能会写很多的if语句，我们看一个例子。

```python

#现在做一个100分制的成绩评价，90分以上为A，80-90为B，70-80为C，60-70为D，60以下为E

score = int(input('请输入0到100之间成绩：'))



if 100 >= score >=90:
    print('A')
if 90 >= score >=80:
    print("B")
if 80 >= score >=70:
    print('C')
if 70 >= score >= 60:
    print('D')
if 60 >= score >= 0:
    print("E")
if score > 100 or score < 0:
    print('输入错误，输入0到100之间成绩')
    
#这样的话需要很多的if
```

但是你也可以这样去写：

```python

score = int(input('请输入0到100之间成绩：'))

if 100 >= score >= 90:
    print('A')
else:
    if 90 >= score >= 80:
        print("B")
    else:
        if 80 >= score >= 70:
            print('C')
        else:
            if 70 >= score >= 60:
                print('D')
            else:
                if 60 >= score >= 0:
                    print("E")
                else:
                    if score > 100 or score < 0:
                        print('输入错误，输入0到100之间成绩')
```

其实我们可以用一个if去搞定：

```python

score = int(input('请输入0到100之间成绩：'))

if 100 >= score >=90:
    print('A')
elif 90 >= score >=80:
    print("B")
elif 80 >= score >=70:
    print('C')
elif 70 >= score >= 60:
    print('D')
elif 60 >= score >= 0:
    print("E")
else:
    print('输入错误，输入0到100之间成绩')
    
```
<font color='red'>注意：elif后面是没有冒号的</font>

这三个是个很简单的例子，但是这里面有一个问题，假设我们第一次输入100,第一种写法会打印出一个A，然后继续向后面的2，3，4，5一次判断，然后条件都不符合，退出程序。

如果现在我们使用第二种或第三种，在第一次判断的时候就会打印出A，而后面的程序将不再执行，直接退出。

假设每一次判读都会耗费一次CPU的时间，那么第一种写法比第二种和第三种要多耗费400%的时间，要成为一个优秀的程序员，必须要养成一个良好的思维逻辑。而python可以锻炼你这方面的能力。


###【2】python可以有效避免“悬挂else”（了解）

什么是“悬挂else”？

举个例子，初学C的人很容易被一下代码欺骗：

```python
	
	if(a >0)
		if(a > 10)
			print('这真的很大！！！')
	else
		print('你个辣鸡！！')
```
这个例子里面，else和if都是最外层的，我们在python里面能看出来它是术语最外面一层if的，但是在C语言里面，有个就近原则，那么它就是里面一层if的。

这样一不小心就会导致错误，这就是著名的‘悬挂else’，但是在python里，它是不可能出现的。python只有保证缩进整齐就可以决定else是谁的

###【3】不同的if-else（条件表达式或三元运算符）

我们说多少元操作符取决于它有多少个操作数。例如赋值`a = 2`它是二元操作符，因为它左右各有一个操作数，那么`-1`它就是一个医院操作符。

想必大家都已经才出来三元操作符了吧。

通过三元运算符你可以简单的完成下面的判断：

```python
a = 1

b = 2

if a<b:
    print('a<b')
else:
    print('a>b')

```

使用三元运算符：

```python

a = 1

b = 2

c = 'a<b' if a<b else 'a>b'
print(c)


#条件成立执行了左边，左边是if的代码体
#条件不成立执行右边，右边是else的代码体
```
###【4】断言、断点

####断言

断言(assert)的语法就像是if条件分支的‘近亲’。

当这个关键字的条件为False的时候，程序会抛出`AssertionError`这样的异常。

在设么情况下会使用assert了？在我们测试的时候,与其让错误的条件继续运行，不如直接把错误抛出来。

我们看下面的例子：


条件为False的结果：

```python

a = 1

b = 2
assert a > b
if a<b:
    print('a<b')
else:
    print('a>b')
    
    
>>>AssertionError
```

条件为True的结果：

```python

a = 1

b = 2
assert a < b  #结果为真，什么都不会发生
if a<b:
    print('a<b')
else:
    print('a>b')
    
    
>>>a<b
```

###【5】while循环语句

python的while循环和if的条件分支类似，在条件为真的情况下，执行一段代码，不同的是，while循环会一直重复执行那段代码，把这段代码称为循环体。

while 条件：
	循环体
	
```python

a = 0;
while  a < 10：
	print(a)
	a += 1
	
```
这是一个死循环

```python

while True:
	print(123)
	
```

###【6】for循环语句

for循环是python的计数器循环，虽然说python是由C语言编写的，但是它的for循环和C语言的for循环不太一样，python的for循环显得更为智能和强大！这主要表现在它会自动调用迭代器 next()，会自动捕获StopIteration异常并结束循环。

```python
string = '1000phone'
for each in string:
	print(each,end='-')

>>>e-a-c-h-
```

###【7】range()、enumerate() 

####range()

range()我们在前面的几章里面已经见识过了。其实它是for最好的小伙伴。

range(start，stop, skip)

start:计数从start开始。默认是从0开始。例如range（5）等价于range（0， 5）;

end:技术到end结束，但不包括end.例如：range（0， 5） 是[0, 1, 2, 3, 4]没有5

skip：每次跳跃的间距，默认为1。例如：range（0， 5） 等价于 range(0, 5, 1)

```python

for i in range(0,101,10):
	print(i)

```
####enumerate() 

enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。

语法：enumerate(sequence, [start=0])

```python
sequence -- 一个序列、迭代器或其他支持迭代对象。
start -- 下标起始位置。

```
```python
list1 = ["这", "是", "一个", "测试"]
for index, item in enumerate(list1):
    print（index, item）


>>>0 这
>>>1 是
>>>2 一个
>>>3 测试
```
使用enumerate()生成键值对元祖

```python

list1 = ["这", "是", "一个", "测试"]

print(list(enumerate(list1)))

>>>[(0, '这'), (1, '是'), (2, '一个'), (3, '测试')]
```

for循环的魅力不止这一点，还有其它的各式各样的搭档帮助实现各种乱七八糟的功能，后面在讲解元祖的时候在介绍给大家

###【8】break、continue

break 语句的作用是终止当前循环，并且跳出循环体。

```python

bingo = '我最帅'
answer = input('请输入我最想听的一句话:')

while True:
    if bingo == answer:
        break
    answer = input('答对了才能出去：')
print('哎哟，不错哦~')

```
continue 语句的作用是终止本轮循环并直接开始下一轮循环


```python
for i in range(10):
    if i % 2 != 0:
        print('')
        continue
    i += 2
    print(i)
```

###海龟制图

python2.6版本中后引入的一个简单的绘图工具，叫做海龟绘图(Turtle Graphics),turtle库是python的内部库,使用导入即可 `import turtle`

先说明一下turtle绘图的基础知识:

####1、画布(canvas)

画布就是turtle为我们展开用于绘图区域, 我们可以设置它的大小和初始位置

#####screensize()
设置画布大小:
turtle.screensize(canvwidth=None, canvheight=None, bg=None)
参数分别为画布的宽(单位像素), 高, 背景颜色

例如：

```python
turtle.screensize(800, 600, "green")
turtle.screensize() #返回默认大小(400, 300)
```
#####setup()
turtle.setup(width=0.5, height=0.75, startx=None, starty=None)

参数:
width, height: 输入宽和高为整数时, 表示像素; 为小数时, 表示占据电脑屏幕的比例
(startx, starty): 这一坐标表示 矩形窗口左上角顶点的位置, 如果为空,则窗口位于屏幕中心

例如：

```python
turtle.setup(width=0.6, height=0.6)
turtle.setup(width=800, height=800, startx=100, starty=100)

```
####2. 画笔

#####画笔的状态
在画布上,默认有一个坐标原点为画布中心的坐标轴, 坐标原点上有一只面朝x轴正方向小乌龟. 这里我们描述小乌龟时使用了两个词语:坐标原点(位置),面朝x轴正方向(方向), turtle绘图中, 就是使用位置方向描述小乌龟(画笔)的状态

#####画笔的属性
画笔(画笔的属性，颜色、画线的宽度)
1) turtle.pensize()：设置画笔的宽度；
2) turtle.pencolor(); 没有参数传入,返回当前画笔颜色,传入参数设置画笔颜色,可以是字符串如"green", "red",也可以是RGB 3元组,

例如：

```python
import turtle as t
t.pencolor('brown')
tup = (0.2, 0.8, 0.55)
t.pencolor(tup)
```

3) turtle.speed(speed): 设置画笔移动速度,画笔绘制的速度范围[0,10]整数, 数字越大越快

#####绘图命令
操纵海龟绘图有着许多的命令,这些命令可以划分为3种:一种为运动命令，一种为画笔控制命令,还有一种是全局控制命令

(1)画笔运动命令:

|命令                      |	说明                                        |
|----                     |---                                           |
|turtle.forward(distance)	|向当前画笔方向移动distance像素长                  |
|turtle.backward(distance)	|向当前画笔相反方向移动distance像素长度             |
|turtle.right(degree)	    |顺时针移动degree°                              |
|turtle.left(degree)	    |逆时针移动degree°                              |
|turtle.pendown()	       |移动时绘制图形,缺省时也会绘制                     |
|turtle.goto(x,y)	       |将画笔移动到坐标为x,y的位置                       |
|turtle.penup()	           |移动时不绘制图形,提起笔，用于另起一个地方绘制时用    |
|turtle.speed(speed)	    |画笔绘制的速度范围[0,10]整数                     |
|turtle.circle()	           |画圆,半径为正(负),表示圆心在画笔的左边(右边)画圆    |


(2)画笔控制命令:

|命令                           |	说明                                     |
|----                          |---                                       |
|turtle.pensize(width)	        | 绘制图形时的宽度                            |
|turtle.pencolor()	            |画笔颜色                                   |
|turtle.fillcolor(colorstring)  |	 绘制图形的填充颜色                         |
|turtle.color(color1, color2)	  | 同时设置pencolor=color1, fillcolor=color2 |
|turtle.filling()	            |返回当前是否在填充状态                       |
|turtle.begin_fill()            |准备开始填充图形                            |
|turtle.end_fill()	            |填充完成；                                 |
|turtle.hideturtle()	         |隐藏箭头显示；                              |
|turtle.showturtle()	         |与hideturtle()函数对应，显示                    |

(3) 全局控制命令

|命令                           |	说明                                     |
|----                          |---                                       |
|turtle.clear()	              |清空turtle窗口，但是turtle的位置和状态不会改变  |
|turtle.reset()	              |清空窗口，重置turtle状态为起始状态             |
|turtle.undo()	              |撤销上一个turtle动作                         |
|turtle.isvisible()	           |返回当前turtle是否可见                       |
|stamp()	                     |复制当前图形                                |
|turtle.write(s[,font=("font-name",font_size,"font_type")])     |	写文本，s为文本内容，font是字体的参数，里面分别为字体名称，大小和类型；font为可选项, font的参数也是可选项|

####3. 命令详解

turtle.circle(radius, extent=None, steps=None)
描述: 以给定半径画圆
参数:

```python
radius(半径); 半径为正(负),表示圆心在画笔的左边(右边)画圆
extent(弧度) (optional);
steps (optional) (做半径为radius的圆的内切正多边形,多边形边数为steps)
```
举例:
```
circle(50) # 整圆;
circle(50,steps=3) # 三角形;
circle(120, 180) # 半圆
```

####4. 绘图举例


画一个太阳花

```python
import turtle as t
import turtle as t
t.color("red", "yellow")
t.speed(10)
t.begin_fill()
for _ in range(50):
    t.forward(200)
    t.left(170)
t.end_fill()
t.done()
```

五角星

```python

import turtle
import time

turtle.pensize(5)
turtle.pencolor("yellow")
turtle.fillcolor("red")

turtle.begin_fill()

for _ in range(5):
    turtle.forward(200)
    turtle.right(144)
turtle.end_fill()
time.sleep(1)

turtle.penup()
turtle.goto(70, -50)
turtle.color("black")
turtle.write("千锋", font=('Arial', 30, 'normal'))
turtle.done()

```


##作业：
###列表都可以存放一些什么东西？
###向列表里面增加元素的方法有那些？
###append()方法好extend()方法都是向列表的末尾增加元素，请问区别？
###list.append(['a','b'])和extend(['a','b'])有真么区别？
###在列表 name = ['1','0','0','h','o','n','e'] 的最后一个0和h之间插入一个's'，怎么插入？
###用循环完成(自己找规律)
name = ['南帝','北丐','中神通','东邪','西毒']

变成(一个循环就可以完成，当然办法有很多)

name = ['0','南帝','1','北丐','2','中神通','3','东邪','4','西毒']

###用for循环和while循环各写一个99乘法表