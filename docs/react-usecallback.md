# 学习如何驯服 React 的 useCallback 钩子

> 原文:# t0]https://kinta . com/blog/react-usecallback/

[React.js 近年来变得广泛流行](https://kinsta.com/blog/web-development-tools/#27-reactjs)已经不是什么秘密了。它现在是许多互联网最杰出的玩家的首选 [JavaScript 库](https://kinsta.com/blog/javascript-libraries/#reactjs)，包括脸书和 WhatsApp。

其兴起的一个主要原因是[版本 16.8](https://github.com/facebook/react/blob/main/CHANGELOG.md#1680-february-6-2019) 中钩子的引入。React 挂钩允许您在不编写类组件的情况下利用 React 功能。现在，带挂钩的功能组件已经成为开发人员使用 React 的首选结构。

在这篇博文中，我们将更深入地探讨一个特定的挂钩——`useCallback`——因为它触及了函数式编程的一个基础部分，即记忆化。您将确切地知道如何以及何时利用`useCallback`钩子，并充分利用它的性能增强功能。

准备好了吗？让我们开始吧！

## 什么是记忆化？

记忆化是指一个复杂函数存储它的输出，以便下次用相同的输入调用它。它类似于缓存，但是在更局部的层次上。它可以跳过任何复杂的计算，并更快地返回已经计算过的输出。

这对内存分配和性能有很大的影响，而这种压力正是`useCallback`钩子要缓解的。


### React 的 useCallback 与 useMemo

在这一点上，值得一提的是`useCallback`与另一个名为`useMemo`的钩子很好地配对。我们将讨论这两个问题，但在这一部分，我们将把重点放在`useCallback`作为主要话题。





> 需要在这里大声喊出来。Kinsta 太神奇了，我用它做我的个人网站。支持是迅速和杰出的，他们的服务器是 WordPress 最快的。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![A picture of Phillip Stemann looking into the camera wearing a blue button down shirt](img/12b77bdcd297e9bf069df2f3413ad833.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Phillip Stemann</cite></footer>

[View plans](https://kinsta.com/plans/)

关键区别在于`useMemo`返回一个记忆化的值，而`useCallback`返回一个记忆化的函数。这意味着`useMemo`用于存储计算值，而`useCallback`返回一个函数，您可以稍后调用。

这些钩子会给你一个缓存的版本，除非它们的依赖关系(比如状态或者属性)发生了变化。

让我们来看看这两个函数的作用:

```
import { useMemo, useCallback } from 'react'
const values = [3, 9, 6, 4, 2, 1]

// This will always return the same value, a sorted array. Once the values array changes then this will recompute.
const memoizedValue = useMemo(() => values.sort(), [values])

// This will give me back a function that can be called later on. It will always return the same result unless the values array is modified.
const memoizedFunction = useCallback(() => values.sort(), [values])
```

上面的代码片段是一个虚构的例子，但是显示了两个回调之间的区别:

1.  `memoizedValue`会变成数组`[1, 2, 3, 4, 6, 9]`。只要 values 变量保持不变，`memoizedValue`也会保持不变，并且永远不会重新计算。
2.  `memoizedFunction`将是一个返回数组`[1, 2, 3, 4, 6, 9]`的函数。

这两个回调的好处在于它们被缓存起来，并一直存在，直到依赖数组发生变化。这意味着在渲染时，它们不会被垃圾收集。

[React.js is now the JavaScript library of choice for many of the internet's biggest players, including Facebook and WhatsApp. 😲 Learn more in this guide ⬇️Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Freact-usecallback%2F&via=kinsta&text=React.js+is+now+the+JavaScript+library+of+choice+for+many+of+the+internet%27s+biggest+players%2C+including+Facebook+and+WhatsApp.+%F0%9F%98%B2+Learn+more+in+this+guide+%E2%AC%87%EF%B8%8F&hashtags=JavaScript%2CReactjs)

## 渲染和反应

为什么在反应时记忆很重要？

它与 React 如何渲染组件有关。React 使用存储在内存中的虚拟 DOM 来比较数据并决定更新什么。

虚拟 DOM 有助于对性能做出反应，并保持您的应用程序快速运行。默认情况下，如果组件中的任何值发生变化，整个组件都将重新呈现。这使得 React 对用户输入作出“反应”,并允许屏幕在不重新加载页面的情况下更新。

您不想呈现您的组件，因为更改不会影响该组件。这就是通过`useCallback`和`useMemo`的记忆派上用场的地方。

当 React 重新呈现组件时，它还会重新创建您在组件内部声明的函数。

注意，当比较一个函数和另一个函数的相等性时，它们总是假的。因为一个函数也是一个对象，它只会等于它自己:

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

```
// these variables contain the exact same function but they are not equal
const hello = () => console.log('Hello Matt')
const hello2 = () => console.log('Hello Matt')

hello === hello2 // false
hello === hello // true
```

换句话说，当 React 重新呈现组件时，它将看到组件中声明为新函数的任何函数。

这在大多数情况下是没问题的，简单的函数很容易计算，不会影响性能。但是在其他时候，当你不希望这个函数被看作是一个新函数时，你可以依靠`useCallback`来帮助你。

你可能会想，“什么时候我不希望一个函数被看作是一个新函数？”嗯，在某些情况下`useCallback`更有意义:

1.  您正在将函数传递给另一个同样被记忆的组件(`useMemo`)
2.  你的函数需要记住一个内部状态
3.  你的函数依赖于另一个钩子，例如`useEffect`

## React useCallback 的性能优势

当`useCallback`被恰当地使用时，它可以帮助加速你的应用程序，并防止组件在不需要的时候被重新渲染。

比方说，您有一个获取大量数据的组件，它负责以[图表或](https://kinsta.com/blog/wordpress-charts/)图形的形式显示这些数据，如下所示:



![A colorful bar graph comparing the overall transaction time of PHP, MySQL, Reddis, and external (other) in milliseconds.](img/1eb05743df38104a927e3f28654de5c2.png)

使用 React 组件生成的条形图。





假设数据可视化组件的父组件重新渲染，但更改的属性或状态不会影响该组件。在这种情况下，您可能不想或不需要重新渲染它并重新提取所有数据。避免这种重新渲染和重新提取可以节省用户的带宽，并提供更流畅的用户体验。

## React useCallback 的缺点

虽然这个挂钩可以帮助您提高性能，但是它也有缺陷。使用`useCallback`(和`useMemo`)之前要考虑的一些事情是:

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

*   **垃圾收集:**其他没有被内存化的函数将被 React 丢弃以释放内存。
*   **内存分配:**与垃圾收集类似，内存化的函数越多，需要的内存就越多。另外，每次使用这些回调时，React 内部都会有一堆代码需要使用更多的内存来为您提供缓存的输出。
*   **代码复杂度:**当你开始在这些[钩子](https://kinsta.com/blog/wordpress-hooks/)中包装函数时，你立刻增加了代码的复杂度。现在需要更多地理解为什么要使用这些钩子，并确认它们的使用是正确的。

意识到上面的陷阱可以让你省去自己碰到它们的麻烦。当考虑使用`useCallback`时，要确保性能优势大于缺点。

## React 回调示例

下面是一个带有按钮组件和计数器组件的简单设置。计数器有两种状态，并呈现出两个按钮组件，每一个都将更新计数器组件状态的一个单独部分。

按钮组件接受两个属性:`handleClick`和名称。每次按钮被渲染，它会[记录到控制台](https://kinsta.com/blog/inspect-element/#touring-the-inspect-element-panel)。

```
import { useCallback, useState } from 'react'

const Button = ({handleClick, name}) => {
  console.log(`${name} rendered`)
  return <button onClick={handleClick}>{name}</button>
}

const Counter = () => {

console.log('counter rendered')
  const [countOne, setCountOne] = useState(0)
  const [countTwo, setCountTwo] = useState(0)
  return (
    <>
      {countOne} {countTwo}
      <Button handleClick={() => setCountOne(countOne + 1)} name="button1" />
      <Button handleClick={() => setCountTwo(countTwo + 1)} name="button1" />
    </>
  )
}
```

在本例中，无论何时单击任一按钮，您都会在控制台中看到以下内容:

```
// counter rendered

// button1 rendered
// button2 rendered
```

现在，如果我们将`useCallback`应用于我们的`handleClick`函数，并将我们的按钮包装在`React.memo`中，我们可以看到`useCallback`为我们提供了什么。`React.memo`类似于`useMemo`，允许我们记忆一个组件。

```
import { useCallback, useState } from 'react'

const Button = React.memo(({handleClick, name}) => {
  console.log(`${name} rendered`)
  return <button onClick={handleClick}>{name}</button>
})

const Counter = () => {
  console.log('counter rendered')
  const [countOne, setCountOne] = useState(0)
  const [countTwo, setCountTwo] = useState(0)
  const memoizedSetCountOne = useCallback(() => setCountOne(countOne + 1), [countOne)
  const memoizedSetCountTwo = useCallback(() => setCountTwo(countTwo + 1), [countTwo])
  return (
    <>
        {countOne} {countTwo}
        <Button handleClick={memoizedSetCountOne} name="button1" />
        <Button handleClick={memoizedSetCountTwo} name="button1" />
    </>
  )
}
```

现在，当我们单击任一按钮时，我们将只看到我们单击以登录控制台的按钮:

```
// counter rendered

// button1 rendered

// counter rendered

// button2 rendered
```

我们已经对按钮组件应用了记忆化，传递给它的属性值是相等的。这两个`handleClick`函数被缓存，并将被 React 视为同一个函数，直到依赖数组中某项的值发生变化(例如`countOne`、`countTwo`)。

准备好学习如何以及何时使用 useCallback 钩子，以及如何充分利用它的性能增强功能了吗？💪从这里开始！🚀 点击推文


## 摘要

尽管`useCallback`和`useMemo`很酷，但是记住它们有特定的用例——你不应该用这些钩子包装每一个函数。如果函数在计算上很复杂，那么传递给内存化组件的另一个钩子或 prop 的依赖关系是您可能想要使用`useCallback`的好指标。

我们希望这篇文章能够帮助您理解这个高级的 React 功能，并帮助您在使用函数式编程的过程中获得更多的信心！

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。