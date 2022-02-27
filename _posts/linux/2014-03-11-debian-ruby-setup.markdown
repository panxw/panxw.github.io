---
layout: post
title: "Debian/Linux ruby setup"
date: 2014-03-11 20:05:01
category: "linux"
tags: [Debian,ruby]
---
有别于Windows下的rubyinstall+devkit安装与配置。Debian/Linux下方便多了。  

#### 一、安装Git
```
sudo apt-get install git
```

#### 二、安装C/C++开发环境
```
sudo apt-get install build-essential
```
<!-- more -->  

#### 三、安装ruby开发环境
```
sudo apt-get install ruby irb rdoc ruby-dev
```

#### 四、安装ruby gem
安装好ruby的基本开发环境后，就可以安装ruby gem了，如jekyll。

```
sudo gem install rdiscount jekyll redcarpet
```
