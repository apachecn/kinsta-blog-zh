# WordPress 数据库——侧边栏如何工作

> 原文：<https://kinsta.com/blog/wordpress-database-how-sidebars-work/>

侧边栏是 WordPress 体验中不可或缺的一部分，但是理解它们如何在数据库层面上工作并不是教程的重点。你可以找到任意数量的关于[创建小部件](https://kinsta.com/blog/wordpress-widgets/)，定制它们，扩展它们等等的帖子，但是它们是如何在最后放在一起，并出现在多个侧边栏中的，这一点经常被忽略。

在这篇文章中——真正的数据库系列——我们将看看侧栏和窗口小部件是如何存储在数据库中的。

*   [什么是微件区](#what-is-a-widget-area)
*   [数据库中的微件区域](#widget-areas-in-the-database)
*   [数据库中的小部件](#widgets-in-the-database)

## 什么是小部件区域

侧边栏这个术语实际上是用词不当，因为这不是我们真正在谈论的。侧边栏这个术语来源于侧边栏开始流行的时候，它们是第一个被“widget 化”的。从那时起，我们发现页脚、页眉和其他部分有时可以受益于小部件——模块化的内容块。

从现在开始，我将引用“部件区域”。侧边栏可以是一个小部件区域，就像网站上的任何其他部分都可能包含小部件一样。简而言之:任何可以包含小部件并可以从管理中的小部件部分控制的区域都构成了一个小部件区域。


## 数据库中的小部件区域

小部件区域——实际上是所有的小部件——都存储在选项表中。要查看的第一行是带有`sidebars_widgets`的`option_name`的那一行。`option_value`列的内容包含所有已定义的侧栏和其中小部件的 ID。如果您使用`var_dump( get_option( 'sidebars_widgets' ) )`，您会看到类似这样的内容:

```
Array
(
    [wp_inactive_widgets] => Array
        (
        )

    [sidebar-1] => Array
        (
            [0] => text-2
            [1] => categories-2
        )

    [array_version] => 3
)
```

在我当前的设置中，我没有任何不活动的小部件，我有一个侧边栏(sidebar-1 ),其中有一个文本小部件和一个类别列表小部件——这些小部件的 ID 显示在数组中。

基于这些信息，我们知道定义了什么侧边栏以及它们包含什么小部件，但是我们不知道关于每个特定小部件的任何配置。为了获得这些信息，我们需要查看更多的行。


## 数据库中的小部件

每个小部件在选项表中都有单独的一行。该选项的值包含该类型的所有已定义小部件及其设置。要获得所有已定义的文本小部件，我们需要查看`widget_text`选项的值。要查看类别列表小部件，我们需要`widget_categories`选项。

```
Array
(
    [1] => Array
        (
        )

    [2] => Array
        (
            [title] => First Text Widget
[text][/text]

=> Fist Content
[filter] =>
)

[_multiwidget] => 1
) 
```

我已经把`get_option( 'text_widget' )`的结果贴在上面了。那里有一个空数组，是被删除的小部件的剩余部分，第二个成员对应于来自`sidebars_widgets`的值的`text-2`。它包含小部件的所有选项。

## 摘要

如果需要的话，我们现在已经有了组装边栏所需的所有数据，并且希望对后台的工作方式有更深的理解。我认为，了解侧边栏在数据库级别上的工作方式，可以让我们深入了解如何使用现成的功能来操作它们，并在需要时以独特的方式操作它们。

想去掉侧边栏吗？查看:[如何移除 WordPress 中的侧边栏(4 种方法)](https://kinsta.com/knowledgebase/remove-sidebar-wordpress/)。

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。