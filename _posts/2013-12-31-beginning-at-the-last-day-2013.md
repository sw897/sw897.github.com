---
layout: post
title: "开始于2013的最后一天"
description: "在OS X上安装Jekyll本地环境,使用Jekyll在GitHub上搭建个人博客"
category: "工具"
keywords: "Jekyll,GitHub,Git,Karmdown,Maruku"
tags: [Jekyll,GitHub,Git]
---
{% include JB/setup %}

终于开始自己的博客了。

今天是一年的最后一天，是一个结束，而预示着一个新的开始。

这个博客准备组织些什么文字，自己还没想好，应该不是过往的专业相关内容的总结，
总体构想是基于MacBook的适应使用过程，结合在读在看的一些东西，随便敲些文字。

一个开头，也不知道写什么，就总结一下选择在GitHub开博的原因与过程吧。

### 为什么选择使用GitHub+Jekyll？

这个也不需要太多解释，

- GitHub带给开源太大的变化，一直一来关注的开源项目大多都转移到这里来了，被逼的
- Jekyll使用Markdown，本来计划使用IPython Notebook来记录学习的，就因为它使用Markdown，现在在这里分享更容易
- 最后一条但很重要，[阮一峰博客](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
中将写博分为三阶段，前两阶段只是实验与观望了，既然要开始，就选择高阶点的吧，也对得起老兵一枚。-_-

### 在MacOS 10.7上搭建基于Jekyll的个人博客

网上基于GitHub+Jekyll的博客搭建教程太多了，再写有些重复，我主要参考了
[Mac OS X 安装 Jekyll 记录][]
这篇文章，操作过程略有不同，这里把结合个人电脑中使用情况来个简单介绍，如果是需要按步骤一步步安装请稳步上面那篇文章。

会带来方便的软件：

- [GitHub for Mac][]

对于不熟悉Git命令的人来说，直接使用GitHub的图形界面，可以省去不少麻烦，在setting中绑定个人github账号后，
创建username.github.com的项目，拷贝jekyll bootstrap的代码到该目录，commit,sync都有图形化界面

- [Homebrew][]

这个也不需过多说明，直接按Linux来打造Mac，让在Mac上开发与Linux无异

- [Sublime Text][]

这里不讨论Mac上到底用什么编辑器更好，只说明Sublime Text是个不错的选择，安装Markdown相关插件，
编辑Markdown相当犀利，高尚显示，直接Ctrl+B还可以直接浏览器预览 ^_^

好了，下面开始重点

### 搭建本地的Jekyll环境

#### 安装准备，更新Mac的Ruby

Mac 10.7自带的Ruby版本为1.8.6，使用其gem安装Jekyll后会有若干莫名其妙的错误，
其原因还是我们的Jekyll需要1.9.2+才行，还是自行安装新版本解决来的快些。
[Mac OS X 安装 Jekyll 记录][]
文档教的方法是使用rvm，这里对于不懂Ruby的人来说，我也不想去装rvm，还是使用[Homebrew][]来搞定吧

<code>$ brew install ruby</code>

默认安装Ruby的最新版本2.1，教程说是最好是1.9.3版本，这里经实验2.1也是没有问题的。

#### 安装本地jekyll

<code>$ sudo gem install jekyll</code>

这里要使用sudo，至于为什么，你可以试试不带sudo进行安装，看看提示就明白了。安装完成后会有一个提示，
这里没有拷贝下来，大体意思就是gem的工具没link到执行目录，可以通过

<code>$ which jekyll</code>

验证一下，发现查无其人(jekyll)。使用其提示的方法

{% highlight sh %}
$ sudo gem pristine --all --only-executables
$ which jekyll
/usr/local/bin/jekyll
{% endhighlight %}

这样就可以，转到username.github.com目录，

<code>$ jekyll serve</code>

访问127.0.0.1:4000就可以查看jekyll bootstrap的默认blog了

#### 同步到GitHub

首次在在本地折腾差不多后，使用GitHub for Mac Commit&Sync到GitHub上，就与大家共享文章了。

新发文章或增加Page时，使用Jekyll Bootstrap提供的小工具很方便，专心写文章吧！

***

这个安装记录写的还真不清楚，按我这个来估计还是不行，还请参考以下文章

* [搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
* [Mac OS X 安装 Jekyll 记录][]

***
>Update 2014-04-25

最近收到了GitHub发来提示说Maruku过时了，最好把MarkDown的解析器换成Kramdown，于是听话的更新一下。方法如下:

* 安装kramdown

`$ gem install kramdown`

* 修改_config.yaml

`markdown:kramdown`

* 重新执行生成网站

`$ jekyll serve`

最后就得到错误，说是缺少karmdown。纳尼？明明刚安装成功了啊，重新来过，还是如此。

没办法，把jekyll都重装，不行

没办法，把ruby更新，还是不行

最最后只能放弃了，重新Google了一个，发现了一个好东西，[GitHub pages-gem](https://github.com/github/pages-gem)，早知道有这个就不折腾了，一句话结束：

`sudo gem install github-pages`




[Homebrew]: http://brew.sh/
[GitHub for Mac]: http://mac.github.com/
[Sublime Text]: http://www.sublimetext.com/2
[Mac OS X 安装 Jekyll 记录]: http://www.chenzixin.com/program/2013/03/06/mac-jekyll-install-log/

