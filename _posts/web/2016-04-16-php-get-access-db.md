---
layout: post
title: "php加入access数据库支持方法"
date: 2016-04-16 20:05:01
category: web
tags: [php, access]
---
要在linux的php环境中要访问access数据库，实属无赖。度娘一下找到了办法：

1.安装php的odbc支持

```
apt-get install php5-odbc
```
<!-- more -->
2.用php探针检测是否安装成功

建一个测试页面：

```
<?php
phpinfo();
?>
```

访问测试页面，查看ODBC Support是否Enable了。

3.使用odbc连接access数据库php代码
```
<?php 
$db = new PDO("odbc:driver={microsoft access driver (*.mdb)};
              dbq=".realpath("data.mdb")) 
              or die("Connect Error");
$rs = $db->query('select * from user');
print "<pre>";
print_r($rs->fetchAll());
print "</pre>";
?>
```





