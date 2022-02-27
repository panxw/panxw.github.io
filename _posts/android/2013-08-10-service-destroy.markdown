---
layout: post
title: "Android退出前的stopService"
date: 2013-08-10 20:05:01
category: "android"
tags: [Service]
---
问题：
Android用System.exit(0)退出时，如果前面有stopService可能使Service未来得及进入onDestroy，整个应用进程就已退出了，更可能产生异常。  

解决办法：延时100ms左右再调stopService.   
