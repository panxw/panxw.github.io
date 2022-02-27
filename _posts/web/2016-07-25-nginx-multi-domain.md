---
layout: post
title: "基于Nginx的Linux VPS 多域名空间配置"
date: 2016-07-25 20:05:01
category: web
tags: [Nginx, VPS, 多域名]
---
#### 一、从虚拟主机说起

以前，在我印象中VPS都是很贵的，总舍不得花那价钱入手。那时，建站基本都是用虚拟主机，这东西不仅便宜，而且使用很简单，基本不需要我们作何配置。主机商们大都很贼，他们一般都允许在一个虚拟机绑定多个域名，然而这些绑定的域名都是指向同一个空间。当访问这些域名时，大家看到的是同一个网站。那么要想让多个域名访问时，各自到达的网站完全不一样，就得再购买新的虚拟空间来绑定域名了。<!-- more -->

少数主机商虽然有多空间版本的虚拟主机出售，然而这类主机的价格要么很高，要不就是空间数目有限，顶多2-3个。后来，随着云计算技术的发展，建站托管的选择越来越丰富。如今，不仅有新生的AWS，阿里云，腾讯云，及各种paas服务可选，还可以选择VPS，及老牌ISP商的各类空间。当前VPS的价格，再也不是从前高不可及的了，甚至一些VPS商提供的套餐价格比虚拟主机还便宜。

#### 二、VPS好处多

使用VPS的主机的好处是，你可以随意折腾，从所装的系统，到系统上安装什么软件，全部由你决定。操作系统任你选，如windows/linux；网站环境随你搭配，如jsp/php/js, mysql/sqlite, nodejs/tomcat/nginx等；软件安装了可卸载/重装，甚至操作系统也能重装或更换，想怎么玩就怎么玩。最得要的是，我们可以利用Nginx实现多空间的服务器，绑定多个域名，各域名独立访问。

反之，缺点也是明显的，安装系统，软件，及相关配置也得由你来定，开始接触时可能会带来不少困扰，折腾一阵子后基本能适应，不能适应的建议放弃VPS这条路吧。

#### 三、Linux Nginx配置多空间服务器

我个人钟爱Debian，它够稳定，且适合折腾，因此我的VPS也就是安装的Debian的Linux OS。下面是安装nginx及配置：

```
apt-get update
apt-get install nginx
```

/etc/nginx/nginx.conf文件下添加多个域名空间：

```
server{
    listen 80;
    server_name www.abc.com;
    root  /var/www/abc.com;
    index index.html index.htm;
    location \ {
      
    }
}

server{
    listen 80;
    server_name www.bcd.com;
    root  /var/www/bcd.com;
    index index.html index.htm;
    location \ {

    }
}
```

配置完成后重启Nginx服务

```
/etc/init.d/nginx restart
```

然后，只需将www.abc.com, www.bcd.com的解析指向VPS的IP，待解析生效后，我们就可以分别访问abc.com, bcd.com了。




