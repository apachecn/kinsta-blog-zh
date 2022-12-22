# WordPress 6.1 的新功能:流畅的排版，改进的模板系统，新的网站健康检查，等等！

> 原文：<https://kinsta.com/blog/wordpress-6-1/>

WordPress 6.1《米莎》已于[2022 年 11 月 1 日](https://wordpress.org/news/2022/11/misha/)发布。今年的第三个主要版本是继 5 月 24 日发布的 [WordPress 6.0 Arturo](https://kinsta.com/blog/wordpress-6-0/) 和 1 月 25 日发布的 [WordPress 5.9 Josephine](https://kinsta.com/blog/wordpress-5-9/) 之后。

正如往常一样，新的 WordPress 版本带来了新的特性、改进和 bug 修复，这些都来自于核心的 Gutenberg 插件的最新版本。WordPress 6.1 也不例外，从 13.1 到 14.1，11 个版本的[古腾堡插件](https://kinsta.com/blog/gutenberg-wordpress-editor/)被合并到核心中。

在本帖中，我们将一窥幕后，介绍 WordPress 新的主要版本带来的激动人心的新功能。

Matias Ventura 在 6.1 的[路线图中给了我们一些见解，他说 6.1 的目标是完善 5.9 和 6.0 引入的经验，并在我们接近古腾堡路线图的第 3 阶段时修复一些东西。](https://make.wordpress.org/core/2022/06/04/roadmap-to-6-1/)

[Want to get a peek behind the curtain at what's new with WordPress 6.1? ✨ Keep reading... 👀Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fbit.ly%2F3AQlbMz&via=kinsta&text=Want+to+get+a+peek+behind+the+curtain+at+what%27s+new+with+WordPress+6.1%3F+%E2%9C%A8+Keep+reading...+%F0%9F%91%80&hashtags=WordPress%2CGutenberg)

**1。模板编辑器改进**:主要的新特性之一是[模板编辑器](https://github.com/WordPress/gutenberg/issues/41241)。WordPress 6.1 应该引入浏览、可视化和编辑网站结构的能力。

**2。模板模式**:目标是[在模板和页面创建中赋予块模式一个核心角色](https://github.com/WordPress/gutenberg/issues/38529)，使它们适应[定制的文章类型](https://kinsta.com/blog/wordpress-custom-post-types/)和块类型，增强锁定功能，改进保存的模式管理等。

**3。全球风格和区块&设计工具** : WordPress 6.1 将允许管理网页字体，实现响应排版，并扩展区块可用的工具集。

也就是说，让我们仔细看看 WordPress 6.1 的一些最强大的特性:









## 流畅的排版和间距

WordPress 6.1 [通过](https://make.wordpress.org/core/2022/08/04/whats-new-in-gutenberg-13-8-3-august/#fluid-typography-support) [`calc`](https://developer.mozilla.org/en-US/docs/Web/CSS/calc) / [`clamp`](https://developer.mozilla.org/en-US/docs/Web/CSS/clamp) CSS 函数增加了对[流体排版](https://make.wordpress.org/core/2022/10/03/fluid-font-sizes-in-wordpress-6-1/)的支持。

表达式[流体排版](https://make.wordpress.org/core/2022/05/27/block-font-sizes-and-fluid-typography/)描述了文本适应视口宽度的能力，平滑地从最小宽度缩放到最大宽度。

这与您使用媒体查询所能实现的有所不同，因为媒体查询允许主题根据特定的视口大小来调整文本大小，但在不同的值之间不做任何事情。

一些主题已经支持流畅的排版。[二十二十二](https://kinsta.com/blog/twenty-twenty-two-theme/)举例来说，使用 CSS `clamp()`函数的几种字体大小。例如:

```
"settings": {
	...
	"custom": {
		"spacing": {
			"small": "max(1.25rem, 5vw)",
			"medium": "clamp(2rem, 8vw, calc(4 * var(--wp--style--block-gap)))",
			"large": "clamp(4rem, 10vw, 8rem)",
			"outer": "var(--wp--custom--spacing--small, 1.25rem)"
		},
		"typography": {
			"font-size": {
				"huge": "clamp(2.25rem, 4vw, 2.75rem)",
				"gigantic": "clamp(2.75rem, 6vw, 3.25rem)",
				"colossal": "clamp(3.25rem, 8vw, 6.25rem)"
			}
		}
	}
}
```

正如您在上面的代码中看到的，每个字体大小都使用了浮动字体大小值。

现在，从 WordPress 6.1 开始，通过声明新的`typography.fluid`属性，主题能够[自动生成流畅的字体大小](https://make.wordpress.org/core/2022/05/27/block-font-sizes-and-fluid-typography/)，如下所示:

```
"settings": {
	....
	"typography": {
		"fluid": true,
		"fontSizes": [
			{
				"size": "2rem",
				"fluid": {
					"min": "2rem",
					"max": "2.5rem"
				},
				"slug": "medium",
				"name": "Medium"
			}
		]
}
```

使用`typography.fluid`和`typography.fontSizes[].fluid`，使用以下[公式](https://richtabor.com/fluid-typography-block-themes/)自动计算每个字体大小的值:

```
--wp--preset--font-size--{slug}: clamp({fluid.min}, {fluid.min} + ((1vw - 0.48rem) * 1.592), {fluid.max});
```

例如:

```
--wp--preset--font-size--large: clamp(2rem, 2rem + ((1vw - 0.48rem) * 1.592), {2.5rem});
```

请注意，在撰写本文时，流畅的排版是一个实验性的特性。你可以在[块支持中深入研究技术细节:添加流体排版](https://github.com/WordPress/gutenberg/pull/39529)。

> 流畅的排版是建立现代网站的一个重大改进。我们刚刚更新了 [@frostwp](https://twitter.com/frostwp?ref_src=twsrc%5Etfw) 来包含这个功能。这里有一篇来自 [@richard_tabor](https://twitter.com/richard_tabor?ref_src=twsrc%5Etfw) 的精彩文章，探讨了它是什么以及它为什么重要。[https://t.co/Bq5YuHX3wi](https://t.co/Bq5YuHX3wi)
> 
> —布莱恩·加德纳(@ bgardner)[2022 年 8 月 8 日](https://twitter.com/bgardner/status/1556636761228513283?ref_src=twsrc%5Etfw)