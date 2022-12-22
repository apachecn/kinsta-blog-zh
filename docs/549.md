# 如何改进 WordPress 搜索(并加快速度)

> 原文：<https://kinsta.com/blog/wordpress-search/>

为什么人们首先使用网站搜索表单？这是因为他们在寻找即时的相关结果，而这些结果是他们无法通过浏览网站或使用导航获得的。

有时，这些搜索结果[会提供他们问题的答案](https://kinsta.com/blog/wordpress-faq-plugins/)(比如关于公司退货政策的信息)或匹配产品或内容的列表(比如与[页面生成器插件](https://kinsta.com/blog/wordpress-page-builders/)相关的博客帖子)。不管他们在找什么，有一件事是肯定的:

访问者希望你的 WordPress 搜索表单能够快速准确地传递结果。

当你把消费者行为作为一个整体来看待时，这是有意义的。谈到在线搜索，谷歌设定了一个几乎不可能的标准。根据 SparkToro 的调查结果，谷歌超过一半的搜索是零点击。基本上，谷歌已经使搜索变得如此高效，以至于人们通常不需要访问一个网站就可以获得他们问题的答案。

当然，你的网站访问者并没有使用内部搜索来期望或者想要一个零点击的结果。他们使用搜索来寻找你网站的其他部分。但是你的 WordPress 搜索和[谷歌搜索](https://kinsta.com/blog/google-search-operators/)*的共同点是:消费者希望从它们那里得到快速、方便和高度相关的结果。*

 *只有一个问题:WordPress 的原生搜索功能不是很好。

这就是为什么，在本指南中，我们将探索你需要知道的一切，以便**为你的访问者优化 WordPress 搜索体验**:

## 内部搜索到底有多重要？

如果你以正确的方式设计了一个网站，访问者自然会沿着你给他们铺好的路走下去。一份[组织有序的菜单](https://kinsta.com/blog/wordpress-menu-plugins/)也有帮助。





> Kinsta 把我宠坏了，所以我现在要求每个供应商都提供这样的服务。我们还试图通过我们的 SaaS 工具支持达到这一水平。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![](img/60f15faa5735bd2437bf9dada5ee9192.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Suganthan Mohanadasan from @Suganthanmn</cite></footer>

[View plans](https://kinsta.com/plans/)

也就是说，内部搜索在这方面发挥着重要作用。

把 WordPress 搜索想象成你网站的快速通行证。当你的搜索功能正常运行时，它可以在几秒钟内将你的访问者从第一步带到第五步。

这对拥有大量内容的 WordPress 网站尤其有用。以下是一些例子:

### 电子商务

像 [Nordic Ware](https://www.nordicware.com.au/) 这样的在线商店可以帮助访问者从主页:

![The Nordic Ware ecommerce and recipe site uses a product search bar in its header.](img/1f245cc50845f0f86f8df4baea89d474.png)

Nordic Ware: home page with search bar in the header



只需使用网站右上角的搜索栏即可缩小产品列表:

![A search for “bundt” on the Nordic Ware website reveals a number of results that match the query.](img/52abced7dc742105623396497051b9b9.png)

Nordic Ware: search results page



通过始终提供产品搜索表单，访问者再也不必在商店的菜单或类别中筛选，以找到他们正在购买的特定商品。

### 博客、播客和新闻网站

像 [Kinsta](https://kinsta.com/) 这样拥有 39 页博客文章(还在增长)的大型内容库的网站，将从搜索栏中受益:

![An example of recent posts published to the Kinsta blog and the pagination revealing 39 pages of posts available to read.](img/d211727179f00138fc4e0dac77f9efec.png)

Kinsta: blog page and pagination



通过在博客顶部放置一个博客专用的搜索表单，读者可以比滚动浏览 39 页更快地找到他们要找的主题:

![Kinsta places a search bar at the top of its blog to help visitors find content around topics that interest them the most.](img/c9c304ca51c062dd20f1ff2f563392e9.png)

WordPress search bar at the top of the Kinsta blog



博客有很多内容，会变得难以浏览。因为你想保持博客页面简短以保持高加载速度，所以增加出现的文章数量并不是一个好主意。

相反，搜索栏会帮助你的访问者更有效地找到与他们当前兴趣无关的帖子。

### 列表网站

搜索是访问者在聚集列表的网站上首先做的事情之一(例如，房地产、旅游、专业服务等)。)，比如这个来自 [Trulia](https://www.trulia.com/) 的例子:

![Trulia, like other listings sites, places a search form on the home page.](img/659b0111fed844e6574704d6f3123008.png)

Trulia: home page search for properties



搜索元素总是简单到足以开始。例如，指定一个地点、人名或职务。但是结果页面总是能让用户尽可能地过滤他们的结果:

![An example of a search results page for “Providence, RI” homes for sale on the Trulia site.](img/c8708de431dd04d2a577cdc199e6b1aa.png)

Trulia: example search results page



### 知识库

对于像[element 或](https://kinsta.com/blog/wordpress-elementor/)这样的产品，搜索是帮助中心和知识库的一个有用组件:

![Elementor divides its knowledgebase up by topic while also showing users how many articles are available for each.](img/9da95bd1cef257d254ed16662b148676.png)

Elementor: knowledgebase article topics and counts



与手动搜索类别相比，搜索可以帮助用户更快地找到问题的答案:

![An example of how to use Elementor to search for “template” and the autopopulated results the search form displays.](img/ba4f78edb9ff64dc8eda7625a241cf56.png)

Elementor: search through documentation for “template”



在许多情况下，用户在使用 [SaaS 产品](https://kinsta.com/blog/saas-products/)时遇到的问题可以由用户自己轻松解决。如果你想让你的[实时聊天](https://kinsta.com/blog/wordpress-live-chat-plugin/)和帮助台支持没有易于解决的问题，让你的知识库易于搜索。

### 结果

如果你的网站上有大量的*内容*，不要认为[导航](https://kinsta.com/blog/website-navigation/)会帮助访问者浏览。建立一个快速的搜索体验，让他们准确地到达他们需要和想要去的地方。


## 如何给你的 WordPress 网站添加搜索

你有几个选项来为你的网站实现和启用基本的 WordPress 搜索:

### 将 WordPress 搜索添加到你的主题菜单中

根据你安装的 WordPress 主题的不同，你只需点击几下就可以将搜索添加到你的菜单中。在这个例子中，我使用的是 [Astra 主题](https://wordpress.org/themes/astra/)，而 btw 的结果是[非常快](https://kinsta.com/blog/fastest-wordpress-theme/#astra)！

首先要做的是进入外观>定制:

![How to locate the WordPress Customize menu.](img/34f7b741a30d89ff5174236f5ebfa641.png)

WordPress – navigate to Customize menu



接下来，进入标题>主菜单。

![How to customize the look and content of a WordPress menu.](img/fdbbeec960a909e3d5171fb563e63272.png)

WordPress – customize the menu



在“菜单中的最后一项”下，从下拉列表中选择“搜索”。

![How to add the search bar to a WordPress menu using the theme’s Customizer settings.](img/079de8545dfbc198b46a2d4a75cd0283.png)

WordPress – add a search bar to menu



这将添加一个搜索图标和栏作为导航菜单的最后一个元素。

![An example of how the basic WordPress search bar looks.](img/3f0113917b1fc9e3b22c6c4a4ef93643.png)

WordPress – search bar added with theme settings



当使用其他 [WordPress 主题](https://kinsta.com/blog/how-to-install-a-wordpress-theme/#where)时，这个搜索激活设置可能不在你的主题定制器中。如果有，你可以在“标题”设置下找到。否则，您必须使用下面的选项之一手动添加它。

### 用 WordPress 小工具添加搜索

WordPress widgets 使你能够将内容添加到围绕你的内容的元素中的专用块，如[侧边栏](https://kinsta.com/blog/wordpress-dynamic-sidebars-widgets/)和[页脚](https://kinsta.com/knowledgebase/add-code-wordpress-header-footer/)。

你可以用 WordPress 小部件创建的一种内容块是搜索栏。

首先定位外观菜单下的小部件:

![How to locate the Widgets menu in WordPress.](img/2f6ff240c2f8b571d55d4094dd8e0618.png)

WordPress – locate the Widgets menu



您可以在这里找到所有加宽区域。根据您使用的主题或模板，您可能只会看到边栏或页脚，或者您可能会看到更全面的选择，如下所示:

![An example of the kinds of widget areas you can add search to in WordPress.](img/32bf9f7bd5e85b01d55523e4f8382c48.png)

Example of widgets and sections



不管怎样，你现在需要做的是决定你希望你的搜索栏出现在哪里。

假设您计划每天发布新的[博客内容](https://kinsta.com/blog/content-length/),并且知道档案将快速增长。因此，在每个博客页面上提供一个搜索栏将是有益的。

滚动到部件的底部，找到名为“搜索”的部件:

![Where to find the Search widget in WordPress.](img/271140cb4615336dc531e3d3de8b8db9.png)

Search widget



您可以通过单击它并选择要添加到哪个部分来添加它，如下所示:

![How to add a Search widget to the sidebar with a dropdown.](img/8bf59f940f8a85c72d7b17a582776dc7.png)

Add Search widget with dropdown



或者，您可以将小部件拖放到您希望它出现的节块中:

![How to add a Search widget to the sidebar by dragging and dropping it into place.](img/26641a18c6ea43958f2097b5b95d807d.png)

Add Search widget with drag-and-drop



一旦你把它放在你想要的地方，给它一个名字:

![How to add a title to a WordPress Search widget.](img/6b8a78e353d26f091806070137a77f62.png)

Give your Search widget a title



保存您的更改，然后访问您的站点以确认它看起来符合您的要求:

![An example of a WordPress search bar added as a widget to a blog.](img/2d202208c94349cc36401a98f4040ec7.png)

Search bar added to blog



你现在可以看到搜索栏位于博客侧边栏的顶部，供读者使用。

### 用 WordPress 工具给你的网站的主要内容添加搜索

虽然把你的搜索栏放在你的网站经常出现的元素中很有用，但是你也可以找到一个理由把它放在你的页面的实际内容中。

有几种方法可以实现这一点:

#### 使用 WordPress 编辑器

古腾堡编辑器无疑使得设计更有创意的页面布局变得更加容易，而不必依赖于 [HTML](https://kinsta.com/knowledgebase/edit-wordpress-code/) 或[短代码](https://kinsta.com/blog/wordpress-shortcodes/)。

多亏了 WordPress 编辑器，你现在可以添加到你的页面中的一个这样的元素是搜索部件:

![How to find the search widget block using the Gutenberg editor.](img/a064fe676d2343586191145842b4c634.png)

Search widget block in Gutenberg



使用此选项时，您可以更好地控制搜索栏的显示方式。例如，您可以更改搜索栏的标题、占位符文本以及按钮:

![Customization options available when you add a search widget with the Gutenberg editor.](img/8b00c854394a253bc9ec47aa754203ec.png)

Customize search bar with Gutenberg



你甚至可以用自定义 CSS 类来改变搜索块的样式。

#### 使用页面生成器插件

对于那些喜欢使用像 Elementor 这样的拖放式页面构建器插件的人来说，也可以使用自己选择的插件来访问搜索小部件。这个过程类似于你对古腾堡所做的。

打开一个新的页面或文章，激活元素编辑器，从你的元素列表中搜索 WordPress 搜索窗口小部件:

![Where to find the WordPress search widget in your Elementor plugin.](img/a8e5c916a6012a6d0cf6f9aca8db3ef5.png)

Search widget in Elementor



将搜索元素拖到您希望它出现在页面上的位置。例如，这是一个 [404 页面](https://kinsta.com/blog/error-404-not-found/)，它通过一个搜索栏帮助用户回到正轨:

![An example of how a 404 error page might present lost visitors with a search bar.](img/d48a122c3f918094f78c2be85e1ea24d.png)

404 page example with search bar



正如你所看到的，页面生成器插件让你比 Gutenberg 更能控制你的 WordPress 搜索栏出现在哪里，允许你在其他内容之上或之内分层。

#### 有主题的

在某些情况下，您可能会发现一个主题和模板，它会自动将搜索添加到您网站的内容中。然而，这样做的主题往往是高度专业化的，比如[住宅房地产主题](https://themeforest.net/item/wp-residence-real-estate-wordpress-theme/7896392):

![A demo of the Residence Real Estate theme in ThemeForest, showing how search is automatically built into the template.](img/ae2776c19d7fab0f0a3d7a98f5f7cf35.png)

Demo of the Residence Real Estate theme



因为在像这样的[列表网站](https://kinsta.com/blog/directory-website-wordpress/)上搜索会变得复杂，所以[主题开发者](https://kinsta.com/blog/hire-wordpress-developer/)将[功能构建到模板](https://kinsta.com/blog/how-to-customize-wordpress-theme/#the-functions-file)中是有意义的。

预订网站主题是内置搜索功能的另一个例子，就像这个来自[旅游预订主题](https://themeforest.net/item/traveler-traveltourbooking-wordpress-theme/10822683)的演示一样:

![A demo of the Travel Booking theme in ThemeForest, showing how search is automatically built into the template.](img/52de16ba8aed5baebf9d6ac975933175.png)

Demo of the Travel Booking theme



正如你所想象的，在你的 WordPress 主题和模板中内置搜索将会省去你自己构建如此复杂的东西的麻烦。如果[主题针对性能](https://kinsta.com/learn/speed-up-wordpress/)进行了优化，那么它的[搜索引擎](https://kinsta.com/blog/alternative-search-engines/)解决方案也应该如此(又少了一件需要担心的事情)。

### 用代码添加 WordPress 搜索

还有一种方法可以在你的网站上添加一个基本的搜索表单，但是这需要你熟悉编码。

为此，请转到外观>主题编辑器:

![How to access the Theme Editor in WordPress.](img/d158b1d3997e1e077cf666591e595d7c.png)

Theme Editor



这里你要做的是使用 functions.php 主题文件为搜索栏创建一个短代码:

![Open the functions.php file from the WordPress theme editor.](img/a751e858fad607d3ea37116767bd70e8.png)

The functions.php theme file



在文件底部，添加以下代码片段:

```
add_shortcode( 'shortcodename', 'get_search_form');
```

在搜索表单中用您自己的名字替换“shortcodename”。确保全部小写，没有空格、数字或符号。一旦你更新了文件，你就可以开始在你的网站上使用你的短代码了。

这里有一个例子:

![How to create and use a custom shortcode to add a search bar anywhere on your WordPress website.](img/19e17f0b9e43b0189512e6db1d78e7c4.png)

A custom shortcode to add a search bar to your site



短代码的添加方式与任何常规文本添加到站点的方式相同。记得用括号[]括起来。

虽然您在编辑器中看不到搜索栏，但请查看页面预览，您会在网站的前端看到它:

![A preview of a page with a search bar that’s been added by shortcode.](img/1b2080bc7fdc3fac4659ede2f1f1ba5d.png)

Search bar added with shortcode



虽然这是一个快速编辑，对本文的目的来说是很好的，但是最佳实践建议永远不要编辑你的主题代码，而是创建一个 [WordPress 子主题](https://kinsta.com/blog/wordpress-child-theme/)。

### 关于 WordPress 搜索限制的说明

有很多选项可以用来给你的网站添加基本的 WordPress 搜索功能。但这就够了吗？

除非你有一个非常小的网站，或者你想把搜索限制在你的博客上，否则很可能不会。让我解释一下。

WordPress 的原生搜索表单在你的网页和博客文章中查找以下类型的内容:

*   页面标题
*   段落文本
*   图像标题
*   图像标题
*   图像替代文本
*   文件名

你可以想象，这对你的用户来说是难以置信的限制。首先，如果你需要从网站上的其他类型的页面或内容中检索结果(比如 [WooCommerce products](https://kinsta.com/blog/woocommerce-tutorial/#new-products) )，基本搜索表单不会为它们显示匹配的结果。网站的其他元素也是如此，比如:

*   小工具
*   [用户评论](https://kinsta.com/blog/wordpress-comment-plugins/)
*   [类别和标签](https://kinsta.com/knowledgebase/what-is-taxonomy/)
*   图像库标题、题注和替代文本
*   [自定义字段](https://kinsta.com/blog/wordpress-custom-post-types/#custom-fields)
*   更多

WordPress 搜索并不仅仅局限于显示的结果。它也受到尺寸的限制。你的网站越大，数据库处理结果的难度就越大，向访问者提供结果的时间也就越长。

那么，如果你需要比 WordPress 搜索允许的更强大和可持续的东西呢？

让我们看看你可以改进它的一些方法。


## 如何改善内部 WordPress 搜索体验

如果至少有一种情况适用于你，你应该阅读下一部分关于修复 WordPress 搜索的内容:

1.  你的网站上有超过一千页的内容或产品。
2.  你的数据表明，内部搜索很受欢迎，但它不会导致任何转化。
3.  你的搜索表单有很多动作，但是你的虚拟主机服务器很难处理这些请求(比如，加载结果需要几秒钟)。
4.  你想扩展你的网站，而不必担心搜索会在某个地方让你(和你的访问者)失望。
5.  基本搜索就是不行。你需要更先进和敏捷的东西来处理你的用户所做的各种搜索。

准备好开始了吗？以下是你可以做的 6 件重要的事情来改善 WordPress 搜索:

### 技巧 1:创建自定义搜索页面

与其给你的访问者留下一个简单的搜索栏来帮助他们浏览你的网站，为什么不创建一个自定义的搜索页面呢？

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

![A user searches for “denim” from the website menu.](img/e355a91dfdfc863f3ee51e959235f61c.png)

Exmple search for “denim” in website menu



这并不是说你的访问者不熟悉使用搜索，但是使用一个专门的搜索页面可以改善他们的体验。

要创建你的自定义页面，你需要通过 [FTP](https://kinsta.com/blog/best-ftp-clients/) 或文件管理器对你的网站进行后台访问。

一旦你进入了 [WordPress 数据库](https://kinsta.com/knowledgebase/wordpress-database/)，你将寻找下面的文件路径:

/WP-content/themes/[你的主题名]/page.php

page.php 是一个定义网页基本结构的文件。换句话说，它是一个页面模板。我们现在要做的是为您的搜索页面创建一个模板。



### 重要的

注意:如果你看到一个名为 search.php 的文件，不要管它。该文件规定了如何显示搜索结果页面，而不是初始搜索页面。



复制 page.php，并将新文件命名为 searchpage.php。然后，打开它进行编辑。

![Using cPanel, a copy of page.php is made and turned into a new file called searchpage.php.](img/9fab3adae63acbd826b270a206af1dfa.png)

Example of page.php code copied into new file



这个文件中的大部分代码需要替换，因为这里定义了一个典型的网页或博客帖子。相反，您需要将它剥离回来，以便它只包含您在搜索页面上需要的内容。下面是我如何构建搜索页面的一个例子:

```
<?php
/*
Template Name: Search Page
*/
?>
<?php
get_header(); ?>

<div class="wrap">
	<div id="primary" class="content-area">
		<main id="main" class="site-main" role="main">
<h1>Search Our Shop</h1>
<p>Welcome to the online shop of awesomeness! Here you will find all kinds of products to revolutionize how you work, live, and play.</p>
<p>Use the search form below to get yourself moving in the right direction.</p>

<?php get_search_form(); ?>

		</main><!-- #main -->
	</div><!-- #primary -->
</div><!-- .wrap -->

<?php get_footer(); ?>
```

WordPress Codex 提供了更多的指导，告诉你在创建一个定制搜索页面的时候可以做什么，不可以做什么。但是，如果您喜欢我将要向您展示的结果，您可能需要更改的唯一内容是出现在以下内容之间的内容:

```
<main id="main" class="site-main" role="main">
```

并且:

```
<?php get_search_form(); ?>
```

一旦你保存了你的 searchpage.php 模板，回到 WordPress。我们现在需要创建一个名为“搜索”的页面。

给页面起一个标题，打开边栏上的“页面属性”。您将看到刚刚创建的“搜索页面”的模板:

![Once a search page templates is created on your server, you can easily create a search page using it in WordPress.](img/72de26e71cf269189258ac35191a3adf.png)

Search Page template created



选择搜索模板并发布页面。现在，您将在实时 URL 上看到它，它应该是:https://yourdomainname.com/search/.，如果您使用类似于上面代码的内容，它将生成类似如下的页面:

![An example of what you can create when you build a custom search page using code and a template.](img/2dfedd814d5f0423c62a51480ded2ea9.png)

Example of a custom search page in WordPress



随着这个页面的创建和发布，你可以随心所欲地使用它。您可以将它添加到您的菜单或链接到其他地方。只要确保链接放在你的访问者容易看到的地方。


### 技巧 2:让你的 WordPress 搜索不仅仅局限于页面和帖子

虽然上面的提示给了你一个运行 WordPress 搜索的新地方，但是它并没有解决搜索什么样的内容的问题。幸运的是，有很多插件可以解决这个问题。

#### 用 WP 扩展搜索升级基本 WordPress 搜索

如果你想在你的网站上梳理更多的内容和元数据，一个好的选择是 [WP 扩展搜索](https://wordpress.org/plugins/wp-extended-search/)。

![WP Extended Search plugin enables WordPress site search to comb through more kinds of data.](img/d8b3fd50c737b09c954691ca558540b5.png)

WP Extended Search settings in WordPress



有了这个插件，你的访问者将能够从以下网站检索结果:

这是一个轻量级的、易于配置的插件，它改进了小型商业网站和博客的基本搜索能力。

#### 用高级 Woo 搜索升级 WooCommerce 搜索

如果你有一个[电子商务网站](https://kinsta.com/blog/ecommerce-strategies/)，你可以使用[高级 Woo 搜索插件](https://wordpress.org/plugins/advanced-woo-search/)来代替。

启用后，你可以把 WooCommerce 搜索表单放在网站上任何你想放的地方。如果你想用它来替换已经存在的所有基本 WordPress 搜索表单，插件有一个快速的“无缝集成”选项，可以自动为你替换它们。

您还可以手动将表单添加为小部件或短代码。这取决于你。

该表单将类似于基本的 WordPress 表单:

![An example of what the search form looks like when embedded with Advanced Woo Search plugin.](img/7cf868d1eb3f0daeb22c8d71711e9fc4.png)

Advanced Woo Search example



这个表格和你之前的表格有两个主要的不同。

第一个是表单搜索您的 WooCommerce 产品内容*和*元数据，包括标题、SKU、摘录、类别、标签和 ID。

这是第二个区别:

![The Advanced Woo Search plugin displays results in real time as visitors type their queries.](img/feffe0ced4ff9c2f0766de3d24dbb41c.png)

Advanced Woo Search: live search results



当你的访问者开始输入他们的搜索查询，匹配的结果就会出现。这就是所谓的“实时”搜索，由于[插件对 AJAX](https://kinsta.com/blog/admin-ajax-php/) 的使用，它可以瞬间完成。

如果这些选项看起来很有前景，但是你正在为你的 WordPress 搜索表单寻找更强大或者更快的升级，请继续阅读。

厌倦了 WordPress 的问题和缓慢的主机？我们提供世界一流的支持，由 WordPress 专家提供 24/7 服务和超快的服务器。[查看我们的计划](https://kinsta.com/plans/?in-article-cta)

### 技巧 3:改进 WordPress 搜索结果的显示方式

接下来，让我们来谈谈你能做些什么来改善搜索结果显示给访问者的方式。

以下是你不能忽略这条建议的原因:

![An example search results page for an ecommerce site shows a large product image.](img/3390cf0c18d59d63ef7af824606a6eed.png)

Default display of search results



默认情况下，WordPress 搜索显示类似于这个页面的结果。页面顶部会显示“搜索结果:[关键词]”，然后是每个匹配的页面或帖子。如果有特色图片(像上面的牛仔裤)，会完整显示。

接下来是一段摘录:

![An example search results page for an ecommerce site shows a large product image with excerpt.](img/8720ca1179c2a4501de8cadcdc50c84b.png)

Search results show large image and excerpt



这只是一个匹配结果。想象一下，如果只有几个“牛仔布”匹配项，浏览这个搜索结果页面会有多困难，更不用说几十个或几百个了。

为了解决这个问题，我们将寻找一个 WordPress 插件来帮助我们。

#### 使用象牙搜索改善表单的外观

像上面提到的插件一样， [Ivory Search](https://wordpress.org/plugins/add-search-to-menu/) 使您能够选择从哪些类型的内容和元数据中提取搜索结果。不过，有了这个，你就不必在基本页面和发布数据或电子商务之间做出选择。你可以在这里随意挑选:

![The Ivory Search plugin gives users more options for content and data to search through.](img/ef89fa652636716d70fbb3574fa9ce19.png)

Ivory Search settings



关于这个插件的另一个值得注意的提示是，它允许你定制你的搜索表单和你网站的其他部分:

![Ivory Search gives users the ability to design their search bar using their theme’s Customizer panel.](img/84d23c47d985f4970d1329b45cbc39f4.png)

Ivory Search: customize design in theme Customizer



您可以控制搜索表单的所有方面:

除此之外，您还可以配置像 live AJAX search 这样的东西，让您的访问者能够实时看到他们的匹配:

![An example of a custom-designed search bar made with Ivory Search and how it displays live results.](img/fb3b1aa712eff276bc9e3f55005daeac.png)

Live search results from custom search bar with Ivory Search



把这个插件看作是 WordPress 搜索的下一步。

#### 使用 Ajax 搜索定制搜索结果的显示方式

现在，不仅仅是你的搜索表单的外观会给你的访问者留下印象。你对结果展示所做的事情也会影响他们的体验。

有了 Ajax Search Lite 和 Pro 插件，你真的会为他们带来更智能、更快速的搜索体验。

以下是您可以做的一些示例:

![Ajax Search plugin users can refine how their search bar behaves when users interact with the website.](img/fa6dc882c055949bde0f632c1f09026f.png)

Ajax Search plugin: search behaviors



**行为**使访问者的搜索体验更加高效，比如当他们开始输入时立即打开搜索表单，无论他们点击回车键还是放大镜图标，都将他们重定向到搜索结果。

![Ajax Search plugin users can enhance search with autocomplete and keyword suggestions.](img/2e934da7728d0c03590152fe6b208360.png)

Ajax Search plugin: autocomplete and suggestions



自动完成&建议利用谷歌搜索功能来加快访问者的搜索速度。

![Ajax Search plugin users can enable keyword highlighting for an enhanced search experience.](img/fafb2214fec126848488b95e6fd053e3.png)

Ajax Search plugin: keyword highlighting



**关键词突出显示**是另一个有用的功能，可以在匹配结果中突出显示用户的关键词。这使得更容易发现更相关的结果。

下面是一个可能出现这种情况的例子:

![An example of a search form with keyword highlighting built by Ajax Search plugin.](img/6c65edf0e2675b56cc5d739fbddd6d6f.png)

Highlighted keywords in search results



这个插件还可以让你指定你的结果应该如何显示:结果页面应该如何布局，应该显示哪些元素(比如特色图片+摘录+作者姓名)。

另外，你可以告诉搜索引擎从某个地方拉图片。例如，如果某个特色图像不可用，您可以请求在搜索结果中使用页面上的第一个图像。

您还可以决定如何裁剪每张[图像](https://kinsta.com/blog/optimize-images-for-web/)以及裁剪的尺寸。这样，您可以使您的搜索结果页面在大小和外观上更易于管理——随着网站内容量的增长，这一点变得格外重要。

还有一点:这个插件不仅仅帮助你让你的搜索结果看起来更好。这也加快了他们出现在访客面前的速度:

![Ajax Search plugin users get the added benefit of built-in performance optimizations and, consequently, faster WordPress searches.](img/7ee74e99f5556698aeb48f19b9a0a31e.png)

Ajax Search plugin: performance optimizations for faster search



在这个插件中，您可以进行三种性能优化:

通过配置这三个设置，您可以帮助您的 web 服务器不被连续的搜索请求淹没。

也就是说，这只是优化 WordPress 搜索速度的冰山一角。继续阅读，了解更多关于 [Elasticsearch](https://kinsta.com/blog/wordpress-search/) 的信息。

### 技巧 4:加速 WordPress 搜索

虽然你的 WordPress 搜索表单的外观和搜索能力很重要，但是它发生的速度也同样重要。

#### 使用 Elasticsearch 获得超快速和复杂的搜索功能

从某种意义上来说，WordPress 搜索插件和你的 MySQL 数据库不再有用了。当你的网站的搜索查询量激增时，确保最佳搜索体验的唯一方法就是使用 Elasticsearch。

[Elasticsearch](https://www.elastic.co/what-is/elasticsearch) 是一个开源搜索和分析引擎，以其速度、稳定性和可扩展性而闻名——它只是 Elastic 堆栈的一部分。当与 Logstash(用于数据处理)和 Kibana(用于[数据可视化](https://kinsta.com/blog/data-visualization-tools/)和管理)结合使用时，Elasticsearch 以你从未见过的方式为你网站的[搜索引擎](https://kinsta.com/blog/submit-website-to-search-engines/)提供动力:

尽管 Elasticsearch 是开源的，可以免费使用，但你需要托管 Elasticsearch 主机(这不是免费的)。您可以通过多种方式获得此信息:

**1。ElasticPress 插件使你能够无缝地将 ElasticPress 搜索功能整合到你的 WordPress 站点中。这个插件是一个流行的解决方案，用来集成支持 Elasticsearch 的 WordPress 主机。**

![ElasticPress settings allow you to add or remove searchable fields and adjust their weight when displaying results.](img/f5e9065936151e485cb86b07e2015ef8.png)

ElasticPress settings



**2。弹性**
如果你想要，可以直奔主题来源:[弹性](https://www.elastic.co/)。您也有几个部署搜索引擎的选项。

您可以[获得完整的堆栈](https://www.elastic.co/products/elastic-stack),并利用其先进的数据处理和管理工具。这是设置和入职流程的一部分:

![Elastic simplifies your first Elasticsearch deployment.](img/a19b003deeb77c37498367131c138e59.png)

Elastic: full stack deployment configuration



此外，您可以控制如何优化您的 Elasticsearch 服务器:

![Elastic users get to choose how their Elasticsearch deployment gets optimized.](img/50779265fca9472e19108e187f941cca.png)

Choosing deployment optimization in Elastic



基于你的网站将要处理的查询类型提供建议，这使得决定如何最好地加速和增强你的[搜索引擎](https://kinsta.com/blog/submit-website-to-search-engines/)变得容易。

如果你想简化设置，可以使用 Elastic 的[网站搜索工具](https://www.elastic.co/products/site-search):

![A look inside the Elastic Site Search tool and dashboard.](img/707a66664d99409a7a2abc77347303ff.png)

Elastic Site Search dashboard



然后，您会被带到这个仪表板，在这里，一旦您的站点被编入索引，您就可以:

它不像 Elastic Stack 那样是一个健壮的解决方案，但如果您只是在寻找一个易于实现和管理的高性能搜索，这是一个很好的选择。

**3。亚马逊弹性搜索**
亚马逊拥有自己的[弹性搜索服务](https://aws.amazon.com/elasticsearch-service/)并不奇怪。如果你已经[使用 AWS 托管](https://kinsta.com/blog/google-cloud-vs-aws/)和部署服务，这将是一个很好的选择。

类似于上面的选项，它是一个托管服务，使您能够为您的站点创建一个具有复杂查询能力的快速搜索引擎。

### 技巧 5:缓存你的搜索结果页面

另一种优化 WordPress 搜索速度的方法是缓存你的搜索结果。通过启用缓存，您的服务器将不必一次又一次地不断处理相同的查询。相反，它将检索并显示一个静态的搜索结果页面，为访问者提供近乎即时的结果。

启用缓存的一种方式是使用一个 WordPress 缓存插件。

排名最高的插件之一， [W3 Total Cache](https://kinsta.com/blog/w3-total-cache/) ，引起了人们对搜索结果页面缓存的关注，所以如果你正在寻找一种能够优先考虑你所需要的性能优化的缓存解决方案，就从这里开始吧。

或者你可以试试 WP 火箭。尽管默认情况下它不会缓存搜索结果页面，但它为此创建了[缓存搜索结果助手插件](https://docs.wp-rocket.me/article/29-caching-the-search-page-result)。

另一种方法是使用前面提到的 Ajax Search Pro 插件。我已经向您展示了该插件的精简版优化搜索性能的几种方式。专业版增加了更多的优化，包括图像预缓存和搜索短语缓存。

### 技巧 6:在谷歌分析中激活搜索跟踪

最后但同样重要的是，记得在[谷歌分析](https://kinsta.com/blog/google-analytics-wordpress/)中激活搜索跟踪。你可以在管理>所有网站数据>视图设置下找到它。

![How to turn on search tracking for your WordPress site in Google Analytics.](img/39216adaba36ec302180a83034bdf887.png)

Activating search tracking in Google Analytics



要打开现场搜索跟踪，请将开关切换到“开”。这将显示一个名为“查询参数”的新字段。这是 URL(和数据库)中定义搜索查询和结果的元素。

![You’ll find the search parameter for your WordPress site in the URL of your search results page.](img/b65646d4d25190349a0d3f36c067f6be.png)

The search parameter for Google Analytics



在这种情况下，字母“s”定义了网站上的搜索查询。如果您不确定自己的搜索参数是什么，请运行测试搜索并找到问号后面的字母或单词。

如果您的搜索允许访问者选择类别和过滤器，您也可以启用站点搜索类别。您可能需要在这里指定多个参数。

一旦你在谷歌分析中设置好搜索，你就可以在行为>网站搜索中找到你的所有数据。

![Where to find your WordPress website search data in Google Analytics.](img/0e7b6dd3aeb2fff5a11e944bd36cbfea.png)

Site search data in Google Analytics



就像谷歌分析的其他部分一样，这些数据为您提供了大量的机会来弄清楚:

密切关注你的访问者在搜索中做了什么，你就可以更有效地为他们塑造其余的现场体验。

[Internal search is normally overlooked but it provides invaluable insights about your users. Learn how to improve and speed up the WordPress search functionality! 🚀🔍Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Fwordpress-search%2F&via=kinsta&text=Internal+search+is+normally+overlooked+but+it+provides+invaluable+insights+about+your+users.+Learn+how+to+improve+and+speed+up+the+WordPress+search+functionality%21+%F0%9F%9A%80%F0%9F%94%8D&hashtags=search%2Cwordpressagency)

## 摘要

WordPress 搜索可能看起来很简单——如果你需要的只是一个基本的搜索功能来帮助访问者浏览十几个页面的话。

你可以在网站的很多区域添加一个简单的 WordPress 搜索功能，比如标题、菜单、侧边栏、页脚，甚至是你的内容。您也可以通过多种方式添加这些搜索元素:

不要忘记:你的网站越大，你的导航变得越复杂，你就越需要一个解决方案来增强你的 WordPress 搜索能力，为你的访问者提供更好的 UX。一个更好的 UX，大多数时候，会增加你的转化率。

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。*