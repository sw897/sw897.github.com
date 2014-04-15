---
layout: post
title: "解决在负载均衡中session共享问题"
description: "解决在负载均衡中session共享问题的几种方法"
category: "技术"
keywords: "负载均衡,session,共享"
tags: [nginx,负载均衡]
published: true
---
{% include JB/setup %}

今天同事偶尔问起来之前一个应用的架构，追问是如何解决session共享的问题的。
回忆了一下，好像真没有解决session共享，只是规避了共享的问题。
做法就是在nginx负载均衡的算法上，选择了ip_hash的方法。虽然只是控制相同session的请求转到同一台机器，但也算一种解决方法。

对于之前的项目，使用的是Nginx+PHP+MySQL，
其中在多台机器上跑PHP-FPM的FastCGI。
在这种结构下，要解决session共享问题有很多方法。

#### 使用ip_hash等分配方法

nginx中负载均衡配置时，可以选择ip_hash算法，这样同一个IP的请求会定向到同一台后端，这个IP下的某个客户端和某个后端建立起重色轻友的session，从而规避了多台后端之间的共享问题。ip_hash的配置如下：

{% highlight Nginx config files %}
upstream nginx.example.com
{
    ip_hash;
    server 192.168.0.1:80; 
    server 192.168.0.2:80;
}
server
{
    listen 80;
    location /
    {
        proxy_pass http://nginx.example.com;
    }
}
{% endhighlight %}

另外，Nginx负载均衡配置中，还可以选择使用upstream_hash这个第三方模块。这个模块多数情况下是用作url_hash的，但同样用来做session共享。

如果不使用Nginx做负载均衡，而使用F5等硬件实现，同样可以配置根据session进行后端分配，解决session同享问题。

#### 使用MySQL存储session

PHP可以配置将session保存在数据库中，这种方法是把存放session的表和其他数据库表放在一起，如果mysql也做了集群了话，每个mysql节点都要有这张表，并且这张session表的数据表要实时同步。
但是用数据库来同步session，会加大数据库的IO，增加数据库的负担。而且数据库读写速度较慢，不利于session的实时同步。

#### 使用memcache存储session

PHP配置文件中设置存储方式为memcache，这样php自己会建立一个session集群，将session数据存储在memcache中。

用这种方式来同步session，不会加大数据库的负担，并且安全性比用cookie大大的提高，把session放到内存里面，比从文件中读取要快很多。但是memcache把内存分成很多种规格的存储块，有块就有大小，这种方式也就决定了，memcache不能完全利用内存，会产生内存碎片，如果存储块不足，还会产生内存溢出。



