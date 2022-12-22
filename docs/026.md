# 了解数据库技术:SQLite 与 MySQL

> 原文：<https://kinsta.com/blog/sqlite-vs-mysql/>

数据库已经成为几乎所有可以想象的应用程序必不可少的后端存储工具。如果您的应用程序包含需要访问的数据，您将需要一个数据库来快速存储和检索它。

数据库管理系统(DBMS)是设计用来使用、检索和定义规则以验证和操作数据库中的数据的软件。DBMS 有很多种类型:关系型、面向对象型、层次型和基于网络的。

选择合适的 DBMS 对于应用程序的成功和速度至关重要。由于有许多开源 DBMSs 可用，包括 [MySQL](https://kinsta.com/knowledgebase/what-is-mysql/) 、 [MariaDB](https://kinsta.com/blog/mariadb-vs-mysql/) 、 [SQLite](https://www.sqlite.org/index.html) 、 [PostgreSQL](https://kinsta.com/knowledgebase/what-is-postgresql/) 和 [Neo4j](https://kinsta.com/blog/open-source-database/) ，为您的项目选择最合适的数据库可能具有挑战性。

让我们比较两个最流行的开源管理系统——MySQL 和 SQLite——详细说明它们是如何工作的，它们的根本区别，优缺点，最后，哪一个更适合 WordPress 托管的 web 应用程序。

## 使用开源数据库的好处

虽然有许多专有的 DBMS 选项，但是[开源数据库](https://kinsta.com/blog/open-source-database/)已经被证明是最受欢迎的。它们的主要好处包括:

*   数据库信息不会与其他人共享，这提供了安全优势。
*   降低扩展成本，以支持更高数量的数据或请求
*   一些开源数据库在可用资源的基础上运行，使它们更灵活地满足应用程序的需求。

## 什么是 SQLite？

如前所述，DBMSes 由四种主要类型组成。这些类型中的大多数以分层模型处理数据，以树状结构组织，并通过链接连接。

SQLite 是一个开源的关系数据库管理系统(RDBMS)。[RDBMS](https://kinsta.com/blog/open-source-database/#5-sqlite)将数据存储在多个二维表中，而不是一个大表中。每个表都由包含唯一值(称为键)的行组成，键用于关联表。这就是这些 DBMSes 被称为关系型的原因。

RDBMS 中有两种类型的键:主键和外键。主键是标识每个数据库行的唯一值，而您可以使用外键来引用其他表。例如，假设您有一个公司雇员的数据库。没有必要将部门名称添加到雇员表中。相反，您可以在 employee 表中添加一个引用(外键)到 department 的列。该外键引用“department”表中的特定行。

顾名思义，SQLite 在设置、管理和存储方面是轻量级的。

大多数数据库需要一个服务器进程，但是 SQLite 是无服务器的，这意味着应用程序可以直接读写数据，而不需要客户端-服务器架构。此外，无服务器 SQLite 不需要安装或配置，因此它是独立的，对操作系统的依赖性更小。

这些特性使得 SQLite 适用于物联网( [IoT](https://kinsta.com/blog/types-of-cloud-computing/#internet-of-things-iot) )、嵌入式应用和桌面应用。

## 什么是 MySQL？

快速、可靠且易于学习，大多数应用程序使用 MySQL 作为他们的首选 DBMS。

与 SQLite 不同，MySQL 遵循客户机-服务器架构，需要一个服务器来运行。服务器使用结构化查询语言(SQL)处理检索、操作和添加数据等命令。

MySQL 还带有一个内置的图形用户界面(GUI ),称为 MySQL Workbench，用于访问数据。它还提供了一个名为 **mysqladmin** 的命令行界面(CLI)来管理可用数据。

此外，MySQL 是独立于平台的，这意味着它可以在任何操作系统上运行，并兼容不同的编程语言，如 Python、Java 和 C++。

成为最受欢迎的 DBMS 还有另一个优势:它的社区。互联网上有数百万的教程可以帮助你学习 MySQL，你几乎可以在网上找到任何问题的答案。由于 Oracle 维护 MySQL，您可以在 [MySQL 网站](https://dev.mysql.com/doc/)上找到教程、证书和支持。你也可以在我们的博客上阅读更多关于 MySQL 的内容。

## SQLite 与 MySQL:用例分解

虽然 MySQL 和 SQLite 都是开源 RDBMSes，但它们有非常不同的架构和用例。

### 体系结构

[MySQL](https://kinsta.com/knowledgebase/what-is-mysql/) 遵循多层的服务器-客户端架构，由客户端、服务器和存储组成。客户端层使用 GUI 或 CLI 处理用户查询和命令。服务器层处理命令的逻辑，为每个请求创建一个新线程。最后，存储层负责存储数据表。

相比之下，SQLite 是一个无服务器的 DBMS，它将 SQL 编译成字节码，然后使用虚拟机执行。后端以 B 树实现的方式将表存储在磁盘上。

### 数据类型

像大多数 DBMSes 一样，MySQL 使用[静态类型](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)进行数据存储，这意味着您必须在创建表时定义列数据类型。

## 注册订阅时事通讯



### 想知道我们是怎么让流量增长超过 1000%的吗？

加入 20，000 多名获得我们每周时事通讯和内部消息的人的行列吧！

[Subscribe Now](#newsletter)

虽然大多数数据库引擎仍然使用静态类型来存储字符串数据，但是 SQLite 使用动态类型来存储数据—存储在列中的值决定了列的数据类型。例如，如果在创建时创建整数类型的表，则可以在此列中存储任何数据类型，因为该类型与值本身相关联，而不是与其容器相关联。此外，MySQL 对常见的静态类型具有向后兼容性。

SQLite 使用[存储类](https://www.sqlite.org/datatype3.html)存储数据，而不是数据类型。它们比数据类型更通用，可以采用以下存储类之一:NULL、INTEGER、TEXT、BLOB 和 REAL。

### 可量测性

MySQL 的服务器-客户端架构是为可伸缩性和大型数据库而精心设计的。服务器层简化了服务器的功能，而无需更新客户端。

相反，SQLite 仅限于单用户访问，难以实现可伸缩性。此外，随着数据库变大，所需的内存量也会增加。

### 轻便

MySQL 需要在移动前压缩成一个文件，随着数据库的增加，这可能需要很长时间。同时，SQLite 将数据库保存到一个文件中，使复制和传输变得容易。因为 SQLite 在虚拟机上运行查询，所以它对操作系统的依赖性很小。

### 安全性

任何人都可以编辑和查看 SQLite 的单个数据文件。SQLite 没有内置的身份验证系统，所以安全性仅限于对该文件设置的权限。

另一方面，MySQL 有许多安全特性，比如支持不同权限级别的用户管理和使用[安全外壳(SSH)](https://kinsta.com/blog/how-to-use-ssh/) 。

### 易于设置

MySQL 需要很多配置，比如服务器配置、用户管理和备份。另一方面，SQLite 易于安装，不需要任何配置就可以运行。

Struggling with downtime and WordPress problems? Kinsta is the hosting solution designed to save you time! [Check out our features](https://kinsta.com/features/)

## SQLite 与 MySQL:利弊

### MySQL 优点:

*   简单易学
*   几乎兼容所有操作系统
*   与许多语言兼容，如 C++，PHP，Java，Perl 等。
*   支持多用户环境
*   高性能

### MySQL 的缺点:

*   一些数据损坏的实例(尽管不严重)
*   调试工具需要一些改进
*   需要大量内存

### SQLite 优点:

*   低服务器性能和内存需求
*   降低能耗
*   独立便携
*   默认包含在所有 PHP 安装中

### SQLite 缺点:

*   不支持多用户环境或 XML 格式
*   一次只能处理一个连接
*   随着数据库大小的增加，性能会降低
*   无法从客户端查询数据库

## SQLite vs MySQL:WordPress 哪个更好？

WordPress 是一个用 PHP 编写的流行的内容管理平台(CMS)，它使用数据库来存储所有的网站信息，如用户数据、帖子、设置和内容。

WordPress 的默认数据库管理系统是 MySQL，这使得它成为大多数 WordPress 站点事实上的选择。它非常适合大型项目，因为它易于扩展并提供更高的安全性。然而，SQLite 非常适合于连接较少的小型项目，尤其是如果您需要跳过复杂的 MySQL 数据库配置的话。

虽然您可以使用变通方法让 SQLite 与 WordPress 一起工作，但这并不简单。WordPress 核心团队已经开始讨论[让 WordPress 官方支持 SQLite](https://make.wordpress.org/core/2022/09/12/lets-make-wordpress-officially-support-sqlite/) 。实现这个特性可能需要一些时间，但是在 WordPress 安装过程中选择数据库类型将会非常有帮助。

还有 MariaDB，它是更大的 MySQL 的一个变种。MariaDB 提供了改进的性能、更敏捷的更新和更好的许可。虽然它们大体相似，但在某些情况下，MariaDB 更好。你可以在这里阅读更多关于 [MariaDB vs MySQL 的内容。](https://kinsta.com/blog/mariadb-vs-mysql/)

## 摘要

数据库对于大多数应用程序来说是必不可少的。虽然数据库有不同的许可类型，但是开源数据库管理系统为其他专有解决方案提供了一个很好的替代方案。

比较 SQLite 和 MySQL 具有挑战性，因为两者都有便利的特性和独特的用例。SQLite 是轻量级和可移植的，更适合物联网和低流量网站等小规模应用。另一方面，MySQL 拥有庞大的社区基础，更适合可伸缩的应用程序。

*合适的工具取决于您应用的独特要求。选择完美的存储和托管解决方案可能很有挑战性。然而，不要烦恼！我们可以帮助。*

* * *

让你所有的[应用程序](https://kinsta.com/application-hosting/)、[数据库](https://kinsta.com/database-hosting/)和 [WordPress 网站](https://kinsta.com/wordpress-hosting/)在线并在一个屋檐下。我们功能丰富的高性能云平台包括:

*   在 MyKinsta 仪表盘中轻松设置和管理
*   24/7 专家支持
*   最好的谷歌云平台硬件和网络，由 Kubernetes 提供最大的可扩展性
*   面向速度和安全性的企业级 Cloudflare 集成
*   全球受众覆盖全球多达 35 个数据中心和 275 多个 pop

在第一个月使用托管的[应用程序或托管](https://kinsta.com/application-hosting/)的[数据库，您可以享受 20 美元的优惠，亲自测试一下。探索我们的](https://kinsta.com/database-hosting/)[计划](https://kinsta.com/plans/)或[与销售人员交谈](https://kinsta.com/contact-us/)以找到最适合您的方式。