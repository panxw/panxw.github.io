---
layout: post
title: "Android Dialog风格Activity"
date: 2011-11-22 20:05:01
category: "android"
tags: [Dialog]
---
在Manifist文件中，对Activity添加一项theme的属性，值为@android:style/Theme.Dialog就能将Activity以对话框形式显示。例如： 
 
```
<activity android:name=".DialogActivity" android:label="@string/new_name"android:theme="@android:style/Theme.Dialog"/>
```
