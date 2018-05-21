#Lesson 19
___
##第十七章
###【1】多任务的原理

现代操作系统(Windows、Mac OS X、Linux、UNIX等)都支持“多任务”

什么叫多任务？？？
操作系统同时可以运行多个任务


单核CPU实现多任务原理：操作系统轮流让各个任务交替执行，QQ执行2us，切换到微信，在执行2us，再切换到陌陌，执行2us……。表面是看，每个任务反复执行下去，但是CPU调度执行速度太快了，导致我们感觉就行所有任务都在同时执行一样



多核CPU实现多任务原理：真正的秉性执行多任务只能在多核CPU上实现，但是由于任务数量远远多于CPU的核心数量，所以，操作西永也会自动把很多任务轮流调度到每个核心上执行

```python
并发：看上去一起执行，任务数多于CPU核心数
并行：真正一起执行，任务数小于等于CPU核心数
```
实现多任务的方式：

```python
1、多进程模式 
2、多线程模式  
3、协程模式
4、多进程+多线程模式
```

###【2】进程

对于操作系统而言，一个任务就是一个进程，比如我们在windows下任务管理器中的都是一个一个的进程。

进程是系统中程序执行和资源分配的基本单位。每个进程都有自己的数据段、代码段、和堆栈段。

####单任务现象

我们看一段代码：

```python
from time import sleep

def run():
    while True:
        print("随便写点啥")
        sleep(1.2)

if __name__ == "__main__":
    while True:
        print("在来电啥")
        sleep(1)

    # 不会执行到run方法，只有上面的while循环结束才可以执行
    run()
```

####启动进程实现多任务

```python
'''
multiprocessing 库
跨平台版本的多进程模块，提供了一个Process类来代表一个进程对象
'''

from multiprocessing import Process
from time import sleep
import os

#子进程需要执行的买吗
def run(str):
    while True:
        # os.getpid()获取当前进程id号
        # os.getppid()获取当前进程的父进程id号
        print("Hal is a %s man--%s--%s"%(str, os.getpid(),os.getppid()))
        sleep(1.2)

if __name__ == "__main__":
    print("主(父)进程启动-%s"%(os.getpid()))
    #创建子进程
    #target说明进程执行的任务
    p = Process(target=run, args=("nice",))
    #启动进程
    p.start()

    while True:
        print("在来电啥")
        sleep(1)

```

####父子进程的先后顺序

```python
from multiprocessing import Process
from time import sleep
import os

def run(str):
    print("子进程启动")
    sleep(3)
    print("子进程结束")

if __name__ == "__main__":
    print("父进程启动")

    p = Process(target=run)
    p.start()

    #join父进程的结束不能影响子进程，让父进程等待子进程结束再执行父进程
    p.join()
    print("父进程结束")

```

####全局变量在多个进程中不能共享

```python
from multiprocessing import Process
from time import sleep

num = 100

def run():
    print("子进程开始")
    #即使使用了global，那还是在函数内部创建了局部变量，因为不在一个进程中。
    global num # num = 100
    num += 1
    print(num)
    print("子进程结束")

if __name__ == "__main__":
    print("父进程开始")

    p = Process(target=run)
    p.start()
    p.join()

    # 在子进程中欧修改全局变量对父进程中的全局变量没有影响
    # 在创建子进程时对全局变量做了一个备份，父进程中的与子进程中的num是完全不同的两个变量
    print("父进程结束--%d"%num)
```

####启动大量子进程

```python
from multiprocessing import Pool
import os, time, random

def run(name):
    print("子进程%d启动--%s" % (name, os.getpid()))
    start = time.time()
    time.sleep(random.choice([1,2,3]))
    end = time.time()
    print("子进程%d结束--%s--耗时%.2f" % (name, os.getpid(), end-start))


if __name__ == "__main__":
    print("父进程启动")

    #创建多个进程
    #进程池
    #表示可以同时执行的进程数量
    #Pool默认大小是CPU核心数
    pp = Pool(2)
    for i in range(3):
        #创建进程，放入进程池同意管理
        pp.apply_async(run,args=(i,))

    #在调用join之前必须先调用close,调用close之后就不能再继续添加新的进程了
    pp.close()
    #进程池对象调用join，会等待进程池中所有的子进程结束完毕再去执行父进程
    pp.join()

    print("父进程结束")

```

####拷贝文件

普通的文件拷贝

```python

import os, time
from multiprocessing import Pool



#实现文件的拷贝
def copyFile(rPath, wPath):
    fr = open(rPath, "rb")
    fw = open(wPath, "wb")
    context = fr.read()
    fw.write(context)
    fr.close()
    fw.close()


path = r"C:\Users\xlg\Desktop\Python-1704\day20\2、进程\file"
toPath = r"C:\Users\xlg\Desktop\Python-1704\day20\2、进程\toFile"


#读取path下的都有的文件
filesList = os.listdir(path)

#启动for循环处理每一个文件
start = time.time()
for fileName in filesList:
    copyFile(os.path.join(path,fileName), os.path.join(toPath,fileName))
end = time.time()
print("总耗时：%0.2f" % (end-start))
```

我们看一下多进程版本高的：

```python
import os, time
from multiprocessing import Pool

#实现文件的拷贝
def copyFile(rPath, wPath):
    fr = open(rPath, "rb")
    fw = open(wPath, "wb")
    context = fr.read()
    fw.write(context)
    fr.close()
    fw.close()

path = r"C:\Users\xlg\Desktop\Python-1704\day20\2、进程\file"
toPath = r"C:\Users\xlg\Desktop\Python-1704\day20\2、进程\toFile"

if __name__ == "__main__":
    # 读取path下的都有的文件
    filesList = os.listdir(path)

    start = time.time()
    pp = Pool(4)
    for fileName in filesList:
        pp.apply_async(copyFile, args=(os.path.join(path,fileName), os.path.join(toPath,fileName)))

    pp.close()
    pp.join()
    end = time.time()
    print("总耗时：%0.2f" % (end-start))
```

####封装进程对象

为什么要封装了？

就是为了看的更加的清晰，我们上面的例子里面一写就一大堆并不好看。

我们先封装：

```python
#myProcess.py

from multiprocessing import Process
import os, time

class MyProcess(Process):
    def __init__(self,name):
        Process.__init__(self)
        self.name = name

    def run(self):
        print("子进程(%s-%s)启动" % (self.name, os.getpid()))
        #子进程的功能
        time.sleep(3)
        print("子进程(%s-%s)结束" % (self.name, os.getpid()))
```

封装好在下面使用：

```python
from myProcess import MyProcess

if __name__ == "__main__":
    print("父进程启动")

    #创建子进程
    p = MyProcess("test")
    # 自动调用p进程对象的run方法
    p.start()
    p.join()

    print("父进程结束")
```

####进程间的通信

```python
from multiprocessing import Process, Queue
import os, time

def write(q):
    print("启动写子进程%s" % (os.getpid()))
    for chr in ["A", "B", "C", "D"]:
        q.put(chr)
        time.sleep(1)
    print("结束写子进程%s" % (os.getpid()))

def read(q):
    print("启动读子进程%s" % (os.getpid()))
    while True:
        value = q.get(True)
        print("value = " + value)
    print("结束读子进程%s" % (os.getpid()))


if __name__ == "__main__":
    #父进程创建队列，并传递给子进程
    q = Queue()
    pw = Process(target=write, args=(q,))
    pr = Process(target=read, args=(q,))

    pw.start()
    pr.start()

    #
    pw.join()
    #pr进程里是个死循环，无法等待其结束，只能强行结束
    pr.terminate()

    print("父进程结束")
```

###【3】线程

在一个进程的内部，要同时干多件事，就需要同时运行多个“子任务”，我们把进程内的这些“子任务”叫做线程


线程通常叫做轻型的进程。线程是共享内存空间的并发执行的多任务，每一个线程都共享一个进程的资源

线程是最小的执行单元，而进程由至少一个线程组成。如何调度进程和线程，完全由操作系统决定，程序自己不能决定什么时候执行，执行多长时间


模块

```python
1、_thread模块       低级模块
#低级模块就是接近底层的模块，越是底层就越难
2、threading模块     高级模块，对_thread进行了封装
```

####启动线程

```python
import threading,time


def run(num):
    print("子线程(%s)开始" % (threading.current_thread().name))

    #实现线程的功能
    time.sleep(2)
    print("打印", num)
    time.sleep(2)

    print("子线程(%s)结束" % (threading.current_thread().name))

if __name__ == "__main__":
    #任何进程默认就会启动一个线程，称为主线程，主线程可以启动新的子线程
    #current_thread()：返回返回当前线程的实例
    print("主线程(%s)启动" % (threading.current_thread().name))

    #创建子线程                     线程的名称
    t = threading.Thread(target=run, name="runThread", args=(1,))
    t.start()

    #等待线程结束
    t.join()

    print("主线程(%s)结束" % (threading.current_thread().name))
```

####线程共享数据

```python

import threading
'''
多线程和多进程最大的不同在于，多进程中，同一个变量，各自有一份拷贝存在每个进程中，互不影响。而多线程中，所有变量都由所有线程共享。所以，任何一个变量都可以被任意一个线程修改，因此，线程之间共享数据最大的危险在于多个线程同时修改一个变量，容易把内容改乱了。
'''

num = 0

def run(n):
    global num
    for i in range(10000000):
        num += n    #  15 = 9 + 6
        num -= n    #  9

if __name__ == "__main__":
    t1 = threading.Thread(target=run, args=(6,))
    t2 = threading.Thread(target=run, args=(9,))
    t1.start()
    t2.start()
    t1.join()
    t2.join()

    print("num =",num)

'''
线程1   num = num + 6
        num - 6  = 3

线程2   num = num + 9
        3 - 9  =  -6

'''
```