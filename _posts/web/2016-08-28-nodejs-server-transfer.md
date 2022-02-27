---
layout: post
title: "VPS服务器环境切换至Node.js"
date: 2016-08-28 20:05:01
category: web
tags: [Node.js, VPS, 入门教程]
---

去年购买的VPS，原先是Ngnix(php,tomcat),mysql,sqlite组合，主要用来作静态博客服务，并顺便用作php, java服务学习时测试。<!-- more -->

VPS内存只有256M，算是比较小的了。tomcat7太吃内存，经常要运行个啥的时候，得把它关掉才行。最近正好接触了Node.js，反正不怎么用java作服务开发，于是决定将tomcat换成Node.js的。

经过一大晚上漫长的摸索，查搜索，反复修改Nginx配置测试，最终将Nginx(php, Node.js), mysql, sqlite环境成功建起来了。

由于Node.js供一套编写高性能并发Web应用的JavaScript框架，使得js可以在服务器端运行，并自带了服务器(httpServer)的功能。对于html+Node.js的项目，由Node.js可完全搞定。这时Nginx仅用来作多域名反向代理，并将一部分请求转发到Node.js服务上来。

其它需要混合php/jsp和html的，html等静态文件交给ngnix处理，php或jsp经nginx转发给php-fpm或tomcat处理。


