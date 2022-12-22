# WordPress Robots.txt 指南:它是什么以及如何使用它

> 原文：<https://kinsta.com/blog/wordpress-robots-txt/>

听说过 robots.txt 这个术语，想知道它是如何应用到你的网站上的吗？大多数网站都有 robots.txt 文件，但这并不意味着大多数网站所有者都理解它。在这篇文章中，我们希望通过深入研究 WordPress robots.txt 文件，以及它如何控制和限制对你的网站的访问来改变这种情况。

 有很多内容要介绍，所以让我们开始吧！

## 什么是 WordPress robots.txt 文件？

在我们讨论 WordPress robots.txt 文件之前，定义一下“机器人”在这里是什么很重要。机器人是访问互联网网站的任何类型的“机器人”。最常见的例子是搜索引擎爬虫。这些机器人在网络上“爬行”,帮助像谷歌这样的搜索引擎对互联网上的数十亿网页进行索引和排序。

因此，总体而言，机器人对互联网来说是一件好事，或者至少是一件必需品。但这并不一定意味着你或其他网站所有者希望机器人不受约束地运行。控制网络机器人如何与网站互动的愿望导致了 20 世纪 90 年代中期**机器人排除标准**的产生。Robots.txt 是该标准的实际实现——**，它允许你控制参与的机器人如何与你的网站互动**。您可以完全阻止机器人，限制它们访问您站点的某些区域，等等。

不过，“参与”部分很重要。Robots.txt 不能*强迫*一个机器人遵循它的指令。恶意的僵尸程序可以并且将会忽略 robots.txt 文件。此外，即使是声誉良好的组织也会忽略*你可以放入 robots.txt 的一些*命令。例如，[谷歌会忽略你添加到 robots.txt 的任何规则](https://developers.google.com/search/blog/2019/07/a-note-on-unsupported-rules-in-robotstxt#:~:text=In%20particular%2C%20we%20focused%20on%20rules%20unsupported%20by%20the%20internet%20draft%2C%20such%20as%20crawl%2Ddelay%2C%20nofollow%2C%20and%20noindex)关于爬虫访问的频率。您可以在 Google 搜索控制台中您酒店的[抓取速率设置](https://www.google.com/webmasters/tools/settings)页面中调整 Google 抓取您网站的速率。

如果你有很多关于机器人的问题，像 [Cloudflare](https://kinsta.com/topic/cloudflare/) 或 [Sucuri](https://sucuri.net/) 这样的安全解决方案可以派上用场。

### 如何找到 robots.txt？

robots.txt 文件位于您网站的根目录中，因此在您的域后添加/robots.txt 应该会加载该文件(如果您有一个的话)。比如 https://kinsta.com**/robots . txt**。





> Kinsta 把我宠坏了，所以我现在要求每个供应商都提供这样的服务。我们还试图通过我们的 SaaS 工具支持达到这一水平。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![](img/60f15faa5735bd2437bf9dada5ee9192.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Suganthan Mohanadasan from @Suganthanmn</cite></footer>

[View plans](https://kinsta.com/plans/)

### 什么时候应该使用 robots.txt 文件？

对于大多数网站所有者来说，一个结构良好的 robots.txt 文件的好处可以归结为两类:

*   优化搜索引擎的抓取资源，告诉他们不要在你不想被索引的页面上浪费时间。这有助于确保搜索引擎专注于抓取您最关心的页面。
*   通过阻止浪费资源的机器人优化您的服务器使用。

### Robots.txt 并不是专门控制哪些页面在搜索引擎中被索引

Robots.txt 并不是控制搜索引擎索引页面的万无一失的方法。如果你的主要目标是阻止某些页面出现在搜索引擎结果中，正确的方法是[使用 meta noindex 标签](https://support.google.com/webmasters/answer/93710?hl=en)或密码保护。

这是因为你的 robots.txt 没有直接告诉搜索引擎不要索引内容——它只是告诉他们不要抓取它。虽然谷歌不会从你的网站内部抓取被标记的区域，但是[谷歌自己声明](https://developers.google.com/search/docs/crawling-indexing/robots/intro#:~:text=If%20other%20pages%20point%20to%20your%20page%20with%20descriptive%20text%2C%20Google%20could%20still%20index%20the%20URL%20without%20visiting%20the%20page.%20If%20you%20want%20to%20block%20your%20page%20from%20search%20results%2C%20use%20another%20method%20such%20as%20password%20protection%20or%20noindex.)如果一个外部网站链接到一个你用 robots.txt 文件排除的页面，谷歌仍然可能索引那个页面。

谷歌网站管理员分析师 John Mueller 也证实，如果一个页面有指向它的链接，即使它被 robots.txt 屏蔽，[仍然可能被索引](https://www.searchenginejournal.com/google-pages-blocked-robots-txt-will-get-indexed-theyre-linked/255911/)。以下是他在一个网站管理员中心的谈话内容:

> 这里需要记住的一点是，如果这些页面被 robots.txt 屏蔽，那么理论上可能会有人随机链接到这些页面中的一个。如果他们这样做，那么**可能会发生这样的情况，我们索引这个没有任何内容的 URL** ,因为它被 robots.txt 阻止了。所以我们不知道你实际上不想让这些页面被索引。
> 
> 而如果它们没有被 robots.txt 阻止，你可以在这些页面上放置一个 noindex meta 标签。如果有人碰巧链接到它们，而我们碰巧抓取了该链接，并认为这里可能有一些有用的东西，那么我们就会知道这些页面不需要被索引，我们可以完全跳过它们。
> 
> 因此，在这方面，如果你在这些页面上有任何你不想索引的东西，那么不要禁止它们，**使用 noindex** 代替。

### 我需要一个 robots.txt 文件吗？

重要的是要记住，你不需要有一个 robots.txt 文件在你的网站上。如果你不介意所有的机器人都可以自由抓取你的所有页面，那么你可能会选择不添加一个，因为你没有真正的指令给爬虫。

在某些情况下，由于您使用的 CMS 的限制，您甚至无法添加 robots.txt 文件。这很好，还有其他方法可以指导机器人如何在不使用 robots.txt 文件的情况下抓取您的页面。

### robots.txt 文件应该返回什么 HTTP 状态代码？

robots.txt 文件必须返回 a 200 OK HTTP 状态代码，以便爬网程序能够访问它。

如果您的页面被搜索引擎索引时遇到问题，值得仔细检查 robots.txt 文件返回的状态代码。除了 200 状态代码之外的任何代码都可能阻止爬虫访问您的站点。

一些网站所有者报告说，由于他们的 robots.txt 文件返回非 200 状态，页面被取消索引。2022 年 3 月，一位网站所有者在谷歌 SEO 办公时间的一次聚会中询问了一个索引问题，John Mueller 解释说，如果 robots.txt 文件存在，它应该返回 200 状态，如果该文件不存在，则返回 4XX 状态。在这种情况下，一个 [500 内部服务器错误](https://kinsta.com/blog/500-internal-server-error/)被返回，Mueller 说这可能导致 Googlebot 将该网站排除在索引之外。

在这条推文中也可以看到同样的情况，一个网站所有者报告说，由于 robots.txt 文件返回 500 错误，他的整个网站被取消索引。

> [快速搜索引擎优化技巧]
> 
> 如果索引有问题，确保 robots.txt 文件返回 200 或 404。
> 
> 如果你的文件返回 500，谷歌最终会对你的网站去索引，就像我在这个项目中看到的那样。[pic.twitter.com/8KiYLgDVRo](https://t.co/8KiYLgDVRo)
> 
> —安托万·埃里普雷特(@ antoineripret)[2022 年 11 月 14 日](https://twitter.com/antoineripret/status/1592132455523581954?ref_src=twsrc%5Etfw)