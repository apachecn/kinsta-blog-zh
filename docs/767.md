# RIP WordPress 和 HHVM——我们已经运行良好

> 原文：<https://kinsta.com/blog/hhvm-wordpress/>

撕裂 HHVM。当谈到给你的 WordPress 网站供电时，是时候告别 HHVM 了。我们不再支持或提供 HHVM 在金斯塔。它从未得到官方支持，WordPress 的团队一年前就停止了测试。 [HHVM v3.30](https://hhvm.com/blog/2018/09/12/end-of-php-support-future-of-hack.html) 也将是最后一个支持 PHP 的发布系列。

由于越来越多的兼容性问题、性能下降以及不再有 PHP 支持，它不再是生产 WordPress 站点的可行选择。因此，我们**已于 2018 年 8 月 20 日对所有客户**淘汰 HHVM。

如果您目前在您的网站上使用 HHVM，请查看下面关于这一变化如何影响您以及您需要做什么的更多详细信息。我们还讨论了为什么**这不是一个负面的变化**。

*   [HHVM 背景](#background-hhvm)
*   HHVM 不再是 WordPress 的一个选择
*   [HHVM 生命周期结束](#hhvm-eol)
*   [从 HHVM 迁移到 PHP](#hhvm-to-php)

## HHVM 的背景

在我们深入探讨为什么 HHVM 要离开之前，让我们先快速看一下为什么金斯塔开始提供它。

这一切都始于一个叫做脸书的小(或者曾经是小)网站。😉它最初是用 PHP 编写的，当网站开始起飞时，为所有请求提供服务所需的计算能力已经超出了图表。这主要是由于当时可用的 PHP 执行引擎效率低下。所以脸书的工程师和开发人员想出了一个绝妙的主意。与其简单地购买更多的服务器，为什么不在软件层面解决问题呢？

所以他们创建了一个名为 [HPHPc](https://en.wikipedia.org/wiki/HipHop_for_PHP) 的 PHP 转 C++编译器。最初的 PHP 代码被编译成可执行的二进制文件(有时文件大小会达到千兆字节！)并且它是运行的，而不是被编译成操作码并被解释。

这导致了大约六倍的性能，这是巨大的！六倍的速度听起来可能不算多，但是如果你从下面的角度来看，这可能有助于正确看待它。你只需要 100 台服务器，而不是购买 600 台服务器来支持一项网络服务。这是相当难以置信的节省，仅仅是因为您简单地改变了运行代码的方式。

然而，正如您可以想象的那样，运行和维护 HipHop 的独立开发人员和调试器版本(分别称为 HPHPi 和 HPHPd)，加上在代码发生几次变化后将数千兆字节的可执行文件分发到每台机器(想想错误修复)，很快就变得令人厌倦和具有挑战性。





> Kinsta 把我宠坏了，所以我现在要求每个供应商都提供这样的服务。我们还试图通过我们的 SaaS 工具支持达到这一水平。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![](img/60f15faa5735bd2437bf9dada5ee9192.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Suganthan Mohanadasan from @Suganthanmn</cite></footer>

[View plans](https://kinsta.com/plans/)

因此在 2013 年，脸书决定弃用 *HPHPc，*但是回收他们在生产中至少三年的代码和经验，并推出 **HipHop 虚拟机(HHVM)** 。这个引擎将 PHP 转换成*字节码*，然后在运行时由*实时(JIT)编译器*转换成*64 位机器码*。这进而导致了更大的性能提升！🚀

![HHVM logo](img/91125ce5aa0b61a3ae71f4f0066db433.png)

HHVM



Kinsta 的许多高要求、高流量的站点多年来一直在使用 HHVM，并且在加载时间上有了惊人的减少。HHVM 还启用了[对象缓存](https://codex.wordpress.org/Class_Reference/WP_Object_Cache)，这是一个由 WordPress 引入的内部缓存系统，用于将数据库中的数据存储在 [PHP 内存](https://kinsta.com/knowledgebase/php-memory-limit/)中。这通过减少数据库调用次数和加快 PHP 执行时间来提高数据库效率。这意味着 HHVM 对于那些有很多不可缓存内容的动态网站来说一直很棒。

但不幸的是，尽管如此，HHVM 在 WordPress 和 PHP 方面已经走到了尽头。我们将在下面深入探讨原因。

## HHVM 不再是 WordPress 的选择

HHVM 不再是 WordPress 或 Kinsta 客户端的合适技术，这只是其中的几个原因。

首先，从 3.30 版本开始，HHVM 已经完全终止了对 PHP 的支持

其次，值得注意的是，HHVM 实际上从未得到 WordPress 的官方支持。多亏了一些痴迷于速度的 WordPress 核心团队成员( [#27881](https://core.trac.wordpress.org/ticket/27881) )。一些 WordPress 主机提供商，如 Kinsta，随后向客户提供了这一功能([我们在 2016 年推出了它](https://kinsta.com/feature-updates/hhvm-environment-switching-available/))，以利用额外的性能收益。

实际上，WordPress】在 2017 年 5 月(一年多前)已经停止将 HHVM 作为其核心测试基础设施的一部分。以下是 WordPress 核心开发者 John Blackbourn 对此的评论:

> 如果你在 HHVM 上运行一个 WordPress 网站，你应该考虑转换到 PHP 7+,它得到了更广泛的支持和测试，并提供了 HHVM 所推动的所有内存和性能优势。

由于 HHVM 不再被 WordPress 核心团队成员测试，错误和兼容性问题已经开始出现。其中很多我们都亲眼目睹了( [#8194](https://github.com/facebook/hhvm/issues/8194) )。近一年前开始的零星故障，随着 HHVM 的最新版本，已经变成了源源不断的故障，它们现在正在影响流行的第三方 WordPress 插件和主题的功能。因此， **HHVM 不再是一个稳定的**或适合 WordPress 网站的解决方案。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

除了对 HHVM 主机的支持，我们的 PHP vs HHVM 基准测试表明 **PHP 7.2 实际上比 HHVM** 运行得更快。有史以来第一次，PHP 在所有的测试中都获得了冠军；其中包括一个独立的 WordPress 网站、WooCommerce 和简单的数字下载。🏆

![WordPress benchmarks (PHP vs HHVM)](img/a4f51151f803d63f6f6cb755c2427d4f.png "WordPress benchmarks (PHP vs HHVM)")

WordPress benchmarks (PHP vs HHVM)



而 **PHP 7.3 和 7.4 更快**。查看我们深入的 [PHP 基准测试结果](https://kinsta.com/blog/php-benchmarks/)。

![WordPress 5.0 PHP benchmarks](img/aa3e50c1190462560cd448720e536908.png)

WordPress 5.0 PHP benchmarks



因此，我们建议使用 PHP 7.4 来获得最佳性能。我们目前在 MyKinsta 仪表板中提供了 PHP [7.2](https://kinsta.com/blog/php-7-2/) 、 [7.3](https://kinsta.com/blog/php-7-3/) 和 [7.4](https://kinsta.com/blog/php-7-4/) 。只需轻轻一点，你就可以轻松地在 PHP 引擎之间切换。

**更新:** [PHP 8.1(正式发布)](https://kinsta.com/feature-updates/php-8-1/) 现已对所有 Kinsta 客户端开放。Kinsta 不再支持 PHP 7.4。请注意，我们支持 PHP 版本 8.0，8.1。

![Active PHP support](img/4ca9c1f5d406eeff04bee20ae3502de2.png)

Active PHP support



您可以直接从 MyKinsta 仪表板切换到我们在 Kinsta 支持的更新的 PHP 版本。

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

![MyKinsta PHP version switching](img/d025c926f88d2e3845e118f4b952d097.png)

Easily switch PHP versions in MyKinsta



## HHVM 寿命终止(EOL)

以下是我们逐步撤出 HHVM 的所有细节和最后期限。

*   自 2018 年 6 月 15 日起，MyKinsta 仪表板不再提供切换至 HHVM 服务。**重要提示:** **如果你在这个日期之后搬离 HHVM，你就不能再搬回来。**
*   2018 年 8 月 20 日，HHVM 被彻底淘汰。这意味着所有的 HHVM 站点都切换到了 PHP 5.6+，HHVM 也完全从 MyKinsta 仪表盘中移除了。

## 从 HHVM 转向 PHP

Kinsta 定期升级服务器端软件以保持最新，这不仅是为了最基本的安全原因，也是为了性能。

和任何软件一样，PHP 有一个发布生命周期，它必须遵守这个生命周期，以便不断推动事情向前发展并做出改进。PHP 的每个主要版本通常在发布后的两年内得到全面支持。在此期间，漏洞和安全问题会定期得到修复和修补。

![Supported PHP Versions for WordPress](img/9fc2e51e31b71fdad45f32eae2cd6743.png)

Supported PHP Versions for WordPress



正如你在上面看到的，PHP 5.6 和 7.0 已经过时了，7.2 将在 2020 年底以类似的方式被淘汰。这就是为什么我们强烈建议尽快迁移到更高版本的 PHP，最好是 PHP 7.3 或 7.4。

为了帮助过渡，我们整理了一个教程，教你如何[测试并正确地将你的网站从 HHVM 迁移到 PHP](https://kinsta.com/knowledgebase/how-to-update-php-in-wordpress/) 。记住，一些插件或主题可能与 PHP 的新版本有兼容性问题，所以你应该遵循我们列出的步骤，以确保平稳过渡而不停机。这也是我们提醒每个人的另一个原因！在截止日期前参加**考试。**

## 摘要

WordPress 在 HHVM 运行良好，对你们中的许多人来说，它提供了极快的速度！但是不要担心，你应该在 PHP 7.4 上看到更快的速度。从长远来看，我们对这种变化感到兴奋。首先，这意味着在你的网站应该使用哪一个 PHP 引擎的问题上不再有困惑。这也意味着在 WordPress 平台上提高核心 PHP 语言的性能将花费更多的时间。

如果您对我们逐步淘汰 HHVM 有任何想法或担忧，请随时联系我们的 24/7 支持团队。我们也很乐意听到你关于转换到 PHP 的反馈。

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。