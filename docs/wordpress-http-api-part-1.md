# HTTP 和 WordPress HTTP API 指南——第 1 部分

> 原文：<https://kinsta.com/blog/wordpress-http-api-part-1/>

在准备过程中，我想我应该看看 HTTP 一般是如何工作的，以及如何使用原生 WordPress 函数来工作，开放你的产品与 Twitter、脸书、Mailchimp 和其他各种工具的集成。

在本文(第 1 部分，共 2 部分)中，我将向您展示 HTTP 请求的基础知识、它们的结构、它们包含的信息以及如何理解这些信息。在第二部分，我们将通过 WordPress 把我们的知识付诸实践。

*   [什么是 HTTP](#what-is-http)
*   [HTTP 请求基础知识](#http-request-basics)
*   [方法名称](#method-names)
*   [HTTP 的结构](#structure-of-http)
*   [使用 HTTP](#using-http)

## 什么是 HTTP

HTTP 是当今网络上使用的主要协议，它代表**超文本传输协议**，负责向你显示 HTML、图像等等。HTTP 客户端——就像你的浏览器——发送**请求**到 HTTP 服务器，服务器发回**响应**。

例如，如果你将浏览器指向[Kinsta.com](https://kinsta.com)，你就向 Kinsta 的服务器发送了一个请求。服务器读取您的请求，判断您需要什么(我们将很快讨论这是如何发生的),并发回包含页面 HTML 代码的响应。您的浏览器读取响应并在屏幕上显示 HTML 代码。
T3】

## HTTP 请求基础

客户端和服务器之间的任何事务都是从 HTTP 请求开始的。请求的两个最重要的部分是方法名和被请求资源的 URL。先说后者。

### 资源

资源是可以用 URL 标识的一段数据。例如:`http://myblog.com/my-awesome-article`可能会返回一个 HTML 文件——呈现您的精彩文章所需的代码。

## 方法名称

方法名称标识您想要对资源执行的操作类型。浏览器几乎总是使用 GET，这表示您想要检索资源。

其他方法包括创建新项目的 POST、更新项目的 PUT、删除项目的 DELETE 和抓取[头信息](https://kinsta.com/blog/cannot-modify-header-information-headers-already-sent-by/)的 HEAD。

这些方法名和 URL 一起提供了 REST APIs 的基础。您可以向`/article/4`发送 get 请求来检索文章 4。您还可以发送一个 PUT 请求和一些数据来修改它，或者发送一个 DELETE 请求来删除它。


## HTTP 的结构

从结构的角度来看，HTTP 请求和响应非常相似。每一个都有四个不同的部分:

*   请求和响应的初始行不同
*   包含请求或响应信息的可选标头
*   空行
*   可选正文内容

### 1.初始线

对于**请求**，初始行包含三条信息:方法名、资源路径和使用的 HTTP 版本。下面是它可能的样子:

```
GET /users/4 HTTP/1.1
```

注意，这一行包含的是**本地相对路径**而不是完整的 URL。基本 URL 是在头(主机头)中发送的，我们很快就会看到头。

**响应**也包含三条信息:HTTP 版本、状态代码和描述状态代码的原因。

```
HTTP/1.1 302 Moved Temporarily
```

要获得所有状态代码的列表以及每个代码的一点信息，请看一下 [HTTP 状态代码](https://kinsta.com/blog/http-status-codes/)规范，这一点非常清楚。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

### 2.头球

头实质上是信息的名称-值对。前面提到的`Host`头就是一个很好的例子，事实上，它是 HTTP 1.1 中唯一需要的头。标题给你更多的控制和更多的信息。

`Accept`头让您指定请求中允许的内容类型。`Accept-Language`标题让您控制您愿意接受的内容的语言。两者都是[内容协商](https://en.wikipedia.org/wiki/Content_negotiation)的形式。

当使用 API 访问只有授权的操作(比如删除一条 Tweet 或访问您的用户帐户)时，您会大量使用`Authorization`头。

### 3.身体

主体是返回资源的地方，或者是遇到错误时给出进一步解释的地方。您可以使用您选择的语言从主体中读取数据并显示出来，或者在内部使用它来处理错误。

## 使用 HTTP

我发现在协商第三方 API 的文档时，理解 HTTP 非常有帮助。使 HTTP 的使用变得复杂的是，你通常在一种[编程语言](https://kinsta.com/blog/scripting-languages/)中使用它，这意味着你需要熟悉该语言如何实现 HTTP 以及 HTTP 本身。

一旦您发出请求，您将需要阅读响应，知道从中获取什么信息，甚至可能通过一些函数运行响应，将它转换成您需要的格式。一旦你有了这些信息，你就可以显示它，把它保存在数据库中，或者对它进行操作。

HTTP 本身并不难，但是除了发出/接收请求之外，您必须执行的任务可能会很快增加，从而将 HTTP 的简单性掩盖在复杂性之中。此外，许多 API 会要求您进行身份验证，这又增加了一层。

### 卷曲

cURL 是与 HTTP 交互的一种方式，但是相当复杂。它可以从终端使用，但是 PHP 也支持 cURL。要获取 URL 的内容，您可以在终端中使用以下命令。

```
curl http://kinsta.com
```

问题是 cURL 在终端中的使用会变得非常复杂。要仅查看标题信息，您需要使用以下表单:

```
curl -s -D - http://danielpataki.com -o /dev/null
```

您可以查看所有参数的列表，但是您可能会在您的 web 应用程序中使用 cURL，所以让我们看看 PHP 中的 cURL，下面是如何获取同一页面的内容:

```
$ch = curl_init();
$timeout = 5;
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, $timeout);
$data = curl_exec($ch);
curl_close($ch);
echo $data;
```

这仍然有点笨拙，但是通过使用 [PHP 指南](http://php.net/manual/en/book.curl.php)你可以弄清楚什么是什么。
T3】

### 使用 WordPress

cURL 很棒，但是添加头和处理返回的信息并不像您习惯的那样容易，如果您一直在使用编码良好的 PHP 类和函数的话。幸运的是，WordPress 的 HTTP API 覆盖了我们。我们将在下一篇文章中详细讨论，现在，这里有一个 WordPress 原生函数的例子，包括添加的标题:

```
$request = wp_remote_get('https://api.twitter.com/1.1/statuses/user_timeline.json?screen_name=kinsta, array(
    'headers' => array(
        'Authorization' => 'Bearer ' . $token,
    ),
));
```

## 摘要

HTTP 是我们在网络上所做的一切的基础，知道请求和响应中发生了什么给了我们强大的故障排除能力，并允许我们更好地控制我们的应用程序。

通过掌握 HTTP 基础知识，您将能够更快更好地利用外部 API，确切地知道如何处理 API 指南中提供给您的信息。

在本系列的下一篇文章中，我将介绍如何使用 WordPress 处理 HTTP 数据，以及如何轻松地将 WordPress 与第三方服务连接起来。

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。