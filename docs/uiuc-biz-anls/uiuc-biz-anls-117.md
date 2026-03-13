#  117：Python中的SQLite探索性查询 🔍

![](img/1263b41adf93f46f9494837d82682e51_0.png)

在本节课中，我们将学习如何使用SQL查询来探索SQLite数据库，其功能类似于在Python中使用Pandas的`info()`和`head()`方法来探索数据框。这对于处理大型数据库至关重要，因为你通常无法将所有数据下载到本地进行分析。我们将学习如何通过SQL查询来识别和筛选需要的数据。

## 建立数据库连接

首先，我们需要导入必要的模块并建立与数据库的连接。我们将使用`pandas`和`sqlite3`模块。

![](img/1263b41adf93f46f9494837d82682e51_2.png)

```python
import pandas as pd
import sqlite3

![](img/1263b41adf93f46f9494837d82682e51_4.png)

# 建立与数据库的连接
conn = sqlite3.connect('techca.db')
```

## 探索数据库结构

上一节我们建立了数据库连接，本节中我们来看看如何探索数据库中有哪些表。

了解数据库中的表及其相互关系是第一步。虽然最好有实体关系图，但在Python环境中，我们可以通过查询来获取这些信息。

![](img/1263b41adf93f46f9494837d82682e51_6.png)

以下是获取数据库中所有表信息的查询：

```python
# 查询SQLite系统表以获取所有用户表的信息
tables_df = pd.read_sql("SELECT * FROM sqlite_master WHERE type='table'", conn)
tables_df.set_index('name', inplace=True)
print(tables_df)
```

执行此查询后，你将看到一个包含表名和创建语句的数据框，这有助于你了解数据库的结构。

![](img/1263b41adf93f46f9494837d82682e51_8.png)

![](img/1263b41adf93f46f9494837d82682e51_9.png)

![](img/1263b41adf93f46f9494837d82682e51_11.png)

## 查看特定表的列信息

在了解了有哪些表之后，我们通常需要查看某个具体表的结构，例如列名、数据类型和主键/外键信息。

![](img/1263b41adf93f46f9494837d82682e51_13.png)

![](img/1263b41adf93f46f9494837d82682e51_15.png)

让我们以`transactions`表为例，查看其模式（schema）。

![](img/1263b41adf93f46f9494837d82682e51_17.png)

```python
# 获取transactions表的创建语句，其中包含列信息
table_schema = tables_df.loc['transactions', 'sql']
print(table_schema)
```

![](img/1263b41adf93f46f9494837d82682e51_19.png)

这段代码会打印出创建`transactions`表的SQL命令，你可以从中看到所有列的定义、数据类型以及外键约束。

## 获取表的行数

在分析数据之前，了解数据量的大小非常重要。我们可以使用SQL的`COUNT(*)`函数来获取表中的总行数。

```python
# 查询transactions表的总行数
row_count_df = pd.read_sql("SELECT COUNT(*) FROM transactions", conn)
print(f"表中共有 {row_count_df.iloc[0,0]} 行数据。")
```

![](img/1263b41adf93f46f9494837d82682e51_21.png)

## 预览表数据

![](img/1263b41adf93f46f9494837d82682e51_23.png)

类似于Pandas的`head()`方法，我们可以使用SQL的`LIMIT`子句来预览表的前几行数据，而无需加载整个表。

![](img/1263b41adf93f46f9494837d82682e51_25.png)

```python
# 查询transactions表的前5行数据
preview_df = pd.read_sql("SELECT * FROM transactions LIMIT 5", conn)
print(preview_df)
```

![](img/1263b41adf93f46f9494837d82682e51_27.png)

![](img/1263b41adf93f46f9494837d82682e51_28.png)

## 检查缺失值

![](img/1263b41adf93f46f9494837d82682e51_30.png)

数据清洗是分析的关键步骤。在SQL中，我们可以查询特定列中缺失值（NULL）的数量。需要注意的是，有时缺失值可能以特定字符串（如`‘NAN’`）存储。

以下是检查`customer_id`列中缺失值的示例：

![](img/1263b41adf93f46f9494837d82682e51_32.png)

```python
# 查询customer_id列为NULL的行数（标准缺失值）
null_count_df = pd.read_sql("SELECT COUNT(*) FROM transactions WHERE customer_id IS NULL", conn)
print(f"标准NULL缺失值数量: {null_count_df.iloc[0,0]}")

# 查询customer_id列为特定字符串‘NAN’的行数（非标准缺失值）
nan_count_df = pd.read_sql("SELECT COUNT(*) FROM transactions WHERE customer_id = 'NAN'", conn)
print(f"字符串‘NAN’的数量: {nan_count_df.iloc[0,0]}")
```

## 根据探索结果读取数据

![](img/1263b41adf93f46f9494837d82682e51_34.png)

经过上述探索，我们可能决定只读取满足特定条件的数据，以节省内存并提高分析效率。

例如，我们只想读取`revenue`大于2的交易记录：

![](img/1263b41adf93f46f9494837d82682e51_36.png)

![](img/1263b41adf93f46f9494837d82682e51_37.png)

```python
# 构建查询语句，筛选revenue > 2的数据
query = "SELECT * FROM transactions WHERE revenue > 2"

# 执行查询并将结果读入Pandas数据框
filtered_df = pd.read_sql(query, conn)
print(filtered_df.info())
```

读取所需数据后，记得关闭数据库连接。

![](img/1263b41adf93f46f9494837d82682e51_39.png)

```python
# 关闭数据库连接
conn.close()
```

## 总结

![](img/1263b41adf93f46f9494837d82682e51_41.png)

本节课中我们一起学习了如何在Python环境中使用SQL查询来探索SQLite数据库。我们掌握了以下技能：
1.  连接数据库。
2.  列出所有表。
3.  查看特定表的详细结构。
4.  获取表的行数。
5.  预览表的前几行数据。
6.  检查数据中的缺失值。
7.  根据探索结果，编写筛选查询并读取所需数据到Pandas中进行后续分析。

![](img/1263b41adf93f46f9494837d82682e51_43.png)

这种方法使你能够有效地探索大型数据库，而无需将全部数据加载到内存中，从而优化了工作流程和资源使用。