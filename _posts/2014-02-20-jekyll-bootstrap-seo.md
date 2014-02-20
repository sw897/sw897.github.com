---
layout: post
title: "基于Jekyll Bootstrap的博客SEO优化"
description: "使用Jekyll Bootstarp的博客SEO优化"
category: "Jekyll"
keywords: "SEO, Jekyll"
tags: [SEO, Jekyll]
published: false
---
{% include JB/setup %}

写博客是为了共享与交流，每当在Google Analyize看到寥寥无几的PV时，怎一个“酸”了得。
这就要想想是为什么了？当然，最重要的一点，博客是创造价值内容的事情，没有内容就没有价值，
从而没有PV，没有交互。但对于一个新博客，不是靠<code>ctrl+c</code>与<code>ctrl+v</code>起家，由于积累少，内容是不会太多的，从而还是不容易被搜索发现。这个第一步怎样走出去？
外事问Google，搜索了一下SEO，看看大家有什么好的主意。这里记录一下针对SEO做的调整。

* 固定链接
修改_config.yml中的permalink，去掉category，防止整理文章时，
修改category后会造成404链接，修改后如下：
    /:year/:month/:day/:title

* posts英文别名
使用rake命令创建post时，创建的markdown文件中会自动把中文去掉，开始认为是对中文支持不好，每每都要rename一下。后来在analyize中看到一浏览记录中那一串串“符号”，发布的文章title中一般带中文，但文件名尽量不要使用中文，虽然当前搜索引擎都支持中文，但看到那一串的不能识别的编码后的字符，自己看google analyize时也会不爽

* 完善meta信息，如title,description,keywords
jekyll bootstrap中使用<code>rake post title="kaka"</code>命令创建post时，
会在头部自动增加title与description,写文章时一定要补全，这样使jekyll会自动添加目标html中。
至于keywords，虽然都说由于大家的滥用其对于SEO的作用减小了，但了胜于无，加上无坏处。
打开<strong>Rakefile</strong>,在69行增加如下代码：
    post.puts 'keywords: ""'
这样下次再使用rake命令创建post时会自动增加keywords声明。然后修改自己在用的模板主文件，如这里是<code>_includes/themes/twitter/default.html</code>，增加如下：
    {% if page.keywords %}<meta name="keywords" content="{{ page.keywords }}">{% endif %}
这样，会在生成html中增加keywords的meta信息。

另外，title默认是文章标题，可以修改模板，增加博客主题内容，我的修改如下，这样在生成的所有页面中，title的内容为title之后加上<strong>sw897's blog</strong>
    <title>{{ page.title }} | sw897's blog</title>

* sitemap.txt转为sitemap.xml
jekyll bootstrap里自带有sitemap.txt，对于sitemap.txt与sitemap.xml的优劣，这里有篇[文章](https://forums.digitalpoint.com/threads/xml-vs-txt-sitemap.114286/)有些见解，
大体读了一下，意思就是xml的比txt的强，既然如此，改一下又不麻烦，删除sitemap.txt，创建sitemap.xml，内容如下：
```xml
---
# Remember to set production_url in your _config.yml file!
layout: nil
title : Sitemap
---
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
{% for post in site.posts %}
    <url>
        <loc>{{site.production_url}}{{ post.url }}</loc>
    </url>
{% endfor %}
{% for page in site.pages %}
    <url>
        <loc>{{site.production_url}}{{ page.url }}</loc>
    </url>
{% endfor %}
</urlset>

```

* 增加robots.txt
robots.txt是一种存放于网站根目录下的ASCII编码的文本文件，它通常告诉网络搜索引擎的漫游器（又称网络蜘蛛），此网站中的哪些内容是不应被搜索引擎的漫游器获取的，哪些是可以被（漫游器）获取的，以上摘自[robots.txt维基百科]()。在根目录下创建robots.txt，内容如下即可：
```markdown
    ---
    title: robots
    ---
    User-agent: *
    Sitemap: <{{site.production_url}}/sitemap.xml>
```

* 增加外链
在SEO中，外链能够极大的增加网站权重，让网站关键词有好的排名，这是因为搜索引擎是通过外链和锚文本来抓取网页内容的，增加外链能增加网站的曝光度，使网站权重得到提升。具体方法有很多，长久的经营方法是，在自己github,bitbuck,google+,facebook,twitter里都增加网站链接，这样虽然保守，但一举多得，不SNS绑定后，可以使用阅读人群更有针对性。


