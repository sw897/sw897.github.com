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
在这种结构下，要解决session共享问题有很多方法，这里总结一下。

* 使用ip_hash

如果使用Nginx的七层负载均衡，在配置文件中做如下设置


* 使用MySQL存储Session

* 使用memcache存储session

* 
