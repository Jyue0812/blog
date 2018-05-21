#Lesson 15
___
##第十六章
###爬虫练习


屌丝扒女装：

```python
import urllib.request
import re,ssl
import os

def imageCrawler(url, toPath):
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
    }
    req = urllib.request.Request(url, headers=headers)
    context = ssl._create_unverified_context()
    response = urllib.request.urlopen(req,context=context)
    HtmlStr = response.read().decode('utf-8')

    # with open(r"yhd.html", "wb") as f:
    #    f.write(HtmlStr)

    pat = r'<img style="width:230px;height:322px" src="//(.*?)"/>'
    re_image = re.compile(pat, re.S)
    imagesList = re_image.findall(HtmlStr)
    print(imagesList)
    num = 1
    for imageUrl in imagesList:
        path = os.path.join(toPath, str(num)+".jpg")
        num += 1
        #把图片下载到本地存储
        urllib.request.urlretrieve("http://"+imageUrl, filename=path)



url = "http://search.yhd.com/c0-0/k%25E5%25A5%25B3%25E8%25A3%2585%2520%25E5%25A4%258F/"
toPath = r"image"
imageCrawler(url, toPath)
```

##第十七章

###TCP

 ![tcp](file\tcp.png)

```python

import socket
'''
客户端：创建TCP链接时，主动发起连接的叫做客户端
服务端：接收客户端的连接
'''

# 1、创建一个socket
#参数1：指定协议  AF_INET  或 AF_INET6
#参数2：SOCK_STREAM执行使用面向流的TCP协议
sk = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 2、建立连接
#参数：是一个元组，第一个元素为要连接的服务器的IP地址，第二个参数为端口
sk.connect(("www.sina.com.cn",80))

sk.send(b'GET / HTTP/1.1\r\nHost: www.sina.com.cn\r\nConnection: close\r\n\r\n')

#等待接收数据
data = []
while True:
    #每次接收1K数据
    tempData = sk.recv(1024)
    if tempData:
        data.append(tempData)
    else:
        break

dataStr = (b''.join(data)).decode("utf-8")

# 断开链接
sk.close()
#print(dataStr)

headers, HTML = dataStr.split('\r\n\r\n', 1)
print(headers)
# print(HTML)
```
下面我们写个完整的客户端和服务端来进行相互通信

####TCP服务端

```python

import socket

#创建一个socket
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
#绑定IP端口
server.bind(('192.168.2.102',8081))
#监听
server.listen(5)
print("服务器启动成功……")
#等待链接
clientSocket, clientAddress  = server.accept()

print("%s --  %s 链接成功" % (str(clientSocket), clientAddress))

while True:
  data = clientSocket.recv(1024)
  print("客户端说：" + data.decode("utf-8"))
  sendData = input("输入返回给客户端的数据")
  clientSocket.send(sendData.encode("utf-8"))


'''
while True:
    #等待客户端链接
    clientSocket, clientAddress = server.accept()
    #启动一个线程，将当前链接的clientSocket交给线程
'''
```

####TCP客户端

```python
import socket


client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(("192.168.2.102", 8081))


while True:
    data = input("请输入给服务器发送的数据")
    client.send(data.encode("utf-8"))
    info = client.recv(1024)
    print("服务器说：", info.decode("utf-8"))

```
###UDP

 ![s](file\udp.png)

```python
'''
TCP 是建立可靠的连接，并且通信双方都可以以流的形式发送数据。相对于TCP，UDP则是面向无连接的协议

使用UDP协议时，不需要建立连接，只需要知道对方的IP地址和端口号，就可以直接发送数据包。但是能不能到达就不知道了。

虽然UDP传输数据不可靠，但他的优点是和TCP比，速度快，对于要求不高的数据可以是用UDP
'''

import socket
import time

#这是飞秋接收消息套接字的特定格式
str = "1_lbt4_10#32499#002481627512#0#0#0:1289671407:a:b:288:凯哥万岁"
'''
udp = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
udp.connect(("10.0.142.206", 2425))
udp.send(str.encode("gbk"))
'''
for i in range(256):
    ip = "10.0.142.%d"%i
    print(ip)
    udp = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    udp.connect((ip, 2425))
    udp.send(str.encode("gbk"))

```

来一个聊天室：

####服务端

```python

import socket

udpServer = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
udpServer.bind(('10.0.142.171', 8900))

while True:
    data, addr = udpServer.recvfrom(1024)
    print("客户端说：", data.decode("utf-8"))

```

####客户端

```python

import socket

client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

while True:
    data = input("请输入数据")
    client.sendto(data.encode("utf-8"), ('10.0.142.171', 8900))

```