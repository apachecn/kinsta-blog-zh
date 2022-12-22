# 性能 API 简介

> 原文：<https://kinsta.com/blog/performance-api/>

[Performance API](https://developer.mozilla.org/docs/Web/API/Performance_API) 测量真实用户设备和网络连接上的实时 web 应用程序的响应性。它可以帮助您识别客户端和服务器端代码中的瓶颈:

*   **用户计时:**自定义测量客户端 [JavaScript 函数](https://kinsta.com/knowledgebase/what-is-javascript/)性能
*   **绘制时间:**浏览器渲染指标
*   **资源计时:**加载性能资产和 Ajax 调用
*   **导航时间:**页面加载指标，包括重定向、DNS 查找、DOM 就绪等

API 解决了与典型性能评估相关的几个问题:

1.  开发人员经常在连接到高速网络的高端电脑上测试应用程序。DevTools 可以模拟较慢的设备，但当大多数客户端运行的是连接到机场 WiFi 的两年前的手机时，它不会总是突出现实世界的问题。
2.  第三方选项如[谷歌分析](https://kinsta.com/blog/how-to-use-google-analytics/)经常被屏蔽，导致结果和假设失真。在某些国家，您可能还会遇到隐私问题。
3.  性能 API 可以比 [`Date()`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date) 等方法更准确地度量各种度量。

[想了解有关使用性能 API 的更多信息吗？👀从这里开始...🚀 点击发布推文](https://twitter.com/intent/tweet?url=https%3A%2F%2Fbit.ly%2F3dl8OA3&via=kinsta&text=Want+to+learn+more+about+using+the+Performance+API%3F+%F0%9F%91%80+Start+here...+%F0%9F%9A%80&hashtags=API%2CWebDev)
以下章节描述了您可以使用性能 API 的方式。建议了解一些 JavaScript 和[页面加载指标](https://kinsta.com/blog/website-speed-test/)的知识。

## 性能 API 可用性

大多数现代浏览器都支持性能 API——包括 IE10 和 IE11(甚至 IE9 也有有限的支持)。您可以使用以下方法检测 API 的存在:





> Kinsta 把我宠坏了，所以我现在要求每个供应商都提供这样的服务。我们还试图通过我们的 SaaS 工具支持达到这一水平。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![](img/60f15faa5735bd2437bf9dada5ee9192.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Suganthan Mohanadasan from @Suganthanmn</cite></footer>

[View plans](https://kinsta.com/plans/)

```
if ('performance' in window) {
  // use Performance API
}
```

完全填充 API 是不可能的，所以要小心遗漏的浏览器。如果 90%的用户都在愉快地使用 Internet Explorer 8 进行浏览，那么您只能测量 10%的客户端拥有更强大的应用程序。

该 API 可以在 [Web Workers](https://developer.mozilla.org/docs/Web/API/Web_Workers_API/Using_web_workers) 中使用，它提供了一种在后台线程中执行复杂计算而不中断浏览器操作的方法。

大多数 API 方法可以在服务器端 Node.js 中使用标准的 [perf_hooks 模块](https://nodejs.org/dist/latest/docs/api/perf_hooks.html):

```
// Node.js performance
import { performance } from 'node:perf_hooks';
// or in Common JS: const { performance } = require('node:perf_hooks');

console.log( performance.now() );
```

Deno 提供了标准的[性能 API](https://doc.deno.land/deno/stable/~/Performance) :

```
// Deno performance
console.log( performance.now() );
```

您将需要使用`--allow-hrtime`权限运行脚本来启用高分辨率时间测量:

```
deno run --allow-hrtime index.js
```

服务器端性能通常更容易评估和管理，因为它取决于负载、CPU、RAM、硬盘和[云服务限制](https://kinsta.com/blog/disk-space-wordpress-hosting/)。硬件升级或过程管理选项，如 [PM2](https://pm2.keymetrics.io/) 、[集群](https://nodejs.org/api/cluster.html)和 [Kubernetes](https://kubernetes.io/) 可能比重构代码更有效。

出于这个原因，下面几节集中讨论客户端性能。

## 自定义性能测量

Performance API 可以用来计时应用程序函数的执行速度。您可能使用过或遇到过使用 [`Date()`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date) 的计时功能:

```
const timeStart = new Date();
runMyCode();
const timeTaken = new Date() - timeStart;

console.log(`runMyCode() executed in ${ timeTaken }ms`);
```

性能 API 提供了两个主要好处:

1.  **更好的准确性:** `Date()`测量到最接近的毫秒，但是性能 API 可以测量毫秒的分数(取决于浏览器)。
2.  **更好的可靠性:**用户或操作系统可以更改系统时间，因此基于`Date()`的指标不会总是准确的。这意味着当时钟向前移动时，你的功能会显得特别慢！

`Date()`等价于 [`performance.now()`](https://developer.mozilla.org/docs/Web/API/Performance/now) ，它返回一个高分辨率的时间戳，当负责创建文档的进程开始时(页面已经加载)，该时间戳被设置为零:

```
const timeStart = performance.now();
runMyCode();
const timeTaken = performance.now() - timeStart;

console.log(`runMyCode() executed in ${ timeTaken }ms`);
```

非标准的 [`performance.timeOrigin`](https://developer.mozilla.org/docs/Web/API/Performance/timeOrigin) 属性也可以返回从 1970 年 1 月 1 日开始的时间戳，尽管这在 IE 和 Deno 中不可用。

进行多次测量时变得不切实际。性能 API 提供了一个缓冲区，您可以通过将标签名称传递给 [`performance.mark()`](https://developer.mozilla.org/docs/Web/API/Performance/mark) 来记录事件，以供以后分析:

```
performance.mark('start:app');
performance.mark('start:init');

init(); // run initialization functions

performance.mark('end:init');
performance.mark('start:funcX');

funcX(); // run another function

performance.mark('end:funcX');
performance.mark('end:app');
```

性能缓冲区中所有标记对象的数组可以通过以下方式提取:

```
const mark = performance.getEntriesByType('mark');
```

示例结果:

```
[

  {
    detail: null
    duration: 0
    entryType: "mark"
    name: "start:app"
    startTime: 1000
  },
  {
    detail: null
    duration: 0
    entryType: "mark"
    name: "start:init"
    startTime: 1001
  },
  {
    detail: null
    duration: 0
    entryType: "mark"
    name: "end:init"
    startTime: 1100
  },
...
]
```

[`performance.measure()`](https://developer.mozilla.org/docs/Web/API/Performance/measure) 方法计算两个标记之间的时间，并将其存储在性能缓冲区中。传递一个新的度量名、起始标记名(或 null 表示从页面加载开始度量)和结束标记名(或 null 表示度量到当前时间):

```
performance.measure('init', 'start:init', 'end:init');
```

一个 [PerformanceMeasure 对象](https://developer.mozilla.org/docs/Web/API/PerformanceMeasure)被附加到具有计算出的持续时间的缓冲区中。要获得这个值，您可以请求一个包含所有度量值的数组:

```
const measure = performance.getEntriesByType('measure');
```

或按名称请求测量:

```
performance.getEntriesByName('init');
```

示例结果:

```
[
  {
    detail: null
    duration: 99
    entryType: "measure"
    name: "init"
    startTime: 1001
  }
]
```

### 使用性能缓冲区

除了标记和度量，性能缓冲区还用于自动记录导航时间、资源时间和绘制时间(我们将在后面讨论)。您可以获得缓冲区中所有条目的数组:

```
performance.getEntries();
```

默认情况下，大多数浏览器都提供了一个最多可以存储 150 个资源指标的缓冲区。对于大多数评估，这应该足够了，但是如果需要，您可以增加或减少缓冲区限制:

```
// record 500 metrics
performance.setResourceTimingBufferSize(500);
```

可以按名称清除标记，也可以指定一个空值来清除所有标记:

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

```
performance.clearMarks('start:init');
```

类似地，可以通过名称或空值来清除所有度量:

```
performance.clearMeasures();
```

### 监控性能缓冲区更新

一个 [**性能观察者**](https://developer.mozilla.org/docs/Web/API/PerformanceObserver) 可以监控性能缓冲区的变化，并在特定事件发生时运行一个函数。如果您使用过 [**变异观察器**](https://developer.mozilla.org/docs/Web/API/MutationObserver) 来响应 DOM 更新，或者使用过 [**交叉观察器**](https://developer.mozilla.org/docs/Web/API/IntersectionObserver) 来检测元素何时被滚动到视口中，那么这个语法应该很熟悉。

您必须用两个参数定义一个观察者函数:

1.  已检测到的观察者条目的数组，以及
2.  观察者对象。如有必要，可以调用其 [`disconnect()`](https://developer.mozilla.org/docs/Web/API/PerformanceObserver/disconnect) 方法来停止观察器。

```
function performanceCallback(list, observer) {

  list.getEntries().forEach(entry => {
    console.log(`name    : ${ entry.name }`);
    console.log(`type    : ${ entry.type }`);
    console.log(`start   : ${ entry.startTime }`);
    console.log(`duration: ${ entry.duration }`);
  });

}
```

该函数被传递给一个新的 PerformanceObserver 对象。它的 [`observe()`](https://developer.mozilla.org/docs/Web/API/PerformanceObserver/observe) 方法是通过一个性能缓冲区 entryTypes 数组来观察的:

```
let observer = new PerformanceObserver( performanceCallback );
observer.observe({ entryTypes: ['mark', 'measure'] });
```

在本例中，添加新的标记或测量会运行`performanceCallback()`功能。虽然它只在这里记录消息，但它可以用来触发数据上传或进行进一步的计算。

### 测量油漆性能

Paint Timing API 仅在客户端 JavaScript 中可用，并自动记录对[核心 Web 生命周期](https://kinsta.com/blog/core-web-vitals/)很重要的两个指标:

1.  **first-paint:** 浏览器已经开始绘制页面。
2.  **first-contentful-paint:** 浏览器已经绘制了 DOM 内容的第一个重要项目，比如标题或图像。

这些可以从性能缓冲区提取到一个数组中:

```
const paintTimes = performance.getEntriesByType('paint');
```

在页面完全加载之前运行它要小心；这些值将不会准备好。要么等待 [`window.load`](https://developer.mozilla.org/docs/Web/API/Window/load_event) 事件，要么使用 [`PerformanceObserver`](https://docs.google.com/document/d/1bO-CdqPOUVV0xaZkQMu5f5eHYxmV1RfoYVwPHXDRvyg/edit#heading=h.y0ea1dh8xmx) 来监控`paint`条目类型。

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

示例结果:

```
[
  {
    "name": "first-paint",
    "entryType": "paint",
    "startTime": 812,
    "duration": 0
  },
  {
    "name": "first-contentful-paint",
    "entryType": "paint",
    "startTime": 856,
    "duration": 0
  }
]
```

第一次绘制缓慢通常是由于 CSS 或 JavaScript 的渲染阻塞造成的。如果浏览器不得不下载一个大的图像或者[渲染复杂的元素](https://kinsta.com/blog/eliminate-render-blocking-javascript-css/)，那么与第一次绘制的差距可能会很大。

## 资源性能测量

图像、样式表和 JavaScript 文件等资源的网络计时会自动记录到性能缓冲区中。虽然您很难解决网络速度问题(除了减小文件大小)，但它可以帮助突出较大资产、缓慢的 Ajax 响应或表现不佳的第三方脚本的问题。

可以使用以下方式从缓冲区中提取一组[performance resource timing](https://developer.mozilla.org/docs/Web/API/PerformanceResourceTiming)指标:

```
const resources = performance.getEntriesByType('resource');
```

或者，您可以通过传递资产的完整 URL 来获取资产的指标:

```
const resource = performance.getEntriesByName('https://test.com/script.js');
```

示例结果:

```
[
  {
    connectEnd: 195,
    connectStart: 195,
    decodedBodySize: 0,
    domainLookupEnd: 195,
    domainLookupStart: 195,
    duration: 2,
    encodedBodySize: 0,
    entryType: "resource",
    fetchStart: 195,
    initiatorType: "script",
    name: "https://test.com/script.js",
    nextHopProtocol: "h3",
    redirectEnd: 0,
    redirectStart: 0,
    requestStart: 195,
    responseEnd: 197,
    responseStart: 197,
    secureConnectionStart: 195,
    serverTiming: [],
    startTime: 195,
    transferSize: 0,
    workerStart: 195
  }
]
```

可以检查以下属性:

*   **名称**:资源 URL
*   **条目类型**:“资源”
*   **initiatorType** :资源是如何被初始化的，如“脚本”或“链接”
*   **serverTiming** :服务器在 [HTTP Server-Timing header](https://developer.mozilla.org/docs/Web/HTTP/Headers/Server-Timing) 中传递的一组 [`PerformanceServerTiming`](https://developer.mozilla.org/docs/Web/API/PerformanceServerTiming) 对象(您的服务器端应用程序可以将指标发送给客户端进行进一步分析)
*   **startTime** :获取开始时的时间戳
*   **nextHopProtocol** :使用的网络协议
*   **workerStart** :启动渐进式 Web App 服务工作器之前的时间戳(如果请求未被服务工作器拦截，则为 0)
*   **redirectStart** :重定向开始时的时间戳
*   **redirectEnd** :最后一个重定向响应的最后一个字节之后的时间戳
*   **fetchStart** :获取资源之前的时间戳
*   **domain lookupstart**:DNS 查找前的时间戳
*   **domain lookupend**:DNS 查找后的时间戳
*   **connectStart** :建立服务器连接前的时间戳
*   **connectEnd** :建立服务器连接后的时间戳
*   **secureConnectionStart**:SSL 握手之前的时间戳
*   **requestStart** :浏览器请求资源之前的时间戳
*   **responseStart** :浏览器收到第一个字节数据时的时间戳
*   **responseEnd** :接收到最后一个字节或关闭连接后的时间戳
*   **持续时间**:start time 和 responseEnd 之差
*   **transferSize** :以字节为单位的资源大小，包括头和压缩体
*   **encodedBodySize** :解压缩前的资源体，以字节为单位
*   **decodedBodySize** :解压缩后的资源体，以字节为单位

这个示例脚本检索由 [Fetch API](https://developer.mozilla.org/docs/Web/API/Fetch_API) 发起的所有 Ajax 请求，并返回总传输大小和持续时间:

```
const fetchAll = performance.getEntriesByType('resource')
  .filter( r => r.initiatorType === 'fetch')
  .reduce( (sum, current) => {
    return {
      transferSize: sum.transferSize += current.transferSize,
      duration: sum.duration += current.duration
    }
  },
  { transferSize: 0, duration: 0 }
);
```

## 导航性能测量

卸载前一页和加载当前页的网络时间会作为单个 [`PerformanceNavigationTiming`](https://developer.mozilla.org/docs/Web/API/PerformanceNavigationTiming) 对象自动记录到性能缓冲区。

使用以下命令将其提取到一个数组中:

```
const pageTime = performance.getEntriesByType('navigation');
```

…或者通过将页面 URL 传递给`.getEntriesByName()`:

```
const pageTiming = performance.getEntriesByName(window.location);
```

这些指标与[资源](https://docs.google.com/document/d/1bO-CdqPOUVV0xaZkQMu5f5eHYxmV1RfoYVwPHXDRvyg/edit#heading=h.k94hcflv9m3o)的指标相同，但也包括特定于页面的值:

*   **条目类型**:如“导航”
*   **类型**:可以是“导航”、“重新加载”、“后退 _ 前进”或“预呈现”
*   **重定向计数**:重定向次数
*   **unloadEventStart** :前一个文档的卸载事件之前的时间戳
*   **unloadEventEnd** :前一个文档卸载事件后的时间戳
*   **domInteractive** :浏览器解析 HTML 并构建 DOM 时的时间戳
*   **domContentLoadedEventStart**:文档的 DOMContentLoaded 事件触发之前的时间戳
*   **domContentLoadedEventEnd** :文档的 DOMContentLoaded 事件完成后的时间戳
*   **DOM complete**:DOM 构造和 DOMContentLoaded 事件完成后的时间戳
*   **loadEventStart** :页面加载事件触发前的时间戳
*   **loadEventEnd** :页面加载事件后的时间戳，所有资产可用

典型问题包括:

*   在**卸载事件结束**和**主互动**之间有很长的延迟。这可能表示服务器响应缓慢。
*   在**domContentLoadedEventStart**和 **domComplete** 之间有很长的延迟。这可能表明页面启动脚本太慢。
*   在 **domComplete** 和 **loadEventEnd** 之间有很长的延迟。这可能表明该页面有太多资产，或者有几个资产加载时间太长。

## 性能记录和分析

Performance API 允许您整理真实世界的使用数据，并将其上传到服务器以供进一步分析。你*可以*使用[的第三方服务，如谷歌分析](https://kinsta.com/blog/google-analytics-alternatives/)来存储数据，但第三方脚本有可能被阻止或引入新的性能问题。您可以根据自己的需求定制自己的解决方案，以确保监控不会影响其他功能。

警惕无法确定统计数据的情况——可能是因为用户使用的是旧浏览器，屏蔽了 JavaScript，或者在公司代理后面。了解缺少哪些数据比根据不完整的信息做出假设更有成效。

理想情况下，您的分析脚本不会因为运行复杂的计算或上传大量数据而对性能产生负面影响。考虑利用 web workers 并尽量减少同步 localStorage 调用的使用。以后总是可以批量处理原始数据的。

最后，要警惕异常值，例如会对统计数据产生负面影响的非常快或非常慢的设备和连接。例如，如果九个用户在两秒钟内加载一个页面，但是第十个用户经历了 60 秒的下载，那么平均延迟接近 8 秒。更现实的指标是中间值(2 秒)或第 90 个百分位数(每 10 个用户中有 9 个用户的加载时间不超过 2 秒)。

## 摘要

对于开发者来说，网页性能仍然是一个关键的 T2 因素。用户希望网站和应用程序能够在大多数设备上响应。搜索引擎优化也会受到影响，因为[速度较慢的网站在谷歌](https://kinsta.com/blog/core-web-vitals/)中被降级。
[开始使用性能 API 所需的一切都在这里💪 点击推文](https://twitter.com/intent/tweet?url=https%3A%2F%2Fbit.ly%2F3dl8OA3&via=kinsta&text=Everything+you+need+to+know+to+get+started+with+the+Performance+API+is+right+here+%F0%9F%92%AA&hashtags=API%2CWebDev)
现在有很多[性能监控工具](https://kinsta.com/blog/application-performance-monitoring/)，但是大多数评估服务器端执行速度或者使用有限数量的有能力的客户端来判断浏览器渲染。Performance API 提供了一种整理真实用户指标的方法，这种方法不可能通过其他方法来计算。

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。