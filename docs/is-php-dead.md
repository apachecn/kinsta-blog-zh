# PHP 死了吗？不要！至少根据 PHP 的使用统计是这样的

> 原文：<https://kinsta.com/blog/is-php-dead/>

你可能听说过新的 WordPress[Gutenberg editor](https://kinsta.com/blog/gutenberg-wordpress-editor/)如何将基于块的编辑引入 WordPress。

普通用户可能不会注意到，幕后正在发生变化，Gutenberg 块是使用 JavaScript (React、JSX 和 ES6)而不是 PHP 制作的。这种变化，以及 web 开发中的其他转变，可能会让您怀疑，“PHP 死了吗？”。

所以…是吗？我们应该打电话给殡仪馆开始准备吗？首先，指出**希望** PHP 死掉和 PHP **实际上**死掉之间有很大的区别是很重要的。

人们多年来一直在呼吁 PHP 的死亡，你可以找到“PHP 死了吗？”最早 2011 年的帖子。然而，PHP 仍然存在…

在本帖中，我们将深入研究数据，并展示 PHP 是如何接近死亡的(即使你真的希望它是)。

*   [PHP 死了吗？只有当你忽略 PHP 使用统计数据](#php-usage-statistics)
*   PHP 也比以前更快更好了
*   [很容易找到 PHP 开发者](#many-php-developers)
*   [你可以不喜欢 PHP，但它不死](#php-is-not-dead)

## PHP 死了吗？只有当您忽略 PHP 使用统计时

好吧， [PHP](https://kinsta.com/knowledgebase/what-is-php/) 可能不是最好或最现代的编程语言。但这并不意味着它已经死了，在这里与 PHP 的统计数据争论是相当困难的…

首先，让我们看看 W3Techs 是怎么说的。

[根据 W3Techs 的数据](https://w3techs.com/technologies/details/pl-php/all/all)，在所有已知服务器端编程语言的**网站中**有 78.9%** 使用 PHP。所以你在互联网上访问的每 10 个网站中几乎有 8 个都在以某种方式使用 PHP。这让我们想到了一个事实…**





> 需要在这里大声喊出来。Kinsta 太神奇了，我用它做我的个人网站。支持是迅速和杰出的，他们的服务器是 WordPress 最快的。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![A picture of Phillip Stemann looking into the camera wearing a blue button down shirt](img/12b77bdcd297e9bf069df2f3413ad833.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Phillip Stemann</cite></footer>

[View plans](https://kinsta.com/plans/)

![is PHP dead?](img/62aa7f3f03be2f6876d7f0b21f49cb4f.png)

PHP cannot die



公平地说，这个数字正在下降。2017 年 11 月，W3Techs 将 PHP 作为 80.1%网站的服务器端语言。这个数字在 2018 年 6 月下降到 79.6%，现在当我们在 2018 年 11 月发表这篇文章时，这个数字下降到 78.9%。

然而，你也必须对一些统计数据持保留态度。这些扫描工具中的一些只是寻找`X-Powered-By` HTTP 头。一些主机提供商，包括 Kinsta，出于安全考虑，在服务器上广播时会删除这些头。因此，使用 PHP 的站点数量实际上可能会更多。

但是当这个数字仍然超过 75%的时候，很难用这个下降来宣告 PHP 的死亡。

如果你仔细想想，这些数字真的不应该令人惊讶。首先，现存最流行的内容管理系统使用 PHP。鉴于 WordPress [为互联网上超过 34%的网站提供支持](https://kinsta.com/wordpress-market-share/)，这就意味着有很多网站在使用 PHP。想知道你运行的是哪个 PHP 版本？查看我们关于[如何创建 phpinfo 页面](https://kinsta.com/knowledgebase/phpinfo/)的指南。

但这也不仅仅是 WordPress。还有很多其他大大小小的用 PHP 构建的网站。比如维基百科背后的软件 MediaWiki，就是用 PHP 写的。哦，对了，Drupal 和 T2 Joomla 也使用 PHP。

## PHP 也比以前更快更好了

有了 PHP 的最新[版本，PHP 比以往任何时候都要快。我们最近的](https://kinsta.com/blog/php-versions/) [PHP 基准测试](https://kinsta.com/blog/php-benchmarks/)显示了 PHP 7 的巨大性能提升。X over PHP 5.6。

在我们使用 WordPress 和 WooCommerce 和 Easy Digital Downloads 等流行电子商务插件的测试中，PHP 7.3 的每秒请求数是 PHP 5.6 的 2-3 倍。而 Kinsta 最近推出的 [PHP 8.1](https://kinsta.com/feature-updates/php-8-1/) 更快。

![WordPress 5.0 PHP benchmarks](img/aa3e50c1190462560cd448720e536908.png)

WordPress 5.0 PHP benchmarks



更好的是，PHP 7 也比其他语言更有优势。

除此之外， [PHP 7。x 版本](https://kinsta.com/blog/php-7-4/)也为开发者带来了新的改进，比如:

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

*   组合比较运算符
*   零合并运算符
*   新型暗示
*   匿名类
*   可空类型
*   Iterable 和 void 返回
*   多重捕获异常处理
*   列表中可用的键
*   尾随逗号
*   更多的负字符串偏移量
*   数字运算符和格式错误的数字
*   [HTTP/2 服务器推送](https://kinsta.com/learn/what-is-http2/)

当然，只有当您实际使用最新版本的 PHP 时，您才会注意到这些改进。不幸的是，事实往往并非如此。

[根据 WordPress.org](https://wordpress.org/about/stats/)的数据，大约 64.0%的 WordPress 网站使用 PHP 7.1 或更低版本，22.9%的网站使用 PHP 5.6:

![WordPress PHP version Stats](img/8685056888b7f7d3ca7ae2dd445bc72a.png)

WordPress PHP version Stats



PHP 7.1 及以下版本自 2018 年和 2019 年起不再获得主动支持并失去安全支持。

事实上，如此多的网站运行在一个正式达到其生命终点的 PHP 版本上，这可能无助于 PHP 在开发者中的声誉。

如果你仍然不确定为什么你需要更新你的 PHP 版本，请阅读这篇文章。

## 很容易找到 PHP 开发人员

因为 PHP 的流行，很容易找到 PHP 开发者。不仅仅是 PHP 开发人员，还有有经验的 PHP 开发人员。

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

更重要的是，PHP 开发人员自己似乎做得很好，Brandon Savage 的这条推文雄辩地指出:

> 如果 PHP 死了，有人忘了告诉我的银行账户。
> 
> —布兰登·萨维奇(@ Brandon Savage)[2018 年 10 月 28 日](https://twitter.com/brandonsavage/status/1056600728872067072?ref_src=twsrc%5Etfw)