---
layout: post
title: "解析错误－解析包时出现问题－解决方法"
date: 2011-10-22 20:05:01
category: "android"
tags: [apk]
---
当使用下列方式安装apk时：  

```
final String filePath = "/data/data/" + getPackageName() + "/files/" + "test.apk";
Intent intent = new Intent();
intent.setAction(android.content.Intent.ACTION_VIEW);
intent.setDataAndType(Uri.parse("file://" + filePath), "application/vnd.android.package-archive");
intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
startActivity(intent);
```<!-- more -->

报“解析包时出现问题”时，log输出如：  

```
	...Permision denied
	W/zipro   ( 1362): Unable to open zip '/data/data....
```

原因在于，apk临时存放在应用的files或cache目录时，其读写权限有限。  
需要修改其文件权限，Runtime执行"chmod 777 filePath"，或以openFileOutput("test.apk", MODE_WORLD_READABLE)创建输出流造成的。  

当然，apk直接创建在SD卡中，也不会有上述错误出现。  

(完~)