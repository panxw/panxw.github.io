---
layout: post
title: "Cocos IDE开发步骤"
date: 2014-09-20 20:05:01
category: "android"
tags: [cocos2d]
---
#### 一、启动Preferences设置
1、General中设置Cocos2d-JS路径。  
2、设置Python，SDK,NDK,ANT,JDK路径。<!-- more -->  

#### 二、开发及调试
1、添加图片等到res目录下，并在src/resources.js中注册。  
2、添加js文件到src目录下，并在project.json中注册到jsList数组中。  
3、构建调试Android应用  
1)Cocos Tools>>Build Custom Runtime>>...build sucess.  
2)Run Configurations>>Android ADB Mode>>Runtime path: Browse>>Project-debug.apk>>Apply.  
3)Run as Cocos JSBinding..  

#### 三、命令行模式
1、新建：cocos new MyGame -l js  
2、运行：cocos run -p web|android|ios  

Cocos2d-JS官网：<http://cocos2d-x.org/wiki/Getting_Started_Cocos2d-js>  
