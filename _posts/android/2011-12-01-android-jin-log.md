---
layout: post
title: "android jni c/c++打印输出"
date: 2011-12-01 20:05:01
category: "android"
tags: [jni]
---
#### 一、加入头文件：
```
#include <android/log.h>
```

#### 二、声明输出标记
```
#define LOG_TAG "TEST"
```

#### 三、输出打印信息方法：
```
__android_log_print(ANDROID_LOG_INFO, LOG_TAG, "input:a=%d, b=%d", a,b);
```<!-- more -->

输出级别除ANDROID_LOG_INFO外，还有ANDROID_LOG_DEBUG，ANDROID_LOG_WARN，ANDROID_LOG_ERROR，ANDROID_LOG_VERBOSE等。  

#### 四、编译时Android.mk中加入：
```
LOCAL_LDLIBS := -llog
```

#### 五、查看
Android应用运行时查看输出信息。
