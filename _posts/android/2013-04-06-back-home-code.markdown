---
layout: post
title:  "返回系统HOME桌面"
date: 2013-04-06 20:05:01
category: "android"
tags: [Android,HOME]
---
在程序里不关闭应用，返回到系统HOME桌面的代码：  

```
Intent intent = new Intent();
intent.setAction(Intent.ACTION_MAIN);
intent.addCategory(Intent.CATEGORY_HOME);
startActivity(intent);
```
