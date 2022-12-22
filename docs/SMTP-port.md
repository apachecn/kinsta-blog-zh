# 如何选择正确的 SMTP 端口(端口 25、587、465 或 2525)

> 原文:# t0]https://kinta . com/blog/SMTP-port/

努力找出正确的 SMTP 端口来使用？去过那里，做过那个！

如果你使用苹果邮件或 Outlook 等电子邮件客户端发送电子邮件，该电子邮件客户端可能也使用 SMTP 将你的外发电子邮件上传到你的邮件服务器(*尽管这些客户端通常使用 IMAP 或 POP3 等其他协议将收到的电子邮件下载到应用程序*)。

此外，如果你正在为 WordPress 上的电子邮件投递能力而挣扎，解决这个问题的最好方法之一是使用[一个 SMTP 发送服务](https://kinsta.com/blog/free-smtp-server/)，比如 [SendGrid](https://kinsta.com/knowledgebase/sendgrid-wordpress/) 、 [Mailgun](https://kinsta.com/knowledgebase/mailgun-wordpress/) 或 [Google Workspace](https://kinsta.com/blog/google-workspace/) 。

但是如果你试图用你的电子邮件客户端或者 WordPress 网站设置 SMTP，你可能会遇到使用哪个 SMTP 端口的问题。

为了帮助你根据自己的需要选择正确的 SMTP 端口，我们将在这篇文章中深入探讨所有与 SMTP 端口相关的内容。

### 更喜欢看[视频版](https://www.youtube.com/watch?v=5lkLFGfb0G8)？



## 什么是 SMTP 端口？

SMTP 是简单邮件传输协议的缩写，是网络上电子邮件传输的标准协议。它是邮件服务器用来在互联网上发送和接收电子邮件的。









例如，当您发送电子邮件时，您的电子邮件客户端需要一种将电子邮件上传到发送邮件服务器的方法。然后，发送邮件服务器需要一种方法将您的电子邮件传输到收件人的接收邮件服务器。

邮件服务器很像网站服务器，虽然可能有一个用户友好的前端域名，但实际的通信是通过 IP 地址进行的，如 222.501.285.45(有关这是如何发生的更多信息，[请查看我们对域名系统或 DNS](https://kinsta.com/knowledgebase/what-is-dns/) 的介绍)。

“端口”是帮助计算机(*就像两台邮件服务器*)相互通信的另一种方式:

*   IP 地址标识一台计算机。
*   端口标识该计算机上运行的特定应用程序/服务，如 SMTP。

这里有一个更人性化的类比:

IP 地址是商业综合体的物理街道地址。端口是该业务组合中特定业务的号码。

如果您想要向业务交付一些东西，您不能仅仅将它提交给业务综合体，您还需要一种方法来确保它到达业务综合体内部的正确位置。

[IANA](https://www.iana.org/) ，负责全球 IP 地址分配和其他任务的组织，也负责注册包括 SMTP 在内的常用互联网服务的端口号。
T3】

## 为什么您的 SMTP 端口很重要？

如果你想连接到一个 SMTP 服务器(比如 [Gmail SMTP 服务器](https://kinsta.com/blog/gmail-smtp-server/)，你需要输入它的 IP 地址和端口号。

然而，有多种常见的 SMTP 端口(接下来会有更多介绍)，并且不是所有的端口都能在所有情况下工作。

例如，在邮件服务器之间移动邮件的标准 SMTP 端口 25 经常被 ISP 和云提供商(包括谷歌云平台，这是 Kinsta 使用的)阻止。

因此，如果您试图通过端口 25 连接到 SMTP 服务器，您会经常遇到问题，因为太多的服务阻塞了端口 25。

### 不同用途的不同端口

除了上述含义之外，不同的 SMTP 端口也有不同的用途。

SMTP 传输分为两个主要阶段:

*   **提交**–向外发邮件服务器提交电子邮件。例如，当您在 Apple Mail 中发送电子邮件时，该邮件需要提交到发送邮件服务器。
*   **中继**——在两台服务器之间中继消息的过程。因此，在电子邮件被“提交”到发送邮件服务器之后，发送邮件服务器将该消息“中继”到收件人的邮件服务器。

如果你正在设置你的电子邮件客户端或 WordPress 网站，你最关心的是这个过程中的“提交”部分。

虽然“中继”绝对是 SMTP 的重要组成部分，但大多数人并不需要配置自己的邮件服务器。

## SMTP 使用什么端口？

在现代网络上，没有单一的 SMTP 端口。相反，有四个常见的 SMTP 端口:

*   Twenty-five
*   Five hundred and eighty-seven
*   Four hundred and sixty-five
*   Two thousand five hundred and twenty-five

让我们过一遍。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

### 25 端口是做什么用的？

端口 25 早在 1982 年就建立了，这使它成为最古老的 SMTP 端口。

端口 25 仍然被认为是标准的 SMTP 端口，它主要用于 **SMTP 中继。**

然而，如果你用 SMTP 设置你的 WordPress 站点或电子邮件客户端，你通常不需要使用端口 25，因为大多数住宅互联网服务提供商和云主机提供商会屏蔽端口 25。

为什么？因为端口 25 通常被滥用来从被入侵的计算机发送垃圾邮件。

记住:SMTP 提交和中继是有区别的。因此，虽然 SMTP 端口 25 非常适合 SMTP 中继，但它不是 SMTP 提交的好选择。

### 587 端口是做什么用的？

端口 587 是现代 web 上 SMTP 提交的默认端口。虽然您可以使用其他端口进行提交(接下来将详细介绍)，但是您应该始终将端口 587 作为默认端口，并且只在情况需要时才使用不同的端口(比如您的主机出于某种原因阻塞了端口 587)。

587 端口还支持 [TLS](https://kinsta.com/knowledgebase/tls-vs-ssl/) ，这意味着你可以安全地提交邮件。

### 465 端口是做什么用的？

端口 465 最初是为 SMTPS 注册的(基于 SSL 的 SMTP)。在该功能中短暂停留后，端口 465 被重新分配用于不同的用途并被废弃。

尽管如此，许多 ISP 和云主机提供商仍然支持 SMTP 提交端口 465。

厌倦了你的 WordPress 站点缓慢的主机？我们提供超快的服务器和来自 WordPress 专家的 24/7 世界级支持。[查看我们的计划](https://kinsta.com/plans/?in-article-cta)

### 2525 端口是做什么用的？

端口 2525 不是正式的 SMTP 端口(由 IETF 或 IANA 认可)。然而，它仍然被广泛用作 SMTP 提交的端口 587 的替代，大多数 ISP 和云托管提供商都支持 SMTP 的端口 2525。

如果端口 587 被阻塞，端口 2525 是一个很好的选择。


## 您应该使用哪个 SMTP 端口？

我们在上面提到了这一点，但是让我们回顾一下如何选择正确的 SMTP 端口，因为做出正确的决定是很重要的。

如果你正在配置你的 WordPress 站点或电子邮件客户端通过 SMTP 发送电子邮件(提交)，你几乎总是想要使用**端口 587** 。同样，这是用于提交的默认 SMTP 端口，它支持通过 TLS 的安全传输。

如果端口 587 由于某种原因被阻塞，**端口 2525** 是一个常见的替代方案。同样，这不是一个官方认可的 SMTP 端口，但是它被大多数提供商普遍使用和支持。

虽然许多提供商仍然支持 SMTP 的**端口 465** ，但它不再是一个被接受的标准，在使用端口 465 之前，你应该总是尝试使用端口 587 和 2525。

最后，虽然**端口 25** 通常用于 SMTP 中继，但你不应该在设置电子邮件客户端或 WordPress 网站时使用它，因为大多数 ISP 和云主机提供商都会阻止端口 25。

### 在 Kinsta 可以使用哪些 SMTP 端口？

在 Kinsta，您可以使用端口:

*   Five hundred and eighty-seven
*   Four hundred and sixty-five
*   Two thousand five hundred and twenty-five

你不能使用端口 25，因为 Kinsta 使用谷歌云平台基础设施，而[谷歌云平台屏蔽了端口 25](https://cloud.google.com/compute/docs/tutorials/sending-mail/) 。

[What are SMTP ports? Why are they so important? Dive into the nitty-gritty of SMTP ports and learn wich one you should use! 💌📤Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Fsmtp-port%2F&via=kinsta&text=What+are+SMTP+ports%3F+Why+are+they+so+important%3F+Dive+into+the+nitty-gritty+of+SMTP+ports+and+learn+wich+one+you+should+use%21+%F0%9F%92%8C%F0%9F%93%A4&hashtags=smtp%2Cemailtips)

## 摘要

SMTP 在互联网上传输电子邮件的过程中扮演着重要的角色。

为了提高你的 WordPress 站点的[交易邮件](https://kinsta.com/help/transactional-email/)的可送达性，你可以配置你的 WordPress 站点通过 SMTP 发送邮件。此外，如果你使用苹果邮件或 [Outlook](https://kinsta.com/blog/outlook-smtp-settings/) 这样的电子邮件客户端，你的电子邮件客户端会使用 SMTP 向邮件服务器提交发送的电子邮件。

为了将你的 WordPress 站点或电子邮件客户端连接到 SMTP 服务器，你需要输入一个特定的 SMTP 端口。

有四种常见的 SMTP 端口:

*   Twenty-five
*   Five hundred and eighty-seven
*   Four hundred and sixty-five
*   Two thousand five hundred and twenty-five

端口 25 通常用于 SMTP 中继，但是您不应该将它用于 SMTP 提交，因为大多数提供商都会阻止它。

如果你想配置你的 WordPress 站点或电子邮件客户端使用 SMTP，你应该首先选择端口 587，因为它是 SMTP 提交的标准端口。

如果 587 端口不行，你可以试试 2525 端口。虽然它不是官方认可的 SMTP 端口，但它得到了广泛的支持，并支持 TLS 进行安全传输。

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。