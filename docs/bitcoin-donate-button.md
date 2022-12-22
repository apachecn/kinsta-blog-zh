# 如何在你的 WordPress 网站上添加一个比特币捐赠按钮

> 原文：<https://kinsta.com/blog/bitcoin-donate-button/>

自 2009 年 1 月 5 日问世以来，比特币风靡全球。然而，2017 年真的被一些人称为“比特币之年”。你现在还没听说过这件事，那你一定是生活在岩石下了。比特币的价值一直在疯狂增长，而且似乎不会很快放缓。

如果你被加密货币的想法迷住了，并且想学习如何在你的 WordPress 网站上添加一个比特币捐赠按钮，那么你来对地方了。但首先，如果你不熟悉它，或者需要复习一下，先说几句关于比特币和它是什么的话。

## 比特币是什么？

简而言之，比特币是一种**完全虚拟的货币**，也就是说你不能用钞票、纸币，甚至是一枚真币来支付比特币。所有的支付都发生在网络空间。其次，比特币数量巨大，今天流通的比特币价值超过 15 亿美元——每分钟都有大量交易发生。

只要商家接受比特币，你就可以用比特币支付任何东西。这包括营销服务、网站会员、公寓、汽车租赁，甚至是一辆[兰博基尼](https://www.cnbc.com/2018/02/07/bitcoin-millionaires-are-buying-lamborghinis-with-cryptocurrency.html)。

[By the time you read this, the price of #Bitcoin will have drastically changed. 😉Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Fbitcoin-donate-button%2F&via=kinsta&text=By+the+time+you+read+this%2C+the+price+of+%23Bitcoin+will+have+drastically+changed.+%F0%9F%98%89)

就在去年，比特币在交易所的价格已经飙升。回到 2016 年 12 月，它的价值略高于 750 美元。截至 2017 年 12 月 12 日，目前为 17，575 美元(**上涨 2157.02%** )。正如你可能猜到的，这种加密电流并不完全是稳定性的缩影。但许多持有比特币的早期投资者几乎在一夜之间成为了百万富翁。

![Bitcoin growth](img/d8832af12d081fb141cb525d90888aa7.png "Bitcoin growth")

Bitcoin growth (Screen from Coinbase)



### 该不该投资比特币？

我们肯定无法回答这个问题，因为比特币非常不稳定，而且确实是一种新的货币。很难说它会做什么。以下是马克·库班在接受《名利场》采访时说的话。





> Kinsta 把我宠坏了，所以我现在要求每个供应商都提供这样的服务。我们还试图通过我们的 SaaS 工具支持达到这一水平。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![](img/60f15faa5735bd2437bf9dada5ee9192.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Suganthan Mohanadasan from @Suganthanmn</cite></footer>

[View plans](https://kinsta.com/plans/)

> 如果你是一个真正的冒险家，你真的想孤注一掷，你可能会拿出 10 %(你的储蓄)放在比特币或以太坊。但是如果你这样做，你必须假装你已经失去了你的钱。就像收集艺术品，就像收集棒球卡，就像收集鞋子。有些东西值得别人为它付出多少。这是一个传单，但我会限制在 10%。

## 如何轻松创建比特币捐赠按钮

在本教程中，我们将向你展示几种不同的方式，你可以使用比特币在你的 WordPress 博客(或任何网站，就此而言)上接收捐款。第一种允许你用比特币当前的价格兑换一美元。第二个、第三个和第四个选项允许你直接接受比特币进入你的数字钱包。

*   [选项 1–创建带条纹和插件的比特币捐赠按钮](#bitcoin-donate-button-stripe)
*   [选项 2–用古尔、吉维和比特币基地创建比特币捐赠按钮](#bitcoin-donate-button-give)
*   [选项 3–用比特币基地(代码)创建比特币捐赠按钮](#bitcoin-donate-button-coinbase)
*   [选项 4–使用比特币地址或二维码变得简单](#bitcoin-donate-simple)

### 选项 1–创建带条纹和插件的比特币捐赠按钮

我们是条纹支付处理器的忠实粉丝。事实上，我们已经为我们所有的客户使用了它们，同时把 Kinsta 的数据提升到了 7 位数。所以我们创建比特币捐赠按钮的第一个方法是结合 WordPress 插件和 Stripe。

Stripe 提供便捷的汇率。因此，你可以用美元指定你的捐款金额，他们会给你美元(从比特币转换后)。每笔成功的比特币交易，Stripe 只收取 0.8%的费用，上限为 5 美元。但是，要当心[交易费](https://bitinfocharts.com/comparison/bitcoin-transactionfees.html)。如果你是小额付款，下面的选项 2 或 3 会更好。

为了开始，我们推荐免费的 [WP 简单付费 Lite for Stripe](https://wordpress.org/plugins/stripe/) 插件，你可以通过 5 个简单的步骤开始。它目前有超过 10，000 个活跃安装，五星评级为 4.5。

[![WP Simple Pay Lite for Stripe WordPress plugin](img/31a8bb40c765633289cd5aefbf1cffed.png)](https://wordpress.org/plugins/stripe/)

WP Simple Pay Lite for Stripe WordPress plugin



注意:在我们的测试中，它运行在 [PHP 7.2](https://kinsta.com/blog/php-7-2/) 上确实有问题。然而，它在 PHP 7.1 上运行良好

#### 第一步

从 WordPress 知识库下载并安装 [WP Simple Pay Lite for Stripe](https://wordpress.org/plugins/stripe/) 插件，或者在你的 WordPress 仪表盘“添加新插件”下搜索。

![Install WP Simple Pay Lite plugin](img/9e38df6c99dc96ae9ddccf91c9d90aa3.png)

Install WP Simple Pay Lite plugin



#### 第二步

你需要做的第一件事是点击进入插件的设置，并输入你的 [Stripe API 密钥](https://dashboard.stripe.com/account/apikeys)，你可以从你的 Stripe 帐户仪表板中获取。然后点击“保存更改”你会注意到有一个“测试模式”。您可以保持启用状态，直到您配置好所有内容。

![Install WP Simple Pay Lite plugin](img/f9c4adbff957f902d2623fc74a1ffe7c.png)

Install WP Simple Pay Lite plugin



#### 第三步

点击进入“默认”设置选项卡。在那里你可以给你的网站命名，设置货币，提供图片等等。一个重要的设置是支付成功页面 URL。如果你在你的捐赠上用一个感谢页跟踪转换，那么你将想要启用这个。参见我们深入的[转换跟踪指南](https://kinsta.com/blog/conversion-tracking/)。然后向下滚动并点击“保存更改”

![WP Simple Pay settings](img/a20982c267df1aad0b67e7c36af04da5.png)

WP Simple Pay settings



#### 第四步

然后你需要创建一个“付款表格”您可以在“支付选项”下设置捐赠金额，并自定义其余的结账流程。这里最重要的部分是启用“比特币”选项。

![WP Simple Pay payment form](img/a0459955a5ad85236c2c56798ab1a053.png)

WP Simple Pay payment form



#### 第五步

然后你可以在你的 WordPress 站点的任何页面或帖子上插入一个支付按钮。只需点击编辑器中的“插入付款表格”按钮。

![Insert payment form](img/b6473be6f61866e9c4e00ea7336def94.png)

Insert payment form



这是点击捐赠比特币按钮后的一个例子。或者我所谓的“给我买杯咖啡”☕:有一个比特币标签，Stripe 会立即进行转换。所以我的 5 美元咖啡捐赠花费了他们 0.011855 比特币(BTC)。注意:这只是一个例子，谨防[交易费用](https://bitinfocharts.com/comparison/bitcoin-transactionfees.html)。如果你是小额付款，下面的选项 2 或 3 会更好。

![Buy me a coffee with Bitcoin](img/6a4a51eab00308f21f164226b217173f.png)

Buy me a coffee with Bitcoin



这就是它的！在你的 WordPress 网站上添加一个条纹比特币捐赠按钮再简单不过了。如果您还没有设置，请确保将实时模式切换到“开”。作为另一种选择，我们也强烈建议查看 [Give Stripe 插件](https://givewp.com/addons/stripe-gateway/)。
T3】

### 选项 2–用古尔、吉维和比特币基地创建比特币捐赠按钮

第二个选择是给那些真正想要得到比特币的人。这可以通过直接向比特币钱包接受捐款来实现。有**在线软件钱包**，也有**实体硬件钱包**，比如 [Trezor](https://trezor.io/) ，你可以用它们来存放你的加密货币。一般来说，如果你在处理大量比特币，硬件钱包是最安全的路线。

在这个例子中，我们将使用流行的在线[比特币基地](https://www.coinbase.com)平台，它既是钱包又是在线交易所。你可以使用的另一种选择是[区块链](https://www.blockchain.com/)。然后，我们将利用几个插件来完成这项工作。

#### 第一步

如果你还没有比特币基地账户，你要做的第一件事就是建立一个。这将创建您的数字钱包，其中包含您的比特币。前往[比特币基地](https://www.coinbase.com/)，点击右上角的“注册”。加入是免费的。**但是要时刻注意交易费用！**每个钱包/交易所处理方式不同。例如，从一个比特币基地钱包发送到另一个比特币基地钱包将使比特币交易费无效。但是，您需要分别查找每个钱包。

![Coinbase account](img/1329cc8a20afcdce1b2224e96f7e6c95.png)

Coinbase account



#### 第二步

登录后，你会看到一个指示板，显示你账户的当前信息:你拥有的比特币数量、等值美元等。你需要拿到你的比特币地址:一个字母数字代码(非机密)，人们可以用它给你汇钱。为此，请点击顶部的“帐户”。然后点击你的比特币(BTC)钱包旁边的“接收”。

![Bitcoin receive](img/594fe2f8dd17bc7b3829ca29edcbbc37.png)

Bitcoin receive



然后你会看到你的比特币地址。请不要关闭此选项卡，或者记下此地址，因为您稍后会用到它。

![Bitcoin wallet address](img/f8ed02dcf175f4cef247197471801bf3.png)

Bitcoin wallet address



#### 第三步

然后安装并激活以下三个插件(都是完全免费的)。

*   [给](https://wordpress.org/plugins/give/)
*   [古尔比特币支付网关&付费下载&会员资格](https://wordpress.org/plugins/gourl-bitcoin-payment-gateway-paid-downloads-membership/)
*   [古尔比特币 Paypal 捐款–Give Addon](https://wordpress.org/plugins/gourl-bitcoin-paypal-donations-give-addon/)

#### 第四步

您现在需要为 GoURL 插件生成您的私钥，因此在 [GoURL.io](https://gourl.io/view/registration) 创建一个免费帐户。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

#### 第五步

然后[创建一个付款箱](https://gourl.io/editrecord/coin_boxes/0)。输入姓名、您的硬币(在这种情况下是比特币)和您在上面第 2 步中的比特币钱包地址。输入你的回拨网址，你可以从插件设置的页面获取。单击“保存”后，您的密钥将会出现。

![GoURL payment box](img/2d267281f981861e7cd266fa0cd07017.png)

古尔付款箱



#### 第六步

回到 GoURL 插件设置，输入你刚刚创建的比特币密钥，点击“保存设置”

![GoURL Bitcoin keys](img/c445def3c6067b9487aff884c45ac827.png)

GoURL Bitcoin keys



#### 第七步

然后你需要在 Give 插件中启用 GoURL 比特币支付网关。所以在捐赠下面点击进入“设置”点击支付网关选项卡，启用 GoURL 比特币/Altcoin 网关。

![Enable Bitcoin in Give plugin](img/aa6013499c9bbf2ef914c2bcfad54ac3.png)

Enable Bitcoin in Give plugin



#### 第八步

在“网关”选项卡下，如果您只想将它用于比特币捐赠，可以取消选中其他网关。另外，一旦你准备好了，一定要记得把它从“测试模式”中取出来。

![Give default gateways](img/aa9e3d9cef44e92e64eeddb3e4c081fc.png)

Give default gateways



#### 第九步

然后你需要用 Give 插件创建一个捐赠表单。在这个例子中，我创建了一个“用比特币给我买杯咖啡”的对话框。一旦你完成了自定义，确保抓住右边的短代码，因为你需要把它放到你的页面或文章中。

![Give donation form](img/817a87f15d9378f57ce7e32d55492f0f.png)

Give donation form



#### 第十步

将短代码放入帖子或页面，你就可以开始了。您也可以使用编辑器中的按钮。

![Give shortcode](img/bbcbded9a8bf4dbaa3f04dc2913b3446.png)

Give shortcode



下面是一个简单的捐赠表格。

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

![Bitcoin donate button](img/616cec2e5baa3c5363cbfa6ec177548e.png)

Bitcoin donate button



一旦有人输入他们的信息并点击“立即捐赠”，他们就会进入下一个页面，在这个页面中，他们可以使用你最喜欢的比特币钱包应用程序[扫描二维码](https://kinsta.com/blog/create-qr-code/)，或者将比特币直接发送到你的钱包地址。Give 插件甚至会为它们生成一张捐赠收据。

![Send bitcoin](img/14da30e4e8d2eb4a6364970318da60b0.png)

Send bitcoin



### 选项 3–用比特币基地创建比特币捐赠按钮(代码)

第三个选项与上面的选项 2 相似，我们只是用代码而不是插件来实现它。因此，再次获取您的比特币基地钱包地址，并遵循以下步骤。

#### 第一步

首先，你需要在 WordPress 中创建一个捐赠按钮。一个开发者做了一个很棒的小项目，叫做 [coinwidget](https://coinwidget.github.io/) 。你可以从他的网站获取最新的代码，或者在下面添加以下内容。首先是在你的 WordPress 文章中添加一些自定义的 [HTML](https://kinsta.com/blog/wordpress-vs-static-html/) 。

*   你需要用你在上面第二步中得到的比特币地址来更新**数据钱包属性**。
*   您可以更新**数据-文本属性**来改变按钮的文本。在我的例子中，我用“用比特币给我买杯咖啡。”

```
<div id="coinwidget" data-icon="true" data-type="primary" data-text="Buy me coffee with Bitcoin" data-wallet="**1JBTco78X6zPhqKvzYAX7HaJvqLmNJE6a4**">
```

#### 第二步

然后，您将需要添加以下自定义 CSS 和 JavaScript。查看如何在 WordPress 中添加自定义代码。

自定义 CSS

```
.ui.button {min-width:300px !important; min-height:50px !important;}
```

Java Script 语言

```
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/ivandiazwm/[[email protected]](/cdn-cgi/l/email-protection)/builds/full.js" charset="utf-8"></script>
```

然后，您将看到一个如下所示的按钮。

![Donate Bitcoins button](img/a90d57e95af59a84c47ab0d8e6a5285a.png)

Donate Bitcoins button



当有人点击按钮，它就会产生一个比特币捐赠箱。他们可以把比特币直接发到你的钱包地址，或者扫描二维码。

![Bitcoin donate box](img/c5157707ffe4bdca80e353695212896f.png)

Bitcoin donate box



注意:如果你好奇为什么我们不使用比特币基地的捐赠按钮创建器，那是因为他们不再接受商家资料。如果你是一个 501(c)3 [非营利组织](https://kinsta.com/blog/wordpress-for-nonprofits/)，我们建议用 [Bitpay](https://bitpay.com/) 创建捐赠按钮，因为它允许更多的定制。

同样重要的是要认识到，默认情况下，在你每次交易后或资金转移时，钱包会自动为你生成一个新地址。这样做是为了保护您的隐私，这样第三方就无法通过使用区块链浏览器查找他们知道是您的地址来查看与您的帐户相关的所有其他交易。然而，许多人仍然使用一个地址接受多项付款或捐赠。事实上，许多人会随意给出他们的地址。

如果你对比特币、比特币基地、区块链和比特币支付之间的区别感到困惑，欢迎来到加密货币。😄但是你可以这样想:

*   比特币是 ***货币***
*   区块链和比特币基地是你的 ***银行***
*   BitPay 本质上和 PayPal ( **支付处理器**)是一回事

就像中央银行和 PayPal 一样，区块链、比特币基地和 BitPay 也有自己的竞争对手和替代品。

### 选项 4–使用比特币地址或二维码变得简单

如果你不想搞砸以上任何一项，想变得超级简单，你可以随时在你的网站上添加你的比特币地址，请求捐款。或者使用免费的[比特币二维码生成器](https://gobitcoin.io/tools/qrcode/)，下载图片，并将其添加到你网站的任何地方。

![Bitcoin QR code generator](img/39d8aefe8478620cb1d8c53e031347c8.png)

Bitcoin QR code generator



## 在你的电子商务网站上接受比特币

如果你想真正大胆，你也可以开始在你的电子商务网站上接受比特币。这里有几个值得一看的插件。

*   [面向网络商务的比特币支付](https://wordpress.org/plugins/bitpay-for-woocommerce/)
*   [轻松数字下载:BitPay 网关](https://devrix.com/shop/product/easy-digital-downloads-bitpay-gateway/)
*   [GoUrl woo commerce–比特币替代币支付网关插件](https://wordpress.org/plugins/gourl-woocommerce-bitcoin-altcoin-payment-gateway-addon/)
*   [GoUrl Easy Digital Downloads(EDD)–比特币替代币支付网关](https://wordpress.org/plugins/gourl-bitcoin-easy-digital-downloads-edd/)

关于如何接受捐赠的更多选择，请查看以下指南:

[如何在 WordPress 中添加条纹捐赠按钮](https://kinsta.com/blog/stripe-donate-button/)

[如何为你的 WordPress 站点创建一个 PayPal 捐赠按钮](https://kinsta.com/blog/paypal-donate-button-wordpress/)

[10 个 WordPress 捐赠插件](https://kinsta.com/blog/wordpress-donation-plugins/)

## 摘要

如你所见，有几种不同的方法可以将比特币捐赠按钮添加到你的 WordPress 站点。如果你还没有完全搞不懂加密货币，那就把自己当成少数派吧。😄看看 2018 年比特币会发生什么，肯定会很有趣。如果有的话，这是一个令人兴奋的金融话题。

但为了向你展示它的波动性，当我们开始写这篇文章时，比特币的价值是 17575 美元，几个小时后，它的价值是 17179.50 美元。因此，在我们写一篇博文的时间内，它的价值已经下降了近 400 美元！

你对比特币有什么看法？你认为它在整个 2018 年会保持增值还是已经处于泡沫之中？请在下面留下您的评论。

*QR Code 是 DENSO WAVE INCORPORATED 在美国和其他国家的注册商标。*

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。