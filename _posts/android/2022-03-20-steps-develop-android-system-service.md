---
layout: post
title: "开发一个Android系统服务的步骤。"
date: 2022-03-20 00:00:00
category: android
tags: [Android, Binder, AIDL, Service]
---
1.AIDL定义服务接口，如IHelloService.aidl，生成模板代码IHelloService.java。 也可以手写继承Bidner类，会麻烦点。  

2.实现服务类MyHelloService，用服务类继承IHelloService.Stub类。实现之前声明接口。  

3.修改SystemServer.java，生成MyHelloService对象，把它注册到ServiceManager。  

4.编写客户端调用的HelloServiceManager类，先通过ServiceManager查询服务，得到Binder对象，再调用asInterface获取到服务访问的远程代理对象，接着过代理对象调用服务接口，就实现了服务访问。  

5.业务代码调用HelloServiceManager提供的方法，实现对自定义服务的访问。  
