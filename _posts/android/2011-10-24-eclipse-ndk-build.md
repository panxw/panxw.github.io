---
layout: post
title: "Windows下eclipse中添加NDK Builder"
date: 2011-10-24 20:05:01
category: "android"
tags: [eclipse,NDK]
---
Windows下NDK开发配合eclipse可在安装好cygwin后，添加一个NDK-Builder。  
1.Project->Properites->Builder>new新建一个NDK-Builder  
2.在Main下面Location栏输入C:\cygwin\bin\bash.exe, Work Directory栏输入C:\cygwin\bin, Arguments栏输入：  

```
--login -c "cd /cygdrive/e/android/ndks/jni && /cygdrive/d/android-sdk-windows/android-ndk-r6b/ndk-build
```<!-- more -->

3.在Refresh下面选上Refresh resources upon completion  

4.Build Options下面设置Run the builder选项为During manual builds及Specify working set of relevant resources  
