---
layout: post
title: "从Sublime Text 3转到Atom做开发"
description: "使用GitHub Atom做开发，替代Sublime Text 3编辑器"
category: "工具"
keywords: "GitHub, Atom, Sublime Text, OS X"
tags: [GitHub, Atom, Sublime Text, OS X]
published: true
---
{% include JB/setup %}

之前一篇["使用Sublime Text 3做Python开发"](/2014/02/13/sublime-text-3-for-python/)
的介绍文档还在鼓舞大家投到ST3的怀抱，我又迅速转投GitHub [Atom](https://atom.io/)，不禁一种愧意上心头，但我也是有苦衷的。

ST3成为首发开发编辑器才没多久，它就开始出现一种莫名其妙的问题，花屏。

<img src="{{ BASE_PATH }}/assets/images/st3messup.png" alt="st3花屏" >

作为核心，出现这种掉链子的状况，实在无法容忍。
不清楚这个问题我的OS X上是个案，还是所有Mac上的通病。
在完成了OS X 10.9.2的某次更新就如此了。ST版本是3059，
由于经济并不宽裕，没有办法资助ST开发者70$，转到dev版测试是否还有这个问题。
而且3059已经半年没有更新了，我没有办法再等下去。

想起了2月份公开测试的Atom。它出身于GitHub，绝对的“富二代”，看起来值得信赖。
看了一下官网介绍，在我身上少有的冒险精神活跃起来，我决定试用一下。

启动Atom，熟悉的界面，和ST非常相似，虽然知道它与ST是完全不同的开发语言与构架，但第一眼，很难不把
两者往一块想。这也说明，Atom是要和ST正面PK了。

<img src="{{ BASE_PATH }}/assets/images/atom.png" alt="atom界面">

看一下网站的介绍：

* Taking the web native

基于Web技术的桌面应用程序。

* Node.js integration

整合NodeJS，访问本地文件与启动子进程。

* Modular design

模块化设计，基于最小化的内核集成了多个开源包

* Full-featured, right out of the box

功能全面。

简单折腾一下，以上所言不虚，但还有如下不适感：

* 启动有一点点慢，与ST比较

* 支持的语言不够多。大多Web开发中的客户端脚本支持完备，其它较少或不充分。这也与其新一代的Web编辑器定位相符

* 自动补全，函数提示等不够友好

* 特别的，针对Python的插件很少，并且不太好用，没有Anaconda这种集大成者插件。

虽然以上种种的不爽，但其能正常使用，足够使用markdown写文档，以及编写一些简单脚本，这就够了。
另外，其快捷键等与ST一致，上手容易，就先这样吧，从这篇文档开始，就Atom了。
