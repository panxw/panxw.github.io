---
layout: post
title: "Ubuntu下Ruby1.9/2.0版本切换"
date: 2016-03-02 20:05:01
category: web
tags: [ubuntu,ruby2]
---
Ubuntu 14.4以上，即便是通过:  

```
sudo apt-get install ruby2.0 ruby2.0-dev
```

指定为2.0版，也会同时安装1.9版本，且系统默认使用1.9版。  

目前，安装Jekyll会提示使用Ruby>=2.0，那么要使用ruby2.0怎么办？有办法，切换一下版本。<!-- more -->建立一个shell脚本，switchruby2.0.sh，内容如下：  

```
cd /usr/bin 
ln -sf ruby2.0 ruby 
ln -sf gem2.0 gem 
ln -sf erb2.0 erb 
ln -sf irb2.0 irb 
ln -sf rake2.0 rake 
ln -sf rdoc2.0 rdoc 
ln -sf testrb2.0 testr 
```

然后添加用户执行权限：  

```
chmod u+x  switchruby2.0.sh
```

然后：  

```
sudo ./ switchruby2.0.sh
```

接着再更新下gem:  

```
gem update --system
gem pristime --all
```

完成后通过 ruby -v确认下当前使用的ruby版本。  
等切换到2.0后，再执行sudo apt-get install jekyll，就会成功了。  

那么，用着有需要切换回1.9怎么办？同理建立一个shell脚本switchruby1.9.sh，内容见下面：  

```
cd /usr/bin/
ln -sf ruby1.9.1 ruby
ln -sf gem1.9.1 gem
ln -sf erb1.9.1 erb
ln -sf irb1.9.1 irb
ln -sf rake1.9.1 rake
ln -sf rdoc1.9.1 rdoc
ln -sf testrb1.9.1 testrb
```

保存，其余操作同切换到2.0.  

参考：http://www.kaijia.me/2014/08/ubuntu-14-04-switch-defaults-to-ruby-2-0/  
