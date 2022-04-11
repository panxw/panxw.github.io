---
layout: post
title: "Android asop 4.4 sync and build summary"
date: 2022-04-10 00:00:00
category: "android"
tags: [Android, asop, build, repo]
---
1.First install ubuntu 16.04 on VirtualBox

2.Update and install pkgs
```
sudo apt-get update

sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm  xz-utils tk-dev libffi-dev liblzma-dev python-openssl lib32z1 lib32ncurses5 g++-multilib lib32stdc++6 libxml2-utils gperf bison flex git
```
3.Install python3.7.1
```
wget https://www.python.org/ftp/python/3.7.1/Python-3.7.1.tgz
tar -zxf Python-3.7.1.tgz
cd Python-3.7.1

vim Modules/Setup.dist
:/_socket
_socket socketmodule.c timemodule.c
_ssl _ssl.c \
-DUSE_SSL -I$(SSL)/include -I$(SSL)/include/openssl \
-L$(SSL)/lib -lssl -lcrypto

./configure –prefix=/opt/python3.7
make
sudo make install
```

4.Install java1.6
```
download jdk-16.0.2_linux-x64_bin.tar.gz  from oracle website.
cd ~/Downloads
tar -zxf jdk-16.0.2_linux-x64_bin.tar.gz
chmod +x jdk-6u45-linux-x64.bin
./jdk-6u45-linux-x64.bin
sudo mv jdk1.6.0_45/ /opt
vim ~/.bashrc
export JAVA_HOME=/opt/jdk1.6.0_45
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH
source ~/.bashrc

sudo update-alternatives --install /usr/bin/java java /opt/jdk1.6.0_45/bin/java 60
sudo update-alternatives --install /usr/bin/javac javac /opt/jdk1.6.0_45/bin/javac 60
sudo update-alternatives --install /usr/bin/javah javah /opt/jdk1.6.0_45/bin/javah 60
sudo update-alternatives --install /usr/bin/javadoc javadoc /opt/jdk1.6.0_45/bin/javadoc 60
sudo update-alternatives --install /usr/bin/javap javap /opt/jdk1.6.0_45/bin/javap 60

sudo update-alternatives --config java
sudo update-alternatives --config javac
sudo update-alternatives --config javah
sudo update-alternatives --config javadoc
sudo update-alternatives --config javap
```

5.Install repo
```
mkdir ~/bin
PATH=~/bin:$PATH
curl https://mirrors.tuna.tsinghua.edu.cn/git/git-repo  > ~/bin/repo --insecure
chmod +x ~/bin/repo
vim ~/.bashrc
export REPO_URL='https://mirrors.tuna.tsinghua.edu.cn/git/git-repo'
export GIT_SSL_NO_VERIFY=1
source ~/.bashrc
```

6.Enviroment check
```
sync --version
sync (GNU coreutils) 8.25

git --version
git version 2.7.4

python --version
Python 2.7.12
Python 3.7.1

make --version
GNU Make 4.1
Built for x86_64-pc-linux-gnu
Copyright (C) 1988-2014 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

java -version
java version "1.6.0_45"
Java(TM) SE Runtime Environment (build 1.6.0_45-b06)
Java HotSpot(TM) 64-Bit Server VM (build 20.45-b01, mixed mode)
```

7.Download asop source
```
mkdir ~/Android
cd ~/Android
git config --global user.email "winfirm@163.com"
git config --global user.name "panxw"

sudo rm /usr/bin/python
sudo ln -s /opt/python3.7/bin/python3.7 /usr/bin/python

repo init -u https://mirrors.tuna.tsinghua.edu.cn/git/AOSP/platform/manifest -b android-4.4.4_r2
repo sync
```

8.Build asop source
```
sudo rm /usr/bin/python
sudo ln -s /usr/bin/python2.7 /usr/bin/python

source build/envsetup.sh
lunch aosp_x86-eng
make clobber
make
```

9.Start emulator
```
emulator
```

Links
https://blog.csdn.net/weixin_40406241/article/details/102837938  
https://www.python.org/ftp/python/3.7.1/  
https://wenku.baidu.com/view/d5ecaece866a561252d380eb6294dd88d0d23da3.html  
https://mirrors.tuna.tsinghua.edu.cn/help/AOSP/  
