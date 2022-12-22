# CPU 漏洞 Kinsta 客户需要了解的信息

> 原文：<https://kinsta.com/blog/cpu-vulnerabilities/>

一月的第一周，关于新发现的 CPU 漏洞的新闻开始传播。这影响了数百万设备，不仅是 Google Cloud 和 AWS 等云计算平台，甚至是您自己的台式机、笔记本电脑和移动设备。在 Kinsta，安全性对我们来说至关重要，因此我们希望让您了解这将如何影响我们的服务和平台。更多细节见下文。

## CPU 漏洞

去年 6 月，Google Project Zero 安全团队发现了影响现代 CPU 的漏洞，包括来自 **AMD、ARM 和英特尔**的漏洞。谷歌原定于 2018 年 1 月 9 日披露这一消息，但媒体实际上很早就开始泄露相关信息，所以他们现在已经提前发布了有关安全缺陷的全部细节。

以下是 Google [对](https://security.googleblog.com/2018/01/todays-cpu-vulnerability-what-you-need.html) it 的总结:

> 我们已经发现，CPU 数据缓存计时可能被滥用，从错误推测的执行中有效地泄漏信息，导致(在最坏的情况下)在各种上下文中跨越本地安全边界的任意虚拟内存读取漏洞。"

到目前为止，该问题有三种已知的变体，也称为 Spectre 和 Meltdown:

*   变体 1:边界检查旁路( [CVE-2017-5753](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5753)
*   变式 2:分支目标注入( [CVE-2017-5715](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5715)
*   变体 3:流氓数据缓存加载( [CVE-2017-5754](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5754)

通俗地说，这些不仅仅是安全缺陷，还会对性能产生影响。阅读来自零项目团队的这篇[文章中的更多详细信息。谷歌还发布了一个帮助页面，解释](https://googleprojectzero.blogspot.com/2018/01/reading-privileged-memory-with-side.html)[哪些产品和服务受到影响](https://support.google.com/faqs/answer/7622138)。

## 这对金斯塔有什么影响

关于金斯塔，有两个不同的层面受到影响。首先，我们的**主机**运行在谷歌计算引擎上，这些**已经被更新**以防止所有已知的漏洞。Google 使用他们的实时虚拟机迁移技术来执行更新，没有用户影响，没有强制维护窗口，也不需要重启。

第二，在我们主机上的虚拟机上运行的所有操作系统也需要打补丁。我们在 Kinsta 使用 Ubuntu，他们已经宣布他们正在[加快补丁的发布日期](https://wiki.ubuntu.com/SecurityTeam/KnowledgeBase/SpectreAndMeltdown)。由于这种威胁的严重性，我们正在密切关注这些更新。~~一旦更新可用，我们将立即应用它们~~。**我们所有的虚拟机都已经更新，现在受到幽灵和熔毁的保护。**

## 你应该做什么

关于你在 Kinsta 的 WordPress 站点，你不需要做任何事情。就您自己的设备而言，以下是一些需要注意的事项:

*   如果你用的是个人电脑，微软正在为他们的操作系统推出一个紧急更新。
*   据开发者亚历克斯·约内斯库称，[苹果显然已经在 MAC OS High Sierra 10 . 13 . 2(12 月 6 日发布)中防止了崩溃。他们还在 1 月 8 日发布了一个](https://twitter.com/aionescu/status/948609809540046849)[补充更新](https://support.apple.com/en-us/HT208397)，以减轻幽灵的影响。
*   Linux 开发人员正在努力在新的内核更新中解决这个问题。
*   微软已经用 [KB4056890](https://blogs.windows.com/msedgedev/2018/01/03/speculative-execution-mitigations-microsoft-edge-internet-explorer/#FdYxYwmOWVAdCZzr.97) 为 Internet Explorer 和 Edge 打了补丁。
*   Mozilla Firefox [已经在其最新版本(57)中包含了一个补丁](https://blog.mozilla.org/security/2018/01/03/mitigations-landing-new-class-timing-attack/)。
*   谷歌正在推出 Chrome 64 版本的补丁。

如果您是 Kinsta 的现有客户，并且对这些最近的安全缺陷有任何其他问题，请随时[联系我们的支持团队](https://kinsta.com/help/wordpress-support-ticket/)或在下面给我们留下评论。

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。