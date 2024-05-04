---
layout: post
title: "Android Fileprovider共享的apk文件读取与安装"
date: 2024-05-04 00:00:00
category: "android"
tags: [Android, FileProvider]
---
Fileprovider共享的文件，外部应用不能通过路径读取。
因为content query到的只有文件名（非完整路径）和文件大小。

例如查询：
```
content query --uri content://com.panxw.appstore.fileprovider/apk-external-cache-root/apk_1GRFD49R1DMTR.apk 
```
输出：
```
Row: 0 _display_name=apk_1GRFD49R1DMTR.apk, _size=11748549
```

Fileprovider提供了ParcelFileDescriptor获取FileDescriptor，通过FileDescriptor可以获取共享文件的输入流。
比如安装服务拿到apkUri之后，先判断，如果是content类型的，则需要读文件流，保存临时apk文件，再安装：
```
//读文件名与大小。
Cursor cursor= context.getContentResolver().query(apkUri, new String[]{
                        OpenableColumns.DISPLAY_NAME, OpenableColumns.SIZE }, null,null, null);                  
//读文件流，保存apk文件
ParcelFileDescriptor parcelFileDescriptor = context.getContentResolver().openFileDescriptor(apkUri, "r");
FileInputStream fileInputStream = new FileInputStream(parcelFileDescriptor.getFileDescriptor());
Logger.debug(TAG, "parcelFileDescriptor:"+fileInputStream.available());
byte buffer[] = new byte[1024];
int len = 0;
int total = 0;

FileOutputStream fileOutputStream = new FileOutputStream(new File("temp.apk")); 
while ((len=fileInputStream.read(buffer))>0){
    total+=len;
    fileOutputStream.write(buffer);
}

fileOutputStream.close();
fileInputStream.close();
```

//再用缓存apk文件安装。

安装完成之后，记得删除缓存apk文件。
