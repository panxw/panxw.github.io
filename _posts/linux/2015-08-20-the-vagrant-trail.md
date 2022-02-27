---
layout: post
title: "Vagrant入手记"
date: 2015-08-20 20:05:01
category: linux
tags: [nginx, vagrant, server]
---
总的来说，Vagrant跑虚拟机的好处有：启动快速，轻量，占内存小。缺点可是能是全命令行模式，没怎么接触过的头大。下面就说说怎么让Vagrant跑起来。<!-- more -->  

#### 1.首先是安装VirtualBox, vargrant程序
```
https://www.vagrantup.com/
https://www.virtualbox.org/
```
安装简单，不停下一步。  

#### 2.安装box
VirtualBox和Vagrant都就绪后，上https://atlas.hashicorp.com/boxes/search找box安装。  
比如我选择的这个https://atlas.hashicorp.com/ubuntu/boxes/trusty64/versions/20151019.0.0，页面有安装命令。  
cmd进d盘建立Vagrant工作目录：

```
mkdir vgrant
cd vagrant
vagrant init ubuntu/trusty64
vagrant up --provider virtualbox
```

#### 3.操作
```
cd vagrant
vagrant up//启动虚拟机
vagrant halt//关闭虚拟机
vagrant suspend//暂停虚拟机
vagrant resume//恢复暂停的虚拟机
vagrant reload //重启
vagrant destroy//删除虚拟机，慎用
```

#### 4.SecurityCRT连接安装
```
127.0.0.1:2222
vagrant/vagrant
```

#### 5.软件安装，如：
```
sudo apt-get update
sudo apt-get install xxxx
```

#### 6.网络配置
修改Vagrantfile可配置网络，参考(http://ninghao.net/blog/2079)  
放开public_network，private_network，forwarded_port实现不同目的。  

完工！  
