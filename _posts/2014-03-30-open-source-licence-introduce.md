---
layout: post
title: "开源GIS与开源协议授权总结"
description: "介绍与对比GPL,LGPL,MIT等常见开源协议，总结GIS开源所采用的开源协议"
category: "技术"
keywords: "OpenSource,开源,GPL,MIT,GIS"
tags: [OpenSource,GIS]
published: true
---
{% include JB/setup %}

### 介绍

开源软件近几年越来越流行，从SourceForge到GitHub,Bitbucket，存在着不计其数的开源项目。在国内，几家大公司也开始开放平台，拥抱开源，CSDN的开源平台也红红火火。GIS行业内，
有那么几个主要的基础库与软件也是得到了广泛的应用，特别是OSGeo组织下的GDAL,MapServer等等。在使用这些开源软件的时候，其协议授权，也就是licence，是我们要特别注意的。这些开源协议明确说明了使用者应该遵循的原则，从而确定了使用者使用开源软件的方式与方法，能否二次开发，进而商业发布，还是只能开源。


### 开源授权

开源协议有很多，任何人写一个开源软件都可以自定义一个licence。常见的有这么6种：
GPL协议系列(v1,v2,v3...)，LGPL协议，BSD协议，Apache licence 2.0，MIT协议和Mozilla协议。
这几种协议规定都是很多页的英文，要仔细读完很需要时间与精力。好在介绍这些协议的文章有很多，最简单明白的是乌克兰程序员Paul Bagwell画的分析图，[阮一峰](http://www.ruanyifeng.com/)将这张图做了中文版，这里引用一下。

<img src="{{ BASE_PATH }}/assets/images/licence-different.png">

有了这张图，在享用开源软件的“免费大餐”时，我们就可以吃得明白放心。


### 开源GIS

GIS行业有一个开源组织叫[OSGeo](http://www.osgeo.org/home)，
全称是The Open Source Geospatial Foundation，就像Apache基金会，
它组织管理了诸多的GIS行业开源软件。还有很多不在OSGeo组织下的开源软件，
如开源地图数据组织[OpenStreetMap](http://www.openstreetmap.org/)，
为支撑其数据同享与采集，也有大量的开源项目。还有一些独立的项目，如[Mapnik](http://mapnik.org/)，也有广泛的应用。

这些软件功能强大，可靠性高，在项目中应用，可以提升开发效率，提高软件稳定性。
按对商业应用、二次开发的友好程度对开源协议进行排序，`MIT>BSD>Apache>LGPL>GPL`。这里将这5个协议按应用灵活度分为以下三组，总结一下部分开源GIS软件或类库的应用场景。


#### MIT,BSD,Apache

这三个协议都对商业应用友好的许可，允许使用或在其代码上开发商业软件发布和销售。因为可以完全控制这些第三方的代码，在必要的时候可以修改或者二次开发。

使用这类协议的开源GIS：Proj4, GDAL/OGR, MapServer, OpenLayers, Leaflet,ZOO-Project,PyCSW,pywps-4


#### LGPL

LGPL是GPL的一个为主要为类库使用设计的开源协议。LGPL允许商业软件通过类库引用(link)方式使用LGPL类库而不需要开源商业软件的代码。这使得采用LGPL协议的开源代码可以被商业软件作为类库引用并发布和销售。但是如果修改LGPL协议的代码或者衍生，则所有修改的代码，涉及修改部分的额外代码和衍生的代码都必须采用LGPL协议。

因此，LGPL协议的开源代码很适合作为第三方类库被商业软件引用，但不适合希望以LGPL协议代码为基础，通过修改和衍生的方式做二次开发的商业软件采用。

使用LGPL的开源GIS：GEOS, FDO, GeoTools, Mapnik, MapGuide Open Source,OpenScales,OSGEarth


#### GPL

GPL的出发点是代码的开源/免费使用和引用/修改/衍生代码的开源/免费使用，但不允许修改后和衍生的代码做为闭源的商业软件发布和销售。由于GPL严格要求使用了GPL类库的软件产品必须使用GPL协议，对于使用GPL协议的开源代码，商业软件或者对代码有保密要求的部门就不适合集成/采用作为类库和二次开发的基础。所以在借鉴这类协议下的开源代码时需要注意了。

使用GPL系列协议的开源GIS：PostGIS, Grass GIS, QGIS, GeoNetwork,PyWPS


### 部分开源GIS与其协议授权对照表

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
    <td>Mapnik</td><td>LGPL</td>
</tr>
<tr>
    <td>GeoServer</td><td>GPLv2</td>
</tr>
<tr>
    <td>MapGuide Open Source</td><td>LGPL</td>
</tr>
<tr>
    <td>QGIS</td><td>GPLv2</td>
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
    <td>OpenScales</td><td>LGPL</td>
</tr>
<tr>
    <td>OsgEarth</td><td>LGPL</td>
</tr>
<tr>
    <td>ZOO-Project</td><td>MIT</td>
</tr>
<tr>
    <td>PyWPS</td><td>GPL</td>
</tr>
<tr>
    <td>pywps-4</td><td>MIT</td>
</tr>
<tr>
    <td>GeoNetwork</td><td>GPLv2</td>
</tr>
<tr>
    <td>PyCSW</td><td>MIT</td>
</tr>
<tr>
    <td>Routino</td><td>Affero GPLv3</td>
</tr>
</table>








