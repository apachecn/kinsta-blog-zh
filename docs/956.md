# HTTP 和 WordPress HTTP API 指南——第 2 部分

> 原文：<https://kinsta.com/blog/wordpress-http-api-part-2/>

在本指南的第 1 部分中，我大致看了一下 HTTP API。我们学习了什么是 HTTP，讨论了 HTTP 请求和响应的结构，以及动作类型和 URL 是如何结合在一起决定请求的交换结果的。在这篇文章中，我们将看看 WordPress HTTP API。

*   [WordPress HTTP API](#wordpress-http-api)
*   [发出请求](#making-requests)
*   [访问 Github API](#accessing-github-api)

## WordPress HTTP API

大约从 2.7 版本开始，WordPress 就有了一个处理 HTTP 的 API。它由 9 个函数组成，其中你可能只会用到几个。这些函数可以分为两个不同的组——一个用于发出请求，一个用于读取结果。

`wp_remote_get()`、`wp_remote_post()`、`wp_remote_head()`分别使用 GET、POST 和 HEAD 方法从给定的 URL 请求数据。`wp_remote_request()`函数是一个通用函数，它允许您指定一个 URL 和一个伴随它的方法。

用于读取响应的函数同样是自描述的。`wp_remote_retrieve_body()`获取响应的主体，`wp_remote_retrieve_header()`函数获取一个命名的头。`wp_remote_retrieve_headers()`函数以数组形式返回所有的头，`wp_remote_retrieve_response_code()`给出响应代码，`wp_remote_retrieve_response_message()`返回响应消息。

这基本上就是全部了，我们需要知道的就是如何指定头部来发出正确的请求。


## 提出请求

让我们使用`wp_remote_get()`函数来发出请求。我们将使用第一个参数设置 URL，第二个参数添加参数。您可以在[Codex](https://codex.wordpress.org/Function_Reference/wp_remote_get)中找到支持的完整参数集，我在这里将重点介绍标题信息。

要从 Twitter 获取用户的状态信息，您需要在使用`https://api.twitter.com/1.1` URL 的同时使用`statuses/user_timeline.json`路径，并传递一个不记名令牌进行认证——这是我之前生成的。需要以`Bearer [TOKEN]`的形式添加不记名令牌作为授权头。

```
$token = 'Sijbwrf82wdaBief'; 
$response = wp_remote_get('https://api.twitter.com/1.1/statuses/user_timeline.json?screen_name=kinsta', array(
    'headers' => array(
        'Authorization' => 'Bearer ' . $token
    ),
));
```

发出这个请求会返回大量信息，这些信息可以通过打印出`$response`变量来获得。你也可以使用`wp_remote_retrieve`类型的函数来获得部分响应。

大多数时候，主体包含必要的信息，通常是 JSON 格式的。在 PHP 中，我们可以轻松地将其转换为数组:

```
$data = json_decode( $response['body'], true ) 
```

## 访问 Github API

让我们构建一个快速的例子，在 WordPress 小部件中列出我们最新的 Github repos。首先，您需要登录 Github，进入您的个人资料，编辑它，然后进入“个人访问令牌”，在那里您可以生成一个令牌。

[![Github Access Tokens](img/3c16604c79a66db7615307b6aa20447a.png)](https://kinsta.com/wp-content/uploads/2015/08/Screen-Shot-2015-08-31-at-14.45.52.png)

Github Access Tokens



下一步，让我们创建一个空的小部件模板。这个小部件有两个选项:一个供您添加 API 令牌的地方和一个标题。这不是最好的方法，因为它将您的令牌保存在[数据库](https://kinsta.com/knowledgebase/wordpress-database/)中，但对于我们的示例目的来说是不错的。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

```
class My_Github_Widget extends WP_Widget {

	public function __construct() {
		parent::__construct(
			'my_github_widget',
			'My Github Repos',
			array( 'description' => 'A widget that showcases your Github repos' )
		);
	}

	public function widget( $args, $instance ) {
		// Widget output
	}

	public function form( $instance ) {
		$token = ! empty( $instance['token'] ) ? $instance['token'] : '';
		$title = ! empty( $instance['title'] ) ? $instance['title'] : 'From Github';
		?>
```

```
<label for="get_field_id( 'title' ); ?>">Title <input class="widefat" id="get_field_id( 'title' ); ?>" name="get_field_name( 'title' ); ?>" type="text" value="">

<label for="get_field_id( 'token' ); ?>">Github API Token <input class="widefat" id="get_field_id( 'token' ); ?>" name="get_field_name( 'token' ); ?>" type="text" value="">

<?php } }
```

我不想在这里过多地讨论小部件是如何创建的。如果你想知道更多，看看法典中的[小部件 API](https://codex.wordpress.org/Widgets_API) 指南。重要的一点是，`widget()`方法的内容将输出我们的小部件的内容。在该函数中，我们将使用 HTTP 请求连接到 Github，然后格式化并输出响应。下面是所有这些是如何完成的——所有下面的代码都进入了`widget()`方法。

```
echo $args['before_widget']; 

if ( ! empty( $instance['title'] ) ) { 
  echo $args['before_title'] . apply_filters( 'widget_title', $instance['title'] ). $args['after_title']; 
} 

$args = array( 
  'headers' => array( 
    'Accept' => 'application/vnd.github.v3+json', 
    'Authorization' => 'token 3f4f654ab31c2f15e839c74c952e5de2f562f1ee' 
  ) 
); 

$response = wp_remote_get( 'https://api.github.com/user/repos', $args ); 
$repos = json_decode( $response['body'], true ); 

if( !empty( $repos ) ) { 
  echo '<ul>'; 
  foreach( $repos as $repo ) { 
    echo '<li><a href="' . $repo['url'] . '" target="_blank">' . $repo['name'] . '</a></li>'; 
  } 
  echo '</ul>'; 
} 

echo $args['after_widget'];
```

它从简单地在顶部添加小部件的包装元素和标题开始，到关闭小部件的包装结束，代码的主要部分在这两者之间。

首先，我设置了 HTTP 请求头。第一个问题可能是:我如何知道要添加哪些参数？`Authorization`头是最重要的部分，我在 API 文档的[认证](https://developer.github.com/v3/#authentication)部分读到过。

`Accept`标题不是必需的，但是在同一文档页面的顶部，指南鼓励您提供这个标题。

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

然后，我在响应体上使用`json_decode()`,并简单地遍历结果数组，创建一个链接列表。


## 后续步骤

如果你认为这很容易，那你就完全对了，很容易！困难的一点是确保你在不浪费资源的情况下涵盖了所有的角度。守则中有两个问题需要我们立即关注。

如果 API 有任何问题——可能包括未知错误、费率受限帐户等等——我们可能会遇到大错误。我们只是在展示名单前检查尸体是否是空的。

如果我们手上有一个错误，那么主体很可能包含错误信息，所以在这种情况下它也不会是空的。我们可能会列出错误响应的元素，但是由于这些元素没有`url`和`name`属性，我们最终会得到空的列表元素和 PHP 警告。

第二个问题是，这只是浪费。我们在每次页面加载时都连接到外部服务，这可能会对我们的服务器造成影响，并可能导致帐户在 Github 上受到限制。即使不是这样，你的 Github 回购列表在两个页面视图之间变化的可能性有多大，在这里拥有第二个信息有多重要？

我个人建议在这种情况下使用[瞬变](https://codex.wordpress.org/Transients_API)。瞬态允许您存储带有到期时间的请求响应。如果您将到期时间设置为一天，将从 Github 中检索一次数据，然后在接下来的 24 小时内直接从您的数据库中检索。到期后，再次从 Github 检索并保存到数据库。

这将您的 API 调用从每次页面加载一次减少到每天一次，这是一个巨大的改进，也不是很大的损失。


## 摘要

WordPress 使得与网络上的 API 交互变得容易。使用几个内置函数将允许您为用户获取更丰富、更相关的数据。

再加上清理、错误检查和缓存机制，您可以构建一个高效的应用程序，它不仅更有用，而且比您想象的更节省资源。

如果你已经使用了 WordPress HTTP API 来连接 WordPress 和第三方 API，请告诉我们，如果能听到你的工作，那就太好了！

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。