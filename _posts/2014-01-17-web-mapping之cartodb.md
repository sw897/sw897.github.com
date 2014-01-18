---
layout: post
title: "Web Mapping之CartoDB"
description: ""
category: ""
tags: [Map,CartoDB]
---
{% include JB/setup %}

> We help people visualize and analyze geospatial data.
> From polygons to points. From hundreds to millions. No limits with CartoDB.

这是CartoDB主页上的介绍，帮助用户分析与可视化地理空间数据。可以应对成千上万的点或多边形数据。

在注册过免费账号后，其当前提供的免费服务内容有：

* 5个专题表
* 5M存储空间
* 每月1万次地图浏览

<img src="https://dl.dropboxusercontent.com/u/57451074/github/sw897/images/cdb_freeserver.png" alt="cdb_freeserver" />

只能用少得可怜来形容。但这些足以来了解其灵活的功能会为您的工作带来的便利。如果有需求，可以转为付费用户。

> 以下以CartoDB Blog上的一个展示为例，数据为美国邮局的shp文件，在以下地址下载[邮局SHP][]，包含位置与建立时间等属性字段。
> 准备好数据后，进入cartodb准备开始

### 试用

* 创建新表，并选择刚下载到本地的shp压缩包

<img src="https://dl.dropboxusercontent.com/u/57451074/github/sw897/images/cdb_newtable.png">

* 自动上传完成后会进入Table的浏览页面


* 选择创建Map View，更换底图(BaseMap)

<img src="https://dl.dropboxusercontent.com/u/57451074/github/sw897/images/cdb_mapview.png">

* 通过Wizards来配置专题地图表现，这里模仿blog中的设置，选择Toque进行时间序列可视化，其它设置如图

<img src="https://dl.dropboxusercontent.com/u/57451074/github/sw897/images/cdb_config.png">

* 发布与分享，通过Publish功能，可以选择:URL,Embed,API三种发布方式，并可将url发布到facebook或twitter

<img src="https://dl.dropboxusercontent.com/u/57451074/github/sw897/images/cdb_publish.png">

这里按embed的方式，引用交互地图

<iframe width='100%' height='520' frameborder='0' src='http://sw897.cartodb.com/viz/68695938-7f47-11e3-9aeb-9b0c6170d3d4/embed_map?title=true&amp;description=true&amp;search=false&amp;shareable=true&amp;cartodb_logo=true&amp;layer_selector=false&amp;legends=false&amp;scrollwheel=true&amp;sublayer_options=1&amp;sql=&amp;zoom=3&amp;center_lat=36.77409249464195&amp;center_lon=-79.453125'> </iframe>


* 创建新的可视化方案，使用密度图方案，效果如下

<iframe width='100%' height='520' frameborder='0' src='http://sw897.cartodb.com/viz/bd2d7962-7f48-11e3-a612-db6222d3edab/embed_map?title=true&amp;description=true&amp;search=false&amp;shareable=true&amp;cartodb_logo=true&amp;layer_selector=false&amp;legends=false&amp;scrollwheel=true&amp;sublayer_options=1&amp;sql=&amp;zoom=3&amp;center_lat=36.77409249464195&amp;center_lon=-79.453125'> </iframe>


> 由于免费账户只有1万的浏览次数，所以很容易挂掉，看不到地图不要惊奇

> 注意：直接从cartodb的public中拷贝的embed script不能直接在jekyll中使用，需要在\</iframe\>结束标签前加入一个空格

### CartoDB

CartoDB的HOST基础设施并无太多介绍，不能判断是否使用了云计算，但知道其使用Ubuntu12.04LTS操作系统，
其上的软件全部使用开源软件，在GitHub可以找到其项目，其特性如下：

* 上传、创建、编辑、可视化和导出空间数据的用户界面

* 利用 PostgreSQL 和 PostGIS 构建空间数据库

* 提供支持SQL查询的API，API使用GeoJSON和KML格式化结果，并基于HTTP提供

* 支持SQL的地图瓦片化，并利用 CartoCSS 支持样式配置

* 基于OAuth的认证

在单台机器上搭建一个CartoDB的服务器，其文档中有在 Ubuntu 10.04 上的安装步骤。以下记录自己的安装过程。

#### STEP1.

#### STEP2.

#### STEP3.




[邮局SHP]: https://viz2.cartodb.com/api/v2/sql?q=SELECT%20*%20FROM%20us_po_offices&format=SHP
