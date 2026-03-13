# 36：NumPy基础教程 🐍

在本教程中，我们将学习Python的NumPy库。NumPy是一个用于高效操作矩阵和向量的库，在进行线性代数运算时非常有用。

## 安装与导入

![](img/a35a8cd140052c25b68a637ef74e6e63_1.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_2.png)

首先，我们需要安装NumPy。在虚拟环境中，可以使用pip进行安装。

![](img/a35a8cd140052c25b68a637ef74e6e63_4.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_6.png)

```bash
pip install numpy
```

安装完成后，我们通常以别名`np`导入NumPy，以便使用其所有功能。

![](img/a35a8cd140052c25b68a637ef74e6e63_8.png)

```python
import numpy as np
```

![](img/a35a8cd140052c25b68a637ef74e6e63_10.png)

为了确保代码的可重复性，我们可以设置一个随机种子。这样，每次运行程序时，生成的随机数序列将是相同的。

```python
np.random.seed(0)
```

![](img/a35a8cd140052c25b68a637ef74e6e63_12.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_14.png)

我们可以打印NumPy的版本来确认安装。

```python
print(np.__version__)
```

![](img/a35a8cd140052c25b68a637ef74e6e63_16.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_17.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_19.png)

## 加载数据

NumPy可以方便地加载数据文件。例如，我们可以加载一个TSV（制表符分隔值）文件。

```python
data = np.loadtxt('data.tsv', delimiter='\t')
print(data)
```

![](img/a35a8cd140052c25b68a637ef74e6e63_21.png)

上述代码会加载文件并打印其内容。接下来，我们将详细解释这些数字的含义。

## 数组索引与切片

![](img/a35a8cd140052c25b68a637ef74e6e63_23.png)

我们主要处理二维数组，即具有行和列的数组。索引从0开始。

以下是如何创建一个NumPy数组并访问其元素。

![](img/a35a8cd140052c25b68a637ef74e6e63_25.png)

```python
data = np.array([[1, 2, 3],
                 [4, 5, 6],
                 [7, 8, 9]])
print(data[0, 0])  # 输出第一行第一列的元素：1
```

要访问多个元素，可以使用切片语法。

以下是选择整行或整列的方法。

```python
# 选择第0行所有列
print(data[0, :])
# 选择所有行第0列
print(data[:, 0])
```

![](img/a35a8cd140052c25b68a637ef74e6e63_27.png)

我们也可以选择连续的部分。

```python
# 选择前两行
print(data[:2, :])
# 选择第二行之后的所有行
print(data[2:, :])
```

![](img/a35a8cd140052c25b68a637ef74e6e63_29.png)

此外，还可以选择非连续的部分。

![](img/a35a8cd140052c25b68a637ef74e6e63_31.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_33.png)

```python
# 选择第0行和第2行
print(data[[0, 2], :])
```

![](img/a35a8cd140052c25b68a637ef74e6e63_35.png)

要获取数组的形状（即维数），可以使用`.shape`属性。

![](img/a35a8cd140052c25b68a637ef74e6e63_37.png)

```python
print(data.shape)  # 输出 (3, 3)
```

![](img/a35a8cd140052c25b68a637ef74e6e63_39.png)

## 向量与数组的区别

![](img/a35a8cd140052c25b68a637ef74e6e63_41.png)

向量是一维数组，而数组可以是多维的。主要区别在于索引方式。

![](img/a35a8cd140052c25b68a637ef74e6e63_43.png)

以下示例展示了如何从数组中提取行向量和列向量。

![](img/a35a8cd140052c25b68a637ef74e6e63_45.png)

```python
x = np.array([[1, 2, 3, 4],
              [5, 6, 7, 8],
              [9, 10, 11, 12],
              [13, 14, 15, 16]])
y = x[0, :]   # 第一行，是一个向量
y1 = x[:, 0]  # 第一列，也是一个向量
print(y)
print(y1)
```

![](img/a35a8cd140052c25b68a637ef74e6e63_46.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_48.png)

向量没有明确的行列概念。为了保留形状信息，可以使用`reshape`函数。

```python
y2 = y.reshape(1, -1)  # 将y重塑为1行N列的数组
print(y2.shape)        # 输出 (1, 4)
```

转置操作对一维向量无效，但对重塑后的二维数组有效。

```python
print(y.T)    # 转置向量，形状不变
print(y2.T)   # 转置二维数组，形状改变
```

![](img/a35a8cd140052c25b68a637ef74e6e63_50.png)

## 有用的NumPy函数

NumPy提供了多种初始化数组的函数。

![](img/a35a8cd140052c25b68a637ef74e6e63_52.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_54.png)

以下是创建特殊矩阵的方法。

```python
# 创建4x4单位矩阵
identity_matrix = np.eye(4)
# 创建3x2的全零矩阵
zeros_matrix = np.zeros((3, 2))
# 创建2x3的全一矩阵
ones_matrix = np.ones((2, 3))
```

![](img/a35a8cd140052c25b68a637ef74e6e63_56.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_57.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_58.png)

我们还可以生成随机数数组。

![](img/a35a8cd140052c25b68a637ef74e6e63_59.png)

```python
# 生成2x2的随机矩阵（默认范围0到1）
random_matrix = np.random.random((2, 2))
# 生成2x2的随机整数矩阵（范围1到10）
random_int_matrix = np.random.randint(1, 10, size=(2, 2))
```

![](img/a35a8cd140052c25b68a637ef74e6e63_61.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_62.png)

## 重塑数组

![](img/a35a8cd140052c25b68a637ef74e6e63_64.png)

`reshape`函数可以改变数组的形状而不改变其数据。

以下是如何重塑一个4x4的矩阵。

![](img/a35a8cd140052c25b68a637ef74e6e63_66.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_67.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_68.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_69.png)

```python
x = np.arange(1, 17).reshape(4, 4)
print(x.shape)  # 输出 (4, 4)

# 重塑为2行8列
x_reshaped = x.reshape(2, 8)
print(x_reshaped)

![](img/a35a8cd140052c25b68a637ef74e6e63_71.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_72.png)

# 重塑为1行，自动计算列数
x_row = x.reshape(1, -1)
print(x_row)

![](img/a35a8cd140052c25b68a637ef74e6e63_74.png)

# 重塑为4行1列
x_column = x.reshape(-1, 1)
print(x_column)
```

![](img/a35a8cd140052c25b68a637ef74e6e63_76.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_78.png)

## 合并数组

我们可以使用`hstack`和`vstack`来水平或垂直合并数组。

![](img/a35a8cd140052c25b68a637ef74e6e63_80.png)

以下是合并两个数组的示例。

![](img/a35a8cd140052c25b68a637ef74e6e63_82.png)

```python
x = np.array([[1, 2],
              [3, 4]])
y = np.array([[5, 6],
              [7, 8]])

# 水平堆叠（增加列）
h_stacked = np.hstack((x, y))
print(h_stacked)

# 垂直堆叠（增加行）
v_stacked = np.vstack((x, y))
print(v_stacked)
```

## 矩阵运算

NumPy支持各种矩阵运算，包括加法、减法、乘法等。

![](img/a35a8cd140052c25b68a637ef74e6e63_84.png)

以下是基本的算术运算。

![](img/a35a8cd140052c25b68a637ef74e6e63_86.png)

```python
x = np.array([[1, 2],
              [3, 4]])
y = np.array([[5, 6],
              [7, 8]])

![](img/a35a8cd140052c25b68a637ef74e6e63_88.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_89.png)

# 加法
print(x + y)
print(np.add(x, y))

# 减法
print(y - x)

![](img/a35a8cd140052c25b68a637ef74e6e63_91.png)

# 乘以常数（广播）
c = 4
print(c * x)
```

矩阵乘法与逐元素乘法不同。

![](img/a35a8cd140052c25b68a637ef74e6e63_93.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_94.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_95.png)

```python
# 矩阵乘法
print(np.dot(x, y))
print(x @ y)

![](img/a35a8cd140052c25b68a637ef74e6e63_96.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_98.png)

# 逐元素乘法
print(x * y)
```

## 数学函数

![](img/a35a8cd140052c25b68a637ef74e6e63_100.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_102.png)

NumPy提供了常见的数学函数，这些函数会逐元素应用于数组。

以下是指数和对数运算的示例。

![](img/a35a8cd140052c25b68a637ef74e6e63_104.png)

```python
x = np.array([[1, 2],
              [3, 4]])

# 指数运算
print(np.exp(x))

![](img/a35a8cd140052c25b68a637ef74e6e63_106.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_107.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_109.png)

# 对数运算
print(np.log(x))
```

![](img/a35a8cd140052c25b68a637ef74e6e63_111.png)

## 聚合函数

聚合函数用于计算数组的统计信息，如最大值、最小值、求和等。

![](img/a35a8cd140052c25b68a637ef74e6e63_113.png)

以下是查找最大值和最小值的方法。

![](img/a35a8cd140052c25b68a637ef74e6e63_114.png)

```python
y_wide = np.hstack((x, y))
print(y_wide)

![](img/a35a8cd140052c25b68a637ef74e6e63_116.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_118.png)

# 第一行的最大值及其索引
first_row = y_wide[0, :]
print(np.max(first_row))        # 最大值
print(np.argmax(first_row))     # 最大值索引

![](img/a35a8cd140052c25b68a637ef74e6e63_120.png)

# 第二列的最小值及其索引
second_col = y_wide[:, 1]
print(np.min(second_col))       # 最小值
print(np.argmin(second_col))    # 最小值索引
```

![](img/a35a8cd140052c25b68a637ef74e6e63_122.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_124.png)

我们还可以比较两个数组的元素。

![](img/a35a8cd140052c25b68a637ef74e6e63_125.png)

```python
a = np.array([1, 3, 5])
b = np.array([2, 4, 3])

# 逐元素比较最大值
print(np.maximum(a, b))
# 逐元素比较最小值
print(np.minimum(a, b))
```

![](img/a35a8cd140052c25b68a637ef74e6e63_127.png)

## 求和

![](img/a35a8cd140052c25b68a637ef74e6e63_129.png)

`sum`函数可以沿指定轴求和。

![](img/a35a8cd140052c25b68a637ef74e6e63_131.png)

以下是沿不同轴求和的示例。

![](img/a35a8cd140052c25b68a637ef74e6e63_133.png)

```python
arr = np.array([[1, 2],
                [3, 4],
                [5, 6]])

![](img/a35a8cd140052c25b68a637ef74e6e63_135.png)

# 沿轴0求和（按列求和）
print(np.sum(arr, axis=0))  # 输出 [9, 12]

# 沿轴1求和（按行求和）
print(np.sum(arr, axis=1))  # 输出 [3, 7, 11]

# 所有元素求和
print(np.sum(arr))          # 输出 21
```

## 总结

![](img/a35a8cd140052c25b68a637ef74e6e63_137.png)

![](img/a35a8cd140052c25b68a637ef74e6e63_139.png)

在本教程中，我们一起学习了NumPy的基础知识。我们介绍了如何安装和导入NumPy，如何创建和操作数组，包括索引、切片、重塑和合并。我们还探讨了NumPy提供的各种数学运算和聚合函数，如加法、乘法、求和、求最大值和最小值等。掌握NumPy是进行机器学习中线性代数运算的重要一步。