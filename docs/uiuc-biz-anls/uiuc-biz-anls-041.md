#  041：使用筛选器探索数据框 📊

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_0.png)

在本节课中，我们将学习如何使用Pandas库来探索和提取数据框的子集。这对于了解数据内容以及后续的数据处理和操作至关重要。

## 概述

我们将介绍几种查看和筛选Pandas数据框的方法，包括使用`head`、`tail`、`sample`方法，以及方括号`[]`、点号`.`、`loc`和`iloc`操作符。这些技巧能帮助你快速浏览数据，并提取出你感兴趣的部分。

---

## 读取与准备数据

首先，我们需要将数据导入Python环境。我们将使用Jupyter Lab进行演示，以便你能直观地看到操作过程。

以下是读取数据的步骤：

1.  导入Pandas库。
2.  使用`read_pickle`函数读取一个压缩的薪资调查数据文件。

```python
import pandas as pd
sd = pd.read_pickle('salary_survey21.xz')
```

运行代码后，我们可以使用`%whos`这个“魔法命令”来确认数据已成功加载，并查看其维度（28135行，18列）。

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_2.png)

---

## 初步查看数据

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_4.png)

在数据加载后，我们通常希望先直观地查看一下数据的内容和结构。

以下是几种快速查看数据的方法：

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_6.png)

*   **`head()`方法**：查看数据框的前5行。
    ```python
    sd.head()
    ```
*   **`tail()`方法**：查看数据框的最后5行。
    ```python
    sd.tail()
    ```
*   **`sample()`方法**：随机抽取指定数量的行。例如，抽取5行。
    ```python
    sd.sample(5)
    ```

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_8.png)

这些方法能让你对数据的整体样貌有一个快速的了解。

---

## 使用方括号 `[]` 筛选

如果我们想查看特定的行和列，甚至重新排列列的顺序，可以使用方括号`[]`进行筛选。

例如，我们想查看第10到20行（注意：结束索引21不包含在内），并且只查看`job_title`、`job_context`、`annual_salary`和`industry`这几列，同时调整它们的显示顺序。

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_10.png)

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_11.png)

```python
sd[10:21][['job_title', 'job_context', 'annual_salary', 'industry']]
```

更重要的是，我们可以将筛选后的结果保存为一个新的数据框，以便后续分析。

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_13.png)

```python
sd_b = sd[10:21][['job_title', 'job_context', 'annual_salary', 'industry']]
```

运行`%whos`命令，可以看到我们创建了一个名为`sd_b`的新数据框，它只有11行和4列。

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_15.png)

---

## 使用点号 `.` 访问列

当我们需要访问单个列时，使用点号`.`表示法非常方便。

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_17.png)

例如，如果我们只想获取`industry`列的第10到20行数据，可以这样做：

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_19.png)

```python
sd.industry[10:21]
```

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_21.png)

这种方法简洁明了，特别适用于提取单列数据。

---

## 使用 `loc` 操作符筛选

`loc`操作符主要用于通过**行标签和列名**进行筛选。它非常灵活，可以处理非连续的行和列。

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_23.png)

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_24.png)

假设我们想查看第4、5、7行，以及从`industry`到`annual_salary`的所有连续列。

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_25.png)

```python
sd.loc[[4, 5, 7], 'industry':'annual_salary']
```

注意，当使用列名和冒号`:`指定范围时，`loc`会包含起始和结束的列。

---

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_27.png)

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_28.png)

## 使用 `iloc` 操作符筛选

`iloc`操作符与`loc`类似，但它是基于**行和列的整数位置（索引）**进行筛选的，索引从0开始。

假设我们想通过索引位置查看相同的行（第4、5、7行）和列（第2到5列，对应`industry`到`annual_salary`）。

```python
sd.iloc[[4, 5, 7], 2:6]
```

请注意，当使用`iloc`和整数切片时，遵循“左闭右开”原则，即包含起始索引2，但不包含结束索引6。

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_30.png)

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_31.png)

---

## 总结

本节课我们一起学习了五种在Pandas中探索和筛选数据框的方法：
1.  **`head()`, `tail()`, `sample()`**：用于快速浏览数据。
2.  **方括号 `[]`**：通过行切片和列名列表来筛选行和列，并可调整列顺序。
3.  **点号 `.`**：方便地访问单个列。
4.  **`loc`操作符**：通过行/列标签名进行灵活筛选，切片包含两端。
5.  **`iloc`操作符**：通过行/列的整数索引位置进行筛选，切片遵循“左闭右开”。

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_33.png)

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_34.png)

![](img/ca8d6e5e9efa1532f7e1803f86a3a4d2_35.png)

掌握这些基础筛选技巧是进行数据探索的第一步。在后续课程中，我们将学习如何使用条件语句来提取满足特定条件的行和列，从而进行更深入的数据分析。