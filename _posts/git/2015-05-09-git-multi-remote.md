---
layout: post
title: "基于bitbucket和github构建私有+开源一体的代码中心"
date: 2015-05-09 20:05:01
category: "git"
tags: [github,bitbucket,git]
---
#### 一、基于bitbucket和github打造代码中心
即private项目仅托管在bitbucket上，而开源项目，除了托管bitbucket外，还push到github上去。<!-- more -->  

#### 二、git添加多个远程库操作
```
cd repo
git remote add origin <bitbucket git address>
git remote set-url --add origin <github git address>
git push origin master
```

最后一句一次性push到2个库里面了
