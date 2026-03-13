# 24：SQL进阶操作与数据聚合 🧮

![](img/5c50caa639b7f09cd91b34a87a5be42c_0.png)

![](img/5c50caa639b7f09cd91b34a87a5be42c_2.png)

![](img/5c50caa639b7f09cd91b34a87a5be42c_4.png)

![](img/5c50caa639b7f09cd91b34a87a5be42c_6.png)

![](img/5c50caa639b7f09cd91b34a87a5be42c_7.png)

![](img/5c50caa639b7f09cd91b34a87a5be42c_9.png)

在本节课中，我们将学习SQL（结构化查询语言）的进阶操作，包括数据过滤、创建与修改表格、数据聚合以及多表连接。这些技能对于管理和分析数据库中的数据至关重要。

上一节我们介绍了SQL的基本查询和过滤操作。本节中，我们将深入探讨更多高级功能，并学习如何通过聚合和连接来整合数据。

## 数据过滤与模式匹配 🔍

在SQL中，`WHERE`子句用于根据条件过滤数据。除了基本的比较运算符（如`=`、`>`、`<`），SQL还提供了强大的模式匹配功能。

### 使用`LIKE`进行模式匹配

`LIKE`运算符允许我们进行文本的模糊匹配。它通常与通配符`%`一起使用，`%`代表零个、一个或多个任意字符。

以下是`LIKE`运算符的使用示例：

```sql
SELECT * FROM cones WHERE flavor LIKE '%berry%';
```

![](img/5c50caa639b7f09cd91b34a87a5be42c_11.png)

此查询将返回所有`flavor`列中包含“berry”子串的行，例如“strawberry”和“blueberry”。

![](img/5c50caa639b7f09cd91b34a87a5be42c_13.png)

![](img/5c50caa639b7f09cd91b34a87a5be42c_15.png)

### 组合过滤条件

我们可以使用逻辑运算符`AND`、`OR`、`NOT`来组合多个过滤条件，构建更复杂的查询。

![](img/5c50caa639b7f09cd91b34a87a5be42c_17.png)

```sql
SELECT * FROM cones WHERE flavor LIKE '%berry%' AND price > 5.00;
```

此查询将返回价格高于5.00且口味包含“berry”的所有冰淇淋甜筒。

## 表格的创建与修改 📝

SQL不仅用于查询数据，还可以创建和修改数据库中的表格结构。

### 创建表格

使用`CREATE TABLE`语句可以基于查询结果创建一个新表格。

```sql
CREATE TABLE fancy_cones AS SELECT * FROM cones WHERE price > 4.50;
```

此语句创建了一个名为`fancy_cones`的新表，其中包含原`cones`表中价格高于4.50的所有行。

### 插入数据

使用`INSERT INTO`语句可以向现有表格中添加新的数据行。

```sql
INSERT INTO cones (id, flavor, color, price) VALUES (7, 'vanilla', 'white', 3.95);
```

![](img/5c50caa639b7f09cd91b34a87a5be42c_19.png)

此语句向`cones`表中插入了一行新数据。

### 更新数据

![](img/5c50caa639b7f09cd91b34a87a5be42c_21.png)

使用`UPDATE`语句可以修改表格中现有的数据。结合`WHERE`子句可以精确地更新特定行。

```sql
UPDATE cones SET price = price * 1.1 WHERE flavor = 'strawberry';
```

此语句将所有草莓口味甜筒的价格提高10%。

![](img/5c50caa639b7f09cd91b34a87a5be42c_23.png)

**注意**：更新操作是永久性的，执行前需谨慎。建议在对重要数据进行操作前进行备份。

## 数据聚合与分组 📊

![](img/5c50caa639b7f09cd91b34a87a5be42c_25.png)

数据聚合是指对多行数据进行计算，返回一个汇总结果。这是数据分析中的核心操作。

![](img/5c50caa639b7f09cd91b34a87a5be42c_27.png)

### 基本聚合函数

SQL提供了多种聚合函数，例如：
*   `COUNT(*)`: 计算行数。
*   `AVG(column)`: 计算某列的平均值。
*   `MIN(column)`: 查找某列的最小值。
*   `MAX(column)`: 查找某列的最大值。
*   `SUM(column)`: 计算某列的总和。

![](img/5c50caa639b7f09cd91b34a87a5be42c_29.png)

![](img/5c50caa639b7f09cd91b34a87a5be42c_31.png)

```sql
SELECT COUNT(*) AS total_cones, AVG(price) AS average_price FROM cones;
```

![](img/5c50caa639b7f09cd91b34a87a5be42c_33.png)

此查询返回甜筒的总数量和平均价格。

### 使用`GROUP BY`进行分组

`GROUP BY`子句允许我们将数据分成多个组，然后对每个组分别进行聚合计算。

```sql
SELECT flavor, COUNT(*) AS count FROM cones GROUP BY flavor;
```

此查询按口味对甜筒进行分组，并统计每种口味的数量。

## 多表连接 🔗

在实际应用中，数据通常分布在多个相关的表中。SQL的`JOIN`操作允许我们将这些表连接起来，进行跨表查询。

![](img/5c50caa639b7f09cd91b34a87a5be42c_35.png)

### 交叉连接（笛卡尔积）

![](img/5c50caa639b7f09cd91b34a87a5be42c_37.png)

最简单的连接是列出多个表，这将返回所有可能的行组合。

```sql
SELECT * FROM cones, sales;
```

此查询返回`cones`表和`sales`表的笛卡尔积，即每一行甜筒数据与每一行销售数据的组合。

![](img/5c50caa639b7f09cd91b34a87a5be42c_39.png)

![](img/5c50caa639b7f09cd91b34a87a5be42c_41.png)

### 内连接

更常见的是根据两个表之间的关联列进行连接，这称为内连接。

```sql
SELECT * FROM sales, cones WHERE sales.cone_id = cones.id;
```

![](img/5c50caa639b7f09cd91b34a87a5be42c_43.png)

![](img/5c50caa639b7f09cd91b34a87a5be42c_45.png)

![](img/5c50caa639b7f09cd91b34a87a5be42c_47.png)

此查询通过`cone_id`和`id`列的匹配，将销售记录与对应的甜筒信息连接起来。这样，我们就可以看到每笔销售具体对应哪种甜筒。

![](img/5c50caa639b7f09cd91b34a87a5be42c_49.png)

掌握了连接操作后，我们就可以提出更复杂的业务问题，例如“哪位收银员创造了最高的销售额？”，并通过组合聚合、分组和连接操作来解答。

---

![](img/5c50caa639b7f09cd91b34a87a5be42c_51.png)

本节课中我们一起学习了SQL的进阶操作。我们探讨了如何使用`LIKE`进行复杂的模式匹配，如何创建、插入数据到和更新表格。更重要的是，我们学习了数据聚合的核心概念，包括使用`COUNT`、`AVG`等函数以及`GROUP BY`子句来总结数据。最后，我们介绍了多表连接的概念，这是关系型数据库整合信息的强大工具。这些技能构成了使用SQL进行有效数据查询和分析的基础。