# Laravel Logging:您需要知道的一切

> 原文：<https://kinsta.com/blog/laravel-logging/>

当开发一个现代的应用程序时，日志应该在优先级列表的顶端。

日志记录提供了一种在开发和生产中可视化您的应用程序的方法，实现了透明性和可见性。通过适当的结构化日志记录，现代应用程序可以变得更容易维护，因为我们可以主动识别应用程序中的故障点和性能瓶颈。

Laravel 框架附带了一个健壮的日志记录系统，它可以处理配置一个开箱即用的适当结构的日志记录系统所涉及的所有障碍。Laravel 6.5 中引入的这个新的日志系统非常强大，我们将在本文中探讨它。

[When developing a modern application, logging should be at the top of the priority list. ✅ Learn more about Laravel logging in this handy guide 🛠Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Flaravel-logging%2F&via=kinsta&text=When+developing+a+modern+application%2C+logging+should+be+at+the+top+of+the+priority+list.+%E2%9C%85+Learn+more+about+Laravel+logging+in+this+handy+guide+%F0%9F%9B%A0&hashtags=Laravel%2CWebDev)

本文将探讨 Laravel 日志记录的基础知识，以及为什么您应该在下一个项目中使用 Laravel 日志记录。我们将详细讨论结构化日志记录和集中式日志记录。此外，我们将学习如何通过构建一个 Todo 应用程序来实现 Laravel 日志记录。

如果您已经掌握了以下内容，那么您将从本文中获得更多信息:

*   良好的网络开发知识
*   对 Laravel 的基本了解
*   使用 Laravel 构建应用程序

## 什么是 Laravel 测井？

Laravel 日志记录是关于 Laravel 如何处理日志记录，或者自动问题报告，使用一个叫做 Monolog 的病毒式 PHP 日志记录系统。然而，由于 Laravel 的哲学是使用流行的现有库来实现不同的框架特性，Laravel 使用 Monolog 来满足其所有的日志记录需求。





> 需要在这里大声喊出来。Kinsta 太神奇了，我用它做我的个人网站。支持是迅速和杰出的，他们的服务器是 WordPress 最快的。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![A picture of Phillip Stemann looking into the camera wearing a blue button down shirt](img/12b77bdcd297e9bf069df2f3413ad833.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Phillip Stemann</cite></footer>

[View plans](https://kinsta.com/plans/)

Monolog 是一个高度灵活和流行的 PHP 日志库，我们可以配置它来将您的日志发送到文件、套接字、[数据库](https://kinsta.com/knowledgebase/laravel-database/)和其他 web 服务。Monolog 提供了一个熟悉的接口，用于将日志从标准文本文件写入高级第三方日志管理服务。Laravel 通常将 Monolog 设置为使用标准日志配置文件。

 有关 Monolog 及其特性的更多信息，请查看官方文档，因为这超出了本文的范围。

在我们开始使用 Monolog 配置和实现 Laravel 日志记录之前，让我们探索一下使用 Laravel 日志记录的更多原因和不同类型。

## 为什么使用 Laravel 日志记录？

为什么日志记录是必要的？

十二要素应用程序宣言将日志记录视为现代应用程序的关键问题之一，因为日志记录是性能和监控的关键。

[日志](https://kinsta.com/help/view-server-logs/)有助于详细了解生产中发生的错误以及它们的来源。此外，通过适当的日志结构，它可以显示特定的用户、导致错误的操作以及更快修复和维护错误的可能解决方案。

结构化日志记录是生产应用程序中的救命稻草，它可以帮助解决生产中的缺陷和问题。此外，您可以使用专门的日志记录工具实时监控和收集所有日志消息，以便进行实时分析和报告。

由于这些原因，您需要在下一个现代应用程序项目中将结构化日志记录作为重中之重。

让我们看一下可用的不同日志样式的概述。

## Laravel 测井基础

学习日志记录的基础知识将帮助您理解 Laravel 如何处理日志记录，以及如何改进您的结构化日志记录实践。

让我们检查日志记录中的两个基本概念，以便更好地理解如何实现我们的日志记录过程。

### Laravel 结构化测井

在软件开发中，结构化日志记录是为应用程序日志实现预先确定的一致的消息格式。与常规文本格式相比，这种格式允许将消息视为可以更好地监控、操作和可视化的数据。

您必须在现代应用程序开发中实现结构化日志记录方法，因为当您的应用程序在生产中出现问题时，日志文件是开发人员的重要资产。

由于 Laravel 使用 Monolog，开发人员可以通过配置日志记录器来接收特定类型的信息，以不同格式存储日志文件，并将日志发送到各种第三方日志管理服务进行可视化，从而快速实现结构化日志记录。

### Laravel 集中测井

在集中式日志记录系统中，日志从多个来源发送到集中式日志管理(CLM)解决方案，以便于整合和可视化。然而，CLM 是一个专门的日志记录解决方案，它从不同的来源收集日志消息，并整合数据，以便于处理和可视化。

除了数据收集之外，预计 CLM 系统还将支持日志数据分析和分析后数据的清晰呈现。

### 结构化日志记录与基本日志记录

让我们研究一下结构化日志记录和基本(非结构化)日志记录之间的区别，以及为什么应该在 Laravel 项目中使用结构化日志记录。

#### 基本日志记录

在基本日志记录中，日志文件以原始格式存储，用于查询和识别单个日志的数据有限。

使用基本日志记录时，[开发人员](https://kinsta.com/knowledgebase/dev-features/)将无法使用第三方分析工具来读取、查看和分析日志，除非他们开发一个定制工具或坚持使用支持其日志格式的有限工具。

避免使用基本日志记录有三大原因:

1.  没有额外的支持，集中式日志管理系统无法处理数据。
2.  需要定制的解决方案来读取和解析基本日志解决方案的数据。
3.  对于管理员来说，读取基本的日志记录数据可能是一项挑战，因为这些数据是原始的、非结构化的。

#### 结构化日志记录

结构化日志记录通过使用支持标准日志结构的开源第三方日志分析工具来读取、查看和分析日志，从而节省了开发人员的时间。

如果日志包含下面列出的正确数据，将会很有帮助，这也是结构化日志记录的目标。我们可以使用结构化日志记录中包含的数据来创建仪表板、图形、图表和任何其他有用的可视化工具，以确定应用程序的健康状况。

这些是我们可以在结构化日志消息中包含的信息的基本示例。此外，您可以完全自定义数据以满足您的需求。

以下是您可以使用结构化日志记录收集的一些数据示例:

1.  用于执行该功能的端口
2.  事件发生的日期和时间
3.  客户用户名或 ID
4.  事件的描述(日志消息)
5.  用于执行该功能的协议
6.  触发事件的位置(指明 API 或正在运行的应用程序)
7.  唯一的事件 ID
8.  触发的操作类型(日志级别)

日志应该包含足够的数据，以便于可视化解决方案或日志事件的原因。另外，请注意，您不应该在日志中存储所有类型的信息，如密码或敏感数据。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

既然我们已经大致了解了 Laravel 日志记录的内容，那么让我们继续通过构建一个应用程序来实现 Laravel 日志记录，将日志记录作为一等公民。

## 如何用 Todo App 实现 Laravel 日志

现在，我们将通过创建一个新的 Laravel 项目并实现 Laravel 日志来应用我们到目前为止所学的内容。

如果你以前没有用过 Laravel，你可以通读[什么是 Laravel](https://kinsta.com/knowledgebase/what-is-laravel/)或者偷看我们的[优秀 Laravel 教程列表](https://kinsta.com/blog/laravel-tutorial/)来入门。

### 设置 Laravel

首先，我们将使用下面的命令创建一个新的 Laravel 实例。你可以查阅[官方文档](https://laravel.com/docs/8.x/installation)了解更多。

在运行下面的命令之前，打开您的控制台并导航到您存储 PHP 项目的位置。确保正确安装和配置了 [Composer](https://getcomposer.org/) 。

```
composer create-project laravel/laravel laravel-logging-app
cd laravel-logging-app // Change directory to current Laravel installation
php artisan serve // Start Laravel development server
```

### 配置和设定数据库种子

接下来，我们将建立我们的数据库，创建一个新的`Todo`模型，并播种 200 个假数据进行测试。

打开数据库客户端并创建一个新数据库。我们将对名称`laravel_logging_app_db`做同样的操作，然后填充我们的**。env** 文件与数据库凭证:

```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_logging_app_db
DB_USERNAME=//DB USERNAME HERE
DB_PASSWORD=//DB PASSWORD HERE
```

接下来，我们将运行以下命令来同时创建迁移和`Todo`模型:

```
php artisan make:model Todo -mc
```

打开新创建的 migration found **数据库/migrations/XXX-create-todos-XXX . PHP**并粘贴以下代码:

```
<?php
use IlluminateSupportFacadesSchema;
use IlluminateDatabaseSchemaBlueprint;
use IlluminateDatabaseMigrationsMigration;
class CreateTodosTable extends Migration
{
  /**
  * Run the migrations.
  *
  * @return void
  */
  public function up()
  {
    Schema::create('todos', function (Blueprint $table) {
      $table->id();
      $table->string('title');
      $table->text('description')->nullable();
      $table->boolean('is_completed')->default(false);
      $table->timestamps();
    });
  }
  /**
  * Reverse the migrations.
  *
  * @return void
  */
  public function down()
  {
    Schema::dropIfExists('todos');
  }
}
```

你可以通过学习使用 faker 在 Laravel 中播种你的数据库来用 Faker 数据播种你的 todos。

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

### 独白概述

使用 Laravel Monolog，您可以将结构化日志流式传输并发送到不同的渠道，如电子邮件、Slack、文件、套接字、收件箱、数据库和各种 web 服务。在 Laravel 中，您可以从位于 **config/logging.php** 中的一个配置文件中配置日志记录。

配置文件带有预定义的日志驱动程序可供选择，默认驱动程序是一个`stack`，它使用`single`通道记录到一个 **laravel.log** 文件，该文件位于**存储/日志**文件夹中。我们将通过使用几个 [Laravel 日志驱动程序](https://laravel.com/docs/8.x/logging#available-channel-drivers)来演示结构化日志记录。

Laravel 提供了一些[方法](https://laravel.com/docs/8.x/logging#writing-log-messages)来与日志交互，正如 TodosController.php 控制器文件**中所展示的那样。**

### 在控制器中写入日志消息

打开新创建的**TodosController.php**控制器文件找到 **app/Http/Controllers** 文件夹，粘贴以下代码:

```
 <?php
namespace AppHttpControllers;
use AppModelsTodo;
use IlluminateHttpRequest;
use AppHttpControllersController;
use IlluminateSupportFacadesAuth;
use IlluminateSupportFacadesLog;
class TodosController extends Controller
{
  public function index(Request $request)
  {
    $todos = Todo::all();
    Log::warning('User is accessing all the Todos', ['user' => Auth::user()->id]);
    return view('dashboard')->with(['todos' => $todos]);
  }
  public function byUserId(Request $request)
  {
    $todos = Todo::where('user_id', Auth::user()->id)->get();
    Log::info('User is accessing all his todos', ['user' => Auth::user()->id]);
    return view('dashboard')->with(['todos' => $todos]);
  }
  public function show(Request $request, $id)
  {
    $todo = Todo::find($id);
    Log::info('User is accessing a single todo', ['user' => Auth::user()->id, 'todo' => $todo->id]);
    return view('show')->with(['todo' => $todo]);
  }
  public function update(Request $request, $id)
  {
    # Validations before updating
    $todo = Todo::where('user_id', Auth::user()->id)->where('id', $id)->first();
    Log::warning('Todo found for updating by user', ['user' => Auth::user()->id, 'todo' => $todo]);
    if ($todo) {
      $todo->title = $request->title;
      $todo->desc = $request->desc;
      $todo->status = $request->status == 'on' ? 1 : 0;
      if ($todo->save()) {
        Log::info('Todo updated by user successfully', ['user' => Auth::user()->id, 'todo' => $todo->id]);
        return view('show', ['todo' => $todo]);
      }
      Log::warning('Todo could not be updated caused by invalid todo data', ['user' => Auth::user()->id, 'todo' => $todo->id, 'data' => $request->except('password')]);
      return; // 422
    }
    Log::error('Todo not found by user', ['user' => Auth::user()->id, 'todo' => $id]);
    return; // 401
  }
  public function store(Request $request)
  {
    Log::warning('User is trying to create a single todo', ['user' => Auth::user()->id, 'data' => $request->except('password')]);
    # Validations before updating
    $todo = new Todo;
    $todo->title = $request->title;
    $todo->desc = $request->desc;
    $todo->user_id = Auth::user()->id;
    if ($todo->save()) {
      Log::info('User create a single todo successfully', ['user' => Auth::user()->id, 'todo' => $todo->id]);
      return view('show', ['todo' => $todo]);
    }
    Log::warning('Todo could not be created caused by invalid todo data', ['user' => Auth::user()->id, 'data' => $request->except('password')]);
    return; // 422
  }
  public function delete(Request $request, $id)
  {
    Log::warning('User is trying to delete a single todo', ['user' => Auth::user()->id, 'todo' => $id]);
    $todo = Todo::where('user_id', Auth::user()->id)->where('id', $id)->first();
    if ($todo) {
      Log::info('User deleted a single todo successfully', ['user' => Auth::user()->id, 'todo' => $id]);
      $todo->delete();
      return view('index');
    }
    Log::error('Todo not found by user for deleting', ['user' => Auth::user()->id, 'todo' => $id]);
    return; // 404
  }
}
```

在`TodoController`的每个方法中，我们添加了具有特定日志级别的`Log` facade 来定义我们想要发送的错误类型。下面是一个使用

在`store`方法中记录外观。

```
public function store(Request $request)
{
  Log::warning('User is trying to create a single todo', ['user' => Auth::user()->id, 'data' => $request->except('password')]);
  # Validations before updating
  $todo = new Todo;
  $todo->title = $request->title;
  $todo->desc = $request->desc;
  $todo->user_id = Auth::user()->id;
  if ($todo->save()) {
    Log::info('User create a single todo successfully', ['user' => Auth::user()->id, 'todo' => $todo->id]);
    return view('show', ['todo' => $todo]);
  }
  Log::warning('Todo could not be created caused by invalid todo data', ['user' => Auth::user()->id, 'data' => $request->except('password')]);
  return; // 422
}
```

### 格式化日志消息

假设您对 Laravel 使用的默认`LineFormatter`感到不舒服，它在提供可读和有用的消息方面做得很好。

在这种情况下，您可以轻松地构建一个定制的格式化程序对象来适应您的用例，并在整个应用程序中使用它。

官方的 Monolog 文档给出了一个完整的可用格式化程序列表，并且可以很容易地创建一个自定义的。

在 Laravel 中，您可以通过将自定义格式化程序添加到位于 **config/logging.php** 的配置文件中的列表中，轻松设置任何驱动程序来使用您的自定义格式化程序:

```
'daily' => [
  'driver' => 'daily',
  'path' => storage_path('logs/laravel.log'),
  'level' => env('LOG_LEVEL', 'debug'),
  'days' => 14,
  'formatter' => MonologFormatterHtmlFormatter::class,
  'formatter_with' => [
    'dateFormat' => 'Y-m-d',
  ]
],
```

上面的例子使用`daily`通道配置中的`formatter`和`formatter_with`键将自定义的`MonologFormatterHtmlFormatter`添加到`daily`驱动程序中，以改变日期的格式。

### 将日志发送到不同的通道

在 Monolog 的帮助下，Laravel 可以同时向不同的通道和多个通道发送日志。

让我们按照这些简单的步骤演示如何将日志发送到我们的 Slack 通道。将默认日志频道改为 Slack，并在您的**中添加 [Slack Webhook](https://api.slack.com/messaging/webhooks) URL。env** 文件。

```
LOG_CHANNEL=slack
LOG_SLACK_WEBBHOOK_URL= Slack_webhook_url_here
```

接下来，通过使用如下所示的`Log`外观在应用程序中记录一条消息来测试您的配置:

```
Log::debug("The API instance is on fire caused by:", ['user' => 1])
```

您可以打开 Slack 通道来检查在生成 Webhook URL 时指定的所需通道中打印的错误。

## 摘要

日志记录与应用程序的任何其他因素一样重要，甚至更重要。这就是为什么十二要素应用程序宣言建议它是任何现代应用程序最关键的关注点之一。

通过有效的日志记录，您可以轻松地读取、查看和可视化生产就绪应用程序中发生的错误和缺陷。为此，从项目一开始就在应用程序中实现结构化日志记录是非常重要的。

[Learn why you should use Laravel logging in your next project... as well as how to implement Laravel logging by building a Todo application, all in this guide 🚀Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Flaravel-logging%2F&via=kinsta&text=Learn+why+you+should+use+Laravel+logging+in+your+next+project...+as+well+as+how+to+implement+Laravel+logging+by+building+a+Todo+application%2C+all+in+this+guide+%F0%9F%9A%80&hashtags=Laravel%2CWebDev)

在本文中，我们探讨了 Laravel 日志记录，以及为什么您应该在下一个项目中使用它。我们详细讨论了结构化日志记录和集中式日志记录。此外，我们学习了如何通过构建一个 Todo 应用程序来实现 Laravel 日志记录。

你打算如何实现登录你的下一个应用程序？请在评论区告诉我们。

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。