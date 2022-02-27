---
layout: post
title: "阿里弹性Web托管屏蔽IP的.htaccess设置"
date: 2016-04-10 20:05:01
category: web
tags: [htaccess, 弹性Web托管]
---
几个站都被几个来自南京的IP恶意访问了。其中一个为阿里弹性Web托管，提工单问技术支持找到了方法。.htaccess加入设置：

```
RewriteEngine On
##Block ip
RewriteCond %{http:X-Forwarded-For} (180.97.106.161|180.97.106.162|180.97.106.36|180.97.106.37) [NC]
RewriteRule (.*) – [F]  
```
<!-- more -->
技术支持提供的另外几个方案，在弹性WEB托管上都无效：

```
order allow,deny
deny from 192.168.0.2
deny from 192.168.0.3
deny from 192.168.0.4
allow from all
```
http://www.biaodianfu.com/block-ip-from-accessing-website-using-htaccess.html




