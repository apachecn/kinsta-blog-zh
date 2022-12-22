# 主顺风 CSS 及其即时(JIT)模式

> 原文：<https://kinsta.com/blog/tailwind-jit/>

实用优先框架帮助我们更快地设计网页，而 [Tailwind CSS](https://kinsta.com/blog/tailwind-css/) 已经成为最流行的框架之一。但是受欢迎不代表完美。

使用 Tailwind CSS 有一些挑战，比如在开发过程中有一个巨大的样式表，我们必须自己启用额外的变体，等等。在本教程中，我们将主要关注这些挑战的解决方案。

在本教程中，我们将讨论 Tailwind CSS 框架的一个非常重要的特性，称为实时编译器，通常称为 JIT 编译器。

我们将强调使用 Tailwind CSS JIT 编译器的特性和好处，如何启用它，并查看一些实际例子。

让我们开始吧。

## 什么是 Tailwind CSS JIT (Just-in-Time)编译器？

在我们谈论实时编译器之前，我们首先需要谈论一下 Tailwind CSS。

Tailwind CSS 是一个实用优先的 CSS 框架，具有一组预定义的 CSS 类，可以直接应用于我们的标记中，以加快网页的设计，并使用预定义的系统保持设计的一致性。





> 需要在这里大声喊出来。Kinsta 太神奇了，我用它做我的个人网站。支持是迅速和杰出的，他们的服务器是 WordPress 最快的。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![A picture of Phillip Stemann looking into the camera wearing a blue button down shirt](img/12b77bdcd297e9bf069df2f3413ad833.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Phillip Stemann</cite></footer>

[View plans](https://kinsta.com/plans/)

在 JIT 编译器发布之前，我们在安装后生成的 Tailwind CSS 文件大小通常高达 3 MB。但是，随着您继续配置和定制 Tailwind，文件会变得越来越大——在某些情况下，您最终会得到一个 15 MB 大的样式表。

尽管我们所有未使用的样式都会在生产过程中被清除，但在开发过程中却不是这样。对于 10 MB 甚至 20 MB 的样式表，我们肯定会遇到问题，导致我们的开发工具滞后。

使用 JIT 编译器，样式是在我们构建项目时生成的。这意味着只有您当前正在使用的实用程序类将被包含在样式表的大小中，而不是 Tailwind CSS 附带的所有实用程序类。


## 使用顺风 CSS JIT 模式的好处

在这一节中，我们将讨论使用 JIT 编译器的一些好处。它们包括:

1.  你的样式表在[开发](https://kinsta.com/knowledgebase/edit-wordpress-code/)和生产中是一样的。
2.  更快的构建时间。
3.  默认情况下，所有变体都是启用的。
4.  开发过程中的编译要快得多。
5.  仅生成使用过的样式。
6.  变体可以堆叠。
7.  改进的开发工具性能。

## 使用 Tailwind CSS JIT 编译器的缺点

根据 [JIT 编译器 GitHub 文档](https://github.com/tailwindlabs/tailwindcss-jit#known-limitations)，目前已知的限制有:

*   不支持高级 PurgeCSS 选项。
*   “您只能使用属于核心、由插件生成或在`@layer`规则中定义的`@apply`类。你不能`@apply`没有在`@layer`规则中定义的任意 CSS 类。”
*   仅支持 PostCSS 8。

`@apply`指令用于在自定义 CSS 中应用实用程序类。当我们定义自定义 CSS 样式，但更喜欢使用一些已经定义的实用程序类时，这是很有用的。下面是一个关于`@apply`指令如何工作的例子:

```
.my-custom-css {
  @apply text-green-500;
}
```

在上面的代码中，我们向自定义 CSS 类添加了绿色。绿色是使用顺风实用程序类应用的。

[Learn about a very important feature of the Tailwind CSS framework, known as the just-in-time compiler, in this helpful guide 🚀.Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Ftailwind-jit%2F&via=kinsta&text=Learn+about+a+very+important+feature+of+the+Tailwind+CSS+framework%2C+known+as+the+just-in-time+compiler%2C+in+this+helpful+guide+%F0%9F%9A%80.&hashtags=Tailwind%2CCSS)

## 如何启用顺风 CSS JIT 模式

请注意，在撰写本文时，Tailwind CSS 版本 3 已经发布，并且在安装 Tailwind CSS 时默认启用。下面关于启用 JIT 编译器的解释不适用于版本 3 和更高版本。本教程中涉及的所有其他示例都与版本 3 兼容。

启用 JIT 编译器非常容易。您所要做的就是通过添加 mode 属性来更新您的 tailwind.config.js 文件，该属性的值应该为“jit”。

您的 tailwind.config.js 应该是这样的:

```
module.exports = {
  mode: 'jit',
  purge: ['./public/*.html'],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
}
```

需要重点关注的一行是我们添加的部分:

```
mode: 'jit'

```

这使我们能够使用 JIT 编译器的特性。

完成后，您可以运行 build 命令并看到文件大小减小了。你只会看到你正在使用的样式。

随着文件大小的减小，开发和生产过程中的样式表将保持不变。开发人员工具滞后的可能性也将被降低到最小，并且当您构建项目时，您的代码会编译得更快。

接下来，我们将看到 JIT 编译器的一些实际应用。

 这使我们能够使用 JIT 编译器的特性。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

完成后，您可以运行 build 命令并看到文件大小减小了。你只会看到你正在使用的样式。

随着文件大小的减小，开发和生产过程中的样式表将保持不变。开发人员工具滞后的可能性也将被降低到最小，并且当您构建项目时，您的代码会编译得更快。

接下来，我们将看到 JIT 编译器的一些实际应用。

## 如何使用 Tailwind CSS JIT 编译器

在这一节中，我们将看到 JIT 编译器的一些实际例子。我们将从帮助我们扩展 Tailwind 设计系统的任意值开始。

### 任意值

可能会出现这样的情况，我们宁愿使用已经创建的设计系统之外的值。这些值可能是我们的颜色、填充、边距、宽度等等。

JIT 编译器使我们能够通过使用任意值来实现这一点。这些任意值允许我们打破设计系统，定义我们自己的自定义值。您会在以下语法中看到这些值:[300px]，[#FA8072]。

为了做到这一点，我们必须将值放在方括号中，这样 Tailwind 就知道我们正在设计系统中定义新的值。下面是一个例子:

```
<div class="mt-[300px] w-[500px]">
</div>
```

在上例中，我们使用了两个新值——300 px 和 500px，这两个值最初在设计系统中并不存在。在 JIT 编译器之前，您可能必须首先在 config.js 文件中定义这些值才能达到同样的效果。

下一个示例显示了如何将新颜色值定义为:

```
<p class="bg-[#FA8072] ">This paragraph has a salmon background </p>
```

这里，我们创建了一个带有鲑鱼色背景的段落。你不会看到一个写着 bg-salmon 的 Tailwind 实用程序类，但是我们可以用一个任意的值来定义它。

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

### 可堆叠的变体

使用 JIT 编译器，默认情况下所有变体都是启用的，所以您可以不用考虑使用 config.js 文件来启用任何变体。除此之外，变体可以被堆叠以实现令人敬畏的结果。

每个变量由冒号分隔。

这里有一个例子:

```
<button class="sm:dark:disabled:focus:hover:bg-blue-300">
```

上面的代码创建了一个关闭了 focus 属性的按钮，当鼠标悬停在按钮上时，按钮变成蓝色。

### 伪元素

JIT 编译器允许我们设计伪元素的样式。伪元素用于样式化元素的特定部分，例如样式化元素的第一个字母或者在元素之前/之后插入内容。

这里有几个例子:

```
<p class="first-letter:bg-green-600">
First letter will have a green color
</p>
```

在上面的例子中，第一个字母“M”是绿色的。

```
<p class="selection:bg-green-600">
Highlight this text to see a green color.
</p>
```

当您突出显示上面代码中的文本时，它会有一个绿色的背景色。

### 每边边框颜色

出于文件大小的考虑，这个特性最初被忽略了，但是随着 JIT 编译器的发布，这个特性发生了变化。我们可以给每个边框不同的颜色。

让我们来看一个例子:

```
<div class="border-2 border-t-red-400 border-r-blue-400 border-b-yellow-400 border-l-green-400">
</div>
```

我们给了 div 多种边框颜色——上边框是红色，右边框是蓝色，下边框是黄色，左边框是绿色。

## 顺风 CSS 版本 3 中的 JIT 模式

从 Tailwind CSS 版本 3 和更高版本开始，当我们安装 Tailwind CSS 时，JIT 编译器是默认启用的，因此我们不必担心修改 **tailwind.config.js** 文件中的任何内容。这使我们能够随时访问 JIT 编译器的所有特性。我们所要做的就是遵循当前版本的安装说明，然后我们就可以开始运行了。

[What's the JIT compiler... and how can it enhance your site? This guide has the answer ✅Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Ftailwind-jit%2F&via=kinsta&text=What%27s+the+JIT+compiler...+and+how+can+it+enhance+your+site%3F+This+guide+has+the+answer+%E2%9C%85&hashtags=Tailwind%2CCSS)

## 摘要

JIT 编译器将 Tailwind CSS 框架提升到了一个全新的水平。它的发布带来了新的有用的特性，让我们可以更好地使用这个框架。我们不再担心我们的文件太大，以至于我们的开发工具滞后，因为只有我们实际使用的样式会生成，所有的都在进行中。

我们看到了一些新功能的例子，如堆叠变体、使用伪元素设计元素样式、使用任意值来扩展我们的设计系统以及非常需要的功能——单独设计元素边框每一侧的样式的能力。我们还远远没有达到 Tailwind 的 JIT 功能的极限，所以您的下一步将是自己进行测试，并探索如何最好地将 JIT 的特性用于您自己的工作。

你利用 JIT 编译器构建了哪些很酷的东西？请在下面的评论中分享你的想法。

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。