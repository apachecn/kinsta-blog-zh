# PHP 7.4 的新特性(特性、弃用、速度)

> 原文：<https://kinsta.com/blog/php-7-4/>

PHP 7.4 是 PHP 7 的下一个次要版本，已于 2019 年 11 月 28 日正式发布。因此，是时候让我们深入了解一些最令人兴奋的新增功能和新特性了，它们将使 PHP 变得更快、更可靠。

**更新:** [PHP 8.1(正式发布)](https://kinsta.com/feature-updates/php-8-1/) 现已面向所有 Kinsta 客户端。Kinsta 不再支持 PHP 7.4。请注意，我们支持 PHP 8.0 和 8.1 版本。

即使 PHP 7.4 显著提升了性能并改善了代码可读性，PHP 8 将是 PHP 性能的真正里程碑，因为包含 JIT 的提议已经被批准了。

无论如何，今天我们将讨论 PHP 7.4 中一些最有趣的特性和变化。请注意，以下是 7.4 版本的重要日期:

*   2019 年 6 月 6 日:PHP 7.4 Alpha 1
*   2019 年 7 月 18 日:PHP 7.4 Beta 1——功能冻结
*   2019 年 11 月 28 日:PHP 7.4 GA 发布

你可以在官方 RFC 页面上查看完整的特性和添加列表。

## PHP 7.4 有什么新特性？

在本帖中，我们将介绍 PHP 7.4 最终版本应该增加的一些变化和特性:





> Kinsta 把我宠坏了，所以我现在要求每个供应商都提供这样的服务。我们还试图通过我们的 SaaS 工具支持达到这一水平。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![](img/60f15faa5735bd2437bf9dada5ee9192.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Suganthan Mohanadasan from @Suganthanmn</cite></footer>

[View plans](https://kinsta.com/plans/)

### 忘记 array_merge: PHP 7.4 在数组表达式中引入了 Spread 运算符

从 PHP 5.6 开始，[参数解包](https://wiki.php.net/rfc/argument_unpacking)是一种将数组和[遍历](https://www.php.net/manual/en/class.traversable.php)解包到参数列表中的语法。要解包数组或可遍历对象，必须在它前面加上… (3 个点)，如下例所示:

```
function test(...$args) { var_dump($args); }
test(1, 2, 3);
```

现在[这个 PHP 7.4 RFC](https://wiki.php.net/rfc/spread_operator_for_array) 提议将这个特性扩展到数组定义:

```
$arr = [...$args];
```

数组表达式中的 **Spread 操作符的第一个好处就是性能。事实上，[RFC 文件规定](https://wiki.php.net/rfc/spread_operator_for_array):**

> 展开运算符应该比`array_merge`有更好的性能。这不仅是因为 spread 操作符是一个语言结构，而`array_merge`是一个函数，还因为编译时优化可以对常量数组执行。

Spread 操作符的一个显著优点是它支持任何可遍历的对象，而`array_merge`函数只支持数组。

以下是数组表达式中参数解包的示例:

```
$parts = ['apple', 'pear'];
$fruits = ['banana', 'orange', ...$parts, 'watermelon'];
var_dump($fruits);
```

如果在 PHP 7.3 或更早版本中运行这段代码，PHP 会抛出一个解析错误:

```
Parse error: syntax error, unexpected '...' (T_ELLIPSIS), expecting ']' in /app/spread-operator.php on line 3
```

相反，PHP 7.4 会返回一个数组:

```
array(5) {
	[0]=>
	string(6) "banana"
	[1]=>
	string(6) "orange"
	[2]=>
	string(5) "apple"
	[3]=>
	string(4) "pear"
	[4]=>
	string(10) "watermelon"
}
```

RFC 声明我们可以多次扩展同一个数组。此外，我们可以在数组中的任何地方使用扩展操作符语法，因为普通元素可以添加在扩展操作符之前或之后。因此，下面的代码将如我们预期的那样工作:

```
$arr1 = [1, 2, 3];
$arr2 = [4, 5, 6];
$arr3 = [...$arr1, ...$arr2];
$arr4 = [...$arr1, ...$arr3, 7, 8, 9];
```

也可以将函数返回的数组直接解包到一个新的数组中:

```
function buildArray(){
	return ['red', 'green', 'blue'];
}
$arr1 = [...buildArray(), 'pink', 'violet', 'yellow'];
```

PHP 7.4 输出以下数组:

```
array(6) {
	[0]=>
	string(3) "red"
	[1]=>
	string(5) "green"
	[2]=>
	string(4) "blue"
	[3]=>
	string(4) "pink"
	[4]=>
	string(6) "violet"
	[5]=>
	string(6) "yellow"
}
```

我们也可以使用[生成器语法](https://www.php.net/manual/en/language.generators.syntax.php):

```
function generator() {
	for ($i = 3; $i <= 5; $i++) {
		yield $i;
	}
}
$arr1 = [0, 1, 2, ...generator()];
```

但是我们不允许解包通过引用传递的数组。考虑下面的例子:

```
$arr1 = ['red', 'green', 'blue'];
$arr2 = [...&$arr1];
```

如果我们试图通过引用解包一个数组，PHP 会抛出下面的解析错误:

```
Parse error: syntax error, unexpected '&' in /app/spread-operator.php on line 3
```

无论如何，如果第一个数组的元素通过引用存储，那么它们也通过引用存储在第二个数组中。这里有一个例子:

```
$arr0 = 'red';
$arr1 = [&$arr0, 'green', 'blue'];
$arr2 = ['white', ...$arr1, 'black'];
```

这是我们从 PHP 7.4 中得到的:

```
array(5) {
	[0]=>
	string(5) "white"
	[1]=>
	**&string(3) "red"**
	[2]=>
	string(5) "green"
	[3]=>
	string(4) "blue"
	[4]=>
	string(5) "black"
}
```

差价运营商提案以 43 比 1 的票数通过。

### 箭头功能 2.0(短闭包)

在 PHP 中，[匿名函数](https://www.php.net/manual/en/functions.anonymous.php)被认为相当冗长，难以实现和维护。[这个 RFC](https://wiki.php.net/rfc/arrow_functions_v2) 提议引入更短、更清晰的**箭头函数**(或者短闭包)语法，这将允许我们显著地清理我们的 PHP 代码。

考虑下面的例子:

```
function cube($n){
	return ($n * $n * $n);
}
$a = [1, 2, 3, 4, 5];
$b = array_map('cube', $a);
print_r($b);
```

PHP 7.4 允许使用更简洁的语法，上面的函数可以重写如下:

```
$a = [1, 2, 3, 4, 5];
$b = array_map(fn($n) => $n * $n * $n, $a);
print_r($b);
```

目前，[匿名函数](https://www.php.net/manual/en/functions.anonymous.php)(闭包)可以继承父作用域中定义的变量，这要归功于`use`语言构造，如下所示:

```
$factor = 10;
$calc = function($num) use($factor){
	return $num * $factor;
};
```

但是在 PHP 7.4 中，父作用域中定义的变量是由值隐式捕获的**(隐式按值作用域绑定)。因此，我们可以在一行中编写上面看到的整个函数:**

```
$factor = 10;
$calc = fn($num) => $num * $factor;
```

在父作用域中定义的变量可以在 arrow 函数中使用，就像我们使用`use($var)`一样，并且不可能从父作用域中修改变量。

新的语法是对该语言的巨大改进，因为它允许我们构建更具可读性和可维护性的代码。我们还可以使用[参数和返回类型](https://kinsta.com/blog/php-7-2/)，默认值，变长参数列表([变量函数](https://en.wikipedia.org/wiki/Variadic_function)，我们可以通过引用传递和返回等等。最后，短闭包也可以用在类方法中，它们可以像常规闭包一样利用`$this`变量。

这个 RFC 已经以 51 票对 8 票获得批准，所以我们可以期待它成为 PHP 7.4 新增内容的一部分。

### 零合并赋值运算符

PHP 7 中添加的[合并操作符](https://www.php.net/manual/en/migration70.new-features.php#migration70.new-features.null-coalesce-op) ( `??`)在我们需要结合`isset()`使用三元操作符时会派上用场。如果第一个操作数存在并且不是`NULL`，则返回第一个操作数。否则，它返回第二个操作数。这里有一个例子:

```
$username = $_GET['user'] ?? ‘nobody';
```

这段代码做的很简单:**它获取请求参数，如果不存在的话设置一个默认值**。那一行的意思很清楚，但是如果我们有更长的变量名，就像 RFC 中的这个例子一样，会怎么样呢？

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

```
$this->request->data['comments']['user_id'] = $this->request->data['comments']['user_id'] ?? 'value';
```

从长远来看，这段代码可能有点难以维护。所以，为了帮助开发者写出更直观的代码，[这个 RFC](https://wiki.php.net/rfc/null_coalesce_equal_operator) 提议引入**零合并赋值操作符** ( `??=`)。因此，我们可以编写以下代码，而不是编写前面的代码:

```
$this->request->data['comments']['user_id'] ??= ‘value’;
```

如果左侧参数的值是`null`，则使用右侧参数的值。
注意，虽然 coalesce 操作符是一个比较操作符，但是`??=`是一个赋值操作符。

这项提议以 37 票对 4 票获得通过。

### 类型化属性 2.0

参数类型声明或类型提示允许指定预期传递给函数或类方法的变量的类型。类型提示是 PHP 5 的一个特性，从 [PHP 7.2](https://kinsta.com/blog/php-7-2/) 开始，我们可以将它们用于`object`数据类型。现在 PHP 7.4 将类型提示向前推进了一步，增加了对[一级属性类型声明](https://wiki.php.net/rfc/typed_properties_v2)的支持。这里有一个非常基本的例子:

```
class User {
	public int $id;
	public string $name;
}
```

支持所有类型，除了`void`和`callable`:

```
public int $scalarType;
protected ClassName $classType;
private ?ClassName $nullableClassType;
```

RFC 解释了不支持`void`和`callable`的原因:

> 不支持 void 类型，因为它没有用并且语义不清楚。

> 不支持可调用类型，因为其行为依赖于上下文。

所以我们可以放心地使用`bool`、`int`、`float`、`string`、`object`、`iterable`、`self`、`parent`，任何类或接口名称，以及[可空](https://kinsta.com/blog/php-7-1-0/#nullable-types)、[类型](https://php.net/manual/en/migration71.new-features.php) ( `?type`)。

类型可用于静态属性:

```
public static iterable $staticProp;
```

它们也允许使用`var`符号:

```
var bool $flag;
```

可以设置默认的属性值，当然它必须与声明的属性类型相匹配，但是只有可空的属性可以有一个默认的`null`值:

```
public string $str = "foo";
public ?string $nullableStr = null;
```

同一类型适用于单个声明中的所有属性:

```
public float $x, $y;
```

如果我们在属性类型上犯了一个错误，会发生什么？考虑以下代码:

```
class User {
	public int $id;
	public string $name;
}

$user = new User;
$user->id = 10;
$user->name = [];
```

在上面的代码中，我们声明了一个字符串属性类型，但是我们将一个数组设置为属性值。在这种情况下，我们会得到以下致命错误:

```
Fatal error: Uncaught TypeError: Typed property User::$name must be string, array used in /app/types.php:9
```

该 RFC 以 70 票对 1 票获得批准。

在 MyKinsta dashboard 中轻松将你的 WordPress 站点迁移到 PHP 7.4。[免费试用 kin sta](https://hubs.ly/H0pklC_0)。【T7

### 弱引用

通过这个 RFC ，PHP 7.4 引入了 [WeakReference](https://www.php.net/manual/en/class.weakreference.php) 类，它允许程序员保留对一个对象的引用，而不会阻止对象本身被销毁。

目前，PHP 通过使用像 pecl-weakref 这样的扩展来支持弱引用。无论如何，新的 API 不同于文档中的`WeakRef`类。

这是这个提议的作者尼基塔·波波夫的一个例子:

```
$object = new stdClass;
$weakRef = WeakReference::create($object);

var_dump($weakRef->get());
unset($object);
var_dump($weakRef->get());
```

第一个`var_dump`打印`object(stdClass)#1 (0) {}`，第二个`var_dump`打印`NULL`，因为被引用对象已经被破坏。

> 我在 [#PHPRussia2019](https://twitter.com/hashtag/PHPRussia2019?src=hash&ref_src=twsrc%5Etfw) 的 PHP 7.4 演讲的幻灯片。是一次伟大的会议！https://t.co/zLr9Bj2aKl
> 
> —尼基塔·波波夫(@ Nikita _ PPV)[2019 年 5 月 19 日](https://twitter.com/nikita_ppv/status/1130188147940352000?ref_src=twsrc%5Etfw)