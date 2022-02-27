---
layout: post
title: "React Native 开发环境搭建过程"
date: 2016-06-10 20:05:01
category: android 
tags: [React, Native, 环境搭建]
---
#### 一、Node.js

先安装Git命令行工具，Python2.7，及Node.js运行环境。

建议更换npm包源，不然npm包加载会很慢！编辑C:\Users\panxw.npmrc，如没有该文件新建即可，加入一行：

```
registry = https://registry.npm.taobao.org
```
<!-- more -->

#### 二、react-native-cli

安装好Node.js后，就可以使用它的包管理命令npm来安装React Native工具包了：

```
npm install -g react-native-cli
npm install -g yarn
```

除了安装了react-native命令行工具，还加装了yarn，可以加快npm install过程。

#### 三、工程初始化

```
react-native init ReactDemo
```

创建了一个新的React Native工程，工程名为ReactDemo，完成后编译运行：

```
cd ReactDemo
react-native run-android 
```

iOS下:

```
react-native run-ios
```

上述命令会最终启动已存在模拟器或真机运行。

#### 四、真机运行

上述生成的包，在真机环境是不能直接运行成功的。先要确保真机与电脑需要处于同一局域网络，然后在App界面按Menu，进入Dev Settings->DEBUGING|Debug server host & port for device，设置IP:port，ip为我们的电脑，port默认为8081。

再次进入Menu，Reload JS如果能看到首页界面说明成功。

#### 五、其它
如果对Native代码作过修改，那么需要重新运行react-native run-anrodi/run-ios重新生成并安装App。

如果仅修改了js代码，只需启动本地服务(npm start)，然后重新Reload即可。
