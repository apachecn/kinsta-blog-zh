# 用符号链接管理 WordPress 开发

> 原文：<https://kinsta.com/blog/managing-wordpress-development-with-symlinks/>

在这篇文章中，我将向你展示一个很好的方法来共享一个插件或主题的单个实例。

*   [什么是符号链接](#what-is-a-symlink)
*   [Symlink 常见使用案例](#symlink-common-use-cases)
*   [创建符号链接](#creating-a-symlink)

## 什么是符号链接

符号链接是一种特殊的文件，实际上是对另一个文件或文件夹的引用。如果你是一个 Windows 用户，你可能已经使用了桌面快捷方式，这是一种符号链接，因为它们指向你系统中其他地方的文件。

对我们来说，关键是它们也可以指向文件夹。从 [WordPress 3.9](https://make.wordpress.org/core/2014/04/14/symlinked-plugins-in-wordpress-3-9/) 开始，插件和主题的符号链接已经被允许，这使得我们可以将它们存储在其他地方，并与我们的安装挂钩。

## Symlink 常见使用案例

让我们假设您有一个带有根目录的[本地主机设置](https://kinsta.com/knowledgebase/what-is-localhost/)。每个目录都是一个独立的 WordPress 安装。通常你会在所有的插件中安装你的新插件。在一个系统中发现的错误需要在所有地方进行修改，这使得整个过程变得漫长且容易出错。

使用符号链接，你可以将你的插件和主题保存在一个单独的文件夹中，并且——使用符号链接——你可以将它指向你的每一个安装。每个安装使用相同的文件，使修改和维护变得轻而易举。

如果你在同一个服务器上有多个域，你可以使用同样的技巧。只要您网站的文件占用相同的文件系统，并且您的环境允许符号链接(大多数都允许)，您就可以使用这种方法。

我最喜欢用这种方法处理 Github 仓库中的主题和插件。我更喜欢使用 git T1 作为我的 T2 版本控制系统 T3，我的项目有一个将实际的主题/插件放在子目录中的结构。

这意味着我不能在 wp-content 文件夹中原样使用该文件夹。通常，我必须手动将更改复制粘贴到回购协议中，或者更改回购协议的结构。有了符号链接，我就可以用符号链接我需要的文件夹。


## 创建符号链接

在基于 Windows 和 Linux 的系统(如 OSX)上创建符号链接的过程是相同的，但语法略有不同。创建它们时，您需要指定符号链接和目标的位置。

在我们的例子中，符号链接的位置是主题或插件目录中的一个文件夹。目标将指向包含实际插件/主题文件的目录。

让我们看一个例子，在这个例子中，我们使用一个符号链接来链接到一个单独文件夹中的插件。在这个例子中，我们项目的根目录包含多个 WordPress 安装和一个包含插件和主题的项目目录。

### Windows 上的符号链接

让我们假设 web 项目的根目录在 C:/websites 中。你需要打开命令提示符，导航到一个 WordPress 安装程序的插件文件夹，在该文件夹中发出以下命令:

```
mklink C:\websites\projects\my-plugin-github\my-plugin\trunk my-plugin
```

这个命令将在你的插件文件夹中创建一个`my-plugin`文件夹，这个文件夹将指向位于`C:\websites\projects\my-plugin-github\my-plugin\trunk`的文件夹。当加载插件列表和处理代码时，WordPress 会跟随这个符号链接，让它看起来像你有一个普通的插件。
T3】

### OSX 和 Linux 上的符号链接

让我们假设 web 项目的根目录在/Users/danielpataki/websites 中。你需要打开终端，导航到 WordPress 安装程序的插件文件夹，在该文件夹中发出以下命令:

```
ln -s /Users/danielpataki/websites/projects/my-plugin-github/my-plugin/trunk my-plugin
```

这个命令将在你的插件文件夹中创建一个`my-plugin`文件夹，这个文件夹将指向位于`/Users/danielpataki/websites/projects/my-plugin-github/my-plugin/trunk`的文件夹。当加载插件列表和处理代码时，WordPress 会跟随这个符号链接，让它看起来像你有一个普通的插件。

## 摘要

你可以根据需要在同一个系统上为你所有的 WordPress 项目重复这个过程。在一天结束时，你所有的安装将使用相同的文件，所以你可以修复一个错误，然后看到它从所有的 WordPress 安装中消失。

我在日常编程中经常使用这种方法。如果你也这样做，并且你有一些锦囊妙计，或者你有更好的做事方法，请在下面的评论中告诉我们！

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。