---
layout: post
title: "动态链接库的搜索"
description: "在OS X, Windows, Linux三大常用桌面系统上的动态链接库的搜索顺序"
category: "技术"
keywords: "Linux, OS X, 动态链接库"
tags: [Linux, OS X, 动态链接库]
---
{% include JB/setup %}


> 在OS X下安装一些开源软件，其动态链接库的依赖比较复杂，为了搞明白还是花了些功夫。
> 在这里把Windows,Linux,OS X这三种常用桌面的动态链接库的搜索方法总结一下。
> 有些问题还是没有搞太清楚，如有错误，请大家指教。
>

### Windows

最早开发程序的运行平台是windows的，这也是学习的起点。当时对动态链接库的认识就是DLL，
以为天下的动态链接库都是DLL。对动态库的喜爱也随着开发的深入，动态库的不同版本之间的冲突带入了恶梦。
怎样解决不同程序间使用的相同动态库的不同版本？了解了windows上动态库的搜索顺序，才有了大约的解决。
如果有对应的\*.manifest文件，则按其文件内的绝对路径，否则按如下的顺序：

* 应用程序所在的路径

* 当前目录

* Windows SYSTEM目录, GetSystemDirectory 函数检索此目录的路径。

* Windows目录, GetWindowsDirectory 函数检索此目录的路径。

* PATH环境变量指定的路径

太久没有做windows开发了，认识也就停留在这个层面，MSDN上的
[这篇文章](http://msdn.microsoft.com/en-us/library/ms682586%28VS.85%29.aspx)
有更新更准确的介绍，这里留个链接，对有需要的朋友转入学习。

### Linux

过去一段时间用的最多的，也是比较熟悉的一个了。也就是从这个系统开始知道：DLL是动态链接库，但动态链接库不一定是DLL。
了解了linux上的动态库的搜索方法，才感叹在windows上处理方法的笨拙。
Linux系统中，动态链接的程序在运行时会自动链接ld.so这个库，ld.so负责找到其他的链接库。
搜索的依据有若干条，优先级最高，也是最推荐的是，在链接的时候加入 -rpath 参数指明所谓的 RUNPATH，这样可执行文件（或者依赖其他动态链接库的动态链接库）就能告诉 ld.so 到哪里去搜索对应的动态链接库了。
对于没有设定 RPATH 的可执行文件或者动态链接库，我们可以用 LD_LIBRARY_PATH 这个环境变量通知 ld.so，
这个方法的问题是，环境变量有时候设置了（如果 export 的话）会导致其他不需要设置的程序载入了不应该载入的动态链接库，
不 export 就得每次先设定再执行。通过 LD_PRELOAD 我们可以要求 ld.so 预先载入某些动态链接库，
这样就能 override 系统的动态链接库（比如使用特殊版本的 libc.so）。
还有就是在<code>/etc/ld.so.conf</code>中指定的路径。

可以通过<code>man ld.so</code>查看更多的帮助，通过<code>ldd</code>查看一个文件依赖的动态链接库通过 <code>chrpath</code>修改文件的 RPATH。
值得注意的是 RPATH 本身也可以通过环境变量 RUNPATH 进行覆盖。

### OS X

苹果的Mac OS X从10.8改为了OS X，也就是在这个时候我开始接触这个操作系统，并准备把工作转到这里进行。
虽然并未准备做OS X或iOS的原生开发，但只是安装一些开源软件也需要把动态链接库的搜索搞明白。
Mac从BSD走来，它与Linux的还是有区别的，特别是实行dmg的安装包，以及FrameWorks的引入，更显复杂了。

它的 dynamic linker 是 dyld 这个程序，动态链接库的载入是依靠它完成解析之类的事情，它支持三个@executable_path,
@loader_path, @rpath，具体可以参考[这篇](https://wincent.com/wiki/@executable_path,_@load_path_and_@rpath),
以及[另一篇](http://www.dribin.org/dave/blog/archives/2009/11/15/rpath/)文章来学习。

可以通过<code>man dyld</code>查看更多帮助，通过<code>otool -L</code>查看一个文件依赖的动态链接库，
通过<code>install_name_tool -change</code>修改动态链接库的位置。
开发阶段往往直接链接到本地的dylib，此时对应的文件里面的路径一般是绝对路径，可以在发布的时候替换成相对路径。
编译动态链接库时，如果是 share 到任意程序的的动态库，通过<code>-install_name</code>插入绝对路径；
否则根据情况，比如是 app bundle 还是 plugin，设定为对应变量的相对位置;
install_name 保证其他文件动态连接它时插入的名字是这个给定的字符串。
install name 可以用<code>install_name_tool -id</code>来修改。它依赖的动态链接库使用<code>-rpath</code>指定，
这样就算连接的动态链接库位置不是系统路径，也能自动找到。
比如我们写了一个 liba.dylib，为了很多其他程序方便用它，如果是类似 Linux 的做法，
install name 可能是<code>/usr/local/lib/liba.dylib</code>，
这样我的程序 app_a 直接写<code>-L/usr/local/lib -la</code>就能正确的找到在<code>/usr/local/lib</code>下的动态链接库。
如果 app_a 在写的时候 liba 也没写完，那么编译 liba 时写成<code>@rpath/liba.dylib</code>更合适，
因为 app_a 通过修改 -rpath 就可以测试正在写的 liba 或者是 deploy 到<code>/usr/local/lib</code>下的两个版本。
尽管仍然是<code>-L some-dir -la</code>链接 app_a 的，这里的 some-dir 可以是<code>/usr/local/lib</code>也可以是开发环境下的目录。










