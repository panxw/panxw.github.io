---
layout: post
title: Faqs when run Ubuntu in VirtualBox on Windows.
category: linux
tags: [linux, ubuntu, virtualbox]
date: 2022-04-16 08:00
---
Faqs when run Ubuntu in VirtualBox on Windows.

#### 1.compact linux space after deleting files on VirtualBox.

a. first execute follow commands in linux:
```
sudo dd if=/dev/zero of=zero.fill
sudo rm -f zero.fill
```
then close virtual mathine.

b. redirect to vm vdi file directory on Windows, execute:
```
'C:\Program Files\Oracle\VirtualBox\VBoxManage.exe' modifyhd ./ubuntu.vdi --compact
```

#### 2.set share folder on VirtualBox.
a. set share folder on Virtualbox settings.

b. linux operation, tools and mount commands:
```
sudo apt-get install virtualbox-guest-utils

sudo mkidr /mnt/shared
sudo mount -t vboxsf share /mnt/shared
```
