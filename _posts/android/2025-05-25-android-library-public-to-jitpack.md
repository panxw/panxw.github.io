---
layout: post
title: "Android开源库托管到JitPack的步骤"
date: 2025-05-25 00:00:00
category: "android"
tags: [Android, Jitpack]
---
#### 1.将开源项目托管在Github上，假设库的模块名为abc-library。

#### 2.项目根目录增加：jitpack.yml，配置：

```
jdk: 1.8
install:
  - ./gradlew :abc-library:publishToMavenLocal
```

#### 3.abc-library模块的build.gradle运用maven-publish插件，在afterEvaluate配置发布任务:

```
apply plugin: 'com.android.library'
apply plugin: 'maven-publish' #运用maven-publish插件

android {
	...
}

afterEvaluate {
    publishing { //配置发布任务
        publications {
            release(MavenPublication) {
                from components.release
                groupId = 'com.github.yourname' //指定group，yourname替换为自己的github用户名
                artifactId = 'abc-library' //要发布的库名
                version = '1.0.0.0' //库版本
            }
        }
    }
}
```

#### 4.push项目到Github之后，创建tag:

```
git push origin master #先提交

git tag 1.0.0.0 #再新建版发布版本，与上一步发布任务中保持一致
git push origin master --tags #提交tag 
```

#### 5.使用abc-library库

到https://jitpack.io/ 查询版本状态，就绪后可引用。根目录build.gradle脚本：

```
allprojects {
	repositories {
	    maven { url 'https://jitpack.io' }
	}
...
}
```

应用app.gradle脚本：

```
dependencies {
    implementation 'com.github.yourname:abc-library:1.0.0.0'
}
```

参考项目（早期托管在JCenter，现已托管在JitPack）：https://github.com/panxw/android-volley-manager







  
