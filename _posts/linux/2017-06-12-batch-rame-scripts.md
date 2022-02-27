---
layout: post
title: "批量文件加前缀的shell脚本"
date: 2017-06-12 20:05:01
category: linux
tags: [批量,文件,前缀,shell脚本]
---
批量文件加前缀的shell脚本(rname.sh)：
```
#!/bin/sh
cmdfile="rname.sh"
addr="bappstore_"

for filename in `ls`
do
	if [ $cmdfile != $filename ] 
	then 
		newfilename=$addr$filename #=不能有空格
		echo $newfilename
		mv $filename $newfilename
	fi
done
```

放入某个目录后，执行./rname.sh即可。

