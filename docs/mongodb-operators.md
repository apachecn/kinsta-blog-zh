# 您需要知道的 9 种 Mongodb 操作符

> 原文：<https://kinsta.com/blog/mongodb-operators/>

在任何业务中，数据都是你最大的资产。通过分析数据，可以对客户趋势和行为预测做出决策。这提高了企业盈利能力和有效的决策。

如果没有[数据库软件](https://kinsta.com/blog/open-source-database/)，在一个充满记录的系统中寻找所有值的平均值这样简单的任务将会很乏味。幸运的是，数据库通过函数和操作符使数据分析变得更加容易和快速。

[Databases have made analyzing data easier and faster with functions and operators- and this guide will make understanding MongoDB a breeze 💪.Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Fmongodb-operators%2F&via=kinsta&text=Databases+have+made+analyzing+data+easier+and+faster+with+functions+and+operators-+and+this+guide+will+make+understanding+MongoDB+a+breeze+%F0%9F%92%AA.&hashtags=MongoDB%2CWebDev)

本文将介绍 MongoDB 数据库软件中使用的操作符。

## 什么是 MongoDB 运算符？

MongoDB 是一个管理面向文档信息的 NoSQL 数据库软件。

MongoDB 的一个关键特性是它的速度。为了更快地返回查询，MongoDB 可能会使用操作符来执行特定的功能。





> 需要在这里大声喊出来。Kinsta 太神奇了，我用它做我的个人网站。支持是迅速和杰出的，他们的服务器是 WordPress 最快的。
> 
> <footer class="wp-block-kinsta-client-quote__footer">
> 
> ![A picture of Phillip Stemann looking into the camera wearing a blue button down shirt](img/12b77bdcd297e9bf069df2f3413ad833.png)
> 
> <cite class="wp-block-kinsta-client-quote__cite">Phillip Stemann</cite></footer>

[View plans](https://kinsta.com/plans/)

运算符是帮助编译器执行数学或逻辑任务的特殊符号。MongoDB 提供了几种类型的操作符来与数据库交互。


## MongoDB 运算符类型

有九种类型的运算符，每一种都以其功能命名。例如，逻辑运算符使用逻辑运算。要执行它们，您需要使用特定的关键字并遵循语法。然而，它们很容易理解！

到本文结束时，您将能够学习每个操作符及其功能的基础知识。

### 逻辑运算符

逻辑运算符通常用于根据给定的条件过滤数据。它们还允许对许多条件进行评估，我们将对此进行更详细的讨论。

下面是一些您可以使用的逻辑运算符:

#### $和

“与”条件对包含两个或更多表达式的数组执行逻辑“与”运算。它选择满足所有表达式条件的文档。

这是`$and`表达式的标准语法:

```
{ $and: [ { <expression1> }, { <expression2> }, ... , { <expressionN> } ] } For example, if we want to select documents where the price is $10 and the quantity is less than 15, we can input the following query:
```

```
db.inventory.find( { $and: [ { quantity: { $lt: 15 } }, { price: 10 } ] } )
```

#### 美元或

“或”条件对包含两个或更多表达式的数组执行逻辑“或”运算。它选择至少有一个表达式为真的文档。

这是`$or`表达式的标准语法:

```
{ $or: [ { <expression1> }, { <expression2> }, ... , { <expressionN> } ] }.
```

例如，如果我们想要选择价格为$10 或数量少于 15 的文档，我们可以输入以下查询:

```
db.inventory.find( { $or: [ { quantity: { $lt: 15 } }, { price: 10 } ] } )
```

我们不必将表达式限制为两个标准，我们可以添加更多标准。例如，下面的查询选择那些价格等于$10、数量低于 15 或者标签固定的文档:

```
db.inventory.find( { $or: [ { quantity: { $lt: 15 } }, { price: 10 }, { tag: stationary }] } )
```

当运行这些子句时，MongoDB 要么执行集合扫描，要么执行索引扫描。如果所有索引都支持子句，那么 MongoDB 使用索引来检查一个`$or`表达式。否则，它将使用集合扫描。

但是如果您想在同一个字段中测试标准，您可能想使用`$in`操作符而不是`$or`操作符。例如，如果您想要数量为 10 或 20 的文档集合，您可能需要运行下面的`$in`查询:

```
db.inventory.find ( { quantity: { $in: [20, 50] } } )
```

稍后，我们将详细介绍`$in`操作符。

#### $nor

该运算符使用一个或多个表达式对数组执行逻辑“或非”运算。接下来，它选择查询表达式失败的文档。更简单地说，它与`$or`条件相反。

这是一般语法:

```
{ $nor: [ { <expression1> }, { <expression2> }, ...  { <expressionN> } ] }
```

让我们考虑以下查询:

```
db.inventory.find( { $nor: [ { price: 3.99 }, { sale: true } ]  } )
```

该查询选择包含以下内容的文档:

*   价格字段值不等于$3.99，销售值不等于 true 或者
*   不等于$3.99 的价格字段值，以及空的或不存在的销售字段；或者
*   没有价格字段，销售字段不等于真；或者
*   价格字段和销售字段均未填充或存在。

#### $不

该运算符对指定表达式的数组执行逻辑“非”运算。然后，它选择与查询表达式不匹配的文档。这包括不包含该字段的文档。

这是一般语法:

```
{ field: { $not: { <operator-expression> } } }
```

例如，以下面的查询为例:

```
db.inventory.find( { price: { $not: { $lt: 3.99 } } } )
```

该查询将选择包含以下内容的文档:

*   其值大于或等于 3.99 美元的价格字段；和
*   价格字段未填写或不存在。



### 信息

`{ $not: { $lt: 3.99 } }`不同于`$gte`运算符。`{ $gte: 3.99 }`仅返回存在价格字段并且其值小于或等于$3.99 的文档( `$not`操作符甚至返回不存在价格字段的文档)。



### 比较运算符

比较运算符可用于比较一个或多个文档中的值。

下面是一个超市商店的简单库存收集的示例代码:

```
{ _id: 1, item: { name: "apple", code: "123" }, qty: 15, tags: [ "A", "B", "C" ] },
{ _id: 2, item: { name: "banana", code: "123" }, qty: 20, tags: [ "B" ] },
{ _id: 3, item: { name: "spinach", code: "456" }, qty: 25, tags: [ "A", "B" ] },
{ _id: 4, item: { name: "lentils", code: "456" }, qty: 30, tags: [ "B", "A" ] },
{ _id: 5, item: { name: "pears", code: "000" }, qty: 20, tags: [ [ "A", "B" ], "C" ] },
{ _id: 6, item: { name: "strawberry", code: "123" }, tags: [ "B" ] }
```

我们将使用这个例子，同时详细说明每个比较操作符。

#### 等于(＄eq)

该运算符匹配等于给定值的值:

```
{ <field>: { $eq: <value> } }
```

例如，如果我们想从 inventory 集合中检索一个具有确切数量值“20”的特定文档，我们可以输入以下命令:

```
db.inventory.find( { qty: { $eq: 20 } } )
```

该查询将返回以下内容:

```
{ _id: 2, item: { name: "banana", code: "123" }, qty: 20, tags: [ "B" ] }, 
{ _id: 5, item: { name: "pears", code: "000" }, qty: 20, tags: [ [ "A", "B" ], "C" ] }
```

#### 大于($gt)

如果值大于给定值，则此运算符匹配:

```
{ field: { $gt: value } }
```

在本例中，我们检索数量大于 15 的文档:

```
db.inventory.find({"qty": { $gt: 15}})
```

该查询将返回以下内容:

```
{ _id: 2, item: { name: "banana", code: "123" }, qty: 20, tags: [ "B" ] }
{ _id: 3, item: { name: "spinach", code: "456" }, qty: 25, tags: [ "A", "B" ] }
{ _id: 4, item: { name: "lentils", code: "456" }, qty: 30, tags: [ "B", "A" ] }
{ _id: 5, item: { name: "pears", code: "000" }, qty: 20, tags: [ [ "A", "B" ], "C" ] }
```

#### 少于($lt)

如果值小于提供的值，则此运算符匹配:

```
{ field: { $lt: value } }
```

让我们找到数量小于 25 的文档:

```
db.inventory.find({"qty": { $lt: 25}})
```

该查询将返回以下内容:

```
{ _id: 1, item: { name: "apple", code: "123" }, qty: 15, tags: [ "A", "B", "C" ] }
{ _id: 2, item: { name: "banana", code: "123" }, qty: 20, tags: [ "B" ] }
{ _id: 5, item: { name: "pears", code: "000" }, qty: 20, tags: [ [ "A", "B" ], "C" ] }
```

#### 大于或等于($gte)

当值大于或等于给定值时，此运算符匹配:

```
{ field: { $gte: value } }
```

在本例中，我们检索数量大于或等于 25 的文档:

```
db.inventory.find({"qty": { $gte: 25}})
```

该查询将返回以下内容:

```
{ _id: 3, item: { name: "spinach", code: "456" }, qty: 25, tags: [ "A", "B" ] }
{ _id: 4, item: { name: "lentils", code: "456" }, qty: 30, tags: [ "B", "A" ] }
```

#### 小于或等于(lte)

仅当值小于或等于给定值时，此运算符才匹配:

```
{ field: { $lte: value } }
```

让我们找到数量小于或等于 25 的文档。

```
db.inventory.find({"qty": { $lte: 25}})
```

我们可以预期该查询将返回以下内容:

```
{ _id: 1, item: { name: "apple", code: "123" }, qty: 15, tags: [ "A", "B", "C" ] }
{ _id: 2, item: { name: "banana", code: "123" }, qty: 20, tags: [ "B" ] }
{ _id: 3, item: { name: "spinach", code: "456" }, qty: 25, tags: [ "A", "B" ] }
{ _id: 5, item: { name: "pears", code: "000" }, qty: 20, tags: [ [ "A", "B" ], "C" ] }
```

#### 英寸(英寸)

该运算符返回与指定值匹配的文档:

```
{ field: { $in: [<value1>, <value2>, ... <valueN> ] } }
```

字段的值等于指定数组中的任何值。例如，要在库存集合中检索值为“30”和“15”的文档，您应该这样做:

```
db.collection.find({ "qty": { $in: [30, 15]}})
```

输出将是:

```
{ _id: 1, item: { name: "apple", code: "123" }, qty: 15, tags: [ "A", "B", "C" ] }
{ _id: 4, item: { name: "lentils", code: "456" }, qty: 30, tags: [ "B", "A" ] }
```



The query run in MongoDB Shell.



#### 不在(nin)

该操作符返回与给定值不匹配的文档。下面是`$nin`操作符的基本语法:

```
{ field: { $nin: [ <value1>, <value2> ... <valueN> ]
```

`$nin`选择文档，其中:

*   字段值不在指定的数组中；或者
*   该字段不存在。

如果该字段包含数组，它将选取值部分中没有指定元素的数组。例如，我们希望选择那些数量既不等于 20 也不等于 15 的文档。

此外，它还匹配没有数量字段的文档:

```
db.collection.find({ "qty": { $nin: [ 20, 15 ]}}, {_id: 0})
```

输出将是:

```
{ _id: 3, item: { name: "spinach", code: "456" }, qty: 25, tags: [ "A", "B" ] }
{ _id: 4, item: { name: "lentils", code: "456" }, qty: 30, tags: [ "B", "A" ] }
{ _id: 6, item: { name: "strawberry", code: "123" }, tags: [ "B" ] }
```

#### 不相等($ne)

`$ne`运算符返回指定值不相等的文档:

```
{ $ne: value } }
```

例如，假设我们想要选择数量不等于 20 的所有文档:

```
db.inventory.find( { qty: { $ne: 20 } } )
```

输出将是:

```
{ _id: 1, item: { name: "apple", code: "123" }, qty: 15, tags: [ "A", "B", "C" ] }
{ _id: 3, item: { name: "spinach", code: "456" }, qty: 25, tags: [ "A", "B" ] }
{ _id: 4, item: { name: "lentils", code: "456" }, qty: 30, tags: [ "B", "A" ] }
{ _id: 6, item: { name: "strawberry", code: "123" }, tags: [ "B" ] }
```

从上面的输出中，我们可以看到查询将选择没有数量字段的文档。

### 元素运算符

元素查询操作符可以使用文档的字段来识别文档。元素运算符由`$exist`和`$type`组成。

#### $存在

该操作符匹配具有指定字段的文档。该操作符有一个布尔值，可以是`true`或`false`。

如果指定为`true`，则匹配包含该字段的文档，包括字段值为空的文档。如果<布尔值>是`false`，那么查询只返回不包含该字段的文档。

以下是标准语法:

```
{ field: { $exists: <boolean> } }
```

让我们举一个例子，我们有一个名为“bagofmarbles”的数组的集合数据，其中每个袋子都包含不同颜色的弹珠:

```
{ red: 5, green: 5, blue: null }
{ red: 3, green: null, blue: 8 }
{ red: null, green: 3, blue: 9 }
{ red: 1, green: 2, blue: 3 }
{ red: 2, blue: 5 }
{ red: 3, green: 2 }
{ red: 4 }
{ green: 2, blue: 4 }
{ green: 2 }
{ blue: 6 }
```

假设我们想要一个查询，只返回那些有红色弹珠的袋子。这意味着我们必须输入布尔值作为`true`。让我们来看看:

```
db.bagofmarbles.find( { red: { $exists: true } } )
```

结果将由包含字段“red”的文档组成，即使值为`null`。但是，它不会包含甚至不存在“红色”字段的文档:

```
{ red: 5, green: 5, blue: null }
{ red: 3, green: null, blue: 8 }
{ red: null, green: 3, blue: 9 }
{ red: 1, green: 2, blue: 3 }
{ red: 2, blue: 5 }
{ red: 3, green: 2 }
{ red: 4 }
```

如果我们只想要那些红色弹珠甚至不存在的袋子，我们可以输入下面的查询:

```
db.bagofmarbles.find( { red: { $exists: false} }
```

结果将由不包含字段“红色”的那些文档组成:

```
{ green: 2, blue: 4 }
{ green: 2 }
{ blue: 6 }
```

#### $类型

该运算符根据指定的字段类型匹配文档。当您有高度非结构化的数据，或者数据类型不可预测时，这很有用。这些字段类型是指定的 BSON 类型，可以通过类型号或别名来定义。

这是`$type`的一般语法:

```
{ field: { $type: <BSON type> } }
```

假设我们有一个包含以下文档的地址簿:

```
db={
  addressBook: [
    {
      "_id": 1,
      address: "2100 Jupiter Spot",
      zipCode: "9036325"
    },
    {
      "_id": 2,
      address: "25 Moon Place",
      zipCode: 26237
    },
    {
      "_id": 3,
      address: "2324 Neptune Ring",
      zipCode: NumberLong(77622222)
    },
    {
      "_id": 4,
      address: "33 Saturns Moon",
      zipCode: NumberInt(117)
    },
    {
      "_id": 5,
      address: "1044 Venus Lane",
      zipCode: [
        "99883637232",
        "73488976234"
      ]
    }
  ]
}
```

观察上面的文档，邮政编码有不同的数据类型。这包括长整型、双精度型、整型和字符串型值。

如果我们只想要那些具有指定数据类型作为 zipcode 的文档——让我们以 string 为例——我们必须向编译器输入以下查询:

```
db.addressBook.find({
  "zipCode": {
    $type: "string"
  }
})
```

这将返回以下文档:

```
[
  {
    "_id": 1,
    "address": "2100 Jupiter Spot",
    "zipCode": "9036325"
  },
  {
    "_id": 5,
    "address": "1044 Venus Lane",
    "zipCode": [
      "99883637232",
      "73488976234"
    ]
  }
]
```



The above query run in a MongoDB Shell.



此外，还有一种“数字”类型，它将所有长整型、整型或双精度型值作为包含指定类型元素的数组包含在内:

```
db.addressBook.find( { "zipCode" : { $type : "number" } } )
```

输出:

```
[
{
      "_id": 2,
      address: "25 Moon Place",
      zipCode: 26237
    },
    {
      "_id": 3,
      address: "2324 Neptune Ring",
      zipCode: NumberLong(77622222)
    },
    {
      "_id": 4,
      address: "33 Saturns Moon",
      zipCode: NumberInt(117)
    }
]
```

如果文档有一个数组字段类型，`$type`操作符返回至少有一个数组元素与传递给操作符的类型相匹配的文档。



### 信息

从 MongoDB 3.6 和更高版本开始，查询`$type: array`将返回字段本身是数组的文档。但是，在使用相同的查询时，以前的版本用于返回字段是数组的文档，并且至少有一个元素的数据类型是数组。



### 数组运算符

MongoDB 还包含数组操作符，用于查询包含数组的文档。

有三个主要操作符:`$all`、`$elemMatch`和`$size`。我们将在下面详细讨论每一个。

#### 所有美元

`$all`操作符选择其中字段值是包含指定元素的数组的文档:

```
{ : { $all: [ <value1> , <value2> ... ] } }
```

例如，假设我们有一个服装店的文档集合，下面是库存。

```
{
   _id: ObjectId("5234cc89687ea597eabee675"),
   code: "shirt",
   tags: [ "sale", "shirt", "button", "y2k", "casual" ],
   qty: [
          { size: "S", num: 10, color: "blue" },
          { size: "M", num: 45, color: "blue" },
          { size: "L", num: 100, color: "green" }
        ]
},

{
   _id: ObjectId("5234cc8a687ea597eabee676"),
   code: "pant",
   tags: [ "y2k", "trendy", "shine" ],
   qty: [
          { size: "6", num: 100, color: "green" },
          { size: "6", num: 50, color: "blue" },
          { size: "8", num: 100, color: "brown" }
        ]
},

{
   _id: ObjectId("5234ccb7687ea597eabee677"),
   code: "pant2",
   tags: [ "trendy", "shine" ],
   qty: [
          { size: "S", num: 10, color: "blue" },
          { size: "M", num: 100, color: "blue" },
          { size: "L", num: 100, color: "green" }
        ]
},

{
   _id: ObjectId("52350353b2eff1353b349de9"),
   code: "shirt2",
   tags: [ "y2k", "trendy" ],
   qty: [
          { size: "M", num: 100, color: "green" }
        ]
}
```

我们希望从库存中检索任何与标签“trendy”和“y2k”相关联的文档(在本例中是衣服)。以下查询使用了`$all`运算符，其中 tags 字段的值是一个数组，其元素包括“y2k”和“trendy”:

```
db.inventory.find( { tags: { $all: [ "y2k", "trendy" ] } } )
```

上述查询返回以下内容:

```
{
   _id: ObjectId("5234cc8a687ea597eabee676"),
   code: "pant",
   tags: [ "y2k", "trendy", "shine" ],
   qty: [
          { size: "6", num: 100, color: "green" },
          { size: "6", num: 50, color: "blue" },
          { size: "8", num: 100, color: "brown" }
        ]
}

{
   _id: ObjectId("52350353b2eff1353b349de9"),
   code: "shirt2",
   tags: [ "y2k", "trendy" ],
   qty: [
          { size: "M", num: 100, color: "green" }
        ]
}
```



The above query run in a MongoDB Shell.



从上面的例子中，我们还发现`$all`操作符只是执行与`$and`操作相同的功能。

或者，我们可以使用下面的查询，它会给出与上面类似的输出:

```
db.collection.find({
  $and: [
    {
      tags: "y2k"
    },
    {
      tags: "trendy"
    }
  ]
})
```



The above query run in a MongoDB shell.



#### $elemMatch

`$elemMatch`操作符匹配包含一个数组字段的文档，该数组字段至少有一个元素匹配所有指定的查询条件:

```
{ : { $elemMatch: { <query1>, <query2>, ... } } }
```

虽然我们可以使用比较操作符，如`$lte`和`$gte`，但是如果我们在`$elemMatch`中只指定了一个查询条件，并且没有使用`$not`或`$ne`操作符，那么可以省略使用`$elemMatch`，因为它本质上执行的是相同的功能。

使用该操作符时，还有一些事情需要记住，主要是:

*   不能在`$elemMatch`操作中指定`$where`表达式。
*   不能在`$elemMatch`操作中指定`$text`查询表达式。

例如，我们在学生成绩集合中有以下文档:

```
{ _id: 1, results: [ 92, 89, 98 ] }
{ _id: 2, results: [ 85, 99, 99 ] }
```

以下查询仅匹配结果数组包含至少一个大于或等于 90 且小于 95 的元素的文档:

```
db.studentresults.find(  { results: { $elemMatch: { $gte: 90, $lt: 95 } } })
```

我们的查询返回以下文档，因为元素 92 既大于或等于 90，又小于 95:

```
{ "_id" : 1, "results" :[ 92, 89, 98 ] }
```

#### 美元大小

`$size`运算符返回数组大小与参数中指定的元素数量相匹配的文档:

```
{ field: { $size: value } }
```

这里有一个例子:

```
db.collection.find( { field: { $size: 2 } });
```

这将返回指定集合中的所有文档，其中字段是一个包含两个元素的数组:`{ field: [ orange, apple] }`和`{ field: [ blue, red] }`，而不是`{ field: blue}`或`{ field: [ raspberry, lemon, grapefruit ] }`。

然而，虽然我们可以输入特定的值作为大小，但我们不能指定值的范围作为大小。

### 地理空间操作员

MongoDB 允许您以 GeoJSON 类型的形式存储地理空间数据。GeoJSON 是一种基于 JavaScript 对象符号的开放标准格式，可以表示地理要素并支持非空间属性。我们将在本文中讨论两种类型的地理空间操作符:几何说明符和查询选择器。

#### $几何

该操作符提到了 GeoJSON 几何，用于以下地理空间查询操作符:`$geoIntersects`、`$geoWithin`、`$nearSphere`和`$near`。`$geometry`利用 EPSG:4326 作为默认坐标参考系统(CRS)。

要提到带有默认 CRS 的 GeoJSON 对象，您可以利用下面的代码片段作为`$geometry`:

```
$geometry: {
   type: "<GeoJSON object type>",
   coordinates: [ <coordinates> ]
}
```

要提到带有定制的 MongoDB CRS 的单环 GeoJSON 多边形，可以使用下面的代码片段(只能对`$geoWithin`和`$geoIntersects`使用这个代码片段):

```
$geometry: {
   type: "Polygon",
   coordinates: [ <coordinates> ],
   crs: {
      type: "name",
      properties: { name: "urn:x-mongodb:crs:strictwinding:EPSG:4326" }
   }
}
```

#### $多边形

`$polygon`操作符可用于为传统坐标对上的地理空间`$geoWithin`查询指定多边形。然后，该查询将返回落在多边形范围内的对。但是， `$polygon`不会查询任何 GeoJSON 对象。要定义多边形，您需要指定一组坐标点，如下所示:

```
{
   : {
      $geoWithin: {
         $polygon: [ [ <x1> , <y1> ], [ <x2> , <y2> ], [ <x3> , <y3> ], ... ]
      }
   }
}
```

在这里，最后一点隐含地与第一点相联系。你可以尽可能多地提及要点或侧面。

例如，以下查询将返回坐标位于由[0，0]、[1，5]和[3，3]定义的多边形内的所有文档:

```
db.places.find(
  {
     loc: {
       $geoWithin: { $polygon: [ [ 0 , 0 ], [ 1 , 5 ], [ 3 , 3 ] ] }
     }
  }
)
```

#### $地理范围内

此运算符可用于选择包含地理空间数据的文档，这些数据完全包含在特定形状中。指定的形状可以是 GeoJSON 多重多边形、GeoJSON 多边形(多环或单环)，也可以是由传统坐标对定义的形状。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

`$geoWithin`操作符将利用`$geometry`操作符来引用 GeoJSON 对象。

要通过默认坐标参考系统(CRS)提及 GeoJSON 多面或多边形，您可以使用下面提到的语法:

```
{
   : {
      $geoWithin: {
         $geometry: {
            type: <"Polygon" or "MultiPolygon"> ,
            coordinates: [ <coordinates> ]
         }
      }
   }
}
```

对于提及面积大于单个半球的 GeoJSON 几何图形的`$geoWithin`查询，使用默认 CRS 将导致对互补几何图形的查询。

要提到带有自定义 MongoDB CRS 的单环 GeoJSON 多边形，您可以利用下面在`$geometry`表达式中提到的原型:

```
{
   : {
      $geoWithin: {
         $geometry: {
           type: "Polygon" ,
           coordinates: [ <coordinates> ],
           crs: {
              type: "name",
              properties: { name: "urn:x-mongodb:crs:strictwinding:EPSG:4326" }
           }
         }
      }
   }
}
```

以下示例拾取完全存在于 GeoJSON 多边形内的所有 loc 数据，多边形的面积小于单个半球的面积:

```
db.places.find(
   {
     loc: {
       $geoWithin: {
          $geometry: {
             type : "Polygon" ,
             coordinates: [ [ [ 0, 0 ], [ 3, 6 ], [ 6, 1 ], [ 0, 0 ] ] ]
          }
       }
     }
   }
)
```

#### $box

您可以使用`$box`为地理空间`$geoWithin`查询指定一个矩形，根据基于点的位置数据提供矩形范围内的文档。当您将`$geoWithin`与`$box`一起使用时，您将获得基于查询坐标的文档。在这种情况下，`$geoWithin`不会查询任何 GeoJSON 形状。

为了利用`$box`操作符，您需要在一个数组对象中提到矩形的右上角和左下角:

```
{ <location field> : { $geoWithin: { $box: [ [ <bottom left coordinates> ],
 [ <upper right coordinates> ] ] } } }
```

上述查询将通过利用平面几何来计算距离。下面的查询将返回位于[0，0]，[0，30]，[30，0]，[30，30]的框内的所有文档:

```
db.places.find ( { 
 loc: { $geoWithin: { $box: [ [ 0,0 ], [ 30,30 ] ] } }
} )
```

#### $nearSphere

您可以使用`$nearSphere`来指出地理空间查询从最近到最远返回文档的点。

MongoDB 使用球面几何来计算`$nearSphere`的距离。它将需要如下地理空间索引:

1.  描述为传统坐标对的位置数据的 2d 索引。要利用 GeoJSON 点上的 2d 索引，需要在 GeoJSON 对象的坐标字段上生成索引。
2.  描述为 GeoJSON 点的位置数据的二维球体索引。

要提及 GeoJSON 点，您可以利用以下语法:

```
{
  $nearSphere: {
     $geometry: {
        type : "Point",
        coordinates : [ <longitude>, <latitude> ]
     },
     $minDistance: <distance in meters>,
     $maxDistance: <distance in meters> 
  }
}
```

这里，`$minDistance`和`$maxDistance`是可选的。`$minDistance`可以将结果限制在距离中心至少指定距离的文档中。您可以将`$maxDistance`用于任一索引。

现在，考虑一个“地点”集合，它由带有 location 字段的文档组成，该字段有一个 2dsphere 索引。以下示例将返回距离您选择的点至少 2000 米、最多 6000 米的点，按从最近到最远的顺序排列:

```
db.places.find(
   {
     location: {
        $nearSphere: {
           $geometry: {
              type : "Point",
              coordinates : [ -43.9532, 50.32 ]
           },
           $minDistance: 2000,
           $maxDistance: 6000
        }
     }
   }
)
```

#### $ geoIntersects

`$geoIntersects`操作符允许您选择其地理空间数据与特定 GeoJSON 对象相交的文档(即指定对象和数据的交汇处非空)。它利用`$geometry`操作符来指定 GeoJSON 对象。

要通过默认坐标参考系统(CRS)提及 GeoJSON 多面或多边形，可以使用以下语法:

```
{ <location field>: {
     $geoIntersects: {
        $geometry: {
           type: "<GeoJSON object type>" ,
           coordinates: [ <coordinates> ]
        }
     }
  }
}
```

以下实例将使用`$geoIntersects`选择与坐标数组描述的多边形相交的所有 loc 数据:

```
db.places.find(
   {
     loc: {
       $geoIntersects: {
          $geometry: {
             type: "Polygon" ,
             coordinates: [
               [ [ 0, 0 ], [ 2, 6 ], [ 4, 1 ], [ 0, 0 ] ]
             ]
          }
       }
     }
   }
)
```

#### $center

`$center`操作符为一个`$geoWithin`查询提到了一个圆，该查询返回该圆范围内的遗留坐标对。

`$center`不返回 GeoJSON 对象。为了利用`$center`操作符，您需要指定一个数组，该数组包含:

1.  圆的半径，以坐标系使用的单位测量。
2.  圆的中心点的网格坐标。

```
{
  <location field> : {
      $geoWithin: { $center: [ [ <x> , <y> ] , <radius> ] }
   }
}
```

下面提到的示例将返回坐标位于以[2，3]为圆心、半径为 40 的圆内的所有文档:

```
db.places.find(
   { loc: { $geoWithin: { $center: [ [2, 3], 40 ] } } }
)
```

### 投影算子

您可以使用投影运算符来表示操作返回的字段。MongoDB projection operators 允许将`find()`函数用于数据过滤参数。这有助于用户仅从文档中提取所需的数据字段。因此，它允许您投射透明和简洁的数据，而不影响整体数据库性能。

#### $elemMatch(投影)

`$elemMatch`操作符负责将查询结果中的字段内容限制为只包含匹配`$elemMatch`条件的第一个元素。

在使用`$elemMatch`之前，你需要记住以下几点:

*   从 MongoDB 4.4 开始，不管文档中字段的顺序如何，现有字段的`$elemMatch`投影返回包含其他现有字段之后的字段。
*   `$elemMatch`和` ,
   { <arrayField> : { $slice: <number> } }
);
```

也可以这样表达:

```
db.collection.find(
  <query> ,
   { <arrayField> : { $slice: [ <number> , <number> ] } }
);
```

为了进行同样的演示，您可以使用以下文档创建一个示例 tweets 集合:

```
db.posts.insertMany([
   {
     _id: 1,
     title: "Nuts are not blueberries.",
     comments: [ { comment: "0\. true" }, { comment: "1\. blueberries aren't nuts."} ]
   },
   {
     _id: 2,
     title: "Coffee please.",
     comments: [ { comment: "0\. Indubitably" }, { comment: "1\. Cuppa tea please" }, { comment: "2\. frappucino" }, { comment: "3\. Mocha latte" }, { comment: "4\. whatever" } ]
   }
])
```

下面的操作将在 tweets 数组上使用`$slice`投影操作符来返回包含前两个元素的数组。如果数组包含的元素少于两个，则返回数组中的所有元素:

```
db.posts.find( {}, { comments: { $slice: 2 } } )
```

该操作将返回以下文档:

```
{
   "_id" : 1,
   "title" : "Nuts are not blueberries.",
   "comments" : [ { "comment" : "0\. true" }, { "comment" : "1\. blueberries aren't nuts." } ]
}
{
   "_id" : 2,
   "title" : "Coffee please.",
   "comments" : [ { "comment" : "0\. Indubitably" }, { "comment" : "1\. Cuppa tea please" } ]
}
```

#### $(预测)

位置运算符`: <condition> ... },
                    { "<array>.$": 1 } )
db.collection.find( { <array.field>: <condition> ...},
                    { "<array>.$": 1 } )
```

在本例中，`students`集合由以下文档组成:

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

```
{ "_id" : 1, "semester" : 2, "grades" : [ 75, 67, 93 ] }
{ "_id" : 2, "semester" : 2, "grades" : [ 60, 68, 72 ] }
{ "_id" : 3, "semester" : 2, "grades" : [ 95, 82, 67 ] }
{ "_id" : 4, "semester" : 3, "grades" : [ 89, 95, 70 ] }
{ "_id" : 5, "semester" : 3, "grades" : [ 68, 98, 82 ] }
{ "_id" : 6, "semester" : 3, "grades" : [ 65, 70, 76 ] }
```

在以下查询中，投影`{ "grades.$": 1 }`仅返回`grades`字段中大于或等于 89 的第一个元素:

```
db.students.find( { semester: 2, grades: { $gte: 89 } },
                  { "grades.$": 1 } )
```

该操作返回以下文档:

```
{"_id": 3, "grades": [95] }
```

### 评估运算符

您可以利用 MongoDB 评估操作符来评估整个数据结构或文档中的单个字段。

我们来看看一些常见的 MongoDB 求值运算符。

#### $mod

您可以使用此运算符来匹配指定字段的值等于除以指定值后的余数的文档:

```
{ field: { $mod: [ divisor, remainder ] } }
```

假设您的展厅中有一张属于不同品牌的汽车表。以下查询将为您提供股票编号是 250 的倍数的所有汽车品牌。

```
db.cars.find ( { qty: { $mod: [ 250,0 ] } } )
```

#### $jsonSchema

`$jsonSchema`允许您匹配与指定 JSON 模式相匹配的文档。MongoDB 对 JSON 模式的实现包括添加了`bsonType`关键字，这允许您在`$jsonSchema`操作符中使用所有 BSON 类型。

`bsonType`可以接受与`type`操作符相同的字符串别名。这就是`$jsonSchema`的语法:

```
{ $jsonSchema: <JSON Schema object> }
```

这里，JSON 模式对象是基于 [JSON 模式标准的草案 4](https://tools.ietf.org/html/draft-zyp-json-schema-04) 格式化的:

```
{ <keyword1>: <value1>, ... }
```

这里有一个例子来演示`$jsonSchema`是如何工作的:

```
{ $jsonSchema: {
     required: [ "name", "major", "gpa", "address" ],
     properties: {
        name: {
           bsonType: "string",
           description: "must be a string and is required"
        },
        address: {
           bsonType: "object",
           required: [ "zipcode" ],
           properties: {
               "street": { bsonType: "string" },
               "zipcode": { bsonType: "string" }
           }
        }
     }
  }
}
```

您还可以在文档验证器中使用`$jsonSchema`,在更新和插入操作中实施指定的模式:

```
db.createCollection(<collection> , { validator: { $jsonSchema: <schema> } } )
db.runCommand( { collMod: <collection>, validator:{ $jsonSchema: <schema> } } )
```

请记住，`$jsonSchema`操作符不支持几件事情:

1.  整数类型。您需要通过 BSON type 关键字利用 BSON 类型 long 或 int。
2.  未知关键字。
3.  JSON 模式的链接属性和超媒体，以及 JSON 引用和 JSON 指针的使用。

#### $text

`$text`操作符将在指定字段的内容中查找文本，并用文本索引进行索引:

```
{  
  $text:  
    {  
      $search: <string>,  
      $language: <string>,  
      $caseSensitive: <boolean>,  
      $diacriticSensitive: <boolean>   
    }  
}
```

在这种情况下，下面的代码片段将筛选出表中包含文本“Porsche”的所有汽车:

```
db.cars.find( { $text: { $search: "Porsche" } } )
```

#### $regex

`$regex`操作符提供了正则表达式能力来匹配查询中的字符串。MongoDB 利用与 Perl 兼容的正则表达式:

```
{<field> : /pattern/ <options>}
```

以下示例有助于筛选出所有包含字符串“$78900”的汽车:

```
db.cars.find( { price: { $regex: /$78900/ } } )
```

#### $expr

`$expr`操作符允许您在查询语言中利用聚合表达式:

```
{ $expr: { <expression> } }
```

您也可以使用`$expr`构建查询表达式，在`$match`阶段比较同一文档中的字段。如果`$match`阶段恰好是`$lookup`阶段的一部分，`$expr`可以借助 let 变量比较字段。

#### $哪里

您可以利用`$where`操作符将包含完整 JavaScript 函数的字符串或 JavaScript 表达式传递给查询系统。`$where`操作符提供了更大的灵活性，但是需要数据库为集合中的每个文档处理 JavaScript 函数或表达式。您可以使用`obj`或`this`在 JavaScript 函数或表达式中引用该文档。

下面是一个语法示例:

```
{ $where: <string|JavaScript Code> }
```

在我们深入使用`$where`操作符的例子之前，有几个关键的注意事项要记住:

*   您应该只对顶级文档使用`$where`查询操作符。像在`$elemMatch`查询中一样，`$where`查询操作符在嵌套文档中不起作用。
*   一般来说，只有当您无法通过另一个操作符表达您的查询时，才应该使用`$where`。如果必须使用`$where`，确保至少包含一个其他标准查询操作符来过滤结果集。独立使用`$where`需要集合扫描才能正确执行。

这里有一个例子来说明这一点:

```
db.cars.find( { $where: function() {  
   return (hex_md5(this.name)== "9a43e617b50cd379dca1bc6e2a8")  
} } );
```

### 按位运算符

按位运算符根据位的位置条件返回数据。简而言之，它们用于匹配数值或二进制值，其中一组位位置中的任何位的值为 1 或 0。

#### $bitsAllSet

此运算符将匹配所有文档，其中查询提供的所有位位置都在字段中设置(即 1):

```
{ <field> : { $bitsAllSet: <numeric bitmask> } }
```

```
{ <field> : { $bitsAllSet: < BinData bitmask> } }
```

```
{ <field> : { $bitsAllSet: [ <position1> , <position2> , ... ] } }
```

字段值应该是 BinData 实例或数字，以便`$bitsAllSet`匹配当前文档。

在下面的例子中，我们利用了包含以下文档的集合:

```
db.collection.save({ _id: 1, a: 54, binaryValueofA: "00110110" })
db.collection.save({ _id: 2, a: 20, binaryValueofA: "00010100" })
db.collection.save({ _id: 3, a: 20.0, binaryValueofA: "00010100" })
db.collection.save({ _id: 4, a: BinData(0, "Zg=="), binaryValueofA: "01100110" })
```

下面提到的查询将使用`$bitsAllSet`操作符来测试字段 a 是否在位置 1 和位置 5 设置了位，其中最低有效位将在位置 0:

```
db.collection.find( { a: { $bitsAllSet: [ 1, 5 ] } }
```

该查询将匹配以下文档:

```
{ "_id" : 1, "a" : 54, "binaryValueofA" : "00110110" }
{ "_id" : 4, "a" : BinData(0,"Zg=="), "binaryValueofA" : "01100110" }
```

#### $bitsAllClear

`$bitsAllClear`操作符将匹配查询提供的所有位位置都是空的文档，或者`0`:

```
{ <field> : { $bitsAllClear: <numeric bitmask> } }
```

```
{ <field> : { $bitsAllClear: < BinData bitmask> } }
```

```
{ <field> : { $bitsAllClear: [ <position1> , <position2> , ... ] } }
```

这里我们将使用用于`$bitsAllSet`的例子来演示`$bitsAllClear`的用法。以下查询将使用此运算符来检查字段 a 是否在位置 1 和 5 清除了位:

```
db.collection.find( { a: { $bitsAllClear: [ 1, 5 ] } } )
```

该查询将匹配以下文档:

```
{ "_id" : 2, "a" : 20, "binaryValueofA" : "00010100" }
{ "_id" : 3, "a" : 20, "binaryValueofA" : "00010100" }
```

### 元运算符

在 MongoDB 中，有各种查询修饰符可以让您修改查询的行为或输出。驱动程序接口可能会提供游标方法，将它们包装起来供您使用。

#### $提示

MongoDB 从 3.2 版起就不推荐使用`$hint`，但是，这个操作符可能仍然适用于 MongoDB 驱动程序，比如 Go、Java、Scala、Ruby、Swift 等等。它可以迫使查询优化器利用特定的索引来完成查询，然后可以通过文档或索引名称来提及该索引。

您还可以使用`$hint`操作符来测试索引策略和查询性能。例如，采取以下操作:

```
db.users.find().hint( { age: 1 } )
```

该操作将通过利用`age`字段上的索引返回名为`users`的集合中的所有文档。

你也可以使用以下两种形式之一来提及提示:

```
db.users.find()._addSpecial( "$hint", { age : 1 } )
db.users.find( { $query: {}, $hint: { age : 1 } } )
```

如果查询形状存在索引过滤器，MongoDB 将简单地忽略`$hint`。

#### $注释

`$comment`操作符允许您在`$query`可能出现的任何上下文中将注释附加到查询中。因为注释会传播到配置文件日志，所以添加注释可以更容易地解释和跟踪您的配置文件。

您可以通过以下三种方式之一利用`$comment`:

```
db.collection.find( { <query> } )._addSpecial( "$comment", <comment> )
db.collection.find( { <query> } ).comment( <comment> )
db.collection.find( { $query: { <query> }, $comment: <comment> } )
```

如果您想在其他上下文中为查询表达式附加注释，比如使用`db.collection.update()`，那么利用`$comment`查询操作符而不是元操作符。

#### 最大值

您可以提到一个`$max`值来指定特定索引的独占上限，以约束`find()`的结果。该操作符将为索引中特定顺序的所有键指定上限。

Mongosh 为您提供了以下`max()`包装器方法:

```
db.collection.find( { <query> } ).max( { field1: <max value> , ... fieldN: <max valueN> } )
```

你也可以用以下两种形式提到`$max`:

```
db.collection.find( { <query> } )._addSpecial( "$max", { field1: <max value1> ,
 ... fieldN: <max valueN> } )
db.collection.find( { $query: { <query> }, $max: { field1: <max value1> ,
 ... fieldN: <max valueN> } } )
```

例如，如果您想要指定独占上限，请记住对包含索引`{ age: 1 }`的名为 collection 的集合的以下操作:

```
db.collection.find( { <query> } ).max( { age: 100 } ).hint( { age: 1 } )
```

该操作将把查询限制在字段 age 小于 100 的文档中，并强制执行一个将从`minKey`到 100 扫描`{ age: 1 }`索引的查询计划。

#### $解释

该操作符将为您提供有关查询计划的信息。它返回一个文档，描述用于返回查询的索引和过程。这在尝试优化查询时会很有用。

您可以用以下任何一种形式提及`$explain`运算符:

```
db.collection.find()._addSpecial( "$explain", 1 )
db.collection.find( { $query: {}, $explain: 1 } )
```

## MongoDB 操作员的最佳实践

在这一节中，我们将看看使用这些 MongoDB 操作符时的一些最佳实践。

### 嵌入和引用

嵌入是数据建模的自然延伸。它允许您避免应用程序连接，这可以减少更新和查询。

您可以在单个文档中嵌入一对一关系的数据。也就是说，具有多:1 关系的数据(其中“多”对象与其父文档一起出现)也可能是很好的候选对象。

将这些类型的数据存储在同一个文档中听起来是一个谨慎的选择。但是，嵌入为这种数据局部性的读操作提供了更好的性能。

嵌入式数据模型还可以帮助开发人员在一次写操作中更新相关数据。这是因为单个文档写入是事务性的。

您应该考虑在下列情况下使用引用:

*   当你更新一个文件片段，它变得越来越长，而其余的文件是静态的。
*   当文档被访问但包含很少使用的数据时。嵌入只会增加内存需求，所以引用更有意义。
*   当文档大小超过 MongoDB 的 16MB 文档限制时。这可能发生在建模多对一关系时(例如，*雇员:部门*)。

### 检查分析和查询模式

对于大多数开发人员来说，[优化性能](https://kinsta.com/blog/performance-testing-tools/)的第一步是理解实际的和预期的查询模式。一旦您足够了解应用程序的查询模式，您就可以建立数据模型并选择适当的索引。

MongoDB 开发人员可以使用各种强大的工具来提高性能。但是这并不意味着可以忽略查询概要文件和模式。

例如，提高性能的一个简单方法是分析查询模式，了解可以在哪里嵌入数据。在确定主要查询模式后，提高 MongoDB 性能的其他方法包括:

*   确保您查询的所有字段都有索引。
*   存储文档上频繁子查询的结果以减少读取负载。
*   查看您的日志以了解缓慢的查询，然后检查您的索引。

### 查看数据索引和建模

在建立数据模型时，您将决定如何对数据之间的关系进行建模。例如，选择何时嵌入一个文档，而不是在不同集合中的不同文档之间创建一个引用，这是一个特定于应用程序的考虑的例子。

JSON 文档的一个主要优点是，它们允许开发人员根据应用程序的需求对数据进行建模。嵌套子文档和数组通过利用简单的文本文档帮助您对数据之间的复杂关系进行建模。

您还可以使用 MongoDB 对以下内容进行建模:

*   地理空间数据
*   表格、平面和柱状结构
*   简单的键值对
*   时间序列数据
*   连通图数据结构的边和节点等

### 监控分片和复制

复制对于提高性能至关重要，因为它通过水平扩展提高了数据可用性。复制可以通过冗余带来更好的性能和更高的安全性。

性能监控可能会很麻烦，需要额外的资源和时间来确保平稳运行。您可以利用市场上可以满足您特定需求的性能监控工具。

例如， [Kinsta APM](https://kinsta.com/apm-tool/) 可以获取你的 WordPress 站点的 MySQL 数据库查询、PHP 进程、外部 HTTP 调用等等的时间戳信息。您也可以使用这个免费工具来调试:

*   长 API 调用
*   长外部 URL 请求
*   缓慢的数据库查询等等。

在 MongoDB 中，复制可以通过副本集来实现，副本集允许开发人员从主节点或服务器跨多个辅助节点复制数据。这使您的复制可以在辅助服务器上运行一些查询，而不是在主服务器上运行，从而避免争用并实现更好的负载平衡。

MongoDB 中的分片集群是潜在提高性能的另一种方式。与复制类似，分片可用于跨多个服务器分布大型数据集。

通过利用碎片密钥，开发人员可以在多台服务器上复制数据的碎片或片段。这些服务器可以协同工作来使用所有的数据。

分片有它的优势，包括写/读的水平扩展、更高的可用性和增加的存储容量。

### 确定内存使用

当一个应用程序的工作集(即频繁访问的数据和索引)在内存中没有问题时，MongoDB 的性能最佳。虽然其他因素对性能至关重要，但 RAM 大小是确定实例大小的最重要因素。

当应用程序的工作集适合 RAM 时，从磁盘读取的活动需要很少。但是，如果您的工作集超过了实例服务器的 RAM 或大小，读取活动将开始激增。

如果您看到这种情况发生，您可以通过转移到一个具有更多内存的更大的实例来解决这个问题。

### 将多值字段放在末尾

如果您正在索引几个字段，并且您想要查询的字段之一使用了那些“多值”操作符中的一个，那么您应该将它们放在索引的末尾。您需要对索引进行排序，以便首先显示精确值的查询字段，最后显示“多值”运算符。

一个例外是根据字段进行排序。将它们放在“多值”和精确字段之间，以减少所需的内存排序量。

## 摘要

对于 MongoDB 来说，速度是游戏的名字。为了快速返回查询，MongoDB 利用操作符来执行数学或逻辑任务。简单来说，理解 MongoDB 运算符是掌握 MongoDB 的关键。

[Ready to dive deep into the world of MongoDB operators? 👀 You've come to the right place 💪Click to Tweet](https://twitter.com/intent/tweet?url=https%3A%2F%2Fkinsta.com%2Fblog%2Fmongodb-operators%2F&via=kinsta&text=Ready+to+dive+deep+into+the+world+of+MongoDB+operators%3F+%F0%9F%91%80+You%27ve+come+to+the+right+place+%F0%9F%92%AA&hashtags=MongoDB%2CWebDev)

本文重点介绍了一些关键的 MongoDB 操作符，例如比较操作符、逻辑操作符、元操作符和投影操作符等等。它还帮助您理解如何使用 MongoDB 操作符，以及让您充分利用它们的最佳实践。

在所有运算符中，您最常用哪一个，为什么？在下面的评论中分享吧——我们很想听听你的想法！

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。