---
layout: post
title: "Ubuntu下tomcat+nginx服务器架设小记"
date: 2015-08-25 20:05:01
category: web
tags: [nginx, vagrant, server]
---
操作环境：一台Vagrant+Ubuntu 14.4 Lts box虚拟机。

实现目标：ngnix实现静态，动态分离。静态ngnix代理，动态代理给fastcgi(php)，tomcat。域名解析到CNAME/ip，让nginx识别挂载到不同目录。<!-- more -->

#### 1.系统软件源更新
```
sudo apt-get update //更新source.list
```

#### 2.安装jdk
```
sudo apt-get install openjdk-7-jdk
```

如果有多个java版本，需要指定：

```
sudo update-alternatives --config java
```

#### 3.安装tomcat
```
sudo apt-get install tomcat7
```

这一步输入http://localhost:8080可以看到tomcat的欢迎页面了。  

插一句，部署war包：

```
sudo cp abc.war   /var/www/
cd /var/www
sudo jar -xvf abc.var
```


#### 4.安装nginx
```
sudo apt-get install nginx
```

到这一步lynx http://localhost可以看到nginx欢迎页了。  

#### 5.mysql安装
输入mysql有提示多个选择可安装，这里安装常用的。

```
sudo apt-get install mysql-server
```

安装mysql-client-core-5.6（或5.5)容易报下面的错误。

```
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)
# ln -s /var/run/mysqld/mysqld.sock /tmp/mysql.sock
```

#### 6.php
安装php（只用下面两个就够与nginx配合使用了)

```
sudo apt-get install php5-cli php5-fpm
mysql -u root
```

解决Java无法通过JDBC连接到Mysql的问题，需要添加相应驱动。  
下载驱动，如：mysql-connector-java-5.0.6-bin.jar  
放到相应用目录，然后考备到java及tomcat的lib目录下：

```
sudo cp mysql-connector-java-5.0.6-bin.jar /usr/share/java/lib
sudo cp mysql-connector-java-5.0.6-bin.jar /usr/share/tomcat7/lib
```

重启下tomcat。  

#### 7.tomcat与nginx配置
每次修改配置相应服务要重启，命令如下：

```
sudo /etc/init.d/tomcat7 restart
sudo /etc/init.d/nginx restart
```

查看服务错误或访问日志：

```
sudo cat /var/log/nginx/access.log(error.log)
sudo cat /var/log/tomcat7/access.log(error.log)
```

#### 8.配置修改举例：
编辑/etc/tomcat7/server.xml Host节点下加入，让ngnix可访问到tomcat。

```
    <Context path="" docBase="/var/www" reloadable="true"/> 
    <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
           prefix="localhost_access_log." suffix=".txt"
           pattern="%h %l %u %t &quot;%r&quot; %s %b" />
```

编辑/etc/nginx/nginx.conf，加入：

(a)只有一个server时：静态，php, jsp，全搞定！

```
##
# Virtual Host Configs
##
server {
        listen 80;
        charset utf-8;
        root /var/www;
        index index.html index.htm index.php index.jsp;
        #server_name  ;
        location / {   #处理静态html
        }

        location ~.php$ { #处理动态php
                fastcgi_pass unix:/var/run/php5-fpm.sock;
                fastcgi_index index.php;
				fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                include fastcgi_params;
        }

        location ~\.(jsp|do|jspx)?$ {#处理动态java，交给tomcat
                index index.jsp index.do;
                proxy_pass http://localhost:8080;
        }

        error_page 404 /404.html;
        error_page 500 502 503 504 /50x.html;
}
```

#下面两项导入不要，禁止跳到nginx默认首页。

```
#include /etc/nginx/conf.d/*.conf;
#include /etc/nginx/sites-enabled/*;
```

(b)处理多个server时：静态，php,  java分别处理，实现多域名绑定：

```
##
# Virtual Host Configs
##
server {#运行html
    listen 80;
    charset utf-8;
    root /var/www;
    index index.php index.html index.htm;
    server_name www.abc.com;
    location / {
    }
}

server { #运行java
    listen 80;
    charset utf-8;
    root /var/www/java;
    index index.jsp index.do index.html index.htm;
    server_name java.abc.com;
    location ~\.(jsp|do|jspx)?$ {
            proxy_pass http://localhost:8080;
    }
}

server { #运行php
    listen 80;
    charset utf-8;
    root /var/www/php;
    index index.php index.html index.htm;
    server_name php.abc.com;
    location ~.php$ {
            fastcgi_pass unix:/var/run/php5-fpm.sock;
            fastcgi_index index.php;
			fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include fastcgi_params;
    }
}
```

#下面两项导入不要，禁止跳到nginx默认首页

```
#include /etc/nginx/conf.d/*.conf;
#include /etc/nginx/sites-enabled/*;
```
