# 对最佳实践做出反应，提升您在 2022 年的竞争力

> 原文：<https://kinsta.com/blog/react-best-practices/>

React 仍然是构建 web 应用程序时创建用户界面最流行的库之一。它被许多公司广泛使用，并有一个活跃的社区。

作为一名 React 开发人员，理解库是如何工作的并不是构建用户友好、易于扩展和维护的项目所需要的唯一事情。

理解某些约定也是必要的，这将使您能够编写干净的 React 代码。这不仅有助于您更好地为用户服务，还能让您和项目中的其他开发人员更容易地维护代码库。[正在进行下一个 React 项目？学习写干净的 React 代码是一个游戏规则肌肉入门这里⬇️ 点击推文](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Freact-best-practices%2F&via=kinsta&text=Working+on+your+next+React+project%3F+Learning+to+write+clean+React+code+is+a+game-changer+muscle+Get+started+here+%E2%AC%87%EF%B8%8F&hashtags=React%2CWebDev)

在本教程中，我们将首先讨论 React 开发人员面临的一些常见挑战，然后深入探讨一些您可以遵循的最佳实践，以帮助您以更有效的方式编写 React 代码。

我们开始吧！

## 开发人员面临的挑战

在这一节中，我们将讨论 [React 开发者](https://kinsta.com/blog/types-of-developers/)在构建 web 应用期间和之后面临的一些主要挑战。

您将在本节看到的所有挑战都可以通过遵循最佳实践来避免，我们将在后面详细讨论。









我们将从影响初学者的最基本的问题开始。

### 做出反应的先决条件

React 开发人员面临的主要挑战之一是[理解库如何工作](https://kinsta.com/knowledgebase/what-is-react-js/)，以及使用它的先决条件。

在学习 React 之前，你需要知道一些事情。由于 React 使用 JSX，[懂 HTML](https://kinsta.com/blog/learn-html/) 和 JavaScript 是必须的。当然，你也应该知道 CSS 或者一个[现代 CSS 框架](https://kinsta.com/blog/tailwind-css/)来设计你的网络应用。

特别是，在深入 React 之前，您应该了解一些核心的 JavaScript 概念和功能。其中一些主要属于 ES6，包括:

*   箭头功能
*   Rest 运算符
*   传播算子
*   模块
*   解构
*   数组方法
*   模板文字
*   承诺
*   `let`和`const`变量

上面列出的 JavaScript 主题将帮助初学者理解 React 是如何工作的。

您还将了解 React 中的新概念，例如:

*   成分
*   JSX
*   状态管理
*   小道具
*   渲染元素
*   事件处理
*   条件渲染
*   列表和键
*   表单和表单验证
*   钩住
*   式样

对 React 概念和使用该库的先决条件有一个坚实的理解将有助于您有效地利用它的特性。

但是不要让这个压倒你。通过不断的实践和学习，您可以很快掌握如何使用 React 来构建出色的项目。这类似于[学习一门新的编程语言](https://kinsta.com/blog/best-programming-language-to-learn/)——只是需要一点时间和练习来理解。

### 状态管理

在 React 中更新变量的状态/值的工作方式不同于使用[普通 JavaScript](https://kinsta.com/knowledgebase/what-is-javascript/) 的方式。

在 JavaScript 中，更新一个变量就像使用等于运算符(`=`)给它赋一个新值一样简单。这里有一个例子:

```
var x = 300;
function updateX(){
  x = 100;
}
updateX();
console.log(x);
// 100
```

在上面的代码中，我们创建了一个名为`x`的变量，初始值为`300`。

使用等于操作符，我们给它分配了一个新的值`100`。这是写在一个`updateX`函数中的。

在 React 中，更新变量的状态/值的工作方式不同。方法如下:

```
import { useState } from 'react';
function App() {
  const [x, setX] = useState(300)
  let updateX =()=>{
    setX(100);
  }
  return (
    <div className="App">
    <h1>{x}</h1>
    <button onClick={updateX}>Update X</button>
    </div>
  );
}
export default App;
```

在 React 中更新变量的状态时，可以使用`useState`钩子。使用该挂钩时有三点需要注意:

*   变量名
*   用于更新变量的函数
*   变量的初始值/状态

在我们的例子中，`x`是变量的名称，`setX`是更新`x`值的函数，而`x`的初始值(`300`)作为参数传递给`useState`函数:

```
 const [x, setX] = useState(300)
```

为了更新`x`的状态，我们使用了`setX`函数:

```
import { useState } from 'react';
let updateX =()=>{
  setX(100);
}
```

所以`updateX`函数调用`setX`函数，然后将`x`的值设置为`100`。

虽然这看起来非常适合更新变量的状态，但是在非常大的项目中，它增加了代码的复杂性。大量的状态挂钩使得代码很难维护和理解，尤其是当你的项目扩展时。

使用状态挂钩的另一个问题是，创建的这些变量不能在组成应用程序的不同组件之间共享。您仍然需要利用 Props 将数据从一个变量传递到另一个变量。

幸运的是，React 中构建了一些库来有效地处理状态管理。它们甚至允许你一次创建一个变量，然后在 React 应用中的任何地方使用它。其中一些库包括 Redux、反冲和 Zustand。

选择第三方库进行状态管理的问题是，您将被迫学习与您在 React 中已经学习的内容无关的新概念。例如，Redux 以拥有大量样板代码而闻名，这使得初学者很难掌握(尽管这一点正在通过 Redux Toolkit 得到解决，它让您比使用 Redux 编写的代码更少)。

### 可维护性和可扩展性

随着产品的用户需求不断变化，总是需要对组成产品的代码进行修改。

当团队不容易维护代码时，通常很难扩展代码。像这样的困难来自于在编写代码时遵循不好的实践。起初，它们看起来很完美，给了你想要的结果，但是任何“目前”有效的东西对于你的项目的未来和发展都是低效的。

在下一节中，我们将回顾一些有助于改进 React 代码编写方式的约定。这也将帮助你在与专业团队合作时更好地合作。
T3】

## 反应最佳实践

在这一节中，我们将讨论在编写 React 代码时应该遵循的一些最佳实践。让我们开始吧。

T3】

### 1.保持清晰的文件夹结构

文件夹结构有助于您和其他开发人员了解项目中使用的文件和资源的排列。

有了一个好的文件夹结构，就可以很容易地导航，节省时间，并有助于避免混乱。文件夹结构因每个团队的偏好而异，但这里有一些 React 中常用的文件夹结构。

#### 按要素或路径对文件夹进行分组

根据路径和功能对文件夹中的文件进行分组有助于将特定功能的所有信息保存在一个空间中。例如，如果您有一个用户仪表板，您可以将与仪表板相关的 JavaScript、CSS 和测试文件放在一个文件夹中。

这里有一个例子来说明:

```
dashboard/
index.js
dashboard.css
dashboard.test.js
home/
index.js
Home.css
HomeAPI.js
Home.test.js
blog/
index.js
Blog.css
Blog.test.js
```

从上面可以看出，该应用程序的每个核心功能都将其所有文件和资产存储在同一个文件夹中。

#### 将相似的文件分组

或者，您可以将相似的文件分组到同一个文件夹中。您还可以为挂钩、组件等创建单独的文件夹。看看这个例子:

```
hooks/
useFetchData.js
usePostData.js
components/
Dashboard.js
Dashboard.css
Home.js
Home.css
Blog.js
Blog.css
```

编码时不必严格遵循这些文件夹结构。如果你有一个特定的方法来排序你的文件，那就去做吧。只要您和其他开发人员对文件结构有一个清晰的理解，您就可以开始了！

### 2.建立结构化的进口订单

随着 React 应用程序的不断增长，您一定会进行额外的导入。导入的结构对帮助您理解组件的组成大有帮助。

按照惯例，将类似的实用程序组合在一起似乎很好。例如，您可以将外部或第三方导入与本地导入分开分组。

看一下下面的例子:

```
import { Routes, Route } from "react-router-dom";
import { createSlice } from "@reduxjs/toolkit";
import { Menu } from "@headlessui/react";
import Home from "./Home";
import logo from "./logo.svg";
import "./App.css";
```

在上面的代码中，我们首先将第三方库组合在一起(这些是我们必须预先安装的库)。

然后，我们导入在本地创建的文件，如样式表、图像和组件。

为了简单和易于理解，我们的示例没有描述非常大的代码库，但请记住，与这种格式的导入保持一致将有助于您和其他开发人员更好地理解您的 React 应用程序。

如果适合您的话，您可以进一步根据文件类型对您的本地文件进行分组——也就是说，将组件、图像、样式表、钩子等等分别分组到您的本地导入之下。

这里有一个例子:

```
import Home from "./Home";
import About from "./About"
import Contact from "./Contact"
import logo from "./logo.svg";
import closeBtn from "./close-btn.svg"
import "./App.css";
import "Home.css"
```

### 3.遵守命名约定

命名约定有助于提高代码的可读性。这不仅适用于组件名，甚至适用于变量名，一直到钩子。

React 文档没有提供任何正式的组件命名模式。最常用的命名约定是 camelCase 和 PascalCase。

PascalCase 主要用于组件名称:

```
import React from 'react'
function StudentList() {
  return (
    <div>StudentList</div>
  )
}
export default StudentList
```

上面的组件被命名为`StudentList`，比`Studentlist`或`studentlist`可读性强得多。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

另一方面，camelCase 命名约定主要用于命名变量、挂钩、函数、数组等:

```
&const [firstName, setFirstName] = useState("Ihechikara");
const studentList = [];
const studentObject = {};
const getStudent = () => {}
```

### 4.使用棉绒

一个 [linter 工具](https://kinsta.com/blog/wordpress-workflow/#take-advantage-of-linting)帮助提高代码质量。用于 JavaScript 和 React 的最流行的 linter 工具之一是 ESlint。但是这对提高代码质量到底有什么帮助呢？

linter 工具有助于代码库的一致性。当[使用 ESLint](https://kinsta.com/blog/wordpress-workflow/#step-6-use-linting) 这样的工具时，你可以设定你希望每个从事该项目的开发者遵守的规则。这些规则可能包括使用双引号而不是单引号的要求、箭头函数的括号、特定的命名约定等等。

该工具会观察您的代码，然后在违反规则时通知您。违反规则的关键字或行通常会用红色下划线标出。

由于每个开发人员都有自己的编码风格，linter 工具可以帮助实现代码一致性。

Linter 工具也可以帮助我们轻松修复 bug。我们可以看到拼写错误，已经声明但没有使用的变量，以及其他类似的功能。其中一些错误可以在您编码时自动修复。

像 ESLint 这样的工具内置在大多数[代码编辑器](https://kinsta.com/blog/free-html-editor/)中，所以你可以随时获得 linter 的功能。您还可以对其进行配置，以满足您的编码需求。

### 5.使用代码片段库

在一个活跃的社区中使用一个框架最酷的一点是可以使用为使开发更容易而创建的工具。

代码片段库可以通过提供开发人员经常使用的预构建代码来加快开发速度。

一个很好的例子是[ES7+React/Redux/React-Native snippets 扩展](https://marketplace.visualstudio.com/items?itemName=rodrigovallades.es7-react-js-snippets)，它有很多用于生成预构建代码的有用命令。例如，如果您想创建一个 React 功能组件，而不需要输入所有的代码，那么您所需要做的就是输入`rfce`并点击**输入**。

上面的命令将继续生成一个功能组件，其名称与文件名相对应。我们使用 ES7+React/Redux/React-Native snippets 扩展生成了以下代码:

```
import React from 'react'
function StudentList() {
  return (
    <div>StudentList</div>
  )
}
export default StudentList
```

另一个有用的代码片段工具是 Tailwind CSS IntelliSense 扩展，它简化了使用 Tailwind CSS 设计网页样式的过程。该扩展可以通过建议实用程序类、语法高亮显示和林挺功能来帮助您完成自动补全。你甚至可以在编码时看到你的颜色是什么样子。


### 6.结合 CSS 和 JavaScript

在处理大型项目时，为每个组件使用不同的样式表文件会使文件结构庞大，难以浏览。

这个问题的解决方案是结合你的 CSS 和 JSX 代码。你可以使用像 Tailwind CSS 和 Emotion 这样的框架/库。

下面是使用 Tailwind CSS 的样式:

```
<p className="font-bold mr-8">resource edge</p>
```

上面的代码给了段落元素一个加粗的字体，并在右边增加了一些空白。我们可以使用框架的实用程序类来实现这一点。

下面是如何使用情感来设计元素的样式:

```
<h1
css={css`
  color: black;
  font-size: 30px;
`}
>
Hello World!
</h1>
```

### 7.限制组件创建

React 的核心特性之一是代码可重用性。您可以创建一个组件并尽可能多地重用其逻辑，而无需重写该逻辑。

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

记住这一点，您应该始终限制您创建的组件的数量。如果不这样做，文件结构就会膨胀，因为不必要的文件本来就不应该存在。

我们将用一个非常简单的例子来说明这一点:

```
function UserInfo() {
  return (
    <div>
    <h1>My name is Ihechikara.</h1>
    </div>
  );
}
export default UserInfo
```

上面的组件显示了用户名。如果我们为每个用户创建一个不同的文件，我们最终会有不合理数量的文件。(当然，我们使用用户信息是为了简单起见。在现实生活中，你可能会处理不同类型的逻辑。)

为了使我们的组件可重用，我们可以使用道具。方法如下:

```
function UserInfo({userName}) {
  return (
    <div>
    <h1>My name is {userName}.</h1>
    </div>
  );
}
export default UserInfo
```

之后，我们可以导入该组件，并根据需要多次使用它:

```
import UserInfo from "./UserInfo";
function App() {
  return (
    <div className="App">
    <UserInfo userName={"Ihechikara"} />
    <UserInfo userName={"John"} />
    <UserInfo userName={"Jane"} />
    </div>
  );
}
export default App;
```

现在我们有三个不同的`UserInfo`组件实例，它们来自一个文件中创建的逻辑，而不是为每个用户创建三个单独的文件。

### 8.实现延迟加载

随着 React 应用的增长，延迟加载非常有用。当你有一个大的代码库时，[网页的加载时间](https://kinsta.com/blog/ttfb/)会变慢。这是因为每个用户每次都要加载整个应用程序。

“延迟加载”是一个用于各种实现的术语。在这里，我们将它与 JavaScript 和 React 联系起来，但是您也可以[在图像和视频上实现延迟加载](https://kinsta.com/blog/wordpress-lazy-load/)。

默认情况下，React 捆绑并部署整个应用程序。但是我们可以使用延迟加载来改变这种行为，也称为代码分割。

基本上，你可以限制你的应用程序在某个特定点被加载的部分。这是通过拆分您的包并只加载那些与用户需求相关的包来实现的。例如，您可以首先仅加载用户登录所需的逻辑，然后仅在用户成功登录后加载用户仪表板的逻辑。

### 9.使用可重复使用的挂钩

React 中的钩子让你可以利用 React 的一些附加功能，比如与组件的状态交互，以及运行与组件中某些状态变化相关的后期效果。我们无需编写类组件就可以完成所有这些工作。

我们还可以使钩子可重用，这样我们就不必在使用它们的每个文件中重新输入逻辑。我们通过创建可以在应用程序中的任何地方导入的自定义挂钩来实现这一点。

在下面的例子中，我们将创建一个从外部 API 获取数据的钩子:

```
import { useState, useEffect } from "react";
function useFetchData(url) {
  const [data, setData] = useState(null);
  useEffect(() => {
    fetch(url)
    .then((res) => res.json())
    .then((data) => setData(data))
    .catch((err) => console.log(`Error: ${err}`));
  }, [url]);
  return { data };
}
export default useFetchData;
```

我们已经创建了一个钩子来从上面的 API 中获取数据。现在它可以被导入到任何组件中。这让我们不必在必须获取外部数据的每个组件中输入所有逻辑。

我们可以在 React 中创建的自定义挂钩的类型是无限的，因此如何使用它们取决于您。请记住，如果某个功能必须在不同的组件之间重复，那么您一定要让它可重用。

### 10.记录和管理错误

React 中有不同的错误处理方式，比如使用错误边界、try and catch 块或者使用外部库`react-error-boundary`。

React 16 中引入的内置错误边界是类组件的功能，所以我们不讨论它，因为建议您使用功能组件而不是类组件。

另一方面，使用`try` 和`catch`块只适用于命令式代码，而不适用于声明式代码。这意味着与 JSX 合作不是一个好的选择。

我们最好的建议是使用像 react-error-boundary 这样的[库。该库提供了可以包装在组件周围的功能，这将帮助您在呈现 React 应用程序时检测错误。](https://github.com/bvaughn/react-error-boundary)

### 11.监控和测试您的代码

在开发过程中测试你的代码有助于你编写[可维护的代码](https://kinsta.com/blog/html-best-practices/)。不幸的是，这是许多开发人员忽略的东西。

尽管许多人可能会认为在构建 web 应用程序时测试没什么大不了的，但它带来了无数的好处。以下是几个例子:

*   测试帮助你[发现错误和缺陷](https://kinsta.com/blog/debugging-wordpress-performance/)。
*   检测错误可以提高代码质量。
*   单元测试可以被记录下来，用于数据收集和将来参考。
*   早期的 bug 检测为您节省了支付开发人员扑灭 bug 可能引发的火灾的费用。
*   无缺陷的应用和网站[赢得了观众的信任和忠诚](https://kinsta.com/blog/trust-badges/)，从而带来了更大的增长。

您可以使用 Jest 或 React 测试库等工具来测试您的代码。有大量的测试工具供你选择——最终选择最适合你的。

你也可以在浏览器中运行应用[来测试你的 React 应用。您通常会在屏幕上显示任何检测到的错误。这类似于使用](https://kinsta.com/blog/microsoft-edge-vs-chrome/) [DevKinsta](https://kinsta.com/devkinsta/) 开发 WordPress 站点——一个允许你在本地机器上设计、开发和部署 WordPress 站点的工具。

### 12.利用功能组件

在 React 中使用功能组件有很多好处:你编写的代码更少，更容易阅读，而且测试版的[官方 React 文档](https://reactjs.org/docs/getting-started.html)正在使用功能组件(钩子)重写，所以你肯定应该习惯使用它们。

有了功能组件，你不必担心使用`this`或者使用类。多亏了钩子，你还可以通过编写更少的代码来轻松管理组件的状态。

您在 React 上找到的大多数更新资源都利用了功能组件，当您遇到问题时，可以很容易地理解和遵循社区创建的有用指南和资源。

### 13.与 React 版本变更保持同步

随着时间的推移，新的功能将被引入，一些旧的功能将被修改。最好的跟踪方法是查看官方文档。

你也可以加入社交媒体上的 React 社区，在发生变化时获取相关信息。

保持 React 的最新版本将有助于您确定何时优化或更改代码库以获得最佳性能。

还有一些围绕 React 构建的外部库，您也应该及时了解——比如 React Router，它用于 React 中的路由。了解这些库做出了哪些更改，可以帮助您对应用程序做出相关的重要更改，并使参与项目的每个人都更容易。

此外，在发布新版本时，某些功能可能会被弃用，某些关键字可能会被更改。为了安全起见，在进行此类更改时，您应该始终阅读文档和指南。

### 14.使用快速、安全的主机提供商

如果您想在构建 web 应用程序后让每个人都可以访问它，您必须托管它。使用快速安全的主机提供商是很重要的。

托管您的网站可以让您访问不同的工具，从而轻松扩展和管理您的网站。托管网站的服务器使您本地机器上的文件能够安全地存储在服务器上。托管你的网站的总体好处是，其他人可以看到你创造的令人敬畏的东西。

有各种各样的平台向开发人员提供免费的托管服务，如 Firebase、Vercel、Netlify、GitHub Pages，或付费服务，如 Azure、AWS、GoDaddy、Bluehost 等等。

也可以使用 [Kinsta 的应用托管平台](https://kinsta.com/application-hosting/)。你所需要做的就是连接一个 GitHub 库，从 Kinsta 的 25 个全球定位的数据中心中选择，然后开始。您将获得快速设置、全天候支持、顶级安全性、自定义域、高级报告和监控工具等。
T3】

## 摘要

学习如何使用 React 并不是创建优秀 web 应用程序的全部要求。与 Angular、Vue 等任何其他框架一样，您应该遵循一些最佳实践来帮助您构建高效的产品。

遵循这些 React 惯例不仅有助于你的应用，而且对你作为一名[前端开发人员](https://kinsta.com/blog/frontend-developer/)也有好处——你学习如何编写高效、可扩展和可维护的代码，并且你在你的领域中脱颖而出成为一名[专家](https://kinsta.com/blog/front-end-developer-salary/)。 [想加紧你的 React 编码游戏？你需要知道的一切尽在本指南 点击推文](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Freact-best-practices%2F&via=kinsta&text=Want+to+step+up+your+React+coding+game%3F+Everything+you+need+to+know+is+in+this+guide&hashtags=React%2CWebDev)

因此，当您使用 React 构建下一个 web 应用程序时，请牢记这些最佳实践，以便让您的用户和开发人员能够轻松使用和管理该产品。

您还知道哪些本文中没有提到的 React 最佳实践？请在下面的评论中分享它们。编码快乐！

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。