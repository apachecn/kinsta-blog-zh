# 在 PHP 7 中不要做的 10 件事

> 原文：<https://kinsta.com/blog/10-things-not-to-do-in-php-7/>

我已经分享了 PHP 7 即将推出的一些[特性，在这篇文章中，我想我应该看看当我们切换到快如闪电的 PHP 7 时应该停止使用的一些不好的模式。别忘了看看我们新的](https://kinsta.com/blog/php-7-4/)[PHP 7.2](https://kinsta.com/blog/php-benchmarks/)最终版本的大型基准测试。

## PHP 7 最佳实践，也就是在 PHP 7 中不要做什么

1.  [不使用 mysql_ Functions](#mysql-functions)
2.  [不要写浪费的代码](#wasteful-code)
3.  [不要使用 PHP 关闭标签](#php-close-tags)
4.  [如果不需要，不要通过引用传递](#pass-by-reference)
5.  [不执行循环查询](#queries-in-a-loop)
6.  [不要在 SQL 查询中使用*](#sql-queries)
7.  [不信任用户输入](#trust-user-input)
8.  [不要逞强](#try-to-be-clever)
9.  [不要重新发明轮子](#reinvent-the-wheel)
10.  不要忽视其他语言

### 1.不要使用 mysql_ Functions

当你不仅仅被建议停止使用`mysql_`功能的时候终于到来了。PHP 7 将把它们从核心中完全移除，这意味着你需要转移到更好的`mysqli_`函数，或者更灵活的 PDO 实现。

### 2.不要写浪费的代码

这可能是一个显而易见的问题，但它将变得越来越重要，因为 PHP 7 中速度的提高可能会隐藏您的一些问题。不要满足于你的网站速度，仅仅因为切换到 PHP 7 使它更快。

要了解速度有多重要，以及你可以做些什么来让事情变得更好，看看我们的[初学者速度优化指南](https://kinsta.com/learn/page-speed/)文章。

作为开发人员，您应该始终确保只在需要的时候加载脚本，尽可能地连接它们，编写高效的数据库查询，[尽可能地使用缓存](https://kinsta.com/blog/wordpress-cache/)等等。

为了快速简单地提升整体优化，也可以考虑缩减代码。Kinsta 已经在 [MyKinsta 仪表板](https://kinsta.com/mykinsta/)中内置了一个[代码缩小功能](https://kinsta.com/help/kinsta-cdn-code-minification/)，允许客户通过简单的点击实现 CSS 和 JavaScript 的自动缩小。

### 3.不要在文件结尾使用 PHP 关闭标签

如果你看一下，当一个文件以 PHP 代码结尾时，大多数核心 WordPress 文件省略了结束 PHP 标签。事实上，Zend 框架明确禁止它。PHP 并不需要它，在文件末尾省略它可以确保不会添加尾随空格。

### 4.如果不需要，不要通过引用传递

我个人不喜欢通过引用。我知道在某些情况下它是有用的，但是在许多其他情况下它使代码更难理解和遵循，尤其是难以预测结果。

很明显，人们认为这能让他们的代码更快，但是根据可敬的 PHP 程序员的说法，这是不正确的。

引用不好的一个例子是内置在`shuffle()`或`sort()`中的 PHP。他们没有返回一个混洗或排序的数组，而是修改了原始数组，这在我看来完全不合逻辑。

### 5.不要在循环中执行查询

在循环中执行数据库查询是一种浪费。这给你的系统带来了不必要的压力，而且你可能在循环之外更快地达到同样的结果。当我遇到需要这样做的情况时，我通常可以用两个独立的查询来解决这个问题，我用这两个查询来构建一个数据数组。然后我在数组上循环，在这个过程中不需要执行查询。

由于 WordPress 的工作方式，可能会有一些例外。虽然`get_post_meta()`将从[数据库](https://kinsta.com/knowledgebase/wordpress-database/)中获取一个元值，但是如果你正在遍历一个特定帖子的元数据，你可以在一个循环中使用它。这是因为当你第一次使用它时，WordPress 实际上获取了所有的元数据并缓存起来。后续调用使用缓存的数据，而不是数据库调用。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

解决这些问题的最好方法是阅读函数文档，并使用类似于[查询监视器](https://kinsta.com/blog/query-monitor/)的工具。

### 6.不要在 SQL 查询中使用*

好吧，这更像是 MySQL 的问题，但是我们倾向于用 PHP 编写 SQL 代码，所以我说这是公平的游戏。在任何情况下，如果可以的话，不要在 SQL 查询中使用通配符，尤其是如果您有一个包含许多列的数据库。

指定您需要的确切列，并且只检索那些列。这有助于最小化您的资源使用，保护您的数据，并使事情尽可能清晰。

当谈到 SQL 时，尽可能了解可用的函数并测试速度。当计算平均值、总和或类似的数字时，使用 SQL 函数而不是 PHP 函数。如果你不确定一个查询的速度，测试它并尝试一些其他的变化——使用最好的一个。

### 7.不要相信用户输入

相信用户的输入是不明智的。总是过滤，消毒，逃逸，检查和使用后援。用户数据有三个问题:我们开发人员没有考虑到每一种可能性，它经常是不正确的，它可能是故意恶意的。

一个经过深思熟虑的系统可以抵御所有这些。在使用数据库时，确保使用像`filter_var()`这样的内置函数来检查正确的值和转义以及其他函数。

WordPress 有很多功能可以帮助你。查看[验证、逃逸和净化用户数据](https://codex.wordpress.org/Validating_Sanitizing_and_Escaping_User_Data)文章了解更多信息。

### 8.不要试图耍小聪明

你的目标应该是编写优雅的代码，最清楚地表达你的意图。通过将所有内容缩短为一个字母的变量，使用多级三进制逻辑和其他聪明的方法，你也许可以在每一页上节省额外的 0.01 秒，但这与你给自己和周围的人带来的麻烦相比，真的不算什么。

恰当地命名变量，记录代码，选择清晰而不是简洁。更好的是，使用标准化的面向对象代码，它或多或少地记录了自己，而不需要大量的行内注释。

### 9.不要重新发明轮子

PHP 已经存在了很长一段时间，而网站的创建时间甚至更长。无论你需要做什么，都有可能有人已经做过了。不要害怕依靠别人的支持， [Github](https://kinsta.com/knowledgebase/what-is-github/) 是你的朋友，[作曲家](https://getcomposer.org/)是你的朋友，[包装家](https://packagist.org/)是你的朋友。

从记录器到颜色操作工具，从分析器到单元测试框架，从 Mailchimp APIs 到 Twitter Bootstrap，只要按一下按钮(或输入一个命令)，一切都可用，使用它们吧！

### 10.不要忽视其他语言

如果你是一个 PHP 开发人员，现在标准的做法是至少了解 HTML、CSS、Javascript 和 MySQL。当你很好地掌握了这些语言，是时候再次学习 Javascript 了。 **Javascript 不是 jQuery** 。您应该适当地学习 Javascript，以便能够有效地利用它。

我还建议[学习所有关于面向对象 PHP 的知识，](https://kinsta.com/blog/php-tutorials/)它是一个救命稻草，会让你的代码好几个数量级。它也将为 C#和 Java 之类的语言打开大门，在你掌握了 OOP 之后，它们会更容易理解。

通过学习包管理器、构建脚本、Coffeescript、LESS、SASS、YAML、模板引擎和其他令人敬畏的工具来扩展你的知识。我强烈建议看看其他的 PHP 开发框架，尤其是 T2 的 Laravel T3。

当你在这些方面做得相当好的时候，那么 Ruby、Ruby on Rails、Android、iPhone、Windows Phone 的应用程序开发呢？你可能会认为这没有意义，因为这超出了你的舒适区和工作需要，但这就是问题所在。每种语言都有一些有用的东西可以教，多学一点知识不会有坏处。所有的顶级 PHP 开发人员都非常了解其他编程语言，这不是偶然的！

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。