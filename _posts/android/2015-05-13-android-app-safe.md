---
layout: post
title: "Android App安全性加强策略"
date: 2015-05-13 20:05:01
category: "android"
tags: [App安全]
---
从以下几个方面来考虑：  
1.重要数据的访问，如本地文件及网络接口需加密及签名检验，网络请求用POST，有HTTPS更好。  
2.加解密，签名，验签等算法以JNI实现，并作相应混淆处理。  
3.最后一步，使用第三方apk加固，如梆梆加固或爱加密，推荐前者。<!-- more -->  


链接：  
http://www.csdn.net/article/2013-06-26/2815995-Android-apk-bangcle  
http://www.bangcle.com/  
http://www.ijiami.cn/  
