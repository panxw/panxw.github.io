---
layout: post
title: "解决ubuntu删除文件不释放空间的问题"
date: 2022-03-13 20:01:01
category: linux
tags: [ubuntu, vdisk, diskpart]
---
It's not reasonable for ubuntu(subsystem) not release space after deleting file. How to solve this problem?

First, search vdisk file path on C:\Users\Myname\AppData\Local\Packages, mine is:

```
C:\Users\Myname\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu20.04LTS_79rhkp1fndgsc\LocalState\ext4.vhdx
```

Then, under Windows PowerShell, execute:

```
wsl --shutdown
diskpart
```

And then execute follows to compat vdisk and release deleted file.

```
select vdisk file='C:\Users\Myname\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu20.04LTS_79rhkp1fndgsc\LocalState\ext4.vhdx'
attach vdisk readonly
compact vdisk
detach vdisk
exit
```

Last, check disk space.



reference link:https://blog.csdn.net/qq_39970131/article/details/119636442
