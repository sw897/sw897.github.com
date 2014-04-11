---
layout: post
title: "使用Dash管理常用帮助文档"
description: "介绍文档管理工具Dash，总结多种生成docset的方法:使用doc2dash转换sphinx生成的python文档;直接使用doxygen生成docset"
category: "工具"
keywords: "Dash, Doc2Dash, Docsets, doxygen, GDAL, OGR"
tags: [Dash, OS X, Docset]
published: true
---
{% include JB/setup %}

### Dash介绍

Dash是OS X上方便宜用的文档管理工具，提供了130+的API文档，
几乎包含了所有常用语言与流行开发框架，并保持着极高的更新速度。如果你是一名OS X上的程序员，对于开发，Dash绝对是神一样的利器。它可以直接在Apple Store上免费下载安装，
但喜欢恶作剧的开发者不会让你用得那么舒服，会不定时地出现等待页面，来打扰你的高效开发。
有时候，你会感觉到，通过Dash节省的Google的那几秒时间不够它等待的。这个时候，你就要在软件内
购买了，人民币128元，如果经济允许，还是可以购入的，因为它提供的文档及其管理功能，是无与伦比的。

### DocSet扩展

对于程序员来说，并不是提供了130+的文档就足够了，必然还有我们自己常用的，更小众的API。
Dash也想到了这点，提供了DIY的介绍。其[生成DocSets帮助文档](http://kapeli.com/docsets)中，有以下几种文档生成Docset的方法介绍：

* [AppleDoc(Objective-C Source Files)](http://kapeli.com/docsets#objectivec)
* [Python,Sphinx or PyDoctor](http://kapeli.com/docsets#python)
* [Javadoc](http://kapeli.com/docsets#javadoc)
* [R-doc or Yard](http://kapeli.com/docsets#rdoc)
* [Scaladoc](http://kapeli.com/docsets#scaladoc)
* [Doxygen(Source Files:C,C++,C#,PHP,Objective-C,Java,Python)](http://kapeli.com/docsets#doxygen)
* [Any HTML Documentation](http://kapeli.com/docsets#dashDocset)

以上基本包含了所有可能自动生成的API文档。具体操作可以参考文档进行。还有更进阶的，提供与分享Feed，启用帮助页面内的JavaScript等等，可以慢慢试用。

#### 使用<code>doc2dash</code>转换Sphinx或PyDoctor生成的API文档

[doc2dash]()可以方便地把使用Sphinx与Pydoctor生成的HTML文档转换成Dash要求的docset。
过程非常简单，以NumPy为例。

* 文档准备

下载[HTML格式的文档](http://docs.scipy.org/doc/numpy/numpy-html-1.8.1.zip)，解压后目录numpy-html。

* 使用PIP安装doc2dash

    pip install doc2dash

* 使用doc2dash生成docset

    doc2dash numpy-html


#### 使用<code>Doxygen</code>直接转换API文档

Doxygen可以自动提取多种语言(包括但不限于 C, C++, C#, PHP, Objective-C, Java, Python )的注释生成HTML等多种格式的文档，其中就可以直接生成Dash需要docset。
以OGR这个GISer熟知的库为例，介绍一下步骤。
(别问我OGR属于GDAL，为什么要专门提出OGR库这个问题，手工生成过这两个库文档的人都懂)

* 下载GDAL源代码准备，最好先编译一下

* 修改doxygen默认配置

生成OGR文档的配置文件为gdal/ogr/doxygen，用文本编译器打开，添加以下配置。
如果有的可以直接修改值。

    GENERATE_DOCSET   = YES
    DISABLE_INDEX     = YES 
    SEARCHENGINE      = NO
    GENERATE_TREEVIEW = NO

* 终端转到gdal/ogr/目录，执行<code>doxygen</code>

运行成功，会在当前目录生成html目录，html目录会包含一个以往生成文档时没有makefile文件。

* 终端转到html目录，执行make

运行成功，即得到docset文件

### 总结

Dash是一款体形小巧、功能强大的文档管理工具，在线提供大量的API下载与更新，同时提供多种扩展方法，对提高开发效率有很大帮助。值得你拥有。

另：一般性html文档制作docset的方法以后再写。









[Dash]: http://kapeli.com/dash
[doc2dash]: https://pypi.python.org/pypi/doc2dash

