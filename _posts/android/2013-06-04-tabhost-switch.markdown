---
layout: post
title: "TabActivity子Activity以代码进行切换"
date: 2013-06-04 20:05:01
category: "android"
tags: [TabActivity]
---
TabActivity子Activity直接以startActivity方式切换子Activity时会有些问题，不过可以这样解决：  

1,在TabActivity中加入切换方法，如AppHostActivity.java中：  

```
public void setCurrentTab(int index) {
		try {
			this.tabHost.setCurrentTab(index);
		} catch (Exception e) {
			e.printStackTrace();
		}
}
```

2,在AppHostActivity子Activity中这样切换到其它Activity:  

```
((AppHostActivity)getParent()).setCurrentTab(1);
```
