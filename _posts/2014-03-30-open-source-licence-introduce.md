---
layout: post
title: "常见开源协议与GIS开源软件归类"
description: "介绍与对比GPL,LGPL,BSD等常见开源协议，总结GIS开源所采用的开源协议"
category: "技术"
keywords: "OpenSource,GPL,BSD,GIS"
tags: [OpenSource,GIS]
published: true
---
{% include JB/setup %}

### 介绍

开源软件近几年越来越流行，从SourceForge到GitHub,Bitbucket，存在着不计其数的开源项目。在国内，几家大公司也开始开放平台，拥抱开源，CSDN的开源平台也红红火火。GIS行业内，
有那么几个主要的基础库与软件也是得到了广泛的应用，特别是OSGEO组织下的GDAL,MapServer等等。在使用这些开源软件的时候，其协议授权，也就是licence，是我们要特别注意的。这些开源协议明确说明了使用者应该遵循的原则，从而确定了使用者使用开源软件的方式与方法，能否二次开发，进而商业发布，还是只能开源。

### 开源授权

开源协议有很多，任何人写一个开源软件都可以自定义一个licence。常见的有这么6种：
GPL协议系列(v1,v2,v3...)，LGPL协议，BSD协议，Apache licence 2.0，MIT协议和Mozilla协议。
这几种协议规定都是很多页的英文，要仔细读完很需要时间与精力。好在介绍这些协议的文章有很多，最简单明白的是乌克兰程序员Paul Bagwell画的分析图，[阮一峰](http://www.ruanyifeng.com/)将这张图做了中文版，这里引用一下。

<img src="{{ BASE_PATH }}/assets/images/licence-different.png">

有了这张图，在享用开源软件的“免费大餐”时，我们就可以吃得明白放心。

### 开源GIS

GIS行业有一个开源组织叫[OSGeo](http://www.osgeo.org/home)，
全称是The Open Source Geospatial Foundation，就像Apache基金会，
它组织管理了诸多的GIS行业开源软件。如果罗列全部软件列表会很长，举几个耳熟能详的名字:GDAL/OGR,GeoTools,GeoServer,MapServer，当然还有OpenLayers,QGIS等等。还有一些不在OSGeo的开源软件，
如开源地图数据组织[OpenStreetMap](http://www.openstreetmap.org/)，
为支撑其数据同享与采集，也有大量的开源项目。还有一些独立的项目，如[Mapnik](http://mapnik.org/)，也有广泛的应用。

这些软件功能强大，可靠性高，在项目中应用，可以提升开发效率，提高软件稳定性。现将常见的一些软件的协议进行总结，根据协议结合上节中的开源授权分析图，可以方便地确定其应用场景。

<table class="gridtable">
<tr>
    <th>开源软件</th><th>协议授权</th>
</tr>
<tr>
    <td>GEOS</td><td>LGPL</td>
</tr>
<tr>
    <td>Proj4</td><td>MIT</td>
</tr>
<tr>
    <td>GDAL/OGR</td><td>MIT</td>
</tr>
<tr>
    <td>FDO</td><td>LGPL</td>
</tr>
<tr>
    <td>GeoTools</td><td>LGPL</td>
</tr>
<tr>
    <td>PostGIS</td><td>GPLv2</td>
</tr>
<tr>
    <td>MapServer</td><td>MIT</td>
</tr>
<tr>
    <td>GeoServer</td><td>GPLv2</td>
</tr>
<tr>
    <td>Mapnik</td><td>LGPL</td>
</tr>
<tr>
    <td>MapGuide Open Source</td><td>LGPL</td>
</tr>
<tr>
    <td>QGIS</td><td>自定义,类LGPL</td>
</tr>
<tr>
    <td>GRASS GIS</td><td>GPLv2</td>
</tr>
<tr>
    <td>OpenLayers</td><td>BSD</td>
</tr>
<tr>
    <td>Leaflet</td><td>自定义,类Apache</td>
</tr>
<tr>
    <td>GeoNetwork</td><td>GPLv2</td>
</tr>
</table>







