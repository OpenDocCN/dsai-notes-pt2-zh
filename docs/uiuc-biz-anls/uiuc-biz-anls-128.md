#  128：循环入门教程 🌀

![](img/83d179a2189f3b256282fd83acdf32ac_1.png)

在本节课中，我们将要学习循环（Loops）的基本概念及其在Python中的几种常见类型。循环是编程中用于避免重复代码、提高效率的重要工具。

## 概述

循环能帮助我们编写DRY（Don't Repeat Yourself）代码，避免WET（Write Every Time）代码。WET代码指通过复制粘贴产生的重复代码，它难以维护且容易出错。我们将介绍四种循环：基本for循环、列表推导式、while循环和pandas的apply方法。

## 基本for循环

上一节我们介绍了循环的基本概念，本节中我们来看看最常用的for循环。for循环用于遍历序列（如列表或数字范围）中的每个元素。

![](img/83d179a2189f3b256282fd83acdf32ac_3.png)

以下是基本for循环的示例代码：

![](img/83d179a2189f3b256282fd83acdf32ac_4.png)

![](img/83d179a2189f3b256282fd83acdf32ac_6.png)

```python
for i in range(5):
    print(f"This is iteration {i}")
```

这段代码使用`range(5)`生成数字0到4的序列。变量`i`依次代表序列中的每个值。缩进部分的代码会在每次迭代中执行。

## 遍历列表的for循环

除了数字范围，for循环还可以直接遍历列表中的元素。

以下是遍历文件名列表的示例：

```python
my_files = ["file1.csv", "file2.csv", "file3.xlsx", "file4.parquet"]
for n in my_files:
    print(n)
```

![](img/83d179a2189f3b256282fd83acdf32ac_8.png)

![](img/83d179a2189f3b256282fd83acdf32ac_9.png)

这里变量`n`依次代表`my_files`列表中的每个文件名。循环会打印出所有文件名。

![](img/83d179a2189f3b256282fd83acdf32ac_11.png)

![](img/83d179a2189f3b256282fd83acdf32ac_12.png)

## 列表推导式

![](img/83d179a2189f3b256282fd83acdf32ac_13.png)

列表推导式（List Comprehension）是for循环的简洁写法，特别适用于需要将结果保存为列表的简单循环。

![](img/83d179a2189f3b256282fd83acdf32ac_15.png)

以下是列表推导式的基本结构：

![](img/83d179a2189f3b256282fd83acdf32ac_17.png)

```python
[expression for item in iterable]
```

以下是将文件名列表中的CSV文件筛选出来的示例：

![](img/83d179a2189f3b256282fd83acdf32ac_19.png)

```python
csv_files = [n for n in my_files if n.find(".csv") >= 0]
```

这段代码会创建一个新列表`csv_files`，其中只包含原始列表中文件名包含“.csv”的元素。

## while循环

while循环在指定条件为真时重复执行代码块，条件变为假时停止。

以下是while循环的示例：

![](img/83d179a2189f3b256282fd83acdf32ac_21.png)

![](img/83d179a2189f3b256282fd83acdf32ac_22.png)

```python
i = 1
while i < 10:
    print(i)
    i += 1  # 等同于 i = i + 1
```

循环从`i=1`开始，每次迭代打印`i`的值并将其加1，直到`i`不再小于10时停止。

![](img/83d179a2189f3b256282fd83acdf32ac_24.png)

## pandas的apply方法

在处理数据框（DataFrame）时，pandas库的`apply`方法可以对多列或多行应用函数，实现类似循环的效果。

以下是将数据框多列转换为数值类型的示例：

```python
import pandas as pd

![](img/83d179a2189f3b256282fd83acdf32ac_26.png)

df = pd.DataFrame({
    'A': ['1', '2', 'a'],
    'B': ['4', '5', '6']
})

df = df.apply(pd.to_numeric, errors='coerce')
```

![](img/83d179a2189f3b256282fd83acdf32ac_28.png)

`apply`方法将`pd.to_numeric`函数应用到数据框的每一列。参数`errors='coerce'`会将无法转换的值（如字母‘a’）替换为缺失值（NaN）。

## 总结

![](img/83d179a2189f3b256282fd83acdf32ac_30.png)

![](img/83d179a2189f3b256282fd83acdf32ac_31.png)

本节课中我们一起学习了四种主要的循环结构：基本for循环用于遍历序列；列表推导式用于简洁地生成列表；while循环用于在条件满足时重复执行；pandas的apply方法用于对数据框进行批量操作。掌握这些循环技巧能帮助你编写更高效、更易维护的DRY代码。