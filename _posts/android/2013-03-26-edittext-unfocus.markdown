---
layout: post
title: "让带EditText界面不聚集(无输入键盘弹出)"
date: 2013-03-26 20:05:01
category: "android"
tags: [EditText,不聚集]
---
如何让带EditText界面不聚集时无输入键盘弹出？ 在EditText建一0x0大小的布局：  
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	android:layout_width="fill_parent"
	android:layout_height="fill_parent"
	android:orientation="vertical" >
	<LinearLayout
		android:layout_width="0px"
		android:layout_height="0px"
		android:focusable="true"
		android:focusableInTouchMode="true" />
	<EditText
		android:layout_width="fill_parent"
		android:layout_height="wrap_content"
		android:text="@string/hello" />
</LinearLayout>
```