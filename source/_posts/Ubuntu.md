建议安装VMware Tools

```python
#教程
https://jingyan.baidu.com/article/c275f6ba07e269e33d756714.html
```

改变分辨率命令

```python
#打印显示器支持哪些分辨率
xrandr
#设置屏幕分辨率为1360x768，这是一次性命令，下次开机就没有了
xrandr -s  1360x768_60.02
#怎么解决，在系统设置的显示栏目里面重新设置并应用

```

使用管理员权限

```python
#命令
sudo su 
#输入密码的密码是自己的（在root没用设置密码的时候，如果root用户设置过密码以后我们需要使用root用户的密码）


```

Ubuntu16.04 系统错误报告屏蔽

```python
sudo rm /var/crash/*
sudo gedit /etc/default/apport

将enabled设置为0
```


ubuntu使用的apt而不是yum


```python
#安装vim
apt -y install vim
```

Ubuntu16.04软件中心闪退

```python
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get install --reinstall software-center

```

apt-get安装源替换清华大学的源

```python

#1、原文件重命名备份
sudo mv /etc/apt/sources.list /etc/apt/source.list.back

#2、编辑源列表文件
sudo gedit /etc/apt/sources.list

#3、用下面的文本作为内容

deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial universe
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates universe
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security universe
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security multiverse


4、更新

sudo apt-get update
sudo apt-get upgrade

```

ubuntu 重启网卡方法

```python
查看网卡信息： ifconfig
设定一个网卡IP：ifconfig eth1 192.168.1.10 netmask 255.255.255.0
重启网卡使设定生效：sudo /etc/init.d/networking restart
用ubuntu的系统——>系统管理——>网络的网络设置
关闭网卡 ifdown eth0
开启网卡 ifup eth0
重启网卡，优点是可以指定网卡，不影响其他网络接口
```

ubuntu中开启、关闭防火墙

```python
1、关闭ubuntu的防火墙 
ufw disable
开启防火墙
ufw enable
```

配置ubuntu ssh远程登录

```python

1.默认使用ubuntu用户登录，密码为服务器配置时设置的密码，可在重置密码中修改



2.修改 root 密码

[plain] view plain copy
sudo passwd root  
3.修改配置文件

[plain] view plain copy
sudo gedit /etc/ssh/sshd_config  
找到下面相关配置：

[plain] view plain copy
# Authentication:  
LoginGraceTime 120  
PermitRootLogin prohibit-password  
StrictModes yes  
更改为：

[plain] view plain copy
# Authentication:  
LoginGraceTime 120  
#PermitRootLogin prohibit-password  
PermitRootLogin yes  
StrictModes yes  
4.重启ssh

[plain] view plain copy
sudo service ssh restart  

```

安装JDK

```
https://blog.csdn.net/pucao_cug/article/details/68948639
https://www.itbulu.com/python-pycharm.html
```



安装pycharm

```
https://jingyan.baidu.com/article/60ccbceb4e3b0e64cab19733.html
```





解决the system is running in low-graphics mode问题

```
打不开图形化，那么就进入命令行
ctrl+alt+F1
输入账号密码进入

cd /etc/X11    
sudo cp xorg.conf.failsafe xorg.conf   
sudo reboot  

现在可以进入图形化界面

打开终端，输入：
sudo apt-get install gdm 

gdm是图形化管理工具，在安装的时候学则gdm3

rm -rf /etc/X11/xorg.conf

sudo reboot
```

apt

```
apt-cache search package 搜索软件包

apt-cache show package  获取包的相关信息，如说明、大小、版本等

sudo apt-get install package 安装包

sudo apt-get install package --reinstall   重新安装包

sudo apt-get -f install   修复安装

sudo apt-get remove package 删除包

sudo apt-get remove package --purge 删除包，包括配置文件等

sudo apt-get update  更新源

sudo apt-get upgrade 更新已安装的包

sudo apt-get dist-upgrade 升级系统

apt-cache depends package 了解使用该包依赖那些包

apt-cache rdepends package 查看该包被哪些包依赖

sudo apt-get build-dep package 安装相关的编译环境

apt-get source package  下载该包的源代码

sudo apt-get clean && sudo apt-get autoclean 清理无用的包

sudo apt-get check 检查是否有损坏的依赖
```

