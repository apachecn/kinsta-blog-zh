# WordPress 代码真的很乱吗？

> 原文：<https://kinsta.com/blog/is-wordpress-code-really-a-mess/>

作者[说](http://www.sitepoint.com/first-look-themosis-framework-wordpress-developers/):

> 我不喜欢 WordPress 不是秘密。我看不起它混乱的代码库，建议任何有技术知识的人不要使用它。

情况有那么糟糕吗？WordPress 的核心代码真的如此糟糕，以至于你应该完全避开它，在你的项目中使用其他的东西吗？在这篇文章中，我将看看这个问题，并帮助它倒一些清晰度。

*   什么是糟糕的代码？
*   [编码员不重要](#coders-dont-matter)
*   [用户不关心](#users-dont-care)
*   [编码员不受影响](#coders-arent-affected)
*   有可能写出好的代码吗？

## 什么是糟糕的代码？

我认为根本的问题是没有人真正说出什么是糟糕和混乱的代码。在纸面上，类似“混乱的代码”听起来很可怕，但是一个不经意的读者知道这意味着什么吗？更重要的是，她/他在乎吗？

一如既往，事情远不止如此。有一些属性会使代码变得“糟糕”,下面是一些例子:

1.  与优化代码相比，未优化代码的执行速度较慢
2.  在项目中混合编码风格
3.  只有作者才能理解的代码
4.  不可扩展的，与他人相处不好的

WordPress 确实犯了其中的一个半错误。编码风格无处不在，这是肯定的。函数名不一致，一些模块使用严格的面向对象的方法，一些模块使用程序代码，许多文件不使用 WordPress 自己的风格指南，只是一些问题。

这意味着 WordPress 在某种程度上使用了意大利面条代码，但是除了令人讨厌之外，这不是一个问题，因为成千上万的人理解它，因为它是一个如此广泛使用的产品。

那么 WordPress 是不是编码很差？是的，就像国际空间站[使用劣质笔记本电脑](http://gizmodo.com/how-astronauts-use-laptops-on-the-international-space-s-1654962539)一样。这两种说法在客观上都是真实的，但在幕后还发生了更多的事情。

真正的问题是，这重要吗？

## 编码员不重要

在我去的每个 WordPress 夏令营，我都会被问到这样一个问题:如果 WordPress 转向完全面向对象的方法，会不会很棒？作为一个程序员，我说，是的，当然，这将是我一生中最快乐的一天。我这个理性的人(肯定不是程序员)宣扬要谨慎，因为这一举动会直接违背 WordPress 所代表的一切。

作为程序员，我们必须记住，归根结底，WordPress 是为用户服务的，而不是为我们服务的。你可能认为在一个项目上花费 100 多个小时是很多的，但是使用你的作品的人可能每天花 8 个小时来使用它，这相当于一年 3000 多个小时，而且这只是在你的作品被单个用户使用的情况下。

[As programmers we have to remember that WordPress at the end of the day is for the users.Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Fis-wordpress-code-really-a-mess%2F&via=kinsta&text=As+programmers+we+have+to+remember+that+WordPress+at+the+end+of+the+day+is+for+the+users.)

## 用户不在乎

用户真的不关心任何与代码相关的事情。他们想要用户友好、[快速安全](https://kinsta.com/blog/wordpress-security/)的东西。WordPress 在这三个方面都做得很好。你可以争辩说糟糕的编码插件[会破坏 WordPress 的速度](https://kinsta.com/blog/wordpress-performance-new-relic/)和安全性，但这就像说我的沃尔沃不安全，因为我以每小时 180 英里的速度撞到了墙上。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

## 编码器不受影响

绝大多数使用 WordPress 的人没有受到这个问题的影响，或者至少不必受到影响。在任何情况下，你都不需要接触项目的核心代码。这意味着你根本不会被核心代码的杂乱所影响。

编码人员反对 WordPress 的唯一理由是它没有遵循 MVC(模型-视图-控制器)架构。这是一个完全站得住脚的批评，但是 MVC 并不是编写干净代码的唯一方式。

事实上，你可以在插件中使用完全面向对象的方法，如果你愿意，甚至可以使用类似 MVC 的结构。真正的问题是主题的构建方式不能仅仅注入 MVC 原则。

也就是说，主题遵循严格的指导方针，结构良好，尽管不是 MVC。如果你知道自己在做什么，这可以归结为每个主题中的一个共同的脉络，使得和他们一起工作变得容易。

## 有可能写出好的代码吗？

问题不在于 WordPress 核心代码是好是坏。WordPress 核心代码有些乱，但仍然是好代码。这并不意味着它不能被极大地改进，但就目的而言，它确实很棒。

问题是:**有没有可能用 WordPress** 写出好的代码。答案是响亮的是。正如我前面提到的，[插件](https://kinsta.com/knowledgebase/wordpress-plugin/)是自由格式的，所以你可以在那里做任何你想做的事情，包括面向对象编程。

我也想强调 OOP 不是万能的。对于简单的插件，一个布局良好的过程化方法可能更清晰。

主题确实把表达和逻辑混在了一起，这无疑是一种不好的做法。然而，主题的指导方针已经被很好的安排好了，通过一些计划和组织，你**可以**写出一个符合逻辑并且容易理解的主题。

随着 [WordPress API](http://v2.wp-api.org/) 的出现，所有其他的批评都烟消云散了，因为你几乎可以在任何地方使用数据库中的数据。你可以使用 [Laravel](https://laravel.com/) 做任何事情，并通过 WordPress API 获取数据。

## 摘要

所以说到底，WordPress 的代码是不是一塌糊涂？是的，有些是。一些插件和主题确实包含不良代码，阻碍了整个社区的发展。像其他项目一样，WordPress 并不完美。就像任何其他项目一样，我同意 WordPress 不应该用于所有事情。

然而，因为“代码一团糟”而不使用 WordPress，说白了，是一个愚蠢而短视的理由。虽然核心代码有点混乱，但它是快速和安全的。在此基础上编写的任何扩展系统**的代码都可以**写得很好。

诀窍是[雇佣专业人士](https://kinsta.com/blog/hire-wordpress-developer/)，使用值得信赖的高质量产品，并妥善维护你的网站。在生活的哪个平台或其他领域不是这样呢？

[Not using WordPress because the code is a mess is a dumb and shortsighted reason.Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Fis-wordpress-code-really-a-mess%2F&via=kinsta&text=Not+using+WordPress+because+the+code+is+a+mess+is+a+dumb+and+shortsighted+reason.)

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。