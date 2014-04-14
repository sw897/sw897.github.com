---
layout: post
title: "制作PostGIS的Dash文档"
description: "以PostGIS为例，将一般HTML文档库制作为Dash支持的Docset格式"
category: "技术"
keywords: "Dash, Docsets, PostGIS"
tags: [Dash,Docset,GIS]
published: true
---
{% include JB/setup %}

### PostGIS介绍

PostGIS 是开源数据库 PostgreSQL 的空间数据支持扩展，PostGIS 实现了Open Geospatial Consortium所提供的Simple Features的SQL实现参考。对于GIS用户而言，PostGIS是一个重要的GIS基础软件，因为目前它是为数不多的开源空间数据库存储方案之一。在国内，由于其开源的特性，
近几年在多领域的GIS系统构建中得到了应用。

### 制作Dash文档

对于GIS行业如此重要的基础软件文档，并未进入Dash官方的法眼，没有提供在线的文档更新源，这就要我们自己动手构建其Docset。下面请跟随我一步步开始<code>postgis.docset</code>制作。

1.创建Docset文件目录

Docset是Dash支持的一种目录结构包，首先为我们的构建目标<code>postgis.docset</code>创建其目录结构。
可以在终端中执行如下命令，也可以手工创建。

    mkdir -p postgis.docset/Contents/Resources/Documents/

2.拷贝PostGIS文档

将下载的最新的PostGIS文档拷贝到目录<code>postgis.docset/Contents/Resources/Documents/</code>。

3.创建Info.plist文件

下载[Info.plist示例文件](http://kapeli.com/dash_resources/Info.plist)，拷贝到目录
<code>postgis.docset/Contents/</code>下，并稍做修改，以下是本文的示例

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>CFBundleIdentifier</key>
    <string>postgis</string>
    <key>CFBundleName</key>
    <string>postgis</string>
    <key>DocSetPlatformFamily</key>
    <string>postgis</string>
    <key>isDashDocset</key>
    <true/>
    <key>DashDocSetFamily</key>
    <string>dashtoc</string>
    <key>dashIndexFilePath</key>
    <string>index.html</string>
</dict>
</plist>
{% endhighlight %}

4.创建SQLite索引数据表

创建SQLite索引数据库文件<code>postgis.docset/Contents/Resources/docSet.dsidx</code>，并在数据库中创建searchIndex数据表与索引anchor。

{% highlight sql%}
CREATE TABLE searchIndex(id INTEGER PRIMARY KEY, name TEXT, type TEXT, path TEXT);
CREATE UNIQUE INDEX anchor ON searchIndex (name, type, path);
{% endhighlight %}

5.添加索引记录

根据postgis文档，为Class,Function或Attribute等提供Dash内搜索的项目创建索引，也就是，
使用如下SQL语句向<code>searchIndex</code>索引表插入一条记录。这个过程需要编写脚本执行。
后面会提供Python示例脚本。

{% highlight sql%}
INSERT OR IGNORE INTO searchIndex(name, type, path) VALUES ('name', 'type', 'path');
{% endhighlight %}

经过以上几步，<code>postgis.docset</code>文档便制作完成。双击加入Dash中即可使用。
相信一步步执行的朋友卡在了第5步，下面就是其Python脚本。

* Python脚本

Dash网站上有使用Python生成`postgredql.docset`的脚本，使用`BeautifulSoup`解析`bookindex.html`生成。在生成`postgis.docset`时，
由于主要查看函数的用法，介绍文档并不关注，结合postgis文档特点，直接遍历Documents目录，
根据文档列表生成Functions列表。

{% highlight python linenos %}
import os
import sqlite3

db = sqlite3.connect('postgis.docset/Contents/Resources/docSet.dsidx')
cur = db.cursor()

try:
    cur.execute('DROP TABLE searchIndex;')
except:
    pass
cur.execute(
    'CREATE TABLE searchIndex(id INTEGER PRIMARY KEY, name TEXT, type TEXT, path TEXT);')

cur.execute('CREATE UNIQUE INDEX anchor ON searchIndex (name, type, path);')

docpath = 'postgis.docset/Contents/Resources/Documents'

for root, dirs, files in os.walk(docpath):
    for path in files:
        (name, ext) = os.path.splitext(path)
        if ext.lower() == '.html':
            if name[0:3] == 'RT_':
                name = name[3:]
            cur.execute(
                'INSERT OR IGNORE INTO searchIndex(name, type, path) VALUES (?,?,?)', (name, 'func', path))
            print 'name: %s, path: %s' % (name, path)

db.commit()
db.close()
{% endhighlight %}


### FAQ
以下是本文的可能的FAQ(常见问题)。

问：我不是程序员，看不懂怎么办？

答：那说明您根本不需要这样一个docset。

问：我知道怎么做，但你这里像Dash手册里一样，啰嗦这么多还是要我一步步自己操作，有什么用？

答：嗯~，为了表示诚意，我还是提供了制作的<code>postgis.docset</code>文件下载的。
在我的github里，点一下[这里](https://github.com/sw897/docset_postgis)就可以了。不定时更新，有最新版本强迫症的朋友请走开。








