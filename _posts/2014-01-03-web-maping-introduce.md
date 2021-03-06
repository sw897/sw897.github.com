---
layout: post
title: "Web地图制图应用介绍"
description: "在线地图制图应用，CartoDb, MapBox, 地图故事, 地图汇"
category: "技术"
keywords: "Map,CartoDB,MapBox"
tags: [Map,CartoDB,MapBox,GIS]
---
{% include JB/setup %}

    本文介绍一下当前流行的在线地图制图应用。

Web地图(WebMap)大家都不陌生，相信没有人没有用过GoogleMaps，它把GIS特别是WebGIS带入的主流的IT队伍中，
大大提高了这个小行业的技术进步速度。Web地图制图这个概念在Wikipedia中文中还没有定义页，但对照英语版有两个，
[Web Cartography][]与[Web Mapping][]，前者重定向于后者。引用Wikipedia里的一句介绍:
> web mapping is more than just web cartography,it is both a service activity and consumer activity.

也就是mapping不止于cartography。这里汇总的应用大体就就当属于cartography，
简单理解就是通过Web在线制作地图(Online Mapping)。
这种应用一般需要解决海量存储等基础设施，所以应当是基于云计算架构的。

这些应用大体可以分这么两类：

### UGC制图

UGC制图是一种交互式制图，用户参与更新底图、扩充POI等数据

* [OpenStreetMap][]
* [Google Map Maker][]
* [Nokia HERE Map Creator][]
* 当然还有移动终端应用[Waze][]，它的众包的概念，个人理解就是UGC的高阶模式

UGC制图公司或机构一般需要拥有海量基础数据，本身就是举足轻重的地图数据提供者，使用UGC的模式，
借助用户来改善地图数据，是“大家帮助大家”的思想。感兴趣的朋友可以加入到其中，做做贡献。

### 在线制图(Online Mapping)

在线制图应用，主要是个人专题地图制图，用户提供专题数据，使用应用平台完成可视化与交互，
这种应用属于云计算的一种形式，即应用即服务。用户使用它完成工作或作品，然后共享分发

* [Mapbox][]
* [CartoDB][]
* [MangoMap][]
* ArcGIS Online[地图故事][]
* SuperMap[地图汇][]

这些应用是最近比较时兴的，它们一般技术先进并开放，把科研人员从基本编码中解放出来，
把非专业人员带入制图的世界，让专业人员更专注于专业的事情。总之，大体路线是提供Cloud Infrastructure和制图服务，
解决基础制图问题，包括底图，符号表达，专题可视化等等，剩下的，就是让用户专注专题数据，专注要表达的信息处理，
同时，可视化表达上，也有多种方案，可以让用户快速完成一个拥有绝佳交互体验与视觉冲击的地图。
但这些应用并不是免费的大餐，付费比较昂贵，对于一般用户，只能免费试用一下。

当然，几家技术路线与背景各有不同，提供的功能也有差别。
国外的几家网站都使用HTML5技术，界面与交互更让人舒适，一种高大上感觉。其中[CartoDB][]与[Mapbox][]后面会单独介绍一下。

ArcGIS做为业内的领军，Online产品也是越来越好，而且商业化模式成功，[地图故事][]应当算是这几个中名气最大的了，本土化支撑，
特别是在高校中举办各种活动，培养新生的GISer们，大家都快感觉"ArcGIS是国产软件"不是错觉了。

超图的[地图汇][]也是其中很有特色的产品，结合建设国内大量在线地图应用的经验，
直接将属性与空间的连接功能(GeoCode,GeoReference)结合进去，
按世界，国家，省，市等几个等级组织，如果属性表里中有标准地名字段，可直接在图上形成专题图。
这种方法大大降低了用户门槛，更适合一般用户使用。另外，还提供了变形地图等少见的可视化方法，也是一个创新。
不过产品比较固化，没有给用户提供更多层次的接口，给人传统网站应用的感觉。
特别国内特色的，针对局域网的部署方案，典型的面向政府部门的应用模式。只能问一句：咱能有点互联网应用的节操么？

这里主要介绍几个制图应用，至于如何选择，还要看大家的需求而定。
个人比较推荐的是[CartoDB][]，本身功能强大，分发方便，又提供多种层次接口，可伸缩性强，适合有一定想法的用户。


[OpenStreetMap]:http://www.openstreetmap.org
[Google Map Maker]:https://www.google.com/mapmaker
[Nokia HERE Map Creator]:http://heremaps.cn/mapcreator
[Waze]:https://www.waze.com/editor/
[Mapbox]:https://tiles.mapbox.com/sw897
[CartoDB]:https://sw897.CartoDB.com/dashboard/
[MangoMap]:https://mangomap.com/maps
[地图故事]:http://storymaps.arcgisonline.cn/home/index.html
[地图汇]:http://www.dituhui.com/
[Web Cartography]:http://en.wikipedia.org/wiki/Web_cartography
[Web Mapping]:http://en.wikipedia.org/wiki/Web_mapping
