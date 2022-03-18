---
layout: post
title: "Install android sdk cmdtools on Linux"
date: 2022-03-16 20:05:01
category: android
tags: [Android, cmdtools, Ubuntu, Linux]
---
on Ubuntu for example:
```
cd ~/
```

download Command line tools from https://developer.android.google.cn/studio
```
upload or download zip to ~/
unzip commandlinetools-linux-8092744_latest.zip
ls |grep cmdline-tools
```
got cmdline-tools directory.


mkdir for sdk_root:
```
mkdir android_sdk
```

update cmdline-tools/:
```
cd cmdline-tools/
mkdir latest
mv bin lib NOTICE.txt source.properties ./latest
```

set sdk_root and install modules:
```
cd latest/bin/
./sdkmanager --sdk_root=~/android_sdk
./sdkmanager --install "platforms;android-26;"
./sdkmanager --install "build-tools:28.0.3"
```

build-tools or platforms will be installed to ~/android_sdk
```
cd ~/
ls 
android_sdk cmdline-tools 
```

done!
