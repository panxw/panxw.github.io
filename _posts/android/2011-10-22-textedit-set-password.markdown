---
layout: post
title:  "Android EditText控件的密码输入框可见性设置"
date: 2011-10-22 20:05:01
category: "android"
tags: [EditText]
---
密码输入框可见性设置：  

```
public void showAsPassword(show) {
	if (show) {
	 passEdit.setInputType(0x90);
	} else {
	 passEdit.setInputType(0x81);
	}
}
```