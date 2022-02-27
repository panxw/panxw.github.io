---
layout: post
title: "Android NDK 编译"
date: 2013-06-20 20:05:01
category: "android"
tags: [cygwin,NDK]
---
安装cygwin，.bashprofile末加入：

```  
ANDROID_NDK=/cygdrive/d/android/android-ndk-r6b
export ANDROID_NDK
```

#### 一、生成.h文件
以Android工程为例，进到目录，执行：

```
javah -classpath bin/classes com.sample.test.HelloWorld
```

#### 二、编译
进到目录，执行：

```
$ANDROID_NDK/ndk-build clean
$ANDROID_NDK/ndk-build
```<!-- more -->
