---
layout: post
title: "让Android ProgressDialog在按返回键可dismiss"
date: 2013-03-08 20:05:01
category: "android"
tags: [ProgressDialog]
---
让ProgressDialog可按返回键时dismiss，但空白区不dismiss：  

```
progressDialog.setCanelable(true);
progressDialog.setCanceledOnTouchOutside(false)
```