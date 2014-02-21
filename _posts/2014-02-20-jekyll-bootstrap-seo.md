---
layout: post
title: "基于Jekyll Bootstrap的博客SEO优化"
description: "使用Jekyll Bootstarp的博客SEO优化"
category: "Jekyll"
keywords: "SEO, Jekyll"
tags: [SEO, Jekyll]
---
{% include JB/setup %}

写博客是为了共享与交流，但一个新博客，其搜索、关注度都很低。
这就要想想是为什么了？当然，最重要的一点，博客需要创造价值内容，没有内容就没有价值，
从而没有阅读，没有评论，没有交互。但对于一个新博客，如果不是靠<code>ctrl+c</code>与<code>ctrl+v</code>起家，由于时间短，内容是不会太多的。这个第一步怎样走出去？
外事问Google，搜索了一下SEO(搜索引擎优化)，看看大家有什么好的办法。这里记录一下本博针对SEO做的调整。

* 固定链接

修改_config.yml中的permalink，去掉category，防止整理文章时，
修改category后会造成404链接，修改后如下：
    permalink: /:year/:month/:day/:title

* posts的URL使用英文

jekyll bootstrap中使用<code>rake post title="xxx"</code>命令创建post时，创建的markdown文件中会自动把中文去掉，开始认为是对中文支持不好，每每都要rename一下。虽然当前搜索引擎都支持中文，但看到那一串的不能识别的编码后的字符，自己看google analytics时也会不爽，统一改为英文和分割线结构，好看又好记。如本篇

    {{site.production_url}}/2014/02/20/jekyll-bootstrap-seo

* 完善meta信息，title,description,keywords一个都不能少

使用rake创建的post，会在头部自动增加title与description配置,写文章时一定要补全，这样使jekyll会自动添加目标html中。

至于keywords，虽然都说由于大家的滥用，搜索引擎降低其作用，但了胜于无，加上无坏处。
打开<strong>Rakefile</strong>,在69行增加如下代码：

    post.puts 'keywords: ""'

这样下次再使用rake命令创建post时会自动增加keywords声明。然后修改自己在用的模板主文件。我这里是<code>\_includes/themes/twitter/default.html</code>，增加如下：

<script src="https://gist.github.com/sw897/b6c9d9aa30cc72a95f3d.js"></script>

这样，会在生成html中增加keywords的meta信息。

另外，title默认是文章标题，可以修改模板，增加博客主题内容，我的修改如下，这样在生成的所有页面中，title的内容为title之后加上<strong>sw897's blog</strong>

    <title> page.title | sw897's blog</title>

* sitemap.txt转为sitemap.xml

jekyll bootstrap里自带有sitemap.txt，对于sitemap.txt与sitemap.xml的优劣，这里有篇[文章](https://forums.digitalpoint.com/threads/xml-vs-txt-sitemap.114286/)有讨论，
大体读了一下，大部分人的意思就是xml的比txt的强，既然如此，改一下又不麻烦，删除sitemap.txt，创建sitemap.xml，内容如下：

<script src="https://gist.github.com/sw897/b1974e27b1f6309d9656.js"></script>

* 增加robots.txt

robots.txt是一种存放于网站根目录下的ASCII编码的文本文件，它通常告诉网络搜索引擎的漫游器（又称网络蜘蛛），此网站中的哪些内容是不应被搜索引擎的漫游器获取的，哪些是可以被（漫游器）获取的，以上摘自[robots.txt维基百科]()。在根目录下创建robots.txt，内容如下即可：

<script src="https://gist.github.com/sw897/ccd18f95beaa7bb6aec4.js"></script>

* 增加外链

在SEO中，外链能够极大的增加网站权重，让网站关键词有好的排名，这是因为搜索引擎是通过外链和锚文本来抓取网页内容的，增加外链能增加网站的曝光度，使网站权重得到提升。具体方法有很多，这里只简单设置一下，在自己github,bitbuck,google+,facebook,twitter里都增加网站链接，虽然不多，但可以让关注的人全面了解一下。

* 持之以恒

最后，也是最重要的，坚持! 自勉！


