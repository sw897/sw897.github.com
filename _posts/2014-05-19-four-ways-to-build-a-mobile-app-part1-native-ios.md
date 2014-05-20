---
layout: post
title: "[译]构建移动应用的4种方法: Native iOS应用"
description: "构建移动应用的4种方法系列文章"
category: "技术"
keywords: "iOS,Android,Mobile,Apps,PhoneGap"
tags: ["Apps", "Mobile", "iOS", "Android", "PhoneGap"]
published: true
---
{% include JB/setup %}

>“构建移动应用的4种方法”是[Peter Traeg](http://www.smashingmagazine.com/author/peter-traeg/?rel=author)博客上的系列文章，是很不错的移动开发的入门介绍与总结。近期帮朋友完成了一个小iOS应用，想起这篇文章，空闲时间翻译一下，也算回顾。

>PS:
>
>   1.非逐句翻译
>   
>   2.例子我也逐步验证了一下，实现代码地址为我的GitHub
>   
>   3.我太懒了，在实现过程中没有拷屏，文中图片全部来自原文。膜拜原作者。

---

原文地址:<http://www.smashingmagazine.com/2013/11/22/four-ways-to-build-a-mobile-app-part1-native-ios/>

---


开发移动应用有很多种方法，比较流行的有以下四种：

* native iOS
* native Android
* PhoneGap
* Appcelerator Titanium

本主题分四篇文章来分别讲解以上四种方法，并通过分别实现相同一个简单的移动应用来大体介绍每种技术的实践。很少有开发人员可以有机会通过这么多种方法和工具来完成自己的移动开发，本主题正好可以扩展你的视野。

希望有了这方面的了解后，在开发移动应用时你可以更好地选择合适的开发工具。本主题的第一篇文章，我将还大体介绍一下背景，并深入介绍iOS下的开发。

为对比展示不同平台与开发工具在开发理念上的不同，我会使用每一种技术构建相同的一个简单应用。本专题不是让你选定其中某个特定的技术，而是让你了解在不同环境下开发时常用的方法与概念，并使用多种工具完成移动应用。

FasTip是一个简单的计算小费的应用，这个例子足够简单，只使用了每个平台的标准UI控件。

<img src="{{ BASE_PATH }}/assets/images/fastip-app-screens-500-opt.png">

上图依次展示了采用native iOS,PhoneGap和native Android实现的该应用程序。Appcelerator Titanium使用的是平台的native控件，因此它分别看起来分别与native iOS和native Android一样。该应用有两个页面：主页面展现计算小费的内容，还有一个设置页面用来设置小费的百分比。为了保持简单，我使用了每个平台的默认风格。所有应用的源代码都可以在[GitHub](https://github.com/sw897/mobile-apps-4-ways)上获取。


### Native iOS 开发

大多数的苹果应用商店里的应用是使用Objective-C语言开发的，开发者一般使用Xcode来完成开发。

<img src="{{BASE_PATH}}/assets/images/xcode-screen-500-opt.png">

#### 获取开发工具

为构建一个iOS应用，必须使用OS X系统，其它的操作系统是不支持的。需要的开发工具有iOS 7 SDK和Xcode 5，这是免费的应用。然后使用iOS模拟器来运行编译好的应用，iOS模拟器是iOS SDK的一部分。如果想在一台设备上运行并在苹果应用商店里发布，就需要每年支付99美元。

* “[关于Xcode](https://developer.apple.com/library/ios/documentation/ToolsLanguages/Conceptual/Xcode_Overview/About_Xcode/about.html),” iOS开发库, Apple
* “[iOS开发者中心](https://developer.apple.com/devcenter/ios/index.action),” Apple
* “[iOS 开发](https://developer.apple.com/programs/ios/),” Apple

#### 创建工程

安装好Xcode后，在欢迎页面选择`Create a new Xcode project`或通过菜单`File>New Project`，创建一个新工程。

<img src="{{BASE_PATH}}/assets/images/xcode-new-project-500-opt.png">

像例子这种简单的应用，一般选择创建`Single View`程序。点击`Next`后出现应用基本信息对话框:

<img src="{{BASE_PATH}}/assets/images/new-project-options-500-opt.png">

`Class Prefix`设置会给使用Xcode创建的所有类添加一个唯一前缀。因为Objective-C不像Java一样支持`namespace`(命名空间)，添加唯一前缀可以避免命名冲突。`Devices`设置用来严格要求应用的运行平台是iPhone或iPad，`universal`选项可以让应用同时支持两者。


#### 导航控制器(NavigationController)与视图控制器(ViewController)

iOS应用的界面实现由视图控制器控制。示例有两个ViewController:一个主页面与一个设置页面。视图控制器包含了与屏幕控件交互的逻辑，并与导航控制器交互。导航控制器实现两个视图之间的转换，它在每个视图顶部提供了一个导航条。导航控制器管理了一个由视图控制器组成的视图栈，从而实现在不同屏幕里移动。

#### Storyboards: 可视化用户开发

从iOS 5开始, Xcode提供了storyboards, storyboards让开发者快速地定义一系列的视图，并分别指定每一页的内容。这是示例应用在storyboard中的展示。

<img src="{{BASE_PATH}}/assets/images/storyboard-overview-500-opt.png">

左侧的对象表示导航控制器，它使用户能够从一屏移到另一屏上。右边的两个对象所代表的是组成示例的两个屏幕或视图控制器。从主屏到设置屏的联线箭头，表示屏与屏之间的过渡。选择起始的视图按键同时按住`Ctrl`键，拖动到目标视图控制器上，可以创建一个新的联线。苹果文件有这个操作的更[详细介绍](https://developer.apple.com/library/ios/recipes/xcode_help-interface_builder/articles-storyboard/StoryboardSegue.html)。

<img src="{{BASE_PATH}}/assets/images/storyboard-properties-500-opt.png">

如上图所示，选择一个文本控件后，可以通过属性面板来调整控件的各种属性。当应用创建时，选择了“universal”选项，应用可以同时支持iPhone和iPad运行。从而，创建了两个版本的storyboard，运行时会根据设备选择_iPhone或_iPad的版本运行。这样可以两种设备上的不同布局，iPad可以使用更大的显示内容。视图控制器会自动加载合适的布局。谨记一点，如果storyboards对iPad和iPhone做了不同的一组表现控件，必须在视图控制器的代码里进行说明(account)。

除了直接在屏幕的特定坐标系里布局对象，从iOS6版本也可以使用自动布局系统(Auto Layout System)。这使你可以在视图的控件间定义约束关系。可以通过storyboard编辑器来[创建和编辑约束](https://developer.apple.com/library/ios/recipes/xcode_help-interface_builder/articles-autolayout/UnderstandingAutolayout.html)。


<img src="{{BASE_PATH}}/assets/images/storyboard-constraints-500-opt.png">

也可以使用程序来控制约束关系。自动布局机制有些复杂，第一次使用时可能会不太容易上手。在苹果的文档里有一个[关于自动布局的扩展指南](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/Introduction/Introduction.html)。

#### 关联Storyboards与代码

为在代码中访问访问storyboard对象，必须指定两者间的关联。相比使用其它的开发环境，通过Xcode关联storyboard与代码很容易。开始关联前，必须先创建好一个视图控制器。这个过程如下：

1.选择`File → New File`.

2.在弹出的对话框中选择`Objective-C class`:

<img src="{{BASE_PATH}}/assets/images/file-new-template-opt.png">

3.在接下来的对话框中设置类名并指定从UIViewController继承:

<img src="{{BASE_PATH}}/assets/images/file-new-options-500-opt.png">

4.点击“Next”，提示创建的类文件存储位置.本例中选择工程根目录。

5.点击“Next”，视图控制器文件创建完成。现在，关联新创建的视图控制器与storyboard中的视图.

6.在storyboard中, 选中视图. 在`Identity Inspector`面板, 选择待被关联的视图类:

<img src="{{BASE_PATH}}/assets/images/class-picker-opt.png">

7.操作完成，视图控制器中的代码就被storyboard入口关联上了。

在Objective-C代码里引用拖放到storyboard上控件时，需要先定义之间的关系。storyboard编辑器里的"assistant editor"视图可以方便完成这个操作。这是一个storyboard与代码的分隔面板。下面我们来看一下如何引用已经在storyboard上定义好的一个按键控件：

1.首先，确认通过以上步骤完成了视图控制器类与storyboard中视图的关联。

2.通过点击类似`assistant-editor-icon`的图标来选择辅助编辑器。

<img src="{{BASE_PATH}}/assets/images/assistant-editor-icon-opt.png">

3.当前会是一个分隔面板，storyboard在左边，视图控制器类在右边。

4.按下`Ctrl`键的同时，在storyboard里选择按键，拖动按键到代码interface区域。

<img src="{{BASE_PATH}}/assets/images/create-outlet-500-opt.png">

5.这时会显示一个对话框，用来创建按钮在代码中的一个“outlet”。给按钮设置一个名字，然后点击"Connect"。这样就完成了在视图控制器中的按钮与代码的关联。

6.现在来创建当点击按钮后触发的方法。选择按钮后，同样按住"Ctrl"拖动到代码的interface部分。

7.在弹出的对话框中，在"Connetion"下拉菜单处选择"action"而不是"outlet"，如下输入方法名字:

<img src="{{BASE_PATH}}/assets/images/create-action-500-opt.png">

“Event”使用默认的“Touch Up Inside”，然后点击"Connect"按按钮。

8.现在，代码的interface部分有两个声明：

{% highlight objective-c %}
@interface FTSettingsViewController ()
@property (weak, nonatomic) IBOutlet UIButton *myButton;
- (IBAction)tappedMyButton:(id)sender;
@end
{% endhighlight %}

IBOutlet用来表示storyboard引用的所有对象类型，IBAction用来表示操作。注意，Xcode创建了一个空方法，用来输入代码，来响应用户在控制上的操作:

{% highlight objective-c %}
- (IBAction)tappedMyButton:(id)sender {
}
{% endhighlight %}

以上步骤需要一些时间来适应，并会越来越直观。经过一些练习，会越来越顺手的。也许[“连接用户交互控制与代码”](https://developer.apple.com/library/ios/documentation/ToolsLanguages/Conceptual/Xcode_Overview/Edit_User_Interfaces/edit_user_interface.html#//apple_ref/doc/uid/TP40010215-CH6-SW3)这个Xcode文档中的书签会给你带来帮助。

正如我们将在后面介绍的，你也可以将对象添加到视图，并以编程方式操作它们的属性。事实上，即使是中等复杂的应用程序都通常在代码中进行大部分的控制。对于复杂的应用程序，一些开发人员避开了storyboard，并几乎完全使用代码替代。


#### 开始编写代码

即使再基本的应用程序，都少不了写代码。到目前为止，我们在storyboard中完成了UI与视图控制器间的映射，但没有编写相关的计算代码，以及保存小费百分比的设置等。这些都是开发人员使用objective-c来完成的。

当应用程序在运行时，其整个生命周期响应“应用程序委托”处理。在程序的生命周期中,由事件触发委托中的各种方法。这些事件有以下几种：

* 程序启动

* 程序转到后台

* 程序转到前台

* 程序结束

* 接收到推送消息

以上的事件在文件AppDelegate中处理。对于我们的示例程序，这些事件的默认处理足够了，不需要特殊的操作。文档中有应用程序的生命周期以及程序状态改变响应的介绍。接下来要注意的是视图控制器。正如应用委托，视图控制器也有其生命周期。视图控制器生命周期中包含以下事件触发时的响应方法：

* 视图控制器加载

* 视图控制器准备在屏幕上显示或已显示

* 视图控制器准备在屏幕上隐藏或已隐藏

* 视图边框改变(如设备旋转)，视图重新加载

示例应用代码主要在FTViewController.m文件中。以下是初始化屏幕的相关代码：

{% highlight objective-c %}
- (void)viewWillAppear:(BOOL)animated
{
    // 保存默认的小费百分比
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    float tipPercentage = [defaults floatForKey:@"tipPercentage"];
    if (tipPercentage > 0) {
        _tipPercentage = tipPercentage;
    } else {
        _tipPercentage = 15.0;
    }
    self.tipAmountLabel.text = [NSString stringWithFormat:@"%0.2f%%", _tipPercentage];
}
{% endhighlight %}

示例应用中，我们要可以使用过去保存的小费百分值。为达到这个目的，可以使用NSUserDefaults，用来保存应用中的设置。要注意，这些值没有经过任何的加密，因此这不是保存类似密码这种敏感数据的好方式。iOS SDK提供KeyChain API来保存这些数据。以上的代码，我们尝试获取小费百分比的设置。如果没有设置，设置默认值为15%。当用户点击了"计算小费"的按钮，运行如下代码:

{% highlight objective-c %}
- (IBAction)didTapCalculate:(id)sender {
    float checkAmount, tipAmount, totalAmount;

    if (self.checkAmountTextField.text.length > 0) {

        checkAmount = [self.checkAmountTextField.text floatValue];
        tipAmount = checkAmount * (_tipPercentage / 100);
        totalAmount = checkAmount + tipAmount;

        self.tipAmountLabel.text = [NSString stringWithFormat:@"$%0.2f", tipAmount];
        self.totalAmountLabel.text = [NSString stringWithFormat:@"$%0.2f", totalAmount];

    }

    [self.checkAmountTextField resignFirstResponder];

}
{% endhighlight %}

读取用户在“金额”输入框内输入的值，然后计算小费。stringWithFormat方法用来格式化计算结果的表现。当用户点击“设置”按钮后，将会转到设置视图控制器。FTSettingsViewController文件用来处理这一屏幕的交互。按下此屏中的“完成”按钮将会运行以下代码：

{% highlight objective-c %}
- (IBAction)didTapDone:(id)sender {

    float tipPercentage;
    tipPercentage = [self.tipPercentageTextField.text floatValue];

    if (tipPercentage > 0) {

        NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
        [defaults setFloat:tipPercentage forKey:@"tipPercentage"];
        [defaults synchronize];

        [[self navigationController] popViewControllerAnimated:YES];

    } else {

        [[[UIAlertView alloc] initWithTitle:@"Invalid input"
                                    message:@"Percentage must be a decimal value"
                                   delegate:nil
                          cancelButtonTitle:@"ok"
                          otherButtonTitles:nil] show];

    }

}
{% endhighlight %}

从文本输入框中获取小费百分比值，验证输入值大于0。然后使用NSUserDefaults保存设置。调用synchronize方法保存值到存储中。保存后，使用导航控制器中的popViewControllerAnimated方法移除设置视图，并返回前一屏幕。如果用户没有填写有效的百分数，将继续保留在该屏幕，并弹出一个提示框。

需要说明的是，以上通过视图控制器与storyboard完成的部分，可以通过编程实现。以下的代码片段实现了创建一个按钮并把它定位在屏幕上。这些对于我们的程序并不需要。

{% highlight objective-c %}
CGRect buttonRect = CGRectMake(100, 75, 150, 80);
UIButton *myButton = [UIButton buttonWithType:UIButtonTypeRoundedRect];
myButton.frame = buttonRect;
[myButton setTitle:@"Click me!" forState:UIControlStateNormal];
[self.view addSubview:myButton];
{% endhighlight %}

一般来说，所有的添加在视图上的控件都扩展自UIView类。比如：按钮，标签，文本输入框等等都是UIView。UIView的实例在视图控制器中，视图控制器中的代码可以通过self.view获取。iOS SDK通过一个frame上的view来定位对象，也就是CGRect。CGRect包含对象的x,y坐标，以及对象的长，宽属性。以上的代码中，按钮通过一个frame(位置与尺寸)实例化并加到视图控制器中。

#### 运行与调试iOS应用程序

安装好Xcode与iOS SDK后，模拟iOS设备的iOS模拟器就安装好了，通过它可以在电脑上虚拟一个iOS设备。通过Xcode中的下拉菜单可以选择不同的设备配置。点击在左上角的“Run”按钮在指定的模拟器中运行应用程序。

<img src="{{BASE_PATH}}/assets/images/device-chooser-500-opt.png">

通过上面的菜单，可以选择Retian或非Retian屏的iPhone或iPad设备。通过点击代码编辑器中行号的左边，进行debug。当程序运行到断点，程序会停止并在代码编辑器下面显示当前时多个变量的值。

<img src="{{BASE_PATH}}/assets/images/breakpoint-variables-500-opt.png">

推送提示等功能不能在模拟器中测试。对于这些功能，必须在一个真实设备上测试，这就要求注册一个每年99美元的苹果开发者帐号。获取帐号后，可以通过usb线连接设备，Xcode会提示你输入你的证书并为你的设备提供一个“provision”。一量设备被识别，就显示在通过选择模拟器的下拉菜单中。

在Xcode中，选择`Window->Organizer`菜单会显示一个管理工具，里面有Xcode中所有设备，以及测试日志等，还可以通过这个工具导出应用程序。


### 总结

到目前为止，我们已经了解了开发一个简单的iOS本地应用的基本内容。大多的应用比这要复杂，但以下基本的构成内容：

* Xcode

开发环境

* Storyboards

用来设计与配置用户接口

* View controllers

storyboard中定义的视图的基本逻辑控制

* Navigation controllers

不同视图间的切换控制


#### 学习资源

学习iOS开发，可以参阅以下资源：

* [iOS Programming: The Big Nerd Ranch Guide](http://www.amazon.com/iOS-Programming-Edition-Guides-ebook/dp/B007OWBAB0/ref=tmm_kin_title_0?ie=UTF8&qid=1365887748&sr=8-1), Joe Conway and Aaron Hillegass

这本书很妙，它包含了Objective-C与iOS的开发，并通过很好的例子来保持你的兴趣。

* [Objective-C Programming: The Big Nerd Ranch Guide](http://www.amazon.com/Objective-C-Programming-Ranch-Guide-Guides/dp/0321706285/ref=pd_bxgy_b_text_y), Aaron Hillegass

这本书提供了Objective-C更详细的信息，可以让你超越iOS开发，深入语言的特性。

* “[Coding Together: Developing iOS 6 Apps for iPhone and iPad](https://itunes.apple.com/us/course/coding-together-developing/id593208016),” Stanford University

该系列的视频在iTunes U上。

* “[WWDC 2013 Session Videos](https://developer.apple.com/wwdc/videos/),” Apple

每届WDC(世界开发者大会)后，苹果发布的大会视频内容。适合所有的iOS开发者。

* “[iOS 7 Design Resources](https://developer.apple.com/library/ios/navigation/),” Apple

该iOS文档很好，有很多关于iOS SDK的关键功能的指南。

* [Ray Wenderlich: Tutorials for iPhone / iOS Developers and Gamers](http://www.raywenderlich.com/)

Ray 分享了极多的教程系列, 并定期添加新的内容. 高级教程成本出售。

我们就这样结束应用开发的第一部分。我希望它让你了解了iOS原生应用开发的基本概念。在本系列的下一篇文章将介绍如何使用Android原生开发工具来构建相同的应用程序。

