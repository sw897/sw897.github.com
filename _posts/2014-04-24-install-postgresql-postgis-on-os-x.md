---
layout: post
title: "在OS X上安装PostgreSQL与PostGIS"
description: "在os x上安装使用postgresql与postgis"
category: "技术"
keywords: "PostgreSQL,PostGIS,GIS"
tags: [GIS]
published: true
---
{% include JB/setup %}

PostgreSQL是流行的先进开源关系型数据库，PostGIS是PostgreSQL空间信息扩展部分，支持空间索引与空间查询。越来越多的GIS应用使用两者的组合来完成后台空间数据的存储与获取，支撑前端应用系统。因其良好的性能与稳定表现，持续得到大家的追捧。避开当前流行的大数据与NoSQL，这种组合是完成一个稳健GIS系统的经典组合。

两个软件虽然都是开源软件，但有很好的社区支持，产品化非常好。特别是针对Windows平台的支持，简单易用的安装包，自带的可视化工具PgAdmin3以及shp2pgsql_GUI，让不熟悉两者，甚至是不熟悉数据库的开发人员也能快速上手：使用shp2pgsql_GUI把Shape文件导入到PostGIS；使用PgAdmin3可视化运行SQL操作数据。在生产环境中，一般选择使用Linux平台，安装可以选择对应的发行包，也可以手工编译安装，`configure && make && make install`一马平川。在OS X系统上，PostgreSQL的安装有多种方法，最简单的，还是类似Windows下的可视化安装包，但使用OS X的用户大多喜欢使用类似Linux的方法。所以，这里我们还是选用神器`brew`的方法，并可深入了解OS X的用户管理与数据库初始化。

### 安装

使用`brew`安装，过程是相当的Nice。

{% highlight tcsh %}
$ brew install postgresql   # 当前最新版本是9.3.4
$ brew install postgis      # 当前最新版本是2.1.2
{% endhighlight %}

安装PostGIS前，最好安装Proj4,GEOS,GDAL,GeoIP等开源GIS库，以支持空间分析、IP定位等。

{% highlight tcsh %}
$ brew install proj     # 当前最新版本是4.8.0
$ brew install geos     # 当前最新版本是3.4.2
$ brew install gdal     # 当前最新版本是1.10.1_1
$ brew install libgeoip
{% endhighlight %}


### 初始化

#### 帐号配置

初始化数据库前需要指定一个用户帐号，使用安装PostgreSQL时默认创建的帐号`_postgres`，可以通过`/etc/passwd`文件查看帐号记录，也可以使用dscl工具进行查看。dscl工具是OS X上完成useradd,userdel,usermod等Linux平台上的工具功用的代替。以下使用dscl查看_postgres用户并修改其zsh登录。
具体选择哪种shell就按个人喜好了，具体系统中支持哪些可以查看`/etc/shells`文件。

{% highlight tcsh %}
$ sudo dscl . list /Users | grep _postgres
$ sudo dscl . read /Users/_postgres
$ sudo dscl . change /Users/_postgres UserShell /usr/bin/false /bin/zsh
{% endhighlight %}

#### 初始化数据库

创建数据库目录，修改目录访问权限并初始化。
{% highlight tcsh %}
$ sudo mkdir /usr/local/var/postgres
$ sudo chown _postgres:_postgres /usr/local/var/postgres/
$ sudo su - _postgres
$ initdb /usr/local/var/postgres
{% endhighlight %}

我的机子，系统为OS X 10.9，按上面执行，在运行initdb时会提示`Permission denied`。问过google后，索性把`/usr/local/var`的权限增加了可写，问题解决。

### 数据库管理控制

#### 使用launchctl管理

* 登录时自动启动

{% highlight tcsh %}
$ mkdir -p ~/Library/LaunchAgents
$ cp /usr/local/Cellar/postgresql/9.3.4/homebrew.mxcl.postgresql.plist ~/Library/LaunchAgents/
$ launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
{% endhighlight %}

* 启动

{% highlight tcsh %}
$ launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
{% endhighlight %}

* 停止

{% highlight tcsh %}
$ launchctl unload  ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
{% endhighlight %}

#### 使用pg_ctl管理

* 启动

{% highlight tcsh %}
$ pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start
{% endhighlight %}

* 停止

{% highlight tcsh %}
$ pg_ctl -D /usr/local/var/postgres stop -s -m fast
{% endhighlight %}

#### 进程验证

`$ ps aux | grep postgres`

### 创建空间数据库

#### 9.1及以上版本的PostgreSQL

使用PostGIS 2.0+创建空间数据库非常的Nice

{% highlight tcsh %}
$ createdb -E UTF8 --template=template0 postgis     #创建postgis数据库
$ psql -d postgis -c "CREATE EXTENSION postgis;"    #增加空间扩展
$ psql -d postgis -c "CREATE EXTENSION postgis_topology;"   #增加空间拓扑扩展
$ psql -d postgis -f legacy.sql                     #兼容旧版扩展
{% endhighlight %}

如果不需要兼容旧版本，或者不需要拓扑扩展等，也可以方便地移除

{% highlight tcsh %}
$ psql -d postgis -f uninstall_legacy.sql
$ psql -d postgis -f uninstall_topology.sql
$ psql -d postgis -f uninstall_postgis.sql
{% endhighlight %}

#### 9.1以下版本PostgreSQL

老版本的Postgre创建空间数据库就稍有点麻烦，但本质上是一样的，也就是将空间扩展部分(数据表、函数、视图等)一个个地扩展到数据库中。为以后使用方便，一般是先创建一个空间数据库模板，这样，以后就以此为模板直接创建。

* 创建空间数据库模板

具体扩展哪些sql根据需求自行操作

{% highlight tcsh %}
$ POSTGIS_SQL_PATH=/usr/local/share/postgis
$ createdb -E UTF8 --template=template0 template_postgis    #创建数据库
$ createlang -d template_postgis plpgsql                    #支持pl/pgsql
$ psql -d postgres -c "UPDATE pg_database SET datistemplate='true' WHERE datname='template_postgis';"                                #设置为模板
$ psql -d template_postgis -f $POSTGIS_SQL_PATH/postgis.sql
$ psql -d template_postgis -f $POSTGIS_SQL_PATH/spatial_ref_sys.sql
$ psql -d template_postgis -c "GRANT ALL ON geometry_columns TO PUBLIC;"
$ psql -d template_postgis -c "GRANT ALL ON geography_columns TO PUBLIC;"
$ psql -d template_postgis -c "GRANT ALL ON spatial_ref_sys TO PUBLIC;"
{% endhighlight %}

* 创建空间数据库及其用户

{% highlight tcsh %}
$ createuser -P -d -e postgis   #创建一个postgis普通用戶,用来登录空间数据库
$ createdb -T template_postgis -E UTF8 postgis # 创建一个空间数据库
{% endhighlight %}

更具体地可参考PostGIS用户手册。

