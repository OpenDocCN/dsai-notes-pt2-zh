# 5：线性代数与 Jupyter 🧮

在本节课中，我们将学习如何在 Jupyter 笔记本中使用 MXNet 框架进行基础的线性代数操作。我们将从导入库开始，逐步学习如何创建和操作标量、向量、矩阵和张量，并执行加法、乘法、点积、矩阵乘法以及范数计算等核心运算。

![](img/ce93a9193d70af295add1121059b1a42_1.png)

---

## 导入库与创建数组

首先，我们需要导入 MXNet 的数组模块。这是进行所有后续操作的基础。

```python
from mxnet import nd
```

![](img/ce93a9193d70af295add1121059b1a42_3.png)

导入完成后，我们可以创建最基本的数组，即标量。

```python
x = nd.array([3])
y = nd.array([2])
```

我们可以对这些标量执行基本的算术运算。

```python
print(x - y)  # 输出: [1.]
```

运算结果符合预期。我们可以将数组转换回 Python 的标量类型，以便在纯 Python 环境中使用。

![](img/ce93a9193d70af295add1121059b1a42_5.png)

```python
x_asscalar = x.asscalar()
```

**注意**：频繁地在深度学习框架和 Python 原生环境之间转换数据可能导致性能下降，尤其是在循环中，应尽量避免。

---

![](img/ce93a9193d70af295add1121059b1a42_7.png)

## 向量操作

向量是一维的标量序列。我们可以使用 `arange` 函数方便地创建向量。

```python
x = nd.arange(5)  # 创建向量 [0., 1., 2., 3., 4.]
```

![](img/ce93a9193d70af295add1121059b1a42_9.png)

我们可以通过索引访问向量的特定元素。

```python
print(x[3])  # 输出: 3.
```

查看向量的形状和维度是常见的操作。

![](img/ce93a9193d70af295add1121059b1a42_11.png)

![](img/ce93a9193d70af295add1121059b1a42_13.png)

```python
print(x.shape)  # 输出: (5,)
```

向量之间可以进行逐元素运算。

![](img/ce93a9193d70af295add1121059b1a42_15.png)

```python
a = nd.array([1, 2, 3])
b = nd.array([10, 20, 30])
print(a + b)  # 输出: [11., 22., 33.]
print(a * b)  # 输出: [10., 40., 90.]
```

---

![](img/ce93a9193d70af295add1121059b1a42_17.png)

## 矩阵与张量

矩阵是二维数组。我们可以通过重塑（reshape）一个向量来创建矩阵。

```python
x = nd.arange(20)
X = x.reshape((2, 10))  # 创建一个 2行10列 的矩阵
print(X.shape)  # 输出: (2, 10)
```

![](img/ce93a9193d70af295add1121059b1a42_19.png)

我们可以获取矩阵的转置。

```python
print(X.T)  # 输出转置后的矩阵，形状为 (10, 2)
```

张量是更高维度的数组。例如，一个三维张量可以表示图像数据（高度、宽度、颜色通道）。

![](img/ce93a9193d70af295add1121059b1a42_21.png)

```python
Y = nd.arange(24).reshape((2, 3, 4))  # 创建一个 2x3x4 的三维张量
print(Y.shape)  # 输出: (2, 3, 4)
```

我们可以用相同的方式对矩阵和张量进行运算。

![](img/ce93a9193d70af295add1121059b1a42_23.png)

```python
A = nd.ones(shape=(2, 3))
print(A * 2)  # 每个元素乘以2
```

---

![](img/ce93a9193d70af295add1121059b1a42_25.png)

## 求和与均值

![](img/ce93a9193d70af295add1121059b1a42_27.png)

我们可以计算数组中所有元素的总和或均值。

```python
x = nd.ones(shape=(3,))
print(nd.sum(x))  # 输出: 3.
```

![](img/ce93a9193d70af295add1121059b1a42_29.png)

对于多维数组，我们可以指定沿某个轴（维度）进行求和。

```python
X = nd.ones(shape=(2, 3))
print(nd.sum(X, axis=0))  # 沿行（维度0）求和，输出形状 (3,)
print(nd.sum(X, axis=1))  # 沿列（维度1）求和，输出形状 (2,)
```

![](img/ce93a9193d70af295add1121059b1a42_31.png)

计算均值是类似的，它本质上是总和除以元素数量。

![](img/ce93a9193d70af295add1121059b1a42_33.png)

```python
print(nd.mean(X))  # 计算整个矩阵的均值
```

![](img/ce93a9193d70af295add1121059b1a42_35.png)

---

![](img/ce93a9193d70af295add1121059b1a42_37.png)

## 点积与矩阵乘法

![](img/ce93a9193d70af295add1121059b1a42_39.png)

点积（内积）是两个向量对应元素相乘后求和。

```python
x = nd.arange(4)
y = nd.ones(4)
dot_product = nd.dot(x, y)
print(dot_product)  # 输出: 6.
# 等价于 print(nd.sum(x * y))
```

矩阵与向量的乘法是线性代数中的核心操作。

```python
A = nd.ones(shape=(3, 4))
x = nd.arange(4)
# 正确的矩阵-向量乘法
matrix_vector_product = nd.dot(A, x)
print(matrix_vector_product)
```

**重要提示**：在 MXNet/NumPy 中，`A * x` 执行的是**广播机制下的逐元素乘法**，而非矩阵乘法。这与 MATLAB 的约定不同，是常见的错误来源。

矩阵乘法遵循标准的数学定义。

![](img/ce93a9193d70af295add1121059b1a42_41.png)

```python
A = nd.ones(shape=(3, 4))
B = nd.ones(shape=(4, 3))
matrix_product = nd.dot(A, B)  # 结果是一个 3x3 的矩阵
print(matrix_product.shape)  # 输出: (3, 3)
```

![](img/ce93a9193d70af295add1121059b1a42_43.png)

---

![](img/ce93a9193d70af295add1121059b1a42_45.png)

## 范数计算

范数用于衡量向量或矩阵的“大小”。L2范数（欧几里得范数）是最常用的。

![](img/ce93a9193d70af295add1121059b1a42_47.png)

```python
x = nd.arange(4)
l2_norm = nd.norm(x)
print(l2_norm)  # 计算 x 的 L2 范数
```

![](img/ce93a9193d70af295add1121059b1a42_49.png)

我们也可以计算 L1 范数（所有元素绝对值之和）。

```python
l1_norm = nd.sum(nd.abs(x))
print(l1_norm)
# 或者使用 norm 函数并指定阶数
l1_norm_alt = nd.norm(x, ord=1)
```

---

## 总结

![](img/ce93a9193d70af295add1121059b1a42_51.png)

本节课中，我们一起学习了在 MXNet 中执行线性代数操作的基础知识。我们从导入库和创建数组开始，逐步探索了向量、矩阵和张量的创建与基本运算，包括索引、形状变换、转置、求和、均值计算。接着，我们深入讲解了核心的线性代数操作：点积、矩阵-向量乘法以及矩阵乘法，并特别指出了广播机制与 MATLAB 的区别。最后，我们介绍了如何计算向量的 L1 和 L2 范数。掌握这些操作是进行更复杂机器学习和深度学习模型构建的重要基石。