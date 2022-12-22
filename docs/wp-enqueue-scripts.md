# WP _ Enqueue _ scripts——如何在 WordPress 中排列你的资产

> 原文：<https://kinsta.com/blog/wp-enqueue-scripts/>

在 WordPress 中，你应该使用一种叫做 enqueueing 的方法，而不是简单地把它们添加到标题中，这是一种处理你的资产的标准化方法，并有管理依赖关系的额外好处。使用`wp_enqueue_scripts`在下面找出如何做。

*   [排队是如何工作的](#how-enqueueing-works)
*   [用 wp_enqueue_scripts 进行基本排队](#enqueueing-basics)
*   [依赖关系管理](#dependency-management)
*   [在页脚加载脚本](#load-scripts-in-footer)
*   [为样式指定媒体](#specifying-media-for-styles)

## 排队是如何工作的

将脚本或样式入队时需要两个步骤。首先你注册它——告诉 WordPress 它在那里——然后你实际上把它排队，最终把它输出到标题中，或者就在结束的 body 标签之前。

有两个步骤的原因与模块化有关。有时你想让 WordPress 知道某项资产，但你可能不想在每一页上都使用它。例如:如果你正在构建一个使用 Javascript 的自定义图库短代码，你实际上只需要在使用短代码时加载 JS——可能不是在每个页面上。

实现这一点的方法是首先注册脚本，只有当显示短代码时才真正将其加入队列(建议阅读:[WordPress 短代码的最终指南](https://kinsta.com/blog/wordpress-shortcodes/))。
T3】

## wp_enqueue_scripts 入队基础知识

要在前端对脚本和样式进行排队，您需要使用`wp_enqueue_scripts`钩子。在挂钩功能中，您可以使用`wp_register_script()`、`wp_enqueue_script()`、`wp_register_style()`和`wp_enqueue_style()`功能。

```
add_action( 'wp_enqueue_scripts', 'my_plugin_assets' );
function my_plugin_assets() {
    wp_register_style( 'custom-gallery', plugins_url( '/css/gallery.css' , __FILE__ ) );
    wp_register_script( 'custom-gallery', plugins_url( '/js/gallery.js' , __FILE__ ) );

    wp_enqueue_style( 'custom-gallery' );
    wp_enqueue_script( 'custom-gallery' );
}
```

在上面的例子中，我在同一个函数中注册和排列了资产，这有点多余。事实上，您可以使用入队函数立即注册和入队，方法是使用与注册函数中相同的参数:

```
add_action( 'wp_enqueue_scripts', 'my_plugin_assets' );
function my_plugin_assets() {
    wp_enqueue_style( 'custom-gallery', plugins_url( '/css/gallery.css' , __FILE__ ) );
    wp_enqueue_script( 'custom-gallery', plugins_url( '/js/gallery.js' , __FILE__ ) );
}
```

如果我要分离这两个函数，我会在不同的[钩子](https://kinsta.com/blog/wordpress-hooks/)中使用它们。在一个真实的例子中，我们可以使用`wp_enqueue_scripts`钩子来注册资产，并使用 shortcode 的函数来对它们进行排队。

```
add_action( 'wp_enqueue_scripts', 'my_plugin_assets' );
function my_plugin_assets() {
    wp_register_style( 'custom-gallery', plugins_url( '/css/gallery.css' , __FILE__ ) );
    wp_register_script( 'custom-gallery', plugins_url( '/js/gallery.js' , __FILE__ ) );

}

add_shortcode( 'custom_gallery', 'custom_gallery' );

function custom_gallery( $atts ){

    wp_enqueue_style( 'custom-gallery' );
    wp_enqueue_script( 'custom-gallery' );

    // Gallery code here
}
```

## 依赖性管理

WordPress 的入队机制内置了对依赖管理的支持，使用了`wp_register_style()`和`wp_register_script()`函数的第三个参数。如果不需要将它们分开，也可以立即使用入队功能。

第三个参数是注册脚本/样式的数组，需要在当前资产入队之前加载。我们上面的例子很可能依赖于 [jQuery](https://kinsta.com/knowledgebase/what-is-jquery/) ,所以现在让我们指定:

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

```
add_action( 'wp_enqueue_scripts', 'my_plugin_assets' );
function my_plugin_assets() {
    wp_enqueue_script( 'custom-gallery', plugins_url( '/js/gallery.js' , __FILE__ ), array( 'jquery' ) );
}
```

我们不需要自己注册或排队 jQuery，因为它已经是 WordPress 的一部分。你可以在 Codex 中找到 WordPress 中可用的[脚本和样式列表。](https://codex.wordpress.org/Function_Reference/wp_enqueue_script#Default_Scripts_Included_and_Registered_by_WordPress)

如果您有自己的依赖项，您将需要注册它们，否则您的脚本将无法加载。这里有一个例子:

```
add_action( 'wp_enqueue_scripts', 'my_plugin_assets' );
function my_plugin_assets() {
    wp_enqueue_script( 'custom-gallery', plugins_url( '/js/gallery.js' , __FILE__ ), array( 'jquery' ) );
    wp_enqueue_script( 'custom-gallery-lightbox', plugins_url( '/js/gallery-lightbox.js' , __FILE__ ), array( 'custom-gallery' ) );
}
```

让我们假设第一个脚本是一个图库，第二个脚本是一个扩展，它使图片在 lightbox 中打开。注意，即使我们的第二个脚本依赖于 jQuery，我们也不需要指定这一点，因为我们的第一个脚本已经加载了 jQuery。也就是说，陈述所有的依赖关系可能是一个好主意，只是为了确保如果你忘记包含一个依赖关系，没有什么会中断。

WordPress 现在知道我们需要哪些脚本，并且可以计算出它们需要被添加到页面的顺序。

## 在页脚加载脚本

只要能够在页脚加载脚本，就应该这样做。这增加了明显的页面加载时间，并可以防止您的网站在加载脚本时挂起，特别是如果它们包含 [AJAX 调用](https://kinsta.com/blog/admin-ajax-php/)。

入队机制可以使用第五个参数(第四个是可选的版本号)将脚本添加到页脚。如果我们稍微修改一下，上面的例子会在页脚加载脚本。

```
add_action( 'wp_enqueue_scripts', 'my_plugin_assets' );
function my_plugin_assets() {
    wp_enqueue_script( 'custom-gallery', plugins_url( '/js/gallery.js' , __FILE__ ), array( 'jquery' ), '1.0', true );
    wp_enqueue_script( 'custom-gallery-lightbox', plugins_url( '/js/gallery-lightbox.js' , __FILE__ ), array( 'custom-gallery', 'jquery' ), '1.0', true );
}
```

将 true 指定为第五个参数会将脚本放在页脚中，使用 false 或省略参数会将内容加载到页眉中。正如我之前提到的，只要有可能，就在页脚加载脚本。


## 为样式指定媒体

使用样式注册/入队函数的第五个参数，您可以控制脚本定义的媒体类型(打印、屏幕、手持等。).通过使用这个参数，您可以将样式的加载限制到特定的媒体类型，这是一个方便的优化小技巧。

```
add_action( 'wp_enqueue_scripts', 'my_plugin_assets' );
function my_plugin_assets() {
    wp_register_style( 'custom-gallery-print', plugins_url( '/css/gallery.css' , __FILE__ ), array(), '1.0', 'print' );

}
```

关于可以使用的媒体类型的完整列表，请看一下 [CSS 规范](http://www.w3.org/TR/CSS2/media.html#media-types)。

## 摘要

将资产排队是处理它们的一种强大方式。它给了你和其他插件/主题制作者对整个系统更多的控制权，并把依赖管理从你手中拿走。

如果这还不够，这是添加你的资产的**方法，如果你不使用这种方法，许多主题市场和 WordPress 知识库本身不会批准你的工作。**

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。