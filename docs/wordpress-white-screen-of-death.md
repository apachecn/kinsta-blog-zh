# 修复 WordPress 白屏死机(WSoD)的 9 种有效方法

> 原文：<https://kinsta.com/blog/wordpress-white-screen-of-death/>

没有什么比浏览你的 WordPress 网站时突然遇到死亡的白屏更糟糕的了。这个错误使得管理员和访问者都无法访问您的网站。

WSoD 也可能令人非常沮丧，因为缺少指向可能原因或解决方案的信息。然而，这也是最常见的 WordPress 错误之一。因此，虽然担心，在大多数情况下，这是可以解决的。

在这篇文章中，我们将解释什么是 WordPress WSoD 以及它的常见原因。最重要的是，我们将向您介绍九种可能的解决方案，让您的网站尽快恢复运行。

我们开始吧！

### 查看我们的视频指南[死亡的白屏](https://www.youtube.com/watch?v=0nsoi8fU0Cw)



## 死亡的 WordPress 白屏是什么？

名副其实，当你面对的不是你试图访问的网页，而是一个空白的白屏时，WordPress 白屏死机(也称为“WSoD”)就发生了。









根据您使用的浏览器，您可能会得到不同的错误信息。下面是 Google Chrome 中的一个例子，其中包括一个 [HTTP 500 错误](https://kinsta.com/blog/500-internal-server-error/)警告“此页面不起作用，无法处理请求”:

![wordpress wsod chrome](img/6202b8f37f0e5215c66cbd602d071e5d.png)

The WordPress White Screen of Death in Google Chrome



现在我们来看看 Mozilla Firefox 中的死亡白屏:

![wordpress wsod firefox](img/1ca882fb5a73b2d2cd2a29f20966406c.png)

The WordPress WSoD in Mozilla Firefox



如你所见，这只是一个普通的白色屏幕。它不包含任何有用的错误或警告消息。

WordPress 白屏死机几乎都是 PHP 代码错误或者[内存极限耗尽](https://kinsta.com/knowledgebase/php-memory-limit/)导致的。

另一个可能的原因是错误的主题或插件。如果[网站的前端关闭了](https://kinsta.com/blog/website-downtime/)，而你的 WordPress 管理区打开了，那么后者很可能就是问题。要快速检查您网站上的[仪表板是否正常工作，只需导航到 yourdomain.com/wp-admin.即可](https://kinsta.com/knowledgebase/wordpress-admin/)

那么，如何修复 WSoD 呢？很高兴你问了！

[The WordPress White Screen of Death is frustrating, confusing, but ultimately, fixable! 😅 Here are 9 easy solutions for you to try ⬇Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Fwordpress-white-screen-of-death%2F&via=kinsta&text=The+WordPress+White+Screen+of+Death+is+frustrating%2C+confusing%2C+but+ultimately%2C+fixable%21+%F0%9F%98%85++Here+are+9+easy+solutions+for+you+to+try+%E2%AC%87&hashtags=wsod%2Cwordpress)

## 如何修复 WordPress 白屏死机(9 种方法)

当你经历 WordPress 白屏死机时，你的首要任务将是尽快修复它。记住这一点，让我们来看看九种可能的解决方法。

### 1.禁用你的 WordPress 插件

修复 WordPress WSoD 最简单也是最常见的方法之一就是简单地[禁用你所有的插件](https://kinsta.com/knowledgebase/disable-wordpress-plugins/)。通常，一个网站关闭是因为一个糟糕的插件更新。

如果您仍然可以访问[您的管理区](https://kinsta.com/knowledgebase/wordpress-admin/)，一个快速的方法是从仪表板导航到**插件**，选择所有插件，然后从**批量操作**下拉菜单中点击**停用**:

![WSOD: Deactivate all WordPress Plugins setting](img/cb6abef0036be172c8e0d015fdab28e8.png)

The Deactivate all WordPress Plugins setting



这将禁用您的所有插件。

如果这样可以解决问题，您需要找到罪魁祸首。要做到这一点，你可以开始一个接一个地激活插件，每次激活后重新加载站点。当你的前端出现故障时，你已经发现了行为不端的插件。

然后你可以向插件开发者寻求帮助，或者[在 WordPress 插件目录中发布一张支持票](https://kinsta.com/blog/wordpress-support/)。

如果你[不能登录 WordPress admin](https://kinsta.com/blog/locked-out-of-wordpress-admin/) ，你可以使用一个[文件传输协议(FTP)客户端](https://kinsta.com/blog/best-ftp-clients/)来访问你网站的文件目录。

在根目录的 **wp-content** 文件夹下，找到**插件**文件夹。将其重命名为类似“plugins_old”的名称:

![WSoD: Rename your plugins folder](img/59da0f96e32e8897dd837f6d0e80347d.png)

Rename your plugins folder



然后，在前端再次检查你的网站。如果这有效，你将需要一个接一个的测试每个插件。将你的插件文件夹重新命名为“插件”*、*，然后分别重命名其中的每个插件文件夹，直到找到有问题的那个。

### 2.切换到默认的 WordPress 主题

如果问题不是插件，你的主题可能是导致白屏的原因。要查看这是否是问题所在，你可以通过切换到默认主题来[替换你的主题](https://kinsta.com/blog/change-wordpress-theme/)。

如果您可以访问您的管理区，请在您的仪表板中进入**外观>主题**。找到并激活一个默认的 WordPress 主题，例如[二十二十](https://kinsta.com/blog/twenty-twenty-theme/):

![WSOD: switch to a default theme](img/8d88807e8bd41c622f970473fb314fac.png)

The Twenty Twenty WordPress theme.



然后，再次测试你的站点。如果成功了，你就会知道问题出在你的主题上。

如果您不能访问您的仪表板，过程与插件是一样的。

使用 FTP 访问你站点的文件，并把你的 **wp-content/themes** 文件夹重命名为其他名称:

![WSoD: theme folder](img/237ae3b5146dcc390c438dea207f92b8.png)

Rename your themes folder



WordPress 将恢复到最新的默认主题，很可能是 Twenty Twenty。如果你没有其他主题，你可以从 WordPress 主题目录下载一个，然后[上传到你的主题文件夹](https://kinsta.com/blog/how-to-install-a-wordpress-theme/)。

之后，继续检查你的网站。如果它工作，也许你的主题有冲突或者一个坏的更新。如果是这种情况，你可能需要向开发者寻求帮助，或者考虑[切换主题](https://kinsta.com/blog/change-wordpress-theme/)。

### 3.清除浏览器和 WordPress 插件缓存

如果你可以访问你的 WordPress 网站的后端，但仍然在前端看到 WSoD，这可能是由于你的缓存有问题。

要修复它，尝试[清除你的网络浏览器的缓存](https://kinsta.com/knowledgebase/how-to-clear-browser-cache/)和你的 [WordPress 缓存插件](https://kinsta.com/blog/wordpress-caching-plugins/)(假设你已经安装了一个)。

如果你在 WordPress 网站上安装了缓存插件，比如 [WP Rocket](https://kinsta.com/blog/wordpress-caching-plugins/#wp-rocket) 或 [WP Super Cache](https://kinsta.com/blog/wordpress-caching-plugins/#wp-super-cache) ，大多数都提供了一种通过插件的设置页面快速清除缓存的方法。

以 WP 超级缓存为例，在你的 WordPress 仪表盘中，你可以导航到**设置** > **WP 超级缓存** > **删除缓存**:

![delete plugin cache](img/0a274d434ad89144233d58e9e2c35609.png)

The WP Super Cache plugin settings page



#### 如何从 MyKinsta 中清除您的缓存

如果你是一个 Kinsta 用户，也有一个简单的方法让你使用 MyKinsta 清除你的缓存。为此，请登录您的帐户。点击**工具**，然后点击**站点缓存**部分下的**清除缓存**:

![kinsta site cache](img/83fda5dd5754aa3da3c6c3dabb7a579b.png)

The Clear cache option in MyKinsta



清空缓存后，保存您的更改。然后重新访问您的网站，看看是否纠正了问题。如果没有，是时候转向另一个解决方案了。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

### 4.打开调试模式

如果你仍然看到 WordPress 白屏死机，管理区不工作，或者你认为你已经发现了问题，但想深入挖掘，你可以[启用调试模式](https://kinsta.com/blog/wordpress-debug/)。这将显示您的网站上发生的任何错误。

要启用调试，你需要[打开 WordPress install 的](https://kinsta.com/blog/wp-config-php/)*[【wp-config.php】](https://kinsta.com/blog/wp-config-php/)*[文件](https://kinsta.com/blog/wp-config-php/)。在其中，您应该可以找到下面一行:

```
define( 'WP_DEBUG', false );
```

将“假”改为“真”，然后重新加载您的站点。如果这一行不存在，您可以将它添加到文件的顶部。

您将得到一个白屏和一些错误消息，而不是白屏。这不是一个巨大的进步，但这只是一个开始。WSoD 错误消息应该指出问题源自哪个文件，如下所示:

```
Cannot redeclare get_posts() (previously declared in 
/var/www/html/wordpress/wp-includes/post.php:1874) in 
/var/www/html/wordpress/wp-content/plugins/my-test-plugin/my-test-plugin.php on line 38
```

您可以在这个示例消息的末尾看到，问题出在一个名为 *my-test-plugin* 的插件的第 38 行。因此，禁用该插件应该可以解决问题。

如果您在启用调试模式后没有看到任何错误，您可能需要[联系您的 web 主机](https://kinsta.com/kinsta-support/)。您的服务器上可能没有正确配置调试。

Kinsta 客户可以选择[使用内置调试工具](https://kinsta.com/blog/wordpress-debug/#how-to-enable-wordpress-debug-mode-in-mykinsta)。在 MyKinsta 仪表板上，点击您网站的名称，然后点击**工具**。在 **WordPress 调试**下，选择**启用**:

![kinsta debugging tool](img/2ad68c238dbf4e137507498dd6a0129b.png)

How to enable WordPress debugging mode in MyKinsta



然后，您可以在 MyKinsta 仪表板的 **Logs** 部分下访问您的错误日志，并浏览它们以了解有关该问题的更多信息。

请记住，打开调试模式会将您网站的一些信息暴露给未经批准的用户。因此，请务必在使用完该模式后将其关闭。



### 信息

愿意给 MyKinsta 一个测试机会吗？[免费创建您的模拟帐户](https://kinsta.com/mykinsta/)并开始使用它。



### 5.增加你的记忆极限

如果在尝试了上面的一些解决方案之后，您仍然看到可怕的 WSoD 空页面，或者您得到一个抱怨内存限制或内存耗尽的错误，您将需要为应用程序分配更多的内存。

这可以通过许多 WordPress 安装上的*wp-config.php*文件来完成。打开文件并添加以下代码:

```
define('WP_MEMORY_LIMIT', '64M');
```

如果这不起作用，你有几个选择。在常规环境下，你可以使用你的*。htaccess* 文件给[增加内存限制](https://kinsta.com/knowledgebase/wordpress-memory-limit/)。只需添加下面一行:

与宕机和 WordPress 问题做斗争？Kinsta 是一款考虑到性能和安全性的托管解决方案！[查看我们的计划](https://kinsta.com/plans/?in-article-cta)

```
php_value memory_limit 64M
```

如果无法访问您的 *[。htaccess](https://kinsta.com/knowledgebase/wordpress-htaccess-file/)* [文件](https://kinsta.com/knowledgebase/wordpress-htaccess-file/)，你可以用你的 [*php.ini*](https://kinsta.com/knowledgebase/the-uploaded-file-exceeds-the-upload_max_filesize-directive-in-php-ini/) 文件来增加内存限制来代替。

为此，请通过 FTP 连接到您的服务器。在您站点的根目录中，查找 *php.ini* 文件。找到它后，在文件中的任意位置添加以下行:

```
memory_limit = 64M
```

如果您仍然没有足够的内存，需要分配更多的内存，那么您的应用程序可能有问题。也许你的主题或者你的插件使用了过多的资源。

此时，你可能想[雇一个开发者](https://kinsta.com/blog/hire-wordpress-developer/)来看看。甚至你的主机也能帮上忙，向你展示你的站点的 SQL 日志和其他资源统计。



Kinsta 客户不需要增加他们的内存限制，因为我们所有的计划都设置了 256 MB 的默认内存限制。



### 6.检查文件权限问题

WSoD 的另一个潜在原因是许可和所有权问题。你自己有可能解决这个问题。然而，除非你真的知道自己在做什么，否则我们建议你不要这么做，因为你可能会无意中[制造出攻击者可以利用的漏洞](https://kinsta.com/knowledgebase/disclose-security-vulnerability/)。

说到 [WordPress 权限](https://wordpress.org/support/article/changing-file-permissions/)，有三个简单的规则要遵循:

*   文件应该设置为 664 或 644。
*   文件夹应设置为 775 或 755。
*   *wp-config.php*文件应设置为 660、600 或 644。

如果您有对您的服务器的 [SSH 访问，您可以使用下面的命令应用适当的规则，从根 WordPress 目录运行它:](https://kinsta.com/blog/how-to-use-ssh/)

```
sudo find . -type f -exec chmod 664 {} +
sudo find . -type d -exec chmod 775 {} +
sudo chmod 660 wp-config.php
```

如果你不确定如何做到这一点，或者有点害怕，请继续向你的主机寻求帮助。

### 7.检查失败的自动更新问题

有时候，WordPress 会遇到更新问题，比如服务器超时。通常，这个问题会自动解决。然而，在一些罕见的情况下，它可能会导致 WordPress 白屏死亡。

你应该做的第一件事是进入你的 WordPress 根目录，看看是否有一个*。维护那里的*文件(文件名也可以缩写)。

你要做的是尝试删除该文件，并再次加载您的网站。

如果更新成功了，但是 WordPress 没有自动删除这个文件，一切都会恢复正常。

如果更新没有完成，它可能会自动重启，在这种情况下，一切都会恢复正常。

如果所有其他方法都失败了，遵循推荐的 WordPress 的[手动更新程序，这将彻底解决问题。](https://kinsta.com/blog/reinstall-wordpress/)

### 8.解决语法错误或恢复备份

WordPress WSoD 的另一个常见原因是当你[在你的 WordPress 站点](https://kinsta.com/knowledgebase/edit-wordpress-code/)上编辑代码时，不小心打错了或者使用了错误的语法。

一个字符出现在错误的地方可能会毁掉你的整个网站，这就是为什么你应该[永远不要在你的现场制作网站](https://kinsta.com/help/staging-environment/)上编辑代码。

不过，别担心。您可以随时通过 FTP 连接到您的站点，并手动恢复您所做的更改。如果你不知道是什么变化导致了这个问题，这就是有了 [WordPress 备份](https://kinsta.com/help/wordpress-backups/)的地方派上用场了。

在 Kinsta，[您只需点击一下鼠标，就可以将您的站点](https://kinsta.com/help/restore-wordpress-backup-staging/)恢复到更早的时间点。为此，请登录 MyKinsta 仪表盘并导航至**备份**:

![The backup feature in MyKinsta](img/278721dc9b6314c8b38e0781e6bddd4a.png)

The backup feature in MyKinsta



请记住，如果你之前在 WordPress 中启用了调试模式，可能会有一个错误消息指出一个语法错误。如果是这种情况，它应该会告诉您在哪里可以找到问题代码。

### 9.增加 PHP 文本处理能力

此时，如果 WSoD 还没有解决，还有一个额外的技巧可以尝试。在极少数情况下，这个问题可能是因为页面或帖子特别长而发生的。

如果是这种情况，您可以尝试通过增加回溯和递归限制来调整您站点上的 PHP 文本处理能力。为此，将以下代码粘贴到您的**wp-config.php**文件中:

```
/* Trick for long posts /
ini_set('pcre.recursion_limit',20000000);
ini_set('pcre.backtrack_limit',10000000);
```

添加代码后，保存您的更改。然后刷新你的网站，看看它现在是否工作。

[Faced with the dreaded WordPress White Screen of Death? 😭 Don't worry... these 9 fixes will get your site back up & running in a flash! 💥Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Fwordpress-white-screen-of-death%2F&via=kinsta&text=Faced+with+the+dreaded+WordPress+White+Screen+of+Death%3F+%F0%9F%98%AD+Don%27t+worry...+these+9+fixes+will+get+your+site+back+up+%26amp%3B+running+in+a+flash%21+%F0%9F%92%A5&hashtags=WordPressErrors%2Cwebdev)

## 摘要

WordPress 的死亡白屏会让人非常沮丧，甚至害怕。有很多事情可能会出错，但谢天谢地，情况通常不像看上去那么糟糕。

在大多数情况下，一个简单的插件和/或主题检查应该可以修复 WSoD 问题。越来越熟悉 [WordPress 调试模式](https://kinsta.com/blog/wordpress-debug/#what-does-wp-debug-do)肯定会让你对问题有更多的了解和指导。

如果你遇到过任何其他的 WordPress 白屏死机的情况，请告诉我们，这样我们可以从中吸取教训并分享经验！

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。