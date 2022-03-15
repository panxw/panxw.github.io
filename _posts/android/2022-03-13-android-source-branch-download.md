---
layout: post
title: "下载Android指定版本源码"
date: 2022-03-13 20:05:01
category: android
tags: [Android, source, repo]
---
```
mkdir ~/bin
PATH=~/bin:$PATH
```

```
curl https://mirrors.tuna.tsinghua.edu.cn/git/git-repo -o > ~/bin/repo
chmod +x ~/bin/repo
```

```
vim ~/.bashrc
export REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo'
source ~/.bashrc
```

```
mkdir WORKING_DIRECTORY
cd WORKING_DIRECTORY
```

```
repo init -u https://mirrors.tuna.tsinghua.edu.cn/git/AOSP/platform/manifest -b android-5.1.0_r1 #android-9.0.0_r61
repo sync
```
