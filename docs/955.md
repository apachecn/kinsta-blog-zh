# 如何使用 WordPress 注册侧边栏功能

> 原文：<https://kinsta.com/blog/wordpress-register-sidebar/>

在这篇文章中，我们将看看使用 [WordPress 注册侧边栏功能](https://developer.wordpress.org/reference/functions/register_sidebar/)的一些方法，以及一些高级技巧！

*   [WordPress 注册侧边栏–单个](#wordpress-register-sidebar-single)
*   [WordPress 注册侧边栏——一次多个侧边栏](#wordpress-register-sidebar-multiple)
*   [更好地注册多个侧边栏](#multiple-sidebars-better)

## WordPress 注册侧边栏–单个

为了让侧边栏在你的主题中工作，你需要首先让 WordPress 知道它——确保它出现在管理中——并添加一些前端代码来显示[小部件](https://kinsta.com/blog/wordpress-widgets/)。要注册侧边栏，你可以选择两个选项之一:用`register_sidebar()`注册一个侧边栏，或者用`register_sidebars()`一次注册多个侧边栏。

`register_sidebar()`函数的基本用法如下:

```
add_action( 'widgets_init', 'my_awesome_sidebar' );
function my_awesome_sidebar() {
  $args = array(
    'name'          => 'Awesome Sidebar',
    'id'            => 'awesome-sidebar',
    'description'   => 'The Awesome Sidebar is shown on the left hand side of blog pages in this theme',
    'class'         => '',
    'before_widget' => '<li id="%1$s" class="widget %2$s">',
    'after_widget'  => '</li>',
    'before_title'  => '<h2 class="widgettitle">',
    'after_title'   => '</h2>' 
  );

  register_sidebar( $args );

}
```

这些函数应该从一个与`widgets_init`挂钩的函数中调用，它采用一个参数数组。当用户组装侧栏时，名称和描述显示在后端，最后四个参数用于显示每个小部件。

标题之前和之后的参数被添加到标题的前面和后面，小部件之前和之后的参数被添加到小部件元素的前面和后面。这使得整个侧边栏的小部件都具有统一的样式。

## 注册侧边栏——一次多个侧边栏

`register_sidebars()`函数与它的单数形式 brother 几乎完全相同，但是需要一个额外的参数来指定要添加的侧边栏的数量。这里有一个简单的例子:

```
add_action( 'widgets_init', 'my_theme_sidebars' );
function my_theme_sidebars() {
  $args = array(
    'name'          => 'Awesome Sidebar %d',
    'id'            => 'awesome-sidebar',
    'description'   => 'One of the awesome sidebars',
    'class'         => '',
    'before_widget' => '<li id="%1$s" class="widget %2$s">',
    'after_widget'  => '</li>',
    'before_title'  => '<h2 class="widgettitle">',
    'after_title'   => '</h2>' 
  );

  register_sidebars( 3, $args );

}
```

这里唯一的不同是使用了`%d`占位符，它将显示侧边栏编号，在我们的例子中是 1、2 或 3。

## 更好地注册多个侧边栏

上述函数的一个问题是，它不允许您定制标题和描述，而且使用“id”参数在技术上是不正确的，因为它应该是唯一的。为了解决这个问题，我通常建立一个信息数组，并通过它来创建我的边栏，下面是方法。

```
add_action( 'widgets_init', 'my_awesome_sidebar' );
function my_awesome_sidebar() {

  $my_sidebars = array(
    array(
      'name'          => 'Header Widget Area',
      'id'            => 'header-widget-area',
      'description'   => 'Widgets shown in the flyout of the header',
    ),
    array(
      'name'          => 'Header Widget Area',
      'id'            => 'header-widget-area',
      'description'   => 'Widgets shown in the flyout of the header',
    ),
    array(
      'name'          => 'Header Widget Area',
      'id'            => 'header-widget-area',
      'description'   => 'Widgets shown in the flyout of the header',
    ),  
  );

  $defaults = array(
    'name'          => 'Awesome Sidebar',
    'id'            => 'awesome-sidebar',
    'description'   => 'The Awesome Sidebar is shown on the left hand side of blog pages in this theme',
    'class'         => '',
    'before_widget' => '<li id="%1$s" class="widget %2$s">',
    'after_widget'  => '</li>',
    'before_title'  => '<h2 class="widgettitle">',
    'after_title'   => '</h2>' 
  );

  foreach( $my_sidebars as $sidebar ) {
    $args = wp_parse_args( $sidebar, $defaults );
    register_sidebar( $args );
  }

}
```

首先，我已经定义了许多侧栏，每个侧栏都有我需要更改的参数。我还创建了一个默认参数集，可以在某处没有数据的情况下使用。在遍历侧边栏数组时，我们将侧边栏特定的参数数组与默认值合并，并将它们传递给`register_sidebar()`函数。

如果你想变得更有趣，你可以将侧边栏数组从这个函数中分离出来，并创建你自己的函数，你可以从一个主题到另一个主题重复使用，你所需要做的就是修改侧边栏数组。

这给了你更多的控制和更多的标准化，如果你提供更新和支持，这是非常好的。

## 摘要

只要你使用默认的 WordPress 函数，你如何注册侧边栏并不重要，但是如果你经常做主题相关的工作或者想要开始创建一些可重用的片段，我强烈推荐使用循环和数据数组。

我个人不喜欢`register_sidebars()`函数，因为它在很多情况下会导致无效的 HTML，而且它不能给你在适当的主题场景中应有的控制。

建议阅读:[如何移除 WordPress 中的侧边栏(4 种方法)](https://kinsta.com/knowledgebase/remove-sidebar-wordpress/)。

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。