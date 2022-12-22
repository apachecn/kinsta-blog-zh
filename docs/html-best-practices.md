# 构建可维护和可伸缩网站的 HTML 最佳实践

> 原文：<https://kinsta.com/blog/html-best-practices/>

HTML 最佳实践帮助开发者提供创新的、高度互动的网站和网络应用。这些最佳实践帮助您开发功能最丰富、以业务为中心的应用程序。此外，组织可以利用这些最佳实践来提供无缝的用户体验。

今天，当我们谈论 [HTML](https://kinsta.com/knowledgebase/what-is-html/) 时，我们通常会讨论 [HTML5(而不是它的前身)](https://kinsta.com/blog/html-vs-html5/)。HTML5 是一种强大的标记语言，允许 web 开发人员创建 web 文档。它易于使用和理解，几乎所有的浏览器都支持它。此外，它几乎是所有内容管理系统(CMS)的基础

作为一个经验很少的 web 开发人员，诸如“我怎样才能写出更好的 HTML？”经常出现。这篇文章旨在帮助你有一个良好的开端。

## 通用 HTML 编码方法

您可能已经掌握了这种标记语言，但这里有一些 HTML5 最佳实践，可以让您更好地编码。

### 始终声明一个 Doctype

当创建一个 HTML 文档时，`DOCTYPE`声明是通知[浏览器](https://kinsta.com/browser-market-share/)你正在使用什么标准所必需的。它的目的是正确地呈现您的标记。

例如:









| 版本 | 文档类型声明 |
| --- | --- |
| HTML 4.01 | `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">` |
| XHTML 1.1 | `<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">` |
| HTML5 | `<!DOCTYPE html>` |

`<DOCTYPE>`声明应该在 HTML 文档的第一行。以下是其正确和错误实现的比较:

| 最佳实践 | 不良做法 |
| --- | --- |
| 

```
<!DOCTYPE html>
<html>...</html>
```

 | 

```
<html>...</html>
```

 |

或者，您可以使用与您想要使用的 HTML/XHTML 版本相对应的 doctype。了解[推荐的 doctype 声明列表](https://www.w3.org/QA/2002/04/valid-dtd-list.html)，帮助您选择正确的声明。
T3】

### HTML 标签放置

开发人员知道标记的目的是帮助 web 浏览器区分 HTML 内容和普通内容。HTML 标签包含开始标签、内容和结束标签。然而，他们经常对标签的正确位置、需要结束标签的元素或者何时省略标签感到困惑。

例如，哪里是放置`<script>`标签的最佳位置？

脚本标签通常放在`<head>`元素中。但是现代 HTML 的最佳实践是将它们放在文档的底部，在关闭标签`<body>`之前，让[延迟它们的下载](https://kinsta.com/blog/defer-parsing-of-javascript/)。网页将首先加载文档对象模型(DOM)，显示给用户，然后请求脚本，[将时间减少到第一个字节(TTFB)](https://kinsta.com/blog/ttfb/) 。

浏览器从上到下逐行解释你的 HTML 文档。因此，当它读取文件头并遇到一个脚本标记时，它会向服务器发出请求以获取文件。这个过程本身没有什么问题，但是如果页面正在加载一个巨大的文件，这将花费很长时间，并极大地影响用户体验。

### 根元素

根元素下是`<lang>`，或*语言*，属性。这个属性有助于将 HTML 文档翻译成适当的语言。最佳实践是使该属性的值尽可能短。

例如，日语主要在日本使用。因此，当[以日语](https://kinsta.com/blog/wordpress-multilingual/#multilingual-advantages-1)为目标时，国家代码不是必需的。

| 最佳实践 | 不良做法 |
| --- | --- |
| `<html lang="ja">` | `<html lang="ja-JP">` |

### HTML 中的注意事项

最常见的 HTML 最佳实践之一是检查*该做的*和*不该做的*。以下是 HTML 编码中一些已知的*禁忌*:

| 描述 | 良好实践 | 不良做法 |
| --- | --- | --- |
| 在文本中，使用 Unicode 字符的等效 HTML 代码，而不是字符本身。 | `<p>Copyright © 2021 W3C<sup>®</sup></p>` | `<p>Copyright © 2021 W3C<sup>®</sup></p>` |
| 消除标签和属性值周围的空格。 | `<h1 class="title">HTML5 Best Practices</h1>` | `<h1 class=" title " > HTML5 Best Practices </h1>` |
| 练习一致性，避免混合字符大小写。 | `<a href="#status">Status</a>` | `<a HREF="#status">Status</a>` |
| 不要用两个或更多的空格分隔属性。 | `<input type="text" name="LastName">` | `<input type="text" name="LastName">` |

### 保持简单

像任何编码实践一样，“保持简单”原则非常适用于 HTML 和 HTML5。一般来说，HTML5 兼容较旧的 HTML 版本和 XHTML。因此，我们建议[避免使用 XML](https://kinsta.com/blog/your-sitemap-appears-to-be-an-html-page/#differences-between-html-and-xml-sitemaps) 声明或属性。

例如:

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!DOCTYPE html> 
```

除非您想编写一个 XHTML 文档，否则不需要这样声明代码。同样，您不需要 XML 属性，例如:

```
<p lang="en" xml:lang="en">...</p> 
```

## 考虑 SEO 的代码

开发者应该考虑 SEO 来编码。没有找到的 Web 内容也不会被编入索引。出于这个原因，这里有一些最好的 SEO 最佳实践供您考虑:

### 添加有意义的元数据

标签`<base>`是一个方便的标签，但是误用它可能会导致一些不直观的行为。因此，如果您声明了一个 base 标记，那么文档中的每个链接都将是相对的，除非明确指定:

```
<base href="http://www.kinsta.com/" />
```

这个语法改变了一些链接的默认行为。例如，链接到只有页面名称和扩展名的外部网页:

```
href="coding.org"
```

否则浏览器会将其解释为:

```
href="[http://www.kinsta.com/coding.org](http://www.example.com/example.org)"
```

这种解释会变得混乱，所以总是使用链接的绝对路径更安全。

另一方面，编写元标签描述严格来说并不是 HTML 最佳实践的一部分，但它仍然同样重要。属性是搜索引擎爬虫索引你的页面时所引用的，所以它对你的搜索引擎优化健康(T2)至关重要。

### 设置适当的标题标签

标签使得网页搜索引擎友好。首先，`<title>`标签中的文本出现在谷歌的搜索引擎结果页面(SERP)和用户的网页浏览器栏和标签中。

举个例子，当你搜索关键词“HTML5”时这个搜索结果中的标题表示具体的标题属性和作者。这在 [SEO 和站点流量生成](https://kinsta.com/blog/wordpress-seo/)中非常重要。

### 图像必须具有 Alt 属性

使用带有`<img>`元素的[有意义的 alt 属性](https://kinsta.com/blog/wordpress-seo/#10-add-alt-text-to-your-images)是编写有效的语义代码所必须的。

在下表中，不良实践列显示了一个没有 alt 属性的`<img>`元素。虽然同一列中的第二个示例有一个 alt 属性，但它的值没有意义。

| 良好实践 | 不良做法 |
| --- | --- |
| 

```
<img id="logo" src="images/kinsta_logo.png" alt="Kinsta logo" />
```

 | 

```
<img id="logo" src="images/kinsta_logo.png" />
<img id="logo" src="images/kinsta_logo.png" alt="kinsta_logo.png" />
```

 |

### 描述性元属性

[元描述](https://kinsta.com/blog/meta-description-wordpress/)是描述和总结网页内容的 HTML 元素。它的目的是让用户找到页面的上下文。尽管元数据不再对 SEO 排名有所帮助，但元描述在页面 SEO 中仍然扮演着重要的角色。

下面是一个示例代码，包括关键字、描述、作者姓名和字符集。字符集用于支持不同语言的几乎所有字符和符号。另一方面，您可以设置 cookies，添加修订日期，并允许页面刷新。

```
<!DOCTYPE html>
<html>
  <head>
    <title>HTML Best Practices in Website Design</title>
    <meta name = "keywords" content = "HTML, Website Design, HTML Best Practices" />
    <meta name = "description" content = "Learn about HTML best practices." />
    <meta name = "author" content = "John Doe" />
    <meta http-equiv = "Content-Type" content = "text/html; charset = UTF-8" />
  </head>
  <body>
    <p>Let's learn how to code HTML5!</p>
  </body>
</html>
```

### 带链接的标题属性

在锚元素中，最佳实践是使用标题属性来提高可访问性。title 属性增加了锚标记的含义。`<a>`标签(或者锚元素)和它的`href`属性[一起创建了一个到网页、电子邮件地址和文件的超链接](https://kinsta.com/blog/anchor-links/)。它用于链接同一页面内的位置或外部地址。

检查“不良实践”栏下的例子——它是多余的。如果用户使用屏幕阅读器来读取锚定标签并向收听者两次读取相同的文本，这种类型的实践是明显的。屏幕阅读器是为视力受损或有学习障碍的人提供的辅助技术。作为一种良好的做法，如果你只是重复主播的文字，那么最好不要使用标题。

| 良好实践 | 不良做法 |
| --- | --- |
| `<a href="http://kinsta.com/our-pricing" title="Learn about our products.">Click here</a>` | `<a href="http://kinsta.com/our-pricing" title="Click Here">Click here</a>` |

## 布局中的 HTML 最佳实践

网站开发不仅仅是创建一堆文本和标题，[链接页面](https://kinsta.com/blog/how-to-drive-traffic-to-your-website/#46-boost-authority-with-internal-links)，然后就大功告成了。有一些 HTML 方面的最佳实践可以考虑，以充分利用你的网站。

### 设置适当的文档结构

没有主要元素:`<html>`、`<head>`和`<body>`，HTML 文档仍然可以工作。但是，如果缺少这些元素，页面可能无法正确呈现。为此，始终如一地使用适当的文档结构非常重要。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

### 将相关部分分组

对于内容的[主题分组，使用 section 元素。根据 W3C 规范，一个`<section>`应该包含一个标题(H1、H2 等。).有些开发人员完全不使用 heading 元素，但是我们建议将它包含在内，以便更好地使用屏幕阅读器:](https://kinsta.com/blog/how-to-drive-traffic-to-your-website/#31-get-your-content-in-featured-snippets)

| 良好实践 | 不良做法 |
| --- | --- |
| 

```
<section>
<h1>HTML Best Practices 2021</h1>
<ul>
<li><img src="img1.jpg" alt="description"></li>
<li><img src="img2.jpg" alt="description"></li>
</ul>
</section>
```

 | 

```
<section>
<ul>
<li><img src="img1.jpg" alt="description"></li>
<li><img src="img2.jpg" alt="description"></li>
</ul>
</section>
```

 |

### 嵌入式内容最佳实践

标签用作外部资源的容器。这包括网页、图片、[视频](https://kinsta.com/blog/embed-youtube-video-wordpress/)或插件。但是，您必须考虑到大多数浏览器不再支持 Java 小程序和插件。更有甚者，任何浏览器都不再支持 ActiveX 控件，现代浏览器也关闭了对 Shockwave Flash 的支持。

我们建议如下:

*   对于图片，使用`<img>`标签。
*   对于从另一个站点获取的 HTML，使用`<iframe>`标签。
*   对于视频或音频，使用`<video>`和`<audio>`标签。

元素中的 alt 属性提供了对搜索引擎和屏幕阅读器有用的图像描述。当图像无法处理时，它对用户来说尤其方便:

| 良好实践 | 不良做法 |
| --- | --- |
| `<img alt="HTML Best Practices" src="/img/logo.png">` | `<img src="/img/logo.png">` |

如果有解释图像的补充文本，请将 alt 属性留空。这是为了避免冗余:

| 良好实践 | 不良做法 |
| --- | --- |
| `<img alt="" src="/img/icon/warning.png"> Warning` | `<img alt="Warning Sign" src="/img/icon/warning.png"> Warning` |

如果`<iframe>`元素的内容有一些限制，则将其留空。空的 iframe 元素总是安全的:

| 良好实践 | 不良做法 |
| --- | --- |
| 

```
<iframe src="/default.html"></iframe>
```

 | 

```
<iframe src="/default.html">
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit</p>
</iframe>
```

 |

开发人员应该为任何`<audio>`或`<video>`元素提供后备内容或备份链接，就像图像一样。回退内容是必需的，尤其是对于 HTML 中新引入的元素:

| 良好实践 | 不良做法 |
| --- | --- |
| 

```
<video>
<source src="/mov/theme.mp4" type="video/mp4">
<source src="/mov/theme.ogv" type="video/ogg">...<iframe src="//www.youtube.com/embed/..." allowfullscreen></iframe>
</video>
```

 | 

```
<video>
<source src="/mov/theme.mp4" type="video/mp4">
<source src="/mov/theme.ogv" type="video/ogg">...</video>
```

 |

### 减少元素的数量

HTML 文档变得复杂，尤其是对于有大量内容的网页。最好将页面上的元素数量减少到您能管理的最少数量。学习如何明智地使用标题元素，并遵循`<h1>`到`<h6>`元素如何表示 HTML 的内容层次结构。这使得你的内容对你的读者、屏幕阅读软件和搜索引擎更有意义。

示例:

```
<h1>The topmost heading</h1>
<h2>This is a subheading that follows the topmost heading.</h2>
<h3>This is a subheading that follows the h2 heading.</h3>
<h4>This is a subheading that follows the h3 heading.</h4>
<h5>This is a subheading that follows the h4 heading.</h5>
<h6>This is a subheading that follows the h5 heading.</h6>
```

对于 [WordPress 开发者](https://kinsta.com/blog/html-to-wordpress/)和内容创建者，使用`<h1>`元素作为博客文章的标题，而不是网站的名称。这有助于搜索引擎抓取，并且这种方法是 SEO 友好的。

此外，使用正确的 HTML 元素来传达它所包含的信息，以实现语义和有意义的内容结构。例如，用`<em>`来强调，用`<strong>`来加重语气，而不用它们的前辈`<i>`或`<b>`，后者现在已经被弃用。

厌倦了低于 1 级的 WordPress 托管支持而没有答案？试试我们世界一流的支持团队！[查看我们的计划](https://kinsta.com/plans/?in-article-cta)

示例:

```
<em>emphasized text</em>
<strong>strongly emphasized text</strong>
```

同样重要的是，对段落使用`<p>`，避免使用`<br />`在段落之间添加新的一行。相反，利用 CSS 边距和/或填充属性来更好地定位您的内容。有时，您可能会发现自己很想使用`<blockquote>`标签来缩进。避免这个陷阱——只在引用文本时使用它。

### 布局中的注意事项

HTML 的最佳实践之一是在页面布局中使用语义适当的元素。有几个元素可以帮助你组织你的布局。

由于 HTML 布局下的主题范围很广，最好在布局中快速突出该做和不该做的事情。例如，HTML 赋予了[页眉和页脚](https://kinsta.com/knowledgebase/add-code-wordpress-header-footer/)元素更多的语义含义，所以不要忽视`<header>`标签的使用，因为它用在任何给定的部分或文章中。除了控制`<title>`和`<meta>`标签以及文档的其他样式元素，它还用于标题、发布日期以及页面或部分的其他介绍性内容。类似地，你可以抛弃页脚只属于版权部分的概念——现在，你可以在任何地方使用它。

对于`<nav>`元素，您应该将其用于站点范围的导航。没有必要声明角色，因为标签中已经隐含了用法。

| 良好实践 | 不良做法 |
| --- | --- |
| `<nav></nav>` | `<nav role="navigation"></nav>` |

至于`<main>`元素，它已经是最新 HTML5 版本的一部分，表示文档主体的主要内容。因此，当我们的主要内容有了更具体的标签时，就不再需要使用`<div>`。

| 良好实践 | 不良做法 |
| --- | --- |
| `<main id="content"></main>` | `<div id="content"></div>` |

`<article>`用于内容块。它是一个独立的概念，不需要做进一步的解释，而标签`<section>`用于[将页面分成不同的主题区域](https://kinsta.com/learn/speed-up-wordpress/#limit-posts-on-your-blog-feed)或者分割一篇文章。不幸的是，许多开发人员仍然交替使用这两者。

考虑到`<section>`标签比`<article>`标签更通用。这意味着前者表示与当前主题相关的内容，但不一定是独立的。相反，后者是一个独立的属性。

但是当没有合适的标记时，你应该使用什么呢？答案是当其他元素都不起作用或者它是一个特定的风格元素时，使用`<div>`。出于我们的目的，使用`<div>`也是一种不好的做法。

让我们回到`<section>`标签，这是一个语义标记标签。它不是一种文体，强调它是很重要的。实际上，一个好的编码实践应该包括一个标题标签。

现在，关于`<section>`的禁忌是，你不应该用它来标记一个包装器、一个容器或者任何其他纯粹的风格块。下面是一个关于`<section>`标签的糟糕编码实践的例子:

```
<section id="wrapper">
  <section class="container-fluid">
    <div id="main">
    </div>
  </section>
</section>
```

这里有一个更好的方法，但是它过度使用了`<div>`标签:

```
<div id="wrapper">
  <div class="container-fluid">
    <div id="main">
    </div>
  </div>
</div>
```

因此，更好的编码实践是:

```
<body id="wrapper">
  <div class="container-fluid">
    <main id="main">
    </main>
  </div>
</body>
```

许多布局的一个流行部分是用于数据表示的图形，而``元素大多与图片一起使用。然而，它可能有更广泛的用途，因为任何与文档相关的东西都可以放在任何地方，并包装在一个``元素中。一些例子包括书中的插图、[表格](https://kinsta.com/blog/wordpress-table-plugins/)或图表。

``的一个有趣的特点是它并不构成文档的轮廓。因此，您可以使用它来对具有共同主题的元素进行分组——例如，具有一个共同``的几个图像，或者甚至是一个代码块。

在用``分组元素时，使用``。``标题应该紧接在开始``标签之后，或者紧接在结束``标签之前:

```

  <img src="image1.jpg" alt="Bird Image">
  <img src="image2.jpg" alt="Tree Image">
  <img src="image3.jpg" alt="Sun Image">
  Three images related to a topic

```

## 脚本中的 HTML 最佳实践

HTML 是 web 开发的核心技术之一。它拥有强大的功能和特性，深受开发者和企业主的欢迎。前端开发不断创新，为了跟上它，开发人员应该知道 HTML [脚本](https://kinsta.com/blog/scripting-languages/)的最佳实践。

### 使用外部样式表

内联样式会让你的代码变得混乱和不可读。为此，请始终链接并使用外部样式表。此外，避免在 CSS 文件中使用 import 语句，因为它们会产生额外的服务器请求。

内联 CSS 和 JavaScript 也是如此。除了可读性问题之外，这将使您的文档更重，更难维护，这样您就可以避免内联代码。

### 使用小写标记

在代码中使用小写字符是行业标准惯例。虽然使用大写或其他文本大小写仍然会呈现您的页面，但问题不是标准化，而是代码可读性。

代码可读性是编码的一个重要方面，因为它有助于应用程序的可维护性和安全性。不仅如此，web 开发主要由团队组成。让您的代码可读性更强，可以让您和您的团队的工作不那么复杂。

| 良好实践 | 不良做法 |
| --- | --- |
| 

```
<div id="test">
<img src="images/sample.jpg" alt="sample" />
<a href="#" title="test">test</a>
<p>some sample text </p>
</div>
```

 | 

```
<DIV>
<IMG SRC="images/sample.jpg" alt="sample"/>
<A HREF="#" TITLE="TEST">test</A>
<P>some sample text</P>
</DIV>
```

 |

### 脚本中的注意事项

虽然在编写 HTML 代码时有许多禁忌，但我们将分享脚本中的两个基本禁忌:

*   编写良好缩进和一致格式的代码:干净和良好编写的代码可以提高你的网站的可读性，这对你的开发者和其他可能使用网站的人来说是一个巨大的帮助。这也显示了很强的专业精神和对细节的关注，很好地反映了你作为开发者的态度。
*   避免包含过多的注释:注释是必不可少的，可以让你的代码更容易理解。然而，HTML 的语法是不言自明的，所以注释是不必要的，除非你必须阐明语义和命名约定。

## 验证和缩小

验证和[缩小](https://kinsta.com/blog/critical-rendering-path/)代码用于在早期识别错误。不要等到你完成了你的 HTML 文档，要养成经常验证和识别错误的习惯。您可以手动进行验证，也可以使用任何已知的验证工具，比如 W3C 标记验证器。

您还可以利用 [MyKinsta 仪表板](https://kinsta.com/mykinsta/)中内置的[代码缩小功能](https://kinsta.com/help/kinsta-cdn-code-minification)。这使得客户只需简单的点击就可以实现 CSS 和 JavaScript 的自动缩小，这将加速他们的网站，而不需要手动操作。

同时，通过删除任何不必要的东西来练习缩小，比如注释或空白。确保您编写的代码简洁明了，以减小 HTML 文件的大小。可以使用 HTML Minifier 等工具。

## 摘要

许多 2021 年 HTML5 最佳实践资源可在线获得，以帮助您。然而，记住编码的一般规则:一致性。本文提供了基本的见解，并帮助您开始前端开发之旅。使用这个指南，你很快就会成为语义正确的 HTML5 专家。

当你准备好了，看看 HTML 能提供什么，探索一些开源 HTML 框架来构建现代的单页 web 应用程序。它们在数据和用户界面之间提供了极好的同步，并且可以与 CSS 和 JavaScript 无缝协作。

我们是否错过了您在自己的编码中使用的 HTML 最佳实践？请在评论区告诉我们！

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。