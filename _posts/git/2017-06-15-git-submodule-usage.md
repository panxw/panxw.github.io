---
layout: post
title: "git submodule(子模块)基本用法"
date: 2017-06-15 20:05:01
category: "git"
tags: [git,submodule,子模块]
---
git提供了submodules机制，可以为当前的git工程引入第三方的git库，而不需要直接将第三库copy过来。当第三方git库有更新时，也能很方便地进行同步。<!-- more -->

下面介绍一下git submoudle命令的基本使用，示例：

1. 初始化，为当前工程(project)指定一个第三子的git子模块(another)：

```
cd project 
git submodule add git@xxxx:/another.git another
```

这段代码会创建.gitmoudles文件记录git子模块信息。并且开始clone子模块的代码到another目录下。

2. 修改project 目录下的.gitignore文件，使其忽略提交another目录下的文件 ：
```
...
another/
```
然后将.gitmodules及.gitignore都提交。

3. 根据.gitmoudles的记录的初始化

当新clone project工程时，完成后是没有another目录的。这时只需在project目录运行：

```
git submodule init
git submodule update
```
就能将another的git库clone进another目录了。

4. 更新git子模块
当子模块有了更新后，我们也可以通过下面的命令更新git子模块。
```
cd another
git pull
```
