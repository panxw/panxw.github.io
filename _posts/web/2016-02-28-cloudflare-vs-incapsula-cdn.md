---
layout: post
title: "CloudFlare与Incapsula免费版CDN实测对比"
date: 2016-02-28 20:05:01
category: web
tags: [CloudFlare,Incapsula,CDN]
---
最近要给龟速的Godaddy网站主机加个访问加速器，对站友们讨论较多的几家CND提供商的免费版进行了测试，主要有百度云加速（国内），CloudFlare及Incapsula。本文只对CloudFlare与Incapsula两家免费版本实际效果进行测试。之所以忽略掉百度云加速，是因为作为一个放在Godaddy主机上的网站，域名没有备案一说，而百度去加速对没备案网站也是使用CloudFlare公司的节点加速的。  
<!-- more -->

#### 1.测试方法：
用两个域名，分别在CloudFlare与Incapsula配置免费版的CDN加速套餐，然后待节点生效后，通过 Ping测试工（http://ping.chinaz.com）对两个域名进行测试，测试线路包括电信，多线，联通，移动，海外。每组进行多轮测试，各选取某轮的测试数据进行对比。  

#### 2.测试结果：
使用CloudFlare加速的实测数据：  
![](/assets/test_result_cloudflare.png)  

使用Incapsula加速的实测数据：  
![](/assets/test_reuslt_incapsula.png)  

通过上面的数据各项指标可以看到，CloudFlare的数据优于Incapsula。另外通过测试两家的加载速度，其结果也是CloudFlare优于Incapsula。  

#### 3.总结
这里没有列出各测试的具体数据，我这里观察的总结是，两家的大部分测试结果都在200-300ms内，而CloudFlare的Ping值落在200ms以内的多于Incapsula，300ms以内的也多于Incapsula。总体而言，CloudFlare的加速效果略胜于Incapsula。  

如果域名有备案，推荐直接使用云加速，可获得较快的国内速度与海外的速度。  
如果没备案，实际发现百度云加速没有直接使用Cloud好。   
