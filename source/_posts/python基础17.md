#Lesson 17
___
##第十七章
###【3】线程

####线程锁解决数据混乱

threading.Lock()互斥锁

```python

'''

两个线程同时工作，一个存钱，一个取钱

可能导致数据异常


思路：加锁，

'''

import threading

#锁对象
lock = threading.Lock()

num = 0
def run(n):
    global num

    for i in range(10000000):
        # 锁
        # 确保了这段代码只能由一个线程从头到尾的完整执行
        # 阻止了多线程的并发执行，包含锁的某段代码实际上只能以单线程模式执行，所以效率大大滴降低了
        # 由于可以存在多个锁，不同线程持有不同的锁，并试图获取其他的锁，可能造成死锁，导致多个线程挂起。只能靠操作系统强制终止
        '''
        lock.acquire()
        try:
            num = num + n    #  15 = 9 + 6
            num = num - n    #  9
        finally:
            #修改完一定要释放锁
            lock.release()
        '''

        #与上面代码功能相同，with lock可以自动上锁与解锁
        with lock:
            num = num + n
            num = num - n

if __name__ == "__main__":
    t1 = threading.Thread(target=run, args=(6,))
    t2 = threading.Thread(target=run, args=(9,))
    t1.start()
    t2.start()
    t1.join()
    t2.join()
    print("num =",num)

```

####threadlocal

如果有一个全局变量的话，那么在线程中是可以共享的，那么就会造成数据混乱的可能。这时候我们可以使用threadlocal，它本身也是一个全局的对象，但是它可以给每个线程创建一个局部变量。


```python

import threading

num = 0
#创建一个全局的ThreadLocal对象
#每个线程有独立的存储空间
#每个线程对ThreadLocal对象都可以读写，但是互不影响
local = threading.local()

def run(x, n):
    x = x + n
    x = x - n

def func(n):
    #每个线程都有local.x，就是线程的局部变量
    local.x = num
    for i in range(1000000):
        run(local.x, n)
    print("%s-%d"%(threading.current_thread().name, local.x))

if __name__ == "__main__":
    t1 = threading.Thread(target=func, args=(6,))
    t2 = threading.Thread(target=func, args=(9,))
    t1.start()
    t2.start()
    t1.join()
    t2.join()

    print("num =",num)

#作用：为每个线程绑定一个数据库链接，HTTP请求，用户身份信息等，这样一个线程的所有调用到的处理函数都可以非常方便地访问这些资源

```

####客户端与服务器间的数据交互

客户端：

```python
#server.py

import socket
import threading

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('172.16.61.1',8081))
server.listen(5)

def run(ck):
  data = clientSocket.recv(1024)
  print("客户端说：" + data.decode("utf-8"))
  sendData = input("输入返回给客户端的数据")
  if len(sendData):
    clientSocket.send(sendData.encode("utf-8"))

print("服务器启动成功，等待客户端的链接")
while True:
  clientSocket, clientAddress = server.accept()
  #print("%s --  %s 链接成功" % (str(clientSocket), clientAddress))
  t = threading.Thread(target=run, args=(clientSocket,))
  t.start()

```

客户端：

```python
#client.py
#客户端可以有多个

import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(("192.168.3.3", 8081))

while True:
    data = input("请输入给服务器发送的数据")
    client.send(data.encode("utf-8"))
    info = client.recv(1024)
    print("服务器说：", info.decode("utf-8"))
```

####信号量控制线程数量

什么是信号量？

也可以叫信号灯，信号量是多线程环境下使用的一种设施。

我们打个比方，比如现在的路口是单行道，而且还是双行道，现在绿灯了，我们假设车的速度都是一样的，那么是不是两两一起过这个路口。

那么我们线程一样的，几个线程一起一执行。

```python

import threading,time

sem = threading.Semaphore(2)
def run():
    with sem:
        for i in range(5):
            print('%s--%d'%(threading.current_thread().name,i))
            time.sleep(1);

if __name__ == "__main__":
    for i in range(5):
        threading.Thread(target=run).start()

```

####分界线控制运行数量

分解线这个我们很常见，它的作用就是讲什么分开。

我们这里的分界线，好比是游乐场玩过山车的，过山车上好比就是8个座位吧，那是不是凑够了8个人才能开一趟。

我们看看例子：

```python

import threading,time

bar = threading.Barrier(2)#凑够了三个一起执行

def run():
    print("%s--start" % (threading.current_thread().name))
    time.sleep(1)
    bar.wait()   #这里开始等待，达到条件了就可以释放了
    print("%s--end" % (threading.current_thread().name))


if __name__ == '__main__':
    for i in range(5):
        threading.Thread(target=run).start()
```

####延时执行线程

```python
import threading

def run():
    print("我被延迟了")

def go():
    print("我是正常的执行的")
#延时执行线程
r = threading.Timer(5, run)
g = threading.Timer(1, go)
r.start()
g.start()

r.join()
g.join()
print("结束")
```

####事件

```python
import threading, time

def func():
    #事件对象
    event = threading.Event()
    def run():
        for i in range(5):
            #阻塞，等待事件的触发
            event.wait()
            #重置
            event.clear()#这里是清除事件的
            print("第%d次循环"%i)
    t = threading.Thread(target=run).start()
    return event

e = func()

#触发事件
for i in range(5):
    time.sleep(2)
    e.set()#这里我们知道这个事件对象是e，那么直接就可以设置事件对象

```

####生产者于消费者

```python
import threading,queue,time,random


#这个是生产者
def product(id,q):
    while True:
        num = random.randint(0,10000)
        q.put(num)
        print('生产者%d生产的%d已经放入队列了'%(id,num))
        time.sleep(3)
    #队列任务完成时
    q.task_done()
#这个是消费者


def customer(id,q):
    while True:
        item = q.get()
        print('消费者%d消费了%d' % (id, item))
        time.sleep(2)
    #队列任务完成时
    q.task_done()

if __name__ == '__main__':
    #实例化消息队列
    q = queue.Queue()
    #启动生产者
    for i in range(5):
        threading.Thread(target=product,args=(i,q)).start()
    #启动消费者
    for i in range(3):
        threading.Thread(target=customer, args=(i, q)).start()

```

####线程调度

我们有的时候需要在第一个线程中运行完一个程序，然后在第二个线程里面在运行，让这两个线程相互切换。

```python
import threading,time

con = threading.Condition()

def run():
    with con:
        for i in range(0,10,2):
            print(threading.current_thread().name,i)
            time.sleep(1)
            #1、我先执行，打印出来以后我开始等待
            con.wait()
            #4、我接受到了通知我🈶开始走了。
            con.notify()

def go():
    with con:
        for i in range(1,10,2):
            print(threading.current_thread().name,i)
            time.sleep(1)
            #2、在你等待的时间里面我走完了，那么我高数你，你也走吧
            con.notify()
            #3、在你执行的时候我开始等待
            con.wait()

if __name__ == '__main__':
    r = threading.Thread(target=run).start()
    g = threading.Thread(target=go).start()
```

###【4】协程

协程不是进程或线程，其执行过程更类似于子例程（就是某个主程序中的一部分代码，函数也是一个子例程），或者说不带返回值的函数调用。

协成的执行看起来好像是两个线程是工作，实际上是在一个线程中完成的。

python需要使用一个叫genertor生成器来实现的。

```python
子程序/函数：在所有语言中都是层级调用，比如A调用B，在B执行的过程中又可以调用C，C执行完毕返回，B执行完毕返回，最后是A执行完毕。是通过栈实现的，一个线程就是执行一个子程序，子程序调用总是一个入口，一次返回，调用的顺序是明确的

概述：看上去也是子程序，但执行过程中，在子程序的内部可中断，然后转而执行别的子程序，不是函数调用

```

```python

def C():
    print("C--start")
    print("C--end")
def B():
    print("B--start")
    C()
    print("B--end")
def A():
    print("A--start")
    B()
    print("A--end")

A()
```



```python

def A():
    print(1)
    print(2)
    print(3)
def B():
    print("x")
    print("y")
    print("z")

```

```python
1
2
x
y
z
3
执行出这个结果
但是A中是没有B的调用
看起来A、B执行过程有点像线程，但协程的特点在于是一个线程执行


与线程相比，协程的执行效率极高，因为只有一个线程，也不存在同时写变量的冲突，在协程中共享资源不加锁，只需要判断状态
```

Python对协程的支持是通过generator实现的

```python
def run():
    print(1)
    yield 10
    print(2)
    yield 20
    print(3)
    yield 30

#协程的最简单风格，控制函数的阶段执行，节约线程或者进程的切换
#返回值是一个生成器
m = run()
print(next(m))
print(next(m))
print(next(m))
```

####数据传输

```python

def run():
    #空变量，存储的作用data始终为空
    data = ""
    r = yield data
    #r = a
    print(1, r, data)
    r = yield "aa"
    #r = b
    print(2, r, data)
    r = yield "bb"
    #r = c
    print(3, r, data)
    r = yield "cc"


m = run()
#启动m
print(m.send(None))
print(m.send("a"))
print(m.send("b"))
print(m.send("c"))
print("******")

```
####生产者与消费者

```python

def product(c):
    c.send(None)
    for i in range(5):
        print("生产者产生数据%d"%i)
        r = c.send(str(i))
        print("消费者消费了数据%s"%r)
    c.close()
def customer():
    data = ""
    while True:
        n = yield data
        if not n:
            return
        print("消费者消费了%s"%n)
        data = "200"
c = customer()
product(c)

```


