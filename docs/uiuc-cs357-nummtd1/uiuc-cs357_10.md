# 稀疏矩阵

> [`cs357.cs.illinois.edu/textbook/notes/sparse.html`](https://cs357.cs.illinois.edu/textbook/notes/sparse.html)

## 稠密矩阵

稠密矩阵存储所有值，包括零。因此，一个 $m \times n$ 的矩阵必须存储 $O(m \times n)$ 个项。例如：

$$A = \begin{bmatrix} 1.0 & 0 & 0 \\ 3.0 & 4.0 & 0 \\ 6.0 & 0 & 7.0 \\ 0 & 0 & 10.0 \end{bmatrix}.$$

为了存储矩阵，所有组件通常以行主序保存。对于上面给出的 $\mathbf{A}$，我们会存储：

$$A_{dense} = \begin{bmatrix} 1.0 & 0 & 0 & 3.0 & 4.0 & 0 & 6.0 & 0 & 7.0 & 0 & 0 & 10.0 \end{bmatrix}.$$

矩阵的维度是单独存储的：

$$A_{shape} = \$n_{row}, n_{col})\\ = \$4, 3)\\.$$

## 稀疏矩阵

一些类型的矩阵包含太多的零，存储所有这些零项是浪费的。稀疏矩阵是一种非零项很少的矩阵。

一个 $m \times n$ 的矩阵如果它有 $O(min(m, n))$ 个非零项，则称为稀疏矩阵。

## 目标

稀疏矩阵旨在以高效的方式存储大型矩阵，而不存储许多零，这允许进行更经济的计算。它还节省了存储空间，这可以减少系统上的内存开销。

添加两个稠密矩阵 $\mathbf{P}$ 和 $\mathbf{Q}$ 所需的操作数是 $O(n(\mathbf{P}) + n(\mathbf{Q}))$，其中 $(n(\mathbf{X}))$ 是 $\mathbf{X}$ 中的元素数量。

添加两个稀疏矩阵 $\mathbf{P}$ 和 $\mathbf{Q}$ 所需的操作数是 $O(nnz(\mathbf{P}) + nnz(\mathbf{Q}))$，其中 $(nnz(\mathbf{X}))$ 是 $\mathbf{X}$ 中非零元素的数量。

## 存储解决方案

存储稀疏矩阵的方法有很多，如坐标（COO）、压缩稀疏行（CSR）、块稀疏行（BSR）、键字典（DOK）等。

我们将重点关注坐标和压缩稀疏行。

让我们探索存储以下示例的方法：

$$\mathbf{A}= \begin{bmatrix} 1.0 & 0 & 0 & 2.0 & 0 \\ 3.0 & 4.0 & 0 & 5.0 & 0 \\ 6.0 & 0 & 7.0 & 8.0 & 9.0 \\ 0 & 0 & 10.0 & 11.0 & 0 \\ 0 & 0 & 0 & 0 & 12.0 \end{bmatrix}.$$

### 坐标格式（COO）

COO 存储行索引、列索引和相应的非零数据值的数组，顺序可以是任意的。这种格式提供了快速构建稀疏矩阵和转换为不同稀疏格式的方法。对于 ${\bf A}$ 的 COO 格式是：

$$\textrm{data} = \begin{bmatrix} 12.0 & 9.0 & 7.0 & 5.0 & 1.0 & 2.0 & 11.0 & 3.0 & 6.0 & 4.0 & 8.0 & 10.0\end{bmatrix}$$ $$\textrm{row} = \begin{bmatrix} 4 & 2 & 2 & 1 & 0 & 0 & 3 & 1 & 2 & 1 & 2 & 3 \end{bmatrix}$$ $$\textrm{col} = \begin{bmatrix} 4 & 4 & 2 & 3 & 0 & 3 & 3 & 0 & 0 & 1 & 3 & 2 \end{bmatrix}$$

$\textrm{row}$ 和 $\textrm{col}$ 是 $nnz$ 个整数的数组。

$\textrm{data}$ 是原始矩阵数据类型的 $nnz$ 数组，在这种情况下是双精度浮点数。

如何解释：$\textrm{data}$，$\textrm{row}$，$\textrm{col}$ 的前几个条目分别是 12.0，4，4，这意味着矩阵的位置 (4, 4) 处有 12.0；第二个条目是 9.0，2，4，所以 (2, 4) 处有 9.0。

COO 矩阵存储 $3 \times nnz$ 个元素。这种方法可以排序，因为行、列和数据数组中的每个索引描述的是相同的元素。

在 Python 中，可以使用 `scipy.sparse` 库将此矩阵转换为 COO 格式。

```py
import scipy.sparse as sparse

A = [[1.,  0.,  0.,  2.,  0.],
 [ 3.,  4.,  0.,  5.,  0.],
 [ 6.,  0.,  7.,  8.,  9.],
 [ 0.,  0., 10., 11.,  0.],
 [ 0.,  0.,  0.,  0., 12.]]

COO = sparse.coo_matrix(A)
data = COO.data
row = COO.row
col = COO.col 
```

您也可以使用 `scipy.sparse` 库在 Python 中将 COO 格式的稀疏矩阵重新创建为稠密或 CSR 矩阵。

```py
import scipy.sparse as sparse

data   = [12.0, 9.0, 7.0, 5.0, 1.0, 2.0, 11.0, 3.0, 6.0, 4.0, 8.0, 10.0]
row    = [4, 2, 2, 1, 0, 0, 3, 1, 2, 1, 2, 3]
col    = [4, 4, 2, 3, 0, 3, 3, 0, 0, 1, 3, 2]

COO = sparse.coo_matrix((data, (row, col)))

A = COO.todense()
CSR = COO.tocsr() 
```

### 压缩稀疏行 (CSR)

CSR，也常称为耶鲁格式，编码行偏移、列索引和相应的非零数据值。行偏移由以下递归关系定义（从 $\textrm{rowptr}[0] = 0$ 开始）：

$$ \textrm{rowptr}[j] = \textrm{rowptr}[j-1] + \mathrm{nnz}(\textrm{row}_{j-1}), \\ $$

其中 $\mathrm{nnz}(\textrm{row}_k)$ 是第 $k$ 行中非零元素的数量。注意，$\textrm{rowptr}$ 的长度是 $n_{rows} + 1$，其中 $\textrm{rowptr}$ 的最后一个元素是 $A$ 中的非零元素数量。对于 CSR 格式的 ${\bf A}$：

$$\textrm{data} = \begin{bmatrix} 1.0 & 2.0 & 3.0 & 4.0 & 5.0 & 6.0 & 7.0 & 8.0 & 9.0 & 10.0 & 11.0 & 12.0 \end{bmatrix}$$ $$\textrm{col} = \begin{bmatrix} 0 & 3 & 0 & 1 & 3 & 0 & 2 & 3 & 4 & 2 & 3 & 4\end{bmatrix}$$ $$\textrm{rowptr} = \begin{bmatrix} 0 & 2 & 5 & 9 & 11 & 12 \end{bmatrix}$$

$\textrm{rowptr}$ 包含行偏移（$m + 1$ 个整数的数组）。

$\textrm{col}$ 包含列索引（$nnz$ 个整数的数组）。

$\textrm{data}$ 包含非零元素（$nnz$ 个数据值类型的数组，在这种情况下是双精度浮点数）。

如何解释：$\textrm{rowptr}$ 的前两个条目给出了第一行的元素。$\textrm{data}$ 和 $\textrm{col}$ 的区间 [0, 2) 对应两个 (data, column) 对：$ (1.0, 0) $ 和 $ (2.0, 3) $，意味着第一行在列 0 处有 1.0，在列 3 处有 2.0。$\textrm{rowptr}$ 的第二个和第三个条目告诉我们 $\textrm{data}$ 和 $\textrm{col}$ 的 [2, 5) 区间对应第二行。三个对 $(3.0, 0)$，$(4.0, 1)$，$(5.0, 3)$ 意味着在第二行中，列 0 处有 3.0，列 1 处有 4.0，列 3 处有 5.0。

CSR 矩阵存储 $2 \times nnz + m + 1$ 个元素。它还提供了在稀疏矩阵之间进行快速算术运算和快速矩阵向量积的功能。

在 Python 中，可以使用 `scipy.sparse` 库将此矩阵转换为 CSR 格式。

```py
import scipy.sparse as sparse

A = [[1.,  0.,  0.,  2.,  0.],
 [ 3.,  4.,  0.,  5.,  0.],
 [ 6.,  0.,  7.,  8.,  9.],
 [ 0.,  0., 10., 11.,  0.],
 [ 0.,  0.,  0.,  0., 12.]]

CSR = sparse.csr_matrix(A)
data = CSR.data
col = CSR.indices
rowptr = CSR.indptr 
```

您也可以使用 `scipy.sparse` 库在 Python 中将 CSR 格式的稀疏矩阵重新创建为稠密或 COO 矩阵。

```py
data   = [ 1.,  2.,  3.,  4.,  5.,  6.,  7.,  8.,  9., 10., 11., 12.]
col    = [ 0, 3, 0, 1, 3, 0, 2, 3, 4, 2, 3, 4]
rowptr = [ 0,  2, 5,  9, 11, 12]

CSR = sparse.csr_matrix((data, col, rowptr))

A = CSR.todense()
COO = CSR.tocoo() 
```

## CSR 矩阵向量积算法

以下代码片段执行方阵的 CSR 矩阵向量积：

```py
import numpy as np
def csr_mat_vec(A, x):
  Ax = np.zeros_like(x)
  for i in range(x.shape[0]):
    for k in range(A.rowptr[i], A.rowptr[i+1]):
      Ax[i] += A.data[k]*x[A.col[k]]
  return Ax 
```

## 复习问题

1.  矩阵稀疏是什么意思？

1.  在决定如何存储稀疏矩阵时，您可能考虑哪些因素？（为什么您会选择一种格式而不是另一种格式来存储矩阵？）

1.  给定一个稀疏矩阵，将其转换为 CSR 格式。

1.  给定一个稀疏矩阵，将其转换为 COO 格式。

1.  对于一个给定的矩阵，存储它需要多少字节的 CSR 格式？

1.  对于一个给定的矩阵，存储它需要多少字节的 COO 格式？

## 更新日志

+   2025 年 10 月 28 日：Dev Singh (dsingh14) — 修复了密集矩阵示例

+   2024 年 10 月 31 日：Kaiyao Ke (kaiyaok2) — 修复了小错误

+   2024 年 2 月 14 日：Kriti Chandak (kritic3) — 添加了幻灯片信息和额外的示例

+   

查看剩余条目



    +   2022 年 3 月 6 日：Victor Zhao (chenyan4) — 添加了如何解释 COO 和 CSR 的说明

    +   2020 年 3 月 1 日：Peter Sentz (sentz2) — 从之前的参考页面中提取了材料

## 作者

+   CS 357 课程工作人员
