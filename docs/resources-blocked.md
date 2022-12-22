# 如何修复“由于资源被阻止，页面可能无法正常呈现”错误

> 原文：<https://kinsta.com/blog/resources-blocked/>

Kinsta 的团队在 24/7 的基础上与 WordPress 一起工作，看到了客户经历的各种不同的错误和警告。相信我们，我们几乎都看过了。每当我们的系统中不断出现错误时，我们一定会记录下来，以便与您分享解决方案。一个不能帮助你解决自己问题的高级主机有什么好处呢？今天我们将深入探讨一个你可能遇到过也可能没有遇到过的谷歌搜索控制台错误:“由于 robots.txt 阻止了资源，页面可能无法正常呈现。”

别担心，我们会解释这意味着什么，以及如何在你的 WordPress 站点上修复它。

## 被阻止的资源

如果你得到一个关于被阻止资源的警告或错误，这通常意味着你的 WordPress 站点上的某些东西没有被正确配置。情况并不总是这样，但是如果你在谷歌搜索控制台看到一条关于任何事情的消息，你应该调查一下。谷歌提供这些信息是有原因的。我们最近经历的[对谷歌的无理处罚](https://kinsta.com/blog/decline-seo-rankings/)肯定证明了这一点。

如果你没有收到关于被阻止资源的消息，你可以登录谷歌搜索控制台来检查你的网站。然后点击谷歌索引→屏蔽资源。正如他们所说:

> Googlebot 需要访问您页面上的许多资源，以便以最佳方式呈现和索引页面。例如，JavaScript、 [CSS](https://kinsta.com/blog/wordpress-css/) 和[图像文件](https://kinsta.com/blog/image-file-types/)应该对 Googlebot 可用，以便它可以像普通用户一样查看页面。
> 
> 这些来自这个主机的资源被你的网站使用，但是被 Googlebot 屏蔽了。如果 Googlebot 不能访问你页面上的重要资源，**页面可能被错误地索引**。(来源:[受阻资源报告](https://support.google.com/webmasters/answer/6153277))

同样，仅仅因为一个资源被屏蔽并不总是意味着它损害了你网站的搜索引擎优化。但是最好的做法是清理这些错误，这样当那些影响你的搜索引擎优化的错误出现时，你可以更容易地修复它们，而不必过滤页面上的错误。

我们喜欢与您分享实时数据。因此，在今天的例子中，我们有一个问题，在我们自己的网站上发生了多个(400 多个)被阻止的资源错误(如下所示)。

![Pages with blocked resources on this host](img/2e6676b0c5d3440fd76f66e9696d0cb1.png "Pages with blocked resources on this host")

Pages with blocked resources on this host



当您在“阻止的资源”部分看到错误时，您可以单击它们以了解更多详细信息。所以我们点击`https://kinsta.com/wp-admin/admin-ajax.php`。`admin-ajax.php`文件只是可能出现在这里的一个例子。您可能还会看到关于 [JavaScript 或 CSS 文件被阻止的错误](https://www.seroundtable.com/google-warning-googlebot-css-js-20665.html)。但是修复它们通常涉及相同的步骤。









在页面上，我们看到以下错误:“由于资源被`https://kinsta.com/robots.txt`阻止，页面可能无法正常呈现。”

他们给出的建议是更新`robots.txt`规则来解锁资源。如果你以前从未听说过这个文件，我们建议你首先阅读我们在 WordPress 中的 [robots.txt 文件。](https://kinsta.com/blog/wordpress-robots-txt/)

![The page many not render properly due resources blocked by robots.txt](img/c539091096ffd892edd0212cea4afb9b.png)

The page may not render properly due resources blocked by robots.txt



你可以使用[谷歌抓取工具](https://www.google.com/webmasters/tools/googlebot-fetch)来查看谷歌看到的页面。这可以帮助您确定被阻止的资源是否影响了页面的外观。同样，如果可能的话，我们只是建议清除这里报告的所有错误。

我们可以看到它抱怨的资源是`https://kinsta.com/wp-admin/admin-ajax.php?action=essb_counts&...`,在我们的例子中，AJAX 正在被我们的 WordPress 社交媒体插件使用。如果我们把它输入到[机器人测试工具](https://www.google.com/webmasters/tools/robots-testing-tool)中，我们可以看到谷歌确实找不到它。这是因为`/wp-admin/`目录实际上被阻塞了，我们将在下面深入探讨。

![Robots.txt tester](img/7a01f374d43cd7e5beca22fde3a8d0a7.png)

Robots.txt tester



Yoast SEO 在一篇包含他们的[示例 robots.txt 文件](https://yoast.com/wordpress-robots-txt-example/)的博客文章中提到了这个“被阻止的资源”问题。基本上，AJAX ( `admin-ajax.php`)被一些 WordPress 主题和插件用来向页面添加内容或执行某种功能。WordPress 实际上在默认情况下会屏蔽这个问题，但是在 WordPress 4.4 中已经被修复了( [#33156](https://core.trac.wordpress.org/ticket/33156) )。谷歌现在可以在 wp-admin 中抓取`admin-ajax.php`。

但是你们中有多少人在 4.4 版本发布之前就已经在运行你的 WordPress 网站了呢？可能你们中 99%的人。和我们一样，您可能有一个定制的`robots.txt`文件，这个文件被您或开发人员修改过，覆盖了新的默认设置。这意味着警告仍然会出现在谷歌搜索控制台中，除非你修复它们。答案就是简单地**更新你的 robots.txt 文件**。

## 更新 Robots.txt 文件

WordPress 默认创建一个虚拟的`robots.txt`文件。然而，我们总是建议创建一个物理的。不确定你是否已经有了？尝试浏览到你的 WordPress 站点的根目录:`https://domain.com/robots.txt`。如果有，你会看到的。否则，您将得到一个 404 错误。

我们在 Kinsta 是 Yoast SEO 的忠实粉丝，我们在我们的网站上使用它，它是我们推荐给你的 WordPress 网站的第一个 SEO 插件。许多人不知道你可以使用它在你的 WordPress 仪表盘上轻松地创建和编辑你的`robots.txt`。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

点击 SEO →工具。然后点击“文件编辑器”如果您禁用了[文件编辑](https://codex.wordpress.org/Hardening_WordPress#Disable_File_Editing)，这将不会出现。如果你想保持禁用，你可以通过 [SFTP](https://kinsta.com/knowledgebase/how-to-use-sftp/) 创建/编辑你的`robots.txt`文件。

![Yoast SEO file editor](img/ff063dad50a368fcd7875156179bb3ac.png)

Yoast SEO file editor



如果你没有实体文件，你可以点击“创建`robots.txt`文件”这将在您的服务器上创建一个物理文件。

![Create robots.txt file](img/d9e65acc9dfc28cbe702f74a8f8014b0.png)

Create robots.txt file



如果您已经有了一个`robots.txt`文件，它可能看起来像这样(或者它可能真的很长！我们看过一些疯狂的 robots.txt 文件):

```
User-agent: *
Disallow: /wp-admin/
```

我们需要添加另一行来修复阻塞资源错误。因此，在我们的例子中，我们添加了下面一行(这是现在默认的`robots.txt`配置，当您在全新安装时使用 Yoast 和 WordPress 创建文件):

```
User-agent: *
Disallow: /wp-admin/
Allow: /wp-admin/admin-ajax.php
```

这使得谷歌现在可以抓取它。

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

![Allow: /wp-admin/admin-ajax.php in robots.txt](img/afc1b507962b8d7ddee5ead3f9f80573.png)

Allow: /wp-admin/admin-ajax.php in robots.txt



关于`admin-ajax.php`文件本身，您不必担心它会意外出现在 Google 或索引中，因为如果您查看该文件，它实际上包含以下 noindex 头。

```
@header( 'X-Robots-Tag: noindex' );
```

这个标签告诉 Google 不要索引它。

![noindex admin-ajax.php](img/406b0c3f1502080c63a372b0d0469509.png)

noindex admin-ajax.php



如果您看到其他类型的资源阻塞错误，如 JavaScript 或 CSS，修复它们的快速方法是恢复到上面的标准`robots.txt`配置。`wp-content/plugins/`和`/wp-includes/`是我们见过的用户误屏蔽的常见目录，这有时会导致这类问题。

[Don't be too aggressive with your robots.txt file. You might find yourself with blocked resources errors. 😨Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fbit.ly%2F3iyNwgv&via=kinsta&text=Don%27t+be+too+aggressive+with+your+robots.txt+file.+You+might+find+yourself+with+blocked+resources+errors.+%F0%9F%98%A8&hashtags=WordPress%2Cwebdev)

你可以在下面看到，在允许上述文件进入我们的`robots.txt`文件后，我们被阻止的资源错误在几天内就在谷歌搜索控制台中得到解决。

![Fixing blocked resources on WordPress site](img/2ebd7f977b738696df4455c20f983158.png)

Fixing blocked resources on WordPress site



## 摘要

修复谷歌搜索控制台中的错误和警告是正确维护你的 WordPress 站点的重要部分。这有助于确保谷歌看到你的网站正确和索引。希望下次遇到阻塞资源错误时，您会知道如何更好地解决问题！

对被封锁的资源有什么想法吗？你在自己的网站上见过这个吗？

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。