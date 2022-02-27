---
layout: post
title: "一步一步在AWS EC2(Ubuntu)上搭建git服务"
date: 2015-08-06 20:05:01
category: "git"
tags: [git, aws, git服务]
---
为实现下面命令行的功能，折腾了多天，终于成功在AWS的EC2(Ubuntu)机子上搭了个私家git服务。本文不讨论SSH, RSA加解密概念之类，只把在AWS EC2(Ubuntu)上搭建git服务的过程记录下来，方便以后用到时查询或供大家参考。<!-- more -->

```
git clone git@ip:/home/git/project.git
```

#### 1.准备工作
```
sudo apt-get update
sudo apt-get install git #安装git服务

sudo useradd -m git  #添加git用户
sudo passwd git #修改git用户密码
```
为安全起见，最好禁止用户名git的用户使用密码登录，编辑/etc/passwd这个文件，在文件末尾可以找到类似这样的行：

```
git:x:1000:1000::/home/git:/bin/sh
```
将bin/sh改为/usr/bin/git-shell，这样一来只能通过密钥登录git帐户了。  


#### 2.密钥配置
客户端生成密钥：

```
ssh-keygen -t RSA
```
命令生成key密钥，一个私钥id_rsa，对应一个公钥id_rsa.pub， id_rsa自己存放，id_rsa.pub要报备git服务器。  
Windows中直接生成的密钥名文件名必须是id_rsa，不能像Linux中可以自行配置。而Linux中需要在~/.ssh/config中配置：

```
Host
    HostName <ip>
    User git
    IdentityFile ~/.ssh/id_rsa
    #PreferredAuthentications publickey
```
生成的公钥文件id_rsa.pub，报备git服务器，即加入到git用户的authorized_keys文件中去。

```
#以EC2的默认用户ubuntu登录
sudo chown git:ubuntu /home/git/.ssh/authorized_keys #将authorized_keys权限临时修改到ubuntu用户下
sudo cat id_rsa.pub >> /home/git/.ssh/authorized_keys #追加id_rsa.pub到get用户的authorized_keys
sudo chown git:git /home/git/.ssh/authorized_keys #将authorized_keys权限改回git用户下
```

#### 3.创建git项目 
在/home/git/目录下新建git项目并初始化：

```
mkdir project.git
cd project.git
git --bare init
cd ..
sudo chown git:git project
sudo chmod 755 project -R
```

#### 4.验证
```
git clone git@ip:/home/git/project.git
```
如果成功，被clone的rep将会出现在本地了。 

#### 5.参考：  
http://chiyx.iteye.com/blog/1872447  
http://www.open-open.com/lib/view/open1356608472385.html  
https://dericteong.wordpress.com/2013/06/12/setup-git-server-in-amazon-ec2/  
http://www.lostdecadegames.com/goodbye-github-hello-aws/  
http://my.oschina.net/aulphar/blog/201813  
http://blog.chinaunix.net/uid-28621021-id-3487552.html  
