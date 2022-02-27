---
layout: post
title: "Android TV开发中特定焦点定位"
date: 2015-09-12 20:05:01
category: "android"
tags: [焦点,定位,TV]
---
TV界面开发中，焦点处理有时候不能完全依赖系统。  
焦点从一个View到另一个View的过程中，会有一个完整的KeyPress过程（KeyEvent.ACTION_DOWN和KeyEvent.ACTION_UP），前一个焦点所在ViewGroup可截获KeyEvent.ACTION_DOWN， 而后一个焦点所在ViewGroup可截获KeyEvent.ACTION_UP。  
<!-- more -->

当需要将焦点定位到某个View时，我们就要在ViewGroup/Activity的dispatchKeyEvent方法中对事件监听，并在KeyEvent.ACTION_DOWN动作时，调用目标View的requestFocus()，再返回true。  
在KeyEvent.ACTION_DOWN事件来临手动定位下一个焦点，是因为KeyEvent.ACTION_UP事件来临时系统已完成焦点处理，再处理已不能达到所需效果了。  
