---
layout: post
title: "Android startActivityForResult返回时需要注意的"
date: 2012-03-02 20:05:01
category: "android"
tags: [Android]
---
在onActivityResult中，即便是从后一个页面按back键返回的也是有resultCode的，且其值为0,其data为null.  
