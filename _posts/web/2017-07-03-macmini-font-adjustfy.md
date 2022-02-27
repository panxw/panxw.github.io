---
layout: post
title: "Mac mini接显示器视觉模糊调节"
date: 2017-06-02 20:05:01
category: "web"
tag: [Mac,mini,显示器,模糊]
---
使用Mac mini+AOC显示器组合有大半年了，一直感觉字体模糊感很强，视觉上很是不舒服。难道是显示器和主机不匹配？

今天上网查找了下，发现不止我一个人有这种疑问，找到下面的方法，试完后视觉效果好多了。打开终端，输入：

```
defaults -currentHost write -globalDomain AppleFontSmoothing -int 1
```
重启后可以看到改变后的效果，1是字体大小，还可以设置为2，3，值越大字体的模糊感越强！
