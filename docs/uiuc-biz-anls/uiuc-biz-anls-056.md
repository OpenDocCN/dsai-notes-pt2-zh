#  056：清理你的代码 🧹

![](img/d41048cc7a96c0a9a5cd91e040f53af0_0.png)

在本节课中，我们将要学习如何清理你的代码，而不是数据。在探索数据并创建了清理工作流之后，确保代码易于阅读且运行高效非常重要。我们将通过一个简单的场景，演示三种清理代码的方法。

## 概述

在探索数据并创建清理工作流后，代码的可读性和运行效率变得至关重要。本节将演示如何通过三个步骤来优化和清理你的代码。

## 初始场景与问题

在Jupyter Lab环境中，我们创建了一个存在多种不整洁问题的数据框。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_2.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_0.png)

这个数据框存在以下问题：
1.  列名 `a category` 中包含空格。
2.  `a category` 列中的值，有些单词首字母大写，有些则没有。
3.  数据中存在一些缺失值。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_4.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_2.png)
![](img/d41048cc7a96c0a9a5cd91e040f53af0_4.png)

## 逐步清理过程

![](img/d41048cc7a96c0a9a5cd91e040f53af0_6.png)

通常，我们会逐步执行代码，并检查每一步是否成功。

例如，要重命名一个列，我会使用 `rename` 函数，将 `a category` 改为 `category`。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_8.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_10.png)

```python
df.rename(columns={'a category': 'category'})
```

运行并验证它是否生效。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_8.png)
![](img/d41048cc7a96c0a9a5cd91e040f53af0_10.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_12.png)

接着，如果我想将 `category` 列中的所有值转换为小写，我会使用字符串的 `lower` 方法。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_14.png)

```python
df['category'] = df['category'].str.lower()
```

![](img/d41048cc7a96c0a9a5cd91e040f53af0_16.png)

然后验证 `category` 列中的所有值是否都已变为小写。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_12.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_18.png)

假设我想用平均值填充 `cost` 列中的缺失值。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_19.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_14.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_21.png)

我会使用 `fillna` 函数，用均值填充这些值。

```python
df['cost'].fillna(df['cost'].mean())
```

然后验证这些值确实已被填充。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_23.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_16.png)

最后，假设我还想删除包含缺失值的行，比如这里的这一行。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_18.png)
![](img/d41048cc7a96c0a9a5cd91e040f53af0_19.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_25.png)

我会运行删除操作，并验证数据中不再有任何缺失值。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_27.png)

```python
df.dropna()
```

![](img/d41048cc7a96c0a9a5cd91e040f53af0_21.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_29.png)

## 代码清理的三个技巧

虽然逐步执行代码很容易，但这个过程有些繁琐，无法一眼看清所有操作，并且需要频繁打印数据框。以下是清理代码的三个技巧。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_23.png)

**技巧一：移除探索性数据展示**
如果你不再需要那些用于探索的数据框或可视化图表，可以将它们从代码中移除。

**技巧二：将代码合并到单个单元格**
你可以将多个步骤的代码合并到一个单元格中，或者合并到更少的单元格里。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_25.png)
![](img/d41048cc7a96c0a9a5cd91e040f53af0_27.png)

**技巧三：通过链式调用合并步骤**
你可以更进一步，通过链式调用将多个步骤合并到一行代码中。

## 链式调用示例

让我们看看如何将所有步骤合并到一行代码中。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_29.png)

我将创建一个新的数据框 `df_clean`，然后链式调用 `rename` 方法。接着是 `assign` 方法（稍后会详细说明），然后是 `fillna` 方法、`dropna` 方法和 `reset_index` 方法。

```python
df_clean = df.rename(...).assign(...).fillna(...).dropna(...).reset_index(...)
```

通过运行这一行代码，我得到了相同的结果，但代码只有一行。

## 提升链式代码的可读性

![](img/d41048cc7a96c0a9a5cd91e040f53af0_31.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_32.png)

你可能会觉得这行代码很难阅读。确实，它很密集。而在用代码分析数据时，可读性非常重要。

让我展示如何让它变得更好。首先，你可以用括号将这行代码括起来。

```python
df_clean = (
    df.rename(...)
    .assign(...)
    .fillna(...)
    .dropna(...)
    .reset_index(...)
)
```

这样做之后，我可以将每个方法放在单独的一行。现在代码变得容易阅读得多，因为我可以清楚地看到：我获取原始数据框、重命名列、使用 `assign` 创建新列、填充缺失值、删除包含缺失值的行以及重置索引。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_34.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_31.png)
![](img/d41048cc7a96c0a9a5cd91e040f53af0_32.png)

另一个好处是，我只需要输入一次数据框的名称 `df`，而在逐步探索的代码中，我不得不反复输入 `df_clean`。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_36.png)

## 关于 `assign` 方法的注意事项

![](img/d41048cc7a96c0a9a5cd91e040f53af0_37.png)

现在，这段代码的一个缺点体现在 `assign` 这一行。`assign` 方法非常有用，它允许你在一个函数内创建新列，而无需反复输入数据框名称和列名。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_34.png)

但它的缺点是，在链式调用中，你不能像平常那样直接引用数据框本身。如果你尝试这样做，会得到一个错误。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_36.png)
![](img/d41048cc7a96c0a9a5cd91e040f53af0_37.png)

因此，我们需要使用一个称为 **Lambda函数** 的短暂匿名函数。如果你不了解Lambda函数，不必过于担心。只需知道，我们不是输入数据框名称，而是输入 `Lambda`，然后是一个字母和冒号，再用这个字母来代表数据框的名称。

```python
.assign(category_lower = lambda x: x['category'].str.lower())
```

总的来说，尽管 `assign` 方法有这个小缺点，但我非常喜欢这种链式写法，因为它极大地提高了代码的可读性。

## 总结 🎯

本节课中我们一起学习了清理代码的三个核心技巧：
1.  **移除不必要的探索性数据展示**。
2.  **将代码合并到单个或更少的单元格中**。
3.  **通过链式调用将步骤合并到更少的代码行中**，并使用括号和换行来提升可读性。

这些技巧能显著提高代码的可读性和运行效率。虽然清理代码并非强制要求，但当你日后回顾代码，或者他人阅读你的代码时，你会庆幸自己这样做了。

![](img/d41048cc7a96c0a9a5cd91e040f53af0_39.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_40.png)

![](img/d41048cc7a96c0a9a5cd91e040f53af0_39.png)
![](img/d41048cc7a96c0a9a5cd91e040f53af0_40.png)