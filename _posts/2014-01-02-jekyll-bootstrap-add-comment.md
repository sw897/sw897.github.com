---
layout: post
title: "给jekyll bootstrap增加评论系统"
description: "给jekyll bootstrap增加多说评论系统"
category: "技术"
keywords: "Jekyll, Jekyll Bootstrap, Comment, 多说"
tags: [Jekyll]
---
{% include JB/setup %}

jekyll bootstrap默认的评论系统是disqus,同时还可以配置使用livefyre,intensedebate,facebook，
这些虽然都不错，不过不符合我国国情，有必要换成国内的常用评论系统，用来支持国内的SNS平台，
比如新浪微博，豆瓣，人人等。国内评论系统也很多，常用的有[多说][]和[友言][]。

虽然不懂Ruby，但jekyll bootstrap把结构做的相当完美，过程很简单，下面把配置[多说][]的方法记录一下。
当然，开始之前需要先注册好[多说][]的个人账号

1 在<code>\_includes/JB/comments-providers</code>文件夹下增加多说的配置文件duoshuo，内容如下

<script src="https://gist.github.com/sw897/9130242.js"></script>

内容已经使用jb的模板变量，不需要修改可以直接拷贝使用。

2 在<code>\_includes/JB</code>目录下，修改comments文件，在第4行插入duoshuo的判断段

<script src="https://gist.github.com/sw897/9131080.js"></script>

3 最后修改<code>\_config.yml</code>文件中comments部分即可

    comments :
        provider : duoshuo
        duoshuo:
           short_name : 你的多说账号

经过以上3步即可配置完成，有兴趣的朋友可以用同样方法可以试试[友言][]，除评论系统账号部分，全部能用，
其实可以向jekyll bootstrap提交一下代码，方便国人配置使用。


<strong>Updated:2014-02-21</strong>

之前一直苦恼于怎样在markdown中直接贴Jekyll的相关代码，因为<strong>{}</strong>、<strong>%</strong>等关键字包含内容会自动解释，后来结合Gist终于解决：把代码创建gist后，再嵌入回来。虽然会影响速度，但完美解决生成HTML时代码解释运行的问题。


[多说]: www.duoshuo.com
[友言]: http://www.uyan.cc/

