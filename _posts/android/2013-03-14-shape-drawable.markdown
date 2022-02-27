---
layout: post
title: "背景为shape selector的drawable的问题"
date: 2013-03-14 20:05:01
category: "android"
tags: [selector]
---
背景为selector(item state_pressed="false" shape)时，里面的条目只能为selector(item state_pressed="true" shape)，否则选中无效果。<!-- more -->

#### 举例：
1.边框背景：  

```
<?xml version="1.0" encoding="UTF-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
	<item><shape>
			<stroke android:width="0.8dp" android:color="#d4d3d3" />
			<solid android:color="#f3f4f4"></solid>
			<corners android:radius="0.5dp"/>
		</shape></item>
</selector>
```

2.条目背景：  

```
<?xml version="1.0" encoding="UTF-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
	<item android:state_pressed="true"><shape>
			<solid android:color="#e6e6e6" />
		</shape></item>
</selector>
```
