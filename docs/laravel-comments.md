# 建立一个 Laravel 实时评论系统

> 原文：<https://kinsta.com/blog/laravel-comments/>

为了在你的在线社区或博客中建立信任，你需要一个设计良好的 Laravel live 评论系统。

然而，第一次尝试就做对并不容易，除非你依赖自托管评论系统，如 [Disqus](https://kinsta.com/blog/wordpress-comment-plugins/#disqus) 或 Commento，它们都有自己的缺点。他们拥有你的数据，提供有限的设计和定制，最重要的是，他们不是免费的。

有了这些限制，如果建立你的实时评论系统的想法——有控制你的数据、设计和定制适合你的博客的外观和感觉的好处——吸引你，继续读下去。

这篇文章将教你如何开发一个具有不同评论功能的设计良好的实时评论系统。遵循用 Vue.js 和 Socket.io 构建[实时聊天应用的原则，我们将使用 Laravel、Pusher 和](https://masteringbackend.com/posts/build-a-real-time-chat-app-with-vue-3-socket-io-and-nodejs) [React](https://kinsta.com/knowledgebase/what-is-react-js/) 来开发实时评论系统。

让我们开始吧！

## 我们将建造什么

我们将建立一个[实时评论系统](https://www.youtube.com/watch?v=zrKgjbSn9F0)，它可以集成到任何网站或博客中，在社区中建立信任。

[To build trust in your online community or blog, one crucial element you’ll want is a well-designed Laravel live commenting system. 💬 Learn how to get started here ⤵Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Flaravel-comments%2F&via=kinsta&text=To+build+trust+in+your+online+community+or+blog%2C+one+crucial+element+you%E2%80%99ll+want+is+a+well-designed+Laravel+live+commenting+system.+%F0%9F%92%AC+Learn+how+to+get+started+here+%E2%A4%B5&hashtags=Laravel%2COnlineCommunity)

## 构建模块概述:Laravel、Pusher 和 Vue

在我们深入开发之前，让我们讨论一下我们将用来开发实时评论系统的技术。









### 拉勒韦尔

Laravel 是一个开源的面向 MVC 的 PHP 框架。它用于构建简单到复杂的 PHP web 应用程序，以其优雅的语法而闻名。[了解什么是 Laravel](https://kinsta.com/blog/laravel-tutorial/)对建立这个评论系统至关重要。

### 推进器

[Pusher](https://pusher.com/) 使开发者能够大规模创建实时功能。本文将结合 [Laravel Echo](https://laravel.com/docs/5.4/broadcasting) 创建一个对 Pusher 服务器的实时广播事件，并用 Vue.js 在前端显示内容

### view . js-检视. js

Vue.js 是我们首选的前端框架。Vue.js 是一个进步的 JavaScript 前端框架，以其简单易学和直接的前端开发方法而闻名。我们将使用 Vue.js 来开发我们的实时评论系统。

## 建立评论系统

如果我们上面概述的评论系统听起来像你想要的，让我们继续构建它。

### 1.安装和设置 Laravel、Pusher 和 Echo

Laravel、Echo 和 Pusher 的安装和设置非常简单，因为 Laravel 已经通过设置和配置 Laravel Echo 与 Pusher 完美配合完成了所有后台任务。

首先，我们将开始安装和配置 Laravel，我们的后端 [PHP 框架](https://kinsta.com/blog/php-frameworks/)。如果您已经全局安装了 [Laravel CLI](https://laravel.com/docs/8.x#the-laravel-installer) ，那么您可以使用这个命令获取 Laravel 的一个新实例:

```
laravel new commenter
```

您的新 Laravel 实例将安装在一个名为 commenter 的文件夹中。让我们打开[虚拟代码](https://kinsta.com/blog/php-editor/#1-visual-studio-code)中的文件夹，并在终端中导航至该文件夹:

```
cd commenter

code .
```

在我们启动开发服务器之前，让我们安装并配置一些将用于项目的必要包。

运行这个命令来安装 Pusher PHP SDK:

```
composer require pusher/pusher-php-server
```

运行此命令为 Vue.js 前端安装必要的 NPM 软件包:

```
npm install --save laravel-echo pusher-js
```

接下来，我们将配置 Laravel Echo 和 Pusher。打开您的**resources/js/bootstrap . js**文件，并粘贴以下脚本:

```
window._ = require("lodash");
window.axios = require("axios");
window.moment = require("moment");
window.axios.defaults.headers.common["X-Requested-With"] = "XMLHttpRequest";
window.axios.defaults.headers.post["Content-Type"] =
    "application/x-www-form-urlencoded";
window.axios.defaults.headers.common.crossDomain = true;
window.axios.defaults.baseURL = "/api";
let token = document.head.querySelector('meta[name="csrf-token"]');
if (token) {
    window.axios.defaults.headers.common["X-CSRF-TOKEN"] = token.content;
} else {
    console.error("CSRF token not found");
}

/**
 * Echo exposes an expressive API for subscribing to channels and listening
 * for events that Laravel broadcasts. Echo and event broadcasting
 * allows your team to build robust real-time web applications quickly.
 */
import Echo from "laravel-echo";
window.Pusher = require("pusher-js");
window.Echo = new Echo({
    broadcaster: "pusher",
    key: process.env.MIX_PUSHER_APP_KEY,
    cluster: process.env.MIX_PUSHER_APP_CLUSTER,
    forceTLS: true
});
```

您会从上面的脚本中注意到，我们只是用默认配置来配置 Axios 实例。接下来，我们将配置 Laravel Echo 来使用 Pusher 及其配置。

### 2.数据库设置和迁移

接下来，我们将创建并设置我们的数据库来存储持久化的注释。我们将使用 SQLite，尽管您可以使用自己选择的任何数据库客户机。

在数据库文件夹中创建一个 **database.sqlite** 文件，并更新您的**。env** 文件如下:

```
DB_CONNECTION=sqlite
DB_DATABASE=/Users/all/paths/to/project/commenter_be/database/database.sqlite
DB_HOST=127.0.0.1
DB_PORT=3306
DB_USERNAME=root
DB_PASSWORD=
```

接下来，运行此命令创建注释迁移，并使用以下脚本对其进行更新:

```
php artisan make:migration create_comments_table
```

打开**数据库/migrations/xxxx _ create _ comments _ table _ xxxx . PHP**文件并粘贴以下代码:

```
<?php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
class CreateCommentsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('comments', function (Blueprint $table) {
            $table->id();
            $table->string('content');
            $table->string('author');
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
        Schema::dropIfExists('comments');
    }
}
```

这将创建一个新的评论数据库表，并添加内容和作者列。

最后，要创建迁移，请运行以下命令:

```
php artisan migrate
```

### 3.创建模型

在 Laravel 中，模型很重要——它们是与我们的数据库通信和处理数据管理的最可靠的方式。

为了在 Laravel 中创建一个模型，我们将运行以下命令:

```
php artisan make:model Comment
```

接下来，打开 **app/models/Comment.php** 文件并粘贴以下代码:

```
<?php
namespace App\Models;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
class Comment extends Model
{
    use HasFactory;
    protected $fillable = ['content', 'author'];
} The $fillable array allows us to create and update the model in mass.
```

### 4.创建控制器

控制器至关重要，因为它们容纳了我们应用程序的所有逻辑、业务和其他内容，所以让我们创建一个控制器来处理注释逻辑:

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

```
php artisan make:controller CommentController
```

接下来，打开**app/Http/Controllers/comment controller . PHP**文件并粘贴以下代码:

```
<?php
namespace App\Http\Controllers;
use App\Models\Comment;
use App\Events\CommentEvent;
use Illuminate\Http\Request;

class CommentController extends Controller
{
    //
    public function index()
    {
        return view('comments');
    }
    public function fetchComments()
    {
        $comments = Comment::all();
        return response()->json($comments);
    }
    public function store(Request $request)
    {
        $comment = Comment::create($request->all());
        event(new CommentEvent($comment));
        return $comment;
    }
}
```

控制器有三种不同的方法:分别返回一个注释视图、获取所有注释和存储一个新注释。最重要的是，我们每次存储新评论时都会触发一个事件，前端会监听这个事件，使用 Pusher 和 Laravel Echo 用新评论实时更新相关页面。

### 5.创建路线

为了正确配置我们的路线，我们需要更新大量的[文件](https://kinsta.com/knowledgebase/wordpress-files/)，所以让我们开始吧。

首先，我们将更新 routes 文件夹中的**api.php**文件。打开文件并添加以下代码:

```
use App\Http\Controllers\CommentController;
//...

Route::get('/', [CommentController::class, 'index']);
Route::get('/comments', [CommentController::class, 'fetchComments']);
Route::post('/comments', [CommentController::class, 'store']);
```

接下来，打开同一个文件夹中的**channels.php**文件，并添加以下代码来授权我们之前触发的事件:

```
Broadcast::channel('comment', function ($user) {
    return true;
});
```

接下来，打开同一个文件夹中的**web.php**文件，并添加下面的代码，将我们的请求重定向到主页，Vue.js 将在那里获取它:

```
use App\Http\Controllers\CommentController;
//...

Route::get('/', [CommentController::class, 'index']);
```

最后，我们将在**资源/视图**文件夹中创建一个名为【comments.blade.php】T2 的新刀片文件，并添加以下代码:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>Commenter</title>
    <meta name="csrf-token" content="{{ csrf_token() }}">
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">

    
    <style>
        .container {
            margin: 0 auto;
            position: relative;
            width: unset;
        }
        #app {
            width: 60%;
            margin: 4rem auto;
        }
        .question-wrapper {
            text-align: center;
        }
    </style>
</head>
<body>

    <div id="app">
        <div class="container">
            <div class="question-wrapper">
                <h5 class="is-size-2" style="color: #220052;">
                    What do you think about <span style="color: #47b784;">Dogs</span>?</h5>
                <br>
                <a href="#Form" class="button is-medium has-shadow has-text-white" style="background-color: #47b784">Comment</a>
            </div>
            <br><br>
            <comments></comments>
            <new-comment></new-comment>
        </div>
    </div>
    <script async src="{{mix('js/app.js')}}"></script>
</body>
</html>
```

该脚本添加了一个文章标题和一个 Vue 组件，以显示上面创建的文章标题并向其添加新的评论。

运行以下命令来测试是否一切都正确:

需要一个给你带来竞争优势的托管解决方案吗？Kinsta 为您提供了令人难以置信的速度、一流的安全性和自动伸缩功能。[查看我们的计划](https://kinsta.com/plans/?in-article-cta)

```
npm run watch

php artisan serve
```

如果您看到了这个页面，那么您已经准备好进入本文的下一步了。

![Live commenting system in Laravel](img/8241c379fe99866f69d93113d0256777.png)

Live commenting system in Laravel



### 6.设置 Vue(前端)

我们将创建并设置我们的 Vue 实例，以创建并显示在这篇[帖子](https://kinsta.com/blog/wordpress-get-post-id/)上发表的所有评论。

我们将从建立我们的 Vuex 商店开始。在 resource/js/store 文件夹中创建以下文件。

#### 创建评论状态

创建 actions.js 并添加以下代码:

```
let actions = {
    ADD_COMMENT({ commit }, comment) {
        return new Promise((resolve, reject) => {
            axios
                .post(`/comments`, comment)
                .then(response => {
                    resolve(response);
                })
                .catch(err => {
                    reject(err);
                });
        });
    },
    GET_COMMENTS({ commit }) {
        axios
            .get("/comments")
            .then(res => {
                {
                    commit("GET_COMMENTS", res.data);
                }
            })
            .catch(err => {
                console.log(err);
            });
    }
};
export default actions;
```

动作文件调用后端的注释端点。

接下来，创建 getters.js 文件并添加以下代码:

```
let getters = {
    comments: state => {
        return state.comments;
    }
};
export default getters;
```

Getter 文件用于检索状态中的所有注释。

创建 mutations.js 文件，并将其粘贴到以下代码中:

```
let mutations = {
    GET_COMMENTS(state, comments) {
        state.comments = comments;
    },
    ADD_COMMENT(state, comment) {
        state.comments = [...state.comments, comment];
    }
};
export default mutations;
```

接下来，创建 state.js 文件并将其粘贴到以下代码中:

```
let state = {
    comments: []
};
export default state;
```

最后，我们将把所有内容添加到导出到 Vue 实例的 index.js 文件中，创建一个 index.js 文件并添加以下内容:

```
import Vue from "vue";
import Vuex from "vuex";
import actions from "./actions";
import mutations from "./mutations";
import getters from "./getters";
import state from "./state";
Vue.use(Vuex);
export default new Vuex.Store({
    state,
    mutations,
    getters,
    actions
});
```

#### 创建组件

最后，我们将创建注释组件来显示和添加新的注释。让我们从创建单个注释组件开始。

在 **resource/js** 文件夹中创建一个名为 components 的文件夹，添加 **comment.vue** 并添加以下代码:

```
<template>
  <li class="comment-wrapper animate slideInLeft">
    <div class="profile">
    </div>
    <div class="msg has-shadow">
      <div class="msg-body">
        <p class="name">
          {{ comment.author }} <span class="date">{{ posted_at }}</span>
        </p>
        <p class="content">{{ comment.content }}</p>
      </div>
    </div>
  </li>
</template>

    <script>
export default {
  name: "Comment",
  props: ["comment"],
  computed: {
    posted_at() {
      return moment(this.comment.created_at).format("MMMM Do YYYY");
    },

  },
};
</script>

    <style lang="scss" scoped>
.comment-wrapper {
  list-style: none;
  text-align: left;
  overflow: hidden;
  margin-bottom: 2em;
  padding: 0.4em;
  .profile {
    width: 80px;
    float: left;
  }
  .msg-body {
    padding: 0.8em;
    color: #666;
    line-height: 1.5;
  }
  .msg {
    width: 86%;
    float: left;
    background-color: #fff;
    border-radius: 0 5px 5px 5px;
    position: relative;
    &::after {
      content: " ";
      position: absolute;
      left: -13px;
      top: 0;
      border: 14px solid transparent;
      border-top-color: #fff;
    }
  }
  .date {
    float: right;
  }
  .name {
    margin: 0;
    color: #999;
    font-weight: 700;
    font-size: 0.8em;
  }
  p:last-child {
    margin-top: 0.6em;
    margin-bottom: 0;
  }
}
</style>
```

接下来，在同一个文件夹中创建以下名为 **comments.vue** 的文件，并添加以下代码:

```
<template>
  <div class="container">
    <ul class="comment-list">
      <Comment
        :key="comment.id"
        v-for="comment in comments"
        :comment="comment"
      ></Comment>
    </ul>
  </div>
</template>

    <script>
import { mapGetters } from "vuex";
import Comment from "./Comment";
export default {
  name: "Comments",
  components: { Comment },
  mounted() {
    this.$store.dispatch("GET_COMMENTS");
    this.listen();
  },
  methods: {
    listen() {
      Echo.channel("comment").listen("comment", (e) => {
        console.log(e);
        this.$store.commit("ADD_COMMENT", e);
      });
    },
  },
  computed: {
    ...mapGetters(["comments"]),
  },
};
</script>

    <style scoped>
.comment-list {
  padding: 1em 0;
  margin-bottom: 15px;
}
</style>
```

最后，创建一个名为 **NewComment.vue** 的文件，并添加以下代码:

```
<template>
  <div id="commentForm" class="box has-shadow has-background-white">
    <form @keyup.enter="postComment">
      <div class="field has-margin-top">
        <div class="field has-margin-top">
          <label class="label">Your name</label>
          <div class="control">
            <input
              type="text"
              placeholder="Your name"
              class="input is-medium"
              v-model="comment.author"
            />
          </div>
        </div>
        <div class="field has-margin-top">
          <label class="label">Your comment</label>
          <div class="control">
            <textarea
              style="height: 100px"
              name="comment"
              class="input is-medium"
              autocomplete="true"
              v-model="comment.content"
              placeholder="lorem ipsum"
            ></textarea>
          </div>
        </div>
        <div class="control has-margin-top">
          <button
            style="background-color: #47b784"
            :class="{ 'is-loading': submit }"
            class="button has-shadow is-medium has-text-white"
            :disabled="!isValid"
            @click.prevent="postComment"
            type="submit"
          >
            Submit
          </button>
        </div>
      </div>
    </form>
    <br />
  </div>
</template>

    <script>
export default {
  name: "NewComment",
  data() {
    return {
      submit: false,
      comment: {
        content: "",
        author: "",
      },
    };
  },
  methods: {
    postComment() {
      this.submit = true;
      this.$store
        .dispatch("ADD_COMMENT", this.comment)
        .then((response) => {
          this.submit = false;
          if (response.data) console.log("success");
        })
        .catch((err) => {
          console.log(err);
          this.submit = false;
        });
    },
  },
  computed: {
    isValid() {
      return this.comment.content !== "" && this.comment.author !== "";
    },
  },
};
</script>

    <style scoped>
.has-margin-top {
  margin-top: 15px;
}
</style>
```

现在，打开 **app.js** 文件，添加以下代码来注册您之前创建的 Vue 组件:

```
// resource/js/app.js

require("./bootstrap");
window.Vue = require("vue");
import store from "./store/index";

Vue.component("comment", require("./components/Comment"));
Vue.component("comments", require("./components/Comments"));
Vue.component("new-comment", require("./components/NewComment"));

const app = new Vue({
    el: "#app",
    store
});
```

[Want to build your own personalized commenting system? 💬 This post has everything you need to get started 🚀Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Flaravel-comments%2F&via=kinsta&text=Want+to+build+your+own+personalized+commenting+system%3F+%F0%9F%92%AC+This+post+has+everything+you+need+to+get+started+%F0%9F%9A%80&hashtags=Laravel%2COnlineCommunity)

## 摘要

就是这样！您刚刚学习了如何使用 Laravel 为您的站点构建一个实时评论系统。

我们已经讨论了在你的社区或博客中建立信任的过程中创建和管理评论系统的好处。我们还探索了如何利用不同的评论功能从头开始开发一个设计良好的实时评论系统。

你可以在[这个 Github repo](https://github.com/Kaperskyguru/commenta) 里克隆这个项目的源代码。

你对我们一起建立的 Laravel 实时评论系统有什么看法？请在评论中告诉我们！

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。