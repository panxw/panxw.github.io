---
layout: post
title: "Jekyll输出特定栏目文章列表的方法"
date: 2016-03-05 20:05:01
category: "web"
tags: [Jekyll, 栏目列表]
---
我们可以通过以下几步来输出某个栏目下的文章列表。

#### 1.新建一个分类文件xxx.md
xxx.md用于显示”XXX“栏目下的文章列表，其内容如下：  
![](/assets/column_list_code.png)  
因jekyll模板代码不能显示在代码块中，因此用图来显示，代码可从<https://github.com/panxw/jekyll-theme-codes>找到！<!-- more -->

#### 2.在写文章时指定category为XXX
```
---
layout: post 
title: "hello world" 
category: XXX
---
```

#### 3.分类链接时使用
```
<a href="xxx.html">XXX</a>
```

#### 4.参考Jekyll模板
其实，本站的几个栏目就是基于这个思路搭建的，如Android开发、Web建站、软件编程等。  
本站所用模板地址：<https://github.com/panxw/panxw.github.com>  
如有相关不明白的问题，可在文章后面直接留言给我！  
