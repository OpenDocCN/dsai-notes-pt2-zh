#  113：基础 SQL 命令 🛠️

![](img/462042c07d7e681b448ad767da12d165_0.png)

在本节课中，我们将学习如何使用基础 SQL 查询从一个数据库中提取数据。我们将首先了解数据库的结构，然后通过一系列简单的命令来探索和操作数据。

![](img/462042c07d7e681b448ad767da12d165_2.png)

![](img/462042c07d7e681b448ad767da12d165_3.png)

## 数据库结构与关系图

在开始使用 SQL 查询之前，理解数据库中的不同表以及它们之间的关系至关重要。我们这里看到的是一个实体关系图（ERD），它由特定的数据库集成开发环境（IDE）生成，本例中使用的是 DBeaver。

![](img/462042c07d7e681b448ad767da12d165_5.png)

这个数据库包含六个表。主表是 `transactions` 表。直接连接到 `transactions` 表的有 `sites` 表、`customer` 表和 `products` 表。`products` 表又连接到 `categories` 表，而 `categories` 表则连接到 `parent` 表。

![](img/462042c07d7e681b448ad767da12d165_7.png)

为了更好地理解 ERD 中的连接关系，可以点击连接线。例如，点击连接 `transactions` 表和 `products` 表的线，可以看到它们通过 `transactions` 表中的 `product_id` 列和 `products` 表中的 `product_id` 列进行关联。图中的标记表明，`transactions` 表中的每一行都对应一个特定的产品 ID，但 `transactions` 表中的多行数据可以关联到 `products` 表中的任意一行。

在每个表的顶部，加粗显示的列被称为**主键**，它是唯一标识表中每一行的列。主键下方的则是其他列名。

将数据存储在数据库中的一个好处是可以减少存储数据的大小。例如，这个数据库文件的大小不到对应 CSV 文件的一半。

## SQL 查询基础概念

在实际进行 SQL 查询之前，有两个重要事项。首先是提供 SQL 查询的基本概览和一些需要牢记的关键概念。

以下是需要掌握的几个关键概念：
1.  **简单关键字**：SQL 使用简单的关键字来执行查询，例如 `SELECT`、`FROM`、`LIMIT`、`WHERE`、`AND`、`OR`、`AS` 等。这些词非常易于理解。
2.  **大小写不敏感**：与 Python 不同，SQL 不区分大小写。无论你使用大写、小写还是混合大小写来拼写列名或表名，结果都一样。但按照惯例，通常将 SQL 命令大写，以帮助区分 SQL 命令和表名/列名。
3.  **特殊字符**：SQL 查询语言包含一些特殊字符，如星号 `*`、百分号 `%` 和引号 `"` 或 `'`。你会在查询中看到它们的使用。
4.  **多行格式**：为了便于阅读，SQL 查询经常被分成多行。这不是必须的，但是一种常见的做法。
5.  **分号结尾**：SQL 查询以分号 `;` 结尾。这允许你将查询语句分成多行。
6.  **注意细节**：有时最小的错误也会导致查询失败。例如，缺少逗号 `,`、空格，或者命令顺序错误，都可能导致 SQL 查询出错。

## 连接并探索数据库

接下来，我们将在命令行环境中演示如何与数据库交互。在 Windows 上可以使用命令提示符，在 Mac 上可以使用终端。在 Jupyter Lab 中，可以通过选择“终端”来打开命令行窗口。

![](img/462042c07d7e681b448ad767da12d165_9.png)

![](img/462042c07d7e681b448ad767da12d165_10.png)

![](img/462042c07d7e681b448ad767da12d165_11.png)

![](img/462042c07d7e681b448ad767da12d165_12.png)

首先，使用 `cd` 命令切换到存储数据库文件的目录。然后使用 `ls` 命令列出文件，确认 `teacha.db` 文件存在。

现在，使用以下命令连接到数据库：
```bash
sqlite3 teacha.db
```
连接成功后，会显示 SQLite 版本信息并出现 `sqlite>` 提示符。

在数据库连接中，可以使用 `.tables` 命令查看所有表名：
```bash
.tables
```
这将显示六个表：`categories`, `parents`, `sites`, `customers`, `products`, `transactions`。这些名称与之前在 ERD 中看到的完全一致。

![](img/462042c07d7e681b448ad767da12d165_14.png)

![](img/462042c07d7e681b448ad767da12d165_15.png)

另一个有用的命令是 `.schema`，它可以查看数据库的结构定义：
```bash
.schema
```
这会输出创建每个表所需的 SQL 语句。例如，对于 `parent` 表，会显示：
```sql
CREATE TABLE parent (parent_id INTEGER PRIMARY KEY, parent_name TEXT NOT NULL);
```
这表示 `parent` 表有两列：`parent_id`（整数类型，主键）和 `parent_name`（文本类型，不允许为空）。虽然可以从模式信息中重建 ERD，但不如图形化的 ERD 直观。

![](img/462042c07d7e681b448ad767da12d165_17.png)

在执行查询前，建议将输出模式设置为列格式，这样显示结果会更美观：
```bash
.mode column
```

![](img/462042c07d7e681b448ad767da12d165_19.png)

## 执行基础 SQL 查询

![](img/462042c07d7e681b448ad767da12d165_21.png)

![](img/462042c07d7e681b448ad767da12d165_22.png)

现在，让我们开始执行 SQL 查询来探索数据。我们将以 `sites` 表为例。

首先，查询 `sites` 表中的所有行和所有列：
```sql
SELECT * FROM sites;
```
`SELECT *` 表示选择所有列，`FROM sites` 指定从 `sites` 表获取数据。执行后会返回表中的所有行。

![](img/462042c07d7e681b448ad767da12d165_24.png)

如果只想查看前几行，可以使用 `LIMIT` 子句：
```sql
SELECT * FROM sites LIMIT 5;
```
这将只返回前 5 行数据。

![](img/462042c07d7e681b448ad767da12d165_26.png)

![](img/462042c07d7e681b448ad767da12d165_28.png)

可以使用 `ORDER BY` 子句对结果进行排序。例如，按 `site_id` 升序排列前5行：
```sql
SELECT * FROM sites ORDER BY site_id LIMIT 5;
```
注意，`ORDER BY` 子句需要放在 `LIMIT` 子句之前，否则会导致语法错误。

![](img/462042c07d7e681b448ad767da12d165_30.png)

### 使用 WHERE 过滤数据

![](img/462042c07d7e681b448ad767da12d165_32.png)

![](img/462042c07d7e681b448ad767da12d165_33.png)

`WHERE` 子句用于根据指定条件过滤行。例如，只查询状态为“closed”的站点：
```sql
SELECT * FROM sites WHERE site_status = "closed";
```
这将只返回 `site_status` 列等于“closed”的行。

![](img/462042c07d7e681b448ad767da12d165_35.png)

可以添加多个条件进行过滤。例如，查询纬度在 40 到 41 之间的站点：
```sql
SELECT * FROM sites WHERE latitude >= 40 AND latitude < 41;
```
`AND` 运算符表示两个条件必须同时满足。

### 使用 LIKE 进行模糊匹配

`WHERE` 子句还可以与 `LIKE` 操作符结合，进行模糊字符串匹配。例如，查询地址中包含“main”这个词的所有站点：
```sql
SELECT * FROM sites WHERE address LIKE "%main%";
```
这里的百分号 `%` 是通配符，表示“任意字符序列”。`%main%` 表示在“main”前后可以有任意字符。

## 总结

本节课我们一起学习了基础 SQL 命令。我们首先了解了数据库的结构和表之间的关系。然后，我们掌握了 SQL 查询的几个关键概念，包括关键字、大小写规则和格式。

![](img/462042c07d7e681b448ad767da12d165_37.png)

通过实际操作，我们学会了如何连接到 SQLite 数据库，查看表结构和列表。最重要的是，我们练习了几个最核心的 SQL 查询命令：
*   `SELECT ... FROM ...` 用于选择数据。
*   `LIMIT` 用于限制返回的行数。
*   `ORDER BY` 用于对结果排序。
*   `WHERE` 用于根据条件过滤行，并可结合 `=`、`>`、`<`、`AND` 等操作符，以及 `LIKE` 进行模糊匹配。

![](img/462042c07d7e681b448ad767da12d165_39.png)

SQL 结构化查询语言非常直观易学。一旦掌握了这些基础命令，就可以轻松地将它们组合起来，构建更复杂的查询。值得注意的是，本节课我们是通过命令行终端与数据库交互的。在后续课程中，我们将探讨如何直接从 Python 环境中与 SQL 数据库进行交互，而不必使用终端或像 DBeaver 这样的数据库 IDE。