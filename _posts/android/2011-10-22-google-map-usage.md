---
layout: post
title: "Google Map API of Android 的使用"
date: 2011-10-22 20:05:01
category: "android"
tags: [Google,Map]
---
今天看了Google Map API，发现后来的百度，图吧等出的Android 版地图API都比较相近。使用Google Map API的步骤：

#### 1.在下面的网址上获取Maps API Key。
申请之前需用到MD5指纹，方法是：WINXP下进入到C:\Documents and Settings\Administrator\.android\目录，再执行：  

```
keytool -list -keystore debug.keystore，提示输入密码，就输入android，之后就得到MD5认证纹了。
```<!-- more -->

然后到，http://code.google.com/intl/zh-CN/android/add-ons/google-apis/mapkey.html，申请。  

#### 2.下载Google 提供的Map Api jar包。
方法是，用SDK安装工具，在Third Party Add-ons下载对应版本的API。  

#### 3.使用。
xml布局文件中加入视图：  

```
<com.google.android.maps.MapView
	android:layout_width="fill_parent"
	android:layout_height="fill_parent"
	android:apiKey="0vrJE9JtlHLq0_hw2Um76MlEHAkLaFviQMgSNxA"
	/>
```

application节点下加入：

```
<uses-library android:name="com.google.android.maps" />
```

manifest下加入：  

```
<uses-permission android:name="android.permission.INTERNET/">
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

#### 4.创建继承MapActivity的类对地图进行控制操作。
在此不多说。  

#### 5.补充一点。
运行地图应用时可能出现类似于：  

```
[2011-08-07 13:13:21 - GMapApp] Installation error: INSTALL_FAILED_MISSING_SHARED_LIBRARY
[2011-08-07 13:13:21 - GMapApp] Please check logcat output for more details.
[2011-08-07 13:13:21 - GMapApp] Launch canceled!
```

运行GOOGLE MAP应用仅添加了maps.jar包是不行的，得使用add-ons版API和add-ons API版模拟器。
