---
layout: post
title: "Jekyll换用kramdown后提示Missing dependency: kramdown真正原因"
description: "Jekyll换用kramdown后提示Missing dependency: kramdown真正原因"
category: "技术"
keywords: "jekyll,kramdown,ruby,gem"
tags: ["jekyll","ruby"]
published: true
---
{% include JB/setup %}

使用Jekyll在GitHub上建立博客以来，一直感觉其简单易用，得心应手。具体安装配置也记录在第一篇文章[“开始于2013的最后一天”](/2013/12/31/beginning-at-the-last-day-2013/)。
问题出现在4月底，GitHub-Pages发邮件提示MarkDown的默认解析器由暮色的Maruku换成朝阳的Kramdown，建议在本地生成html时最好也做一下更新。

#### 初次尝试

1.执行`sudo gem install kramdown`安装kramdown

2.修改在_config.yaml中的配置：`markdown: kramdown`

3.执行`jekyll serve`启动本地服务器

提示“You are missing a library required for Markdown. Please run: $ [sudo] gem install kramdown”。重新安装kramdown还是如此。

#### 二次尝试

出现以上问题后，没有深究原因，在GitHub上查了一下，找到了项目[GitHub pages-gem](https://github.com/github/pages-gem)，直接安装GitHub-Pages，执行：

    $sudo gem install github-pages

偶然地，这样竟然没问题。洋洋得意，直接把方法更新在[第一篇](/2013/12/31/beginning-at-the-last-day-2013/)的记录里了。

#### 最终方案

一段时间，在使用Brew更新过Ruby后，再次遇到一样的问题。这次要仔细一下了，不然更新一下，无休止出现这种问题，让人太恼火了。问了Google，stackoverflow，没有发现相同问题的。于是就怀疑是自己的环境问题。

* 回顾环境

1.Mac OS X 10.9.2系统

2.最新的brew环境

* 安装过程

执行以下命令安装ruby,github-pages

    $brew install ruby
    $sudo gem install github-pages

* 查找原因

1.检查ruby,gem版本

    $which ruby
    /usr/local/bin/ruby
    $which gem
    /usr/local/bin/ruby

结果是是brew安装的最新版本2.1.2。而不是OS X自带的老版本。

2.检查jekyll版本

    $which jekyll
    /usr/bin/jekyll

竟然是`/usr/bin`下的，其加载的gems库是`/Library/Ruby/Gems/2.0.0/gems`目录，不是brew安装的gem对应的库。再看一下brew安装gem对应的jekyll情况

    $gem which jekyll
    /usr/local/Cellar/ruby/2.1.2/lib/ruby/gems/2.1.0/gems/jekyll-1.5.1/lib/jekyll.rb

哈，原因找到了：安装jekyll后，没有将执行文件jekyll拷贝到可执行目录，一直在用的是/usr/bin/jekyll，也就是系统ruby下安装的。

* 解决办法

link gem对应的jekyll到`/usr/local/bin`下，使jekyll默认为该版本

    $sudo ln -s /usr/local/Cellar/ruby/2.1.2/bin/jekyll /usr/local/bin

执行`jekyll serve`，一直正常。收官！












