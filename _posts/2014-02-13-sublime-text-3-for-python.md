---
layout: post
title: "使用Sublime Text 3做Python开发"
description: "在Sublime Text 3下搭建python的开发环境,推荐Anaconda插件"
category: "Python"
keywords: "Sublime Text, Python, Anaconda, OS X"
tags: [Sublime Text, Python, Anaconda, OS X]
---
{% include JB/setup %}

### 引言

刚转到OS X平台时，寻找写Python,JavaScript,Markdown等文件的工具时，比较了许多工具，
最终选择了Sublime Text 2，主要原因是其跨平台，
想着以后再转到windows下开发时，不需要再重新适应其他工具。
Sublime Text 2学习曲线不像Vim那么陡峭，但想用得顺手，还是需要时间。在使用Sublime Text 2以后，还是有一段时间在怀念Notepad++的各种好，幻想notpad++明天会有OS X版本。
这段时间过后，越来越感觉到Sublime的强大，notepad++开始淡出了记忆。
Sublime Text 3的beta版本推出很长时间了，但其中文介绍文档非常少，多数介绍也只是停留在如何安装Package Control上，对开发相关插件介绍很少。正因为如此，许多人都在担心自己使用的plugins还不支持版本3，于是就一直不进行升级，我也是这种心态的其中一个。
这段时间有空，终于决定折腾一下。

开始之前，看到[Package Contorl网站][]上的一张统计图，给自己吃了个定心丸

<img src="https://dl.dropboxusercontent.com/u/57451074/github/sw897/images/sublime_pc_stat.png" alt="sublime text package control stat">

可以看到，绝大部的插件已完成3版本的兼容，而且还有少量专为3定制的新插件。所以，大家可以放心转到3版本上来试用了。后面介绍的python开发环境支持插件就是从Sublime 3独有，具体是哪个这里暂不解密。

当然，不排除有些奇葩插件还不支持3版本，但如果这样，我的建议就是把那个插件换掉吧，更新这么不及时，一定不是最合适的了。

### 安装Package Control

现在Sublime Text 3的安装方法和版本2一样，只是粘贴的代码内容稍有不同，在[Package Contorl网站][]上有安装方法。使用快捷键<code>ctrl+\`</code>或通过菜单选项<code>View > Show Console</code>进入控制台Console，然后粘贴如下代码，回车运行。

{% highlight python %}
import urllib.request,os,hashlib; h = '7183a2d3e96f11eeadd761d777e62404e330c659d4bb41d3bdf022e94cab3cd0'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
{% endhighlight %}

安装完成后我们就正式开始配置Sublime Text!

### 安装Plugins的万能方法

通过<code>ctrl+shift+p</code>进入<code>Command Palette</code>，
输入<code>Package Contorl: Install Package</code>或简写为<code>ip</code>，
回车执行，进入插件的搜索窗口，查找选择到需要的插件后，回车即可等待完成安装，招待状态在sublime最下面的状态栏内会有文字提示。

### 一般配置

* 主题

sublime text可以通过插件安装很多主题，肯定有一款适合你。这里还是推荐在Sublime Text 2上一直使用的[Theme - Soda Dark][]主题，
颜色模板使用[Color Scheme - Tomorrow Night][]，两者的搭配应该算的上经典，从notepad++转到Sublime Text 2时基本所有的介绍文档都是这么推荐的。
大家可以通过上面介绍的插件安装方法尝试一下。


* 配置文件内容

{% highlight javascript %}
// Colors
"color_scheme": "Packages/Tomorrow Color Schemes/Tomorrow-Night.tmTheme",
"theme": "Soda Dark 3.sublime-theme",
// Font
"font_size": 12.0,
"font_options": ["subpixel_antialias", "no_bold"],
"line_padding_bottom": 1,
"line_padding_top": 1,
// Editor view
"draw_white_space": "all",
"fold_buttons": false,
"highlight_line": true,
"auto_complete": false,
"show_minimap": false,
"show_full_path": true,
// Editor behavior
"scroll_past_end": false,
"highlight_modified_tabs": true,
"find_selected_text": true,
// Whitespace - no tabs, trimming, end files with \n
"tab_size": 4,
"translate_tabs_to_spaces": true,
"trim_trailing_white_space_on_save": true,
"ensure_newline_at_eof_on_save": true,
// Sidebar
"file_exclude_patterns":
[
    ".DS_Store",
    "*.pid",
    "*.pyc"
],
"folder_exclude_patterns":
[
    ".git",
    "__pycache__"
],
// Package Control
"ignored_packages":
[
    "Vintage"
]
{% endhighlight %}

个人不喜欢自动切分换行功能，于是没有配置，所以后面把PEP8中的E501排除掉了

### 开发环境插件

* [Git][]

版本库是软件开发中不可缺少的工具，该插件把Git常用命令加入了<code>Command Palette</code>，让开发人员进行代码管理方便不少。

<img src="https://dl.dropboxusercontent.com/u/57451074/github/sw897/images/sublime_git.png">

* [GitGutter][]

这个小插件是在修改后的文件行号前增加一些标识图片，方便与版本库对比，修改内容一目了然。

<img src="https://dl.dropboxusercontent.com/u/57451074/github/sw897/images/sublime_gitgutter.png">

* [Gist][]

创建、管理gist的插件，Gist是GitHub提供的又一强力工具，用Git将用户常用的代码片段在线管理起来。安装此插件后，打开其User-Setting，
增加个人的GitHub访问Token后，即可通过快捷键或Console使用。

* [Anaconda][]

[Anaconda][]绝对是换到Sublime Text 3后最令我兴奋的插件，没有之一。在Sublime Text 2的时代，为配置一个好用的python开发环境，
我们需要分别安装All Autocomplete,SublimeREPL,Pylinter和PEP8等诸多插件。
Geek就是让一切变得更简单，该插件作者就为了简便，把这些功能集中起来了。
[Anaconda][]把PyFlakes, pep8 和 McCabe以插件的方式集成起来。安装[Anaconda][]后，通过配置即可完成一个良好的Python开发环境。

> Anaconda is a python development suite that includes autocompletion, IDE features, linting with PyLint or PyFlakes + pep8, AutoPEP8 , Vagrant and more for Sublime Text 3.

安装时可以通过Package Control安装，也可以使用Git追踪最新版本。[GitHub地址](https://github.com/DamnWidget/anaconda)

安装成功后在插件配置内打开[Anaconda][]的REAMME，可以参考进行个性配置。我这里做了如下的修改：

* 增加对象的点操作符时的自动提示

在<code>Packages/User</code>目录下创建<code>Python.sublime-settings</code>文件，增加如下内容

{% highlight json %}
{
    "auto_complete_triggers": [{"selector": "source.python - string - comment - constant.numeric", "characters": "."}]
}
{% endhighlight %}

* 增加括号操作符后的参数自动完成

在<code>Anaconda Setting</code>中修改<code>complete_parameters</code>参数的值为<code>true</code>。
这里还有一个参数为<code>complete_all_parameters</code>，设置其为<code>true</code>后，则带默认值的参数也会自动完成。

* 忽略<code>AutoFormat PEP8</code>中E501的提示

{% highlight javascript %}
"pep8_ignore":["E501"]
{% endhighlight %}

其他设置均使用默认值。

<img src="https://dl.dropboxusercontent.com/u/57451074/github/sw897/images/sublime_anaconda.png">

### 结束

只需要这几个插件的安装与配置，就能使sublime text 3成为一个高效的python开发工具，接下来，感受 Sublime Text 3的快如疾风，风驰电掣吧！


### Update:2014-02-26

使用OS X时间长了都忘记广大Windows用户存在GBK编码问题了。今天打开以前在Windows上写的
一些代码才发现中文注释都乱码了。解决办法很简单，安装插件[ConvertToUTF8][]即可。
另外，在Sublime Text 2上的插件[GBK Encoding Support][]不支持3版本，不能安装使用了。

* [ConvertToUTF8][]

支持GBK等多种编码的文件的编辑与保存。



[Package Contorl网站]: https://sublime.wbond.net
[Theme - Soda Dark]: http://buymeasoda.github.io/soda-theme/
[Color Scheme - Tomorrow Night]: https://github.com/theymaybecoders/sublime-tomorrow-theme
[Anaconda]: https://sublime.wbond.net/packages/Anaconda
[Git]: https://sublime.wbond.net/packages/Git
[GitGutter]: https://sublime.wbond.net/packages/GitGutter
[Gist]: https://sublime.wbond.net/packages/Gist
[ConvertToUTF8]: https://sublime.wbond.net/packages/ConvertToUTF8
[GBK Encoding Support]: https://sublime.wbond.net/packages/GBK%20Encoding%20Support



