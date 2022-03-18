---
layout: post
title: "Steps to run legu on Linux(access by Xshell)"
date: 2021-11-20 20:05:01
category: android
tags: [Android, legu, Linux]
---

Steps to run legu on Linux(access by XShell):

1.install Android cmd tools and legu tools on Linux(ubuntu). 
```
android_sdk cmdtools newlegu run_upload.sh  run_legu.sh upload
```

2.execute ./run_upload.sh to upload source Apk!  
3.execute ./run_legu.sh to protect rebuild apk,  and last start download process!


run_upload.sh 
```
#!/bin/bash
echo "please wait to compelete!"
cd ./upload
rz
cd ../
echo "done!"
exit
```

run_legu.sh 
```
#!/bin/bash
if [ "$1" == "" ];then
  echo "Please input path as: ./run.sh ./upload/xxxx.apk"
  exit 5
fi

cd ./newlegu

echo "path: $1"
resFile=`basename "root/$1"` 
echo $resFile

signedFile="./Jiagu_$resFile"
echo $signedFile


./jiagu "/root/$1" ./unsigned.apk base.conf 

/root/android_sdk/build-tools/28.0.3/apksigner sign --ks abc.keystore --ks-key-alias bestv --ks-pass pass:abc12345690  --key-pass pass:abc12345690 --out $signedFile  ./unsigned.apk

rm -f ./unsigned.apk

cd ../
sz "./newlegu/$signedFile"

echo "done!"
exit
```