# PHP 8.2 的新特性——新特性、弃用、变化等等

> 原文：<https://kinsta.com/blog/php-8-2/>

PHP 8.2 建立在由 [PHP 8.0](https://kinsta.com/blog/php-8/) 和 [PHP 8.1](https://kinsta.com/blog/php-8-1/) 提出的更新基础之上。既然 [PHP 8.2](https://www.php.net/releases/8.2/en.php) 已经发布，让我们详细介绍一下 PHP 8.2 中的新特性——从它的新特性和改进到弃用和小改动，我们将一一介绍。

随着 PHP 8.2 于 2022 年 7 月 19 日进入特性冻结期，你可以预期这个列表不会有重大的增加。

激动吗？我们也是。

我们开始吧！

## PHP 8.2 的新特性和改进

让我们从探索所有最新的 PHP 8.2 特性开始。这是一个很长的列表:

### 新的`readonly`类

PHP 8.1 为类属性引入了 [`readonly`特性。现在，PHP 8.2 增加了对](https://kinsta.com/blog/php-8-1/#new-readonly-properties)[声明整个类为`readonly`](https://wiki.php.net/rfc/readonly_classes) 的支持。









如果你声明一个类为`readonly`，它的所有属性将自动继承`readonly`特性。因此，声明一个类`readonly`等同于将每个类属性声明为`readonly`。

例如，在 PHP 8.1 中，您必须编写这段冗长的代码来将所有类属性声明为`readonly`:

```
class MyClass
{
public readonly string $myValue,
public readonly int $myOtherValue
public readonly string $myAnotherValue
public readonly int $myYetAnotherValue
}
```

想象一下更多的属性也是如此。现在，有了 PHP 8.2，你可以这样写:

```
readonly class MyClass
{
public string $myValue,
public int $myOtherValue
public string $myAnotherValue
public int $myYetAnotherValue
}
```

也可以将抽象类或最终类声明为`readonly`。在这里，关键字的顺序并不重要。

```
abstract readonly class Free {}
final readonly class Dom {}
```

也可以声明一个没有属性的`readonly`类。这有效地防止了动态属性，同时仍然允许子类显式声明它们的`readonly`属性。

接下来，`readonly`类只能包含类型化属性——声明单个**只读**属性的规则相同。

如果不能声明严格类型属性，可以使用`mixed`类型属性。

试图声明一个没有类型化属性的`readonly`类将导致致命错误:

```
readonly class Type {
    public $nope;
}
Fatal error: Readonly property Type::$nope must have type in ... on line ... 
```

此外，您不能为某些 PHP 特性声明`readonly`:

*   **枚举**(作为[它们不能包含任何属性](https://kinsta.com/blog/php-8-1/#enums))
*   **特质**
*   **接口**

试图将这些特性中的任何一个声明为`readonly`都会导致解析错误。

```
readonly interface Destiny {}
Parse error: syntax error, unexpected token "interface", expecting "abstract" or "final" or "readonly" or "class" in ... on line ...
```

和所有 PHP 关键字一样，`readonly`关键字不区分大小写。

PHP 8.2 也不赞成动态属性(稍后会详细介绍)。但是您不能阻止将动态属性添加到类中。然而，对一个`readonly`类这样做只会导致致命的错误。

```
Fatal error: Readonly property Test::$test must have type in ... on line ...
```

### 允许`true`、`false`和`null`作为独立类型

PHP 已经包含了标量类型，如`int`、`string`和`bool`。这在 PHP 8.0 中得到了扩展，增加了[联合类型](https://kinsta.com/blog/php-8/#union-types-2-0)，允许不同类型的值。同一个 RFC 还允许使用`false`和`null`作为联合类型的一部分——但是不允许它们作为独立类型。

如果您试图将`false`或`null`声明为独立类型——而不是联合类型的一部分——就会导致致命错误。

```
function spam(): null {}
function eggs(): false {}

Fatal error: Null can not be used as a standalone type in ... on line ...
Fatal error: False can not be used as a standalone type in ... on line ...
```

为了避免这种情况，PHP 8.2 增加了对使用 [`false`和`null`](https://wiki.php.net/rfc/null-false-standalone-types) 作为独立类型的支持。有了这个补充，PHP 的类型系统更有表现力，也更完整。现在，您可以精确地声明返回、参数和属性类型。

此外，PHP 仍然没有包含一个`true`类型，它似乎是`false`类型的自然对应。PHP 8.2 修复了这个问题，[也增加了对`true`类型](https://wiki.php.net/rfc/true-type)的支持。它不允许强制，就像`false`类型的行为一样。

`true`和`false`类型本质上都是 PHP 的`bool`类型的联合类型。为了避免冗余，不能在一个联合类型中同时声明这三种类型。这样做会导致编译时致命错误。

### 析取范式(DNF)类型

[析取范式(DNF)](https://en.wikipedia.org/wiki/Disjunctive_normal_form) 是组织布尔表达式的标准化方式。它由连接词的析取组成——用布尔术语来说，就是一个**或 and**。

将 DNF 应用于类型声明允许以一种标准的方式编写解析器可以处理的联合和交集类型。如果使用得当，PHP 8.2 的[新 DNF 类型](https://wiki.php.net/rfc/dnf_types)特性简单而强大。

RFC 给出了下面的例子。它假设下列接口和类定义已经存在:

```
interface A {}
interface B {}
interface C extends A {}
interface D {}

class W implements A {}
class X implements B {}
class Y implements A, B {}
class Z extends Y implements C {}
```

使用 DNF 类型，可以对属性、参数和返回值执行类型声明，如下所示:

```
// Accepts an object that implements both A and B,
// OR an object that implements D
(A&B)|D

// Accepts an object that implements C, 
// OR a child of X that also implements D,
// OR null
C|(X&D)|null

// Accepts an object that implements all three of A, B, and D, 
// OR an int, 
// OR null.
(A&B&D)|int|null
```

在某些情况下，属性可能不是 DNF 形式。这样声明它们会导致解析错误。但是您总是可以将它们重写为:

```
A&(B|D)
// Can be rewritten as (A&B)|(A&D)

A|(B&(D|W)|null)
// Can be rewritten as A|(B&D)|(B&W)|null
```

您应该注意，DNF 类型的每个段必须是唯一的。例如，声明`(A&B)|(B&A)`无效，因为两个**或** ed 段在逻辑上是相同的。

除此之外，作为另一个段的严格子集的段也是不允许的。这是因为超集已经拥有了子集的所有实例，所以使用 DNF 是多余的。

### 修订回溯中的敏感参数

像几乎所有的编程语言一样， [PHP](https://kinsta.com/php/) 允许在代码执行的任何时候跟踪它的调用栈。堆栈跟踪使得调试代码以修复错误和性能瓶颈变得容易。它构成了像 [Kinsta APM](https://kinsta.com/apm-tool/) ，我们为 WordPress 站点定制的[性能监控工具](https://kinsta.com/blog/application-performance-monitoring/)这样的工具的主干。

![Tracking slow WooCommerce transactions through the Kinsta APM tool. ](img/57f3f72221328aabee1f515273ecc76d.png)

Tracking slow WooCommerce transactions with Kinsta APM.



执行堆栈跟踪不会停止程序的执行。通常情况下，大多数堆栈跟踪在后台运行，并被静默记录，以便日后需要时进行检查。

然而，如果您与第三方服务共享这些详细的 PHP 堆栈跟踪，其中一些可能是一个缺点——通常用于[错误日志分析](https://kinsta.com/knowledgebase/wordpress-error-log/)，错误跟踪等。这些堆栈跟踪可能包括敏感信息，如用户名、密码和环境变量。

[RFC 提案](https://wiki.php.net/rfc/redact_parameters_in_back_traces)给出了一个这样的例子:

> 一个常见的“违规者”是 PDO，它将数据库密码作为构造函数参数，并立即尝试在构造函数中连接到数据库，而不是拥有一个纯构造函数和一个 **separate - > connect()** 方法。因此，当数据库连接失败时，堆栈跟踪将包括数据库密码:
> 
> ```
> PDOException: SQLSTATE[HY000] [2002] No such file or directory in /var/www/html/test.php:3
> 
> Stack trace: #0 /var/www/html/test.php(3): PDO->__construct('mysql:host=loca...', 'root', 'password')
> 
> #1 {main}
> ```

PHP 8.2 允许你用一个新的`\SensitiveParameter`属性[标记这些敏感参数](https://wiki.php.net/rfc/redact_parameters_in_back_traces)。任何标记为敏感的参数都不会在回溯中列出。因此，您可以与任何第三方服务共享它们。

这里有一个简单的例子，只有一个敏感参数:

```
<?php

function example(
    $ham,
    #[\SensitiveParameter] $eggs,
    $butter
) {
    throw new \Exception('Error');
}

example('ham', 'eggs', 'butter');

/*
Fatal error: Uncaught Exception: Error in test.php:8
Stack trace:
#0 test.php(11): test('ham', Object(SensitiveParameterValue), 'butter')
#1 {main}
thrown in test.php on line 8
*/
```

当您生成一个回溯时，任何带有`\SensitiveParameter`属性的参数都将被替换为一个`\SensitiveParameterValue`对象，并且它的真实值永远不会存储在跟踪中。`SensitiveParameterValue`对象封装了实际的参数值——如果你出于任何原因需要它的话。

### 新的`mysqli_execute_query`功能和`mysqli::execute_query`方法

您是否曾经使用带有危险转义用户值的`mysqli_query()`函数来运行一个参数化的 MySQLi 查询？

PHP 8.2 通过新的`mysqli_execute_query($sql, $params)`函数和`mysqli::execute_query`方法使得[运行参数化 MySQLi 查询变得更加容易](https://wiki.php.net/rfc/mysqli_execute_query)。

本质上，这个新函数是`mysqli_prepare()`、`mysqli_execute()`和`mysqli_stmt_get_result()`函数的组合。有了它，MySQLi 查询将在函数本身中准备、绑定(如果传递任何参数)和执行。如果查询成功运行，它将返回一个`mysqli_result`对象。如果不成功，它将返回`false`。

RFC 提案给出了一个简单而有力的例子:

```
foreach ($db->execute_query('SELECT * FROM user WHERE name LIKE ? AND type_id IN (?, ?)', [$name, $type1, $type2]) as $row) {
print_r($row);
}
```

### 获取`const`表达式中的`enum`属性

[这个 RFC 提议](https://wiki.php.net/rfc/fetch_property_in_const_expressions)允许`->/?->`操作符在`const`表达式中获取 [`enum`](https://kinsta.com/blog/php-8-1/#enums) 属性。

这个新特性的主要原因是你不能在某些地方使用`enum`对象，比如数组键。在这种情况下，您必须重复`enum` case 的值才能使用它。

允许在不允许使用`enum`对象的地方获取`enum`属性可以简化这个过程。

这意味着以下代码现在有效:

```
const C = [self::B->value => self::B];
```

为了安全起见，这个 RFC 还包括对 nullsafe 操作符`?->`的支持。

### 特征中允许常量

PHP 包含了一种重用代码的方法，称为 Traits。它们非常适合跨类重用代码。

目前，Traits 只允许定义方法和属性，而不允许定义常量。这意味着您不能在特征本身中定义特征所期望的不变量。为了绕过这个限制，您需要在它的组成类或由它的组成类实现的接口中定义常量。

该 RFC 提议允许在特征中定义常数。可以像定义类常量一样定义这些常量。这个直接取自 RFC 的例子澄清了它的用法:

```
trait Foo {
    public const FLAG_1 = 1;
    protected const FLAG_2 = 2;
    private const FLAG_3 = 2;

    public function doFoo(int $flags): void {
        if ($flags & self::FLAG_1) {
            echo 'Got flag 1';
        }
        if ($flags & self::FLAG_2) {
            echo 'Got flag 2';
        }
        if ($flags & self::FLAG_3) {
        echo 'Got flag 3';
        }
    }
}
```

Trait 常量也被合并到构成类的定义中，就像 Trait 的属性和方法定义一样。它们也有类似的限制作为性状的属性。正如 RFC 中所提到的，这个提议——虽然是一个好的开始——需要进一步的工作来充实这个特性。


## php 8.2 中的解除

我们现在可以开始研究 PHP 8.2 中所有的不赞成之处。这个列表没有它的新特性那么大:

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter) ### 弃用动态属性(和新的`#[AllowDynamicProperties]`属性)

在 PHP 8.1 之前，您可以在 PHP 中动态设置和检索未声明的类属性。例如:

```
class Post {
    private int $pid;
}

$post = new Post();
$post->name = 'Kinsta';
```

 `这里，`Post`类没有声明`name`属性。但是因为 PHP 允许动态属性，所以可以在类声明之外设置它。这是它最大的——也可能是唯一的——优势。

动态属性允许代码中突然出现意想不到的错误和行为。例如，如果您在类外声明类属性时犯了任何错误，很容易就会失去对它的跟踪——尤其是在调试该类内的任何错误时。

从 PHP 8.2 开始，[动态属性被弃用](https://wiki.php.net/rfc/deprecate_dynamic_properties)。为未声明的类属性设置值将在第一次设置该属性时发出反对通知。

```
class Foo {}
$foo = new Foo;

// Deprecated: Creation of dynamic property Foo::$bar is deprecated
$foo->bar = 1;

// No deprecation warning: Dynamic property already exists.
$foo->bar = 2;
```

 `然而，从 PHP 9.0 开始，同样的设置会抛出一个`ErrorException`错误。

如果您的代码充满了动态属性——有很多 PHP 代码就是如此——并且如果您想在升级到 PHP 8.2 后停止这些反对通知，您可以使用 PHP 8.2 的新`#[AllowDynamicProperties]`属性来允许类上的动态属性。

```
#[AllowDynamicProperties]
class Pets {}
class Cats extends Pets {}

// You'll get no deprecation warning
$obj = new Pets;
$obj->test = 1;

// You'll get no deprecation warning for child classes
$obj = new Cats;
$obj->test = 1;
```

根据 RFC，标记为`#[AllowDynamicProperties]`的类及其子类可以继续使用动态属性，而不会被弃用或删除。

您还应该注意到，在 PHP 8.2 中，唯一标记为`#[AllowDynamicProperties]`的绑定类是`stdClass`。此外，通过`__get()`或`__set()` [PHP 魔法方法](https://www.php.net/manual/en/language.oop5.magic.php)访问的任何属性都不被视为动态属性，因此它们不会抛出反对通知。

### 不推荐使用的部分支持的可调用程序

PHP 8.2 的另一个变化是[不支持部分支持的可调用函数](https://wiki.php.net/rfc/deprecate_partially_supported_callables)，尽管影响更小。

这些可调用程序被称为部分支持，因为您不能通过`$callable()`直接与它们交互。您只能通过`call_user_func($callable)`功能来访问它们。这种可调用的列表并不长:

```
"self::method"
"parent::method"
"static::method"
["self", "method"]
["parent", "method"]
["static", "method"]
["Foo", "Bar::method"]
[new Foo, "Bar::method"]
```

从 PHP 8.2 开始，任何调用此类可调用函数的尝试——比如通过`call_user_func()`或`array_map()`函数——都会抛出一个不赞成警告。

最初的 RFC 给出了支持这种反对意见的可靠理由:

> *除了最后两种情况，所有这些调用都是上下文相关的。`"self::method"`引用的方法取决于从哪个类执行调用或可调用性检查。实际上，当以`[new Foo, "parent::method"]`的形式使用时，这通常也适用于后两种情况。*
> 
> *减少可调用程序的上下文依赖是这个 RFC 的次要目标。在这个 RFC 之后，唯一剩下的作用域依赖就是方法可见性:`"Foo::bar"`可能在一个作用域中可见，但在另一个作用域中不可见。如果将来可调用的方法被限制为公共方法(而私有方法将必须使用一级可调用的方法或`Closure::fromCallable()`来独立于范围)，那么可调用的类型将被很好地定义，并可以被用作属性类型。但是，不建议将可见性处理的变更作为 RFC* 的一部分。

按照最初的 RFC，`is_callable()`函数和`callable`类型将继续接受这些可调用的异常。但是直到 PHP 9.0 以后对它们的支持被完全移除。

为了避免混淆，这个弃用通知的范围[被一个新的 RFC](https://wiki.php.net/rfc/partially-supported-callables-expand-deprecation-notices) 扩展了——它现在包括了这些例外。

很高兴看到 PHP 朝着定义良好的`callable`类型发展。

### 弃用`#utf8_encode()`和`utf8_decode()`功能

PHP 的内置函数`utf8_encode()`和`utf8_decode()`将 ISO-8859-1(“latin1”)编码的字符串与 UTF-8 进行相互转换。

然而，它们的名字暗示了比它们的实现所允许的更广泛的用途。“Latin 1”编码通常会与其他编码混淆，如“Windows 代码页 1252”

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

此外，当这些函数不能正确转换任何字符串时，您通常会看到 [Mojibake](https://en.wikipedia.org/wiki/Mojibake) 。缺少错误信息也意味着很难发现它们，尤其是在大量清晰易读的文本中。

PHP 8.2 [不赞成`#utf8_encode()`和`utf8_decode()`函数](https://wiki.php.net/rfc/remove_utf8_decode_and_utf8_encode)。如果您调用它们，您将看到这些弃用通知:

```
Deprecated: Function utf8_encode() is deprecated
Deprecated: Function utf8_decode() is deprecated
```

RFC 建议使用 [PHP 支持的扩展](https://kinsta.com/blog/install-php/#all-about-php-extensions)，比如`mbstring`、`iconv`和`intl`。

### 反对`${}`字符串插值

PHP 允许以几种方式在带双引号(`"`)和 heredoc ( `<<<`)的字符串中嵌入变量:

1.  直接嵌入变量— `“$foo”`
2.  变量外有大括号— `“{$foo}”`
3.  美元符号后有大括号— `“${foo}”`
4.  可变变量— `“${expr}”` —相当于使用`(string) ${expr}`

前两种方法各有利弊，后两种方法的语法复杂且相互冲突。PHP 8.2 [不赞成最后两种字符串插值方式](https://wiki.php.net/rfc/deprecate_dollar_brace_string_interpolation)。

你应该避免以这种方式插入字符串:

```
"Hello, ${world}!";
Deprecated: Using ${} in strings is deprecated

"Hello, ${(world)}!";
Deprecated: Using ${} (variable variables) in strings is deprecated
```

从 PHP 9.0 开始，这些弃用将被升级为抛出异常错误。

### 不推荐 Base64/QPrint/Uuencode/HTML 实体使用 mbstring 函数

PHP 的 mbstring(多字节字符串)函数帮助我们处理 Unicode、HTML 实体和其他遗留文本编码。

然而，Base64、Uuencode 和 QPrint 不是文本编码，仍然是这些函数的一部分——主要是由于传统原因。PHP 还包括这些编码的单独实现。

至于 HTML 实体，PHP 有内置函数——`htmlspecialchars()`和`htmlentities()`——来更好地处理这些。例如，与 mbstring 不同，这些函数也将转换`<`。`>`和`&`字符转换为 HTML 实体。

而且 PHP 一直在改进内置函数——[就像 PHP 8.1 有 HTML 编码解码函数](https://kinsta.com/blog/php-8-1/#html-encoding-and-decoding-functions-now-use-ent_quotes--ent_substitute)一样。

因此，记住所有这些，PHP 8.2 是[反对使用 mbstring 作为这些编码](https://github.com/php/php-src/commit/9308974f8cc6c1046f228be5320fe067913ba987)(标签不区分大小写):

*   BASE64
*   哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜哇呜
*   HTML-实体
*   HTML(HTML 实体的别名)
*   报价-可打印
*   qprint(报价-可打印的别名)

从 PHP 8.2 开始，使用 mbstring 编码/解码上述任何一种都会发出一个弃用通知。PHP 9.0 将完全移除对这些编码的 mbstring 支持。

## PHP 8.2 中的其他小变化

最后，我们可以讨论 PHP 8.2 的微小变化，包括它移除的特性和功能。

### 从 mysql 中移除对 libmysql 的支持

截至目前，PHP 允许`mysqli`和`PDO_mysql`驱动程序构建`mysqlnd`和`libmysql`库。然而，从 PHP 5.4 开始，默认和推荐的驱动程序是`mysqlnd`。

这两种驱动程序都有许多优点和缺点。然而，移除对其中一个的支持——理想情况下，[移除`libmysql`](https://wiki.php.net/rfc/mysqli_support_for_libmysql) ,因为它不是默认的——将简化 PHP 的代码和单元测试。

为了证明这一点，RFC 列出了`mysqlnd`的许多优点:

*   它与 PHP 捆绑在一起
*   它使用 PHP 内存管理来监控内存使用情况
    [提高性能](https://kinsta.com/blog/laravel-performance/)
*   提供生活质量功能(如`get_result()`)
*   使用 PHP 原生类型返回数值
*   它的功能不依赖于外部库
*   可选插件功能
*   支持异步查询

RFC 还列出了`libmysql`的一些优势，包括:

*   自动重新连接是可能的(`mysqlnd`不支持这一功能，因为它很容易被利用)
*   LDAP 和 SASL 认证模式(`mysqlnd` [可能很快也会添加这个功能](https://github.com/php/php-src/pull/6447)

此外，RFC 列出了`libmysql`的许多缺点——与 PHP 内存模型不兼容、许多失败的测试、内存泄漏、不同版本之间的不同功能等等。

记住这一点，PHP 8.2 移除了对针对`libmysql`构建`mysqli`的支持。

如果你想添加任何只有`libmysql`才有的功能，你必须把它作为一个特性请求明确地添加到 `mysqlnd`。此外，您不能添加自动重新连接。

### 独立于区域设置的大小写转换

在 [PHP 8.0](https://kinsta.com/blog/php-8/) 之前，PHP 的区域设置是从系统环境继承的。但是在某些边缘情况下，这可能会导致问题。

安装 Linux 时设置您的语言将会为[的内置命令](https://kinsta.com/blog/linux-commands/)设置合适的用户界面语言。然而，它也意外地改变了 C 库的字符串处理功能的工作方式。

例如，如果您在安装 Linux 时选择了“土耳其语”或“哈萨克语”，您会发现调用`toupper('i')`来获得它的大写字母将获得[点状大写 I](https://www.wikiwand.com/en/%C4%B0) (U+0130，`İ`)。

PHP 8.0 通过将默认语言环境设置为“C”来阻止这种异常，除非用户通过`setlocale()`明确更改它。

PHP 8.2 走得更远，通过[去除了大小写转换的地区敏感性](https://wiki.php.net/rfc/strtolower-ascii)。本 RFC 主要更改`strtolower()`、`strtoupper()`及相关功能。阅读 RFC 以获得所有受影响的函数的列表。

作为替代，如果您想使用本地化的大小写转换，那么您可以使用`mb_strtolower()`。

### 随机延伸改进

PHP 正计划[彻底检查其随机功能](https://wiki.php.net/rfc/rng_extension)。

到目前为止，PHP 的随机功能严重依赖于 [Mersenne Twister 状态](https://en.wikipedia.org/wiki/Mersenne_Twister)。然而，这种状态被隐式地存储在 PHP 的全局区域中——用户无法访问它。在初始播种阶段和预期用途之间添加随机化函数会破坏代码。

当您的代码使用外部包时，维护这样的代码会更加复杂。

因此，PHP 当前的随机功能不能一致地再现随机值。它甚至无法通过均匀随机数生成器的经验统计测试，如 [TestU01 的 Crush 和 BigCrush](http://simul.iro.umontreal.ca/testu01/tu01.html) 。Mersenne Twister 的 32 位限制进一步加剧了这种情况。

因此，如果你需要加密的安全随机数，不推荐使用 PHP 的内置函数——`shuffle()`、`str_shuffle()`、`array_rand()`。在这种情况下，您需要使用`random_int()`或类似的函数实现一个新的函数。

然而，[在投票开始后，该 RFC](https://wiki.php.net/rfc/random_extension_improvement) 出现了几个问题。这一挫折迫使 PHP 团队在一个单独的 RFC 中记录所有问题，并为每个问题创建一个投票选项。只有在达成共识后，他们才会决定进一步行动。

## PHP 8.2 中的附加 RFC

PHP 8.2 还包括许多新功能和微小的变化。我们将在下面提到它们，并提供附加资源的链接:

1.  [新的`curl_upkeep`函数](https://github.com/php/php-src/pull/8720) : PHP 8.2 在其 Curl 扩展中增加了这个新函数。它调用 libcurl 中的`curl_easy_upkeep()`函数，libcurl 是 PHP Curl 扩展使用的底层 C 库。
2.  [新`ini_parse_quantity`函数](https://php.watch/versions/8.2/ini_parse_quantity) : PHP INI 指令接受带乘数后缀的数据大小。例如，你可以把 25 兆字节写成`25M`，或者把 42 千兆字节写成`42G`。这些后缀在 PHP INI 文件中很常见，但在其他地方并不常见。这个新函数解析 [PHP INI 值](https://kinsta.com/blog/increase-max-upload-size-wordpress/#create-or-modify-the-phpini-file)，并以字节为单位返回它们的数据大小。
3.  [新增`memory_reset_peak_usage`函数](https://github.com/php/php-src/pull/8151/files):该函数重置`memory_get_peak_usage`函数返回的内存使用峰值。当您多次运行同一个操作，并希望记录每次运行的内存使用峰值时，这非常方便。
4.  [支持`preg_*`函数](https://github.com/php/php-src/pull/7583)中的无捕获修饰符(`/n`):在 regex 中，`()`元字符表示一个捕获组。这意味着括号内的表达式的所有匹配都被返回。PHP 8.2 增加了一个 no-capture 修饰符(`/n`)来阻止这种行为。
5.  [让`iterator_*()`家族接受所有可迭代的](https://wiki.php.net/rfc/iterator_xyz_accept_array):截至目前，PHP 的`iterator_*()`家族只接受`\Traversables`(即不允许使用普通数组)。这是不必要的限制，这个 RFC 解决了这个问题。

## 摘要

PHP 8.2 建立在 PHP 8.0 和 PHP 8.1 的巨大改进之上，这绝非易事。我们认为 PHP 8.2 最令人兴奋的特性是它新的独立类型、只读属性和大量的性能改进。

我们迫不及待地想用各种 [PHP 框架](https://kinsta.com/blog/php-frameworks/)和 [CMSs](https://kinsta.com/cms-market-share/) 对 PHP 8.2 进行基准测试。

请确保将这篇博客文章加入书签，以供将来参考。

*你最喜欢 PHP 8.2 的哪些特性？哪些贬低是你最不喜欢的？请在评论中与我们的社区分享你的想法！*

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。``