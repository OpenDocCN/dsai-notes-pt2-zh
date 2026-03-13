# 最小二乘拟合

> 原文：[`cs357.cs.illinois.edu/textbook/notes/linear-least-squares.html`](https://cs357.cs.illinois.edu/textbook/notes/linear-least-squares.html)

## 学习目标

+   从一组数据中建立一个线性最小二乘问题

+   使用奇异值分解来解决最小二乘问题

+   量化最小二乘问题中的误差

## 基于一组数据的线性回归

给定 $m$ 个数据点（其中 $m>2$），$\{(t_1,y_1),(t_2,y_2),\dots,(t_m,y_m)\}$，我们想要找到一条最佳拟合这些数据点的直线。从数学上讲，我们正在寻找 $x_0$ 和 $x_1$，使得

$$ y_i = x_0 + x_1\,t_i , \quad \forall i \in [1,m]. $$

以矩阵形式，得到的线性系统为：

$$ \begin{bmatrix} 1 & t_1 \\ 1& t_2 \\ \vdots & \vdots\\ 1& t_m \end{bmatrix} \begin{bmatrix} x_0\\ x_1 \end{bmatrix} = \begin{bmatrix} y_1\\ y_2\\ \vdots\\ y_m \end{bmatrix} $$$${\bf A x} = {\bf b}$$

其中 ${\bf A}$ 是一个 $m\times n$ 矩阵，${\bf x}$ 是一个 $n\times 1$ 矩阵，${\bf b}$ 是一个 $m\times 1$ 矩阵。

理想情况下，我们想要找到 ${\bf A}$ 的列的适当线性组合，以构成向量 ${\bf b}$。如果存在一个满足 ${\bf A x} = {\bf b}$ 的解，那么 ${\bf b} \in range({\bf A})$。

然而，在这个线性方程组系统中，我们拥有的方程比未知数多，通常上述问题没有精确的解。

当 $ m>n$ 时，我们称这个线性系统为 ***超定*** 的，并且 ${\bf A x} = {\bf b}$ 的等式通常不能精确满足，因为 ${\bf b}$ 可能不在 ${\bf A}$ 的列空间中。

因此，超定系统最好写成

$${\bf A x} \cong {\bf b}$$

## 线性最小二乘问题

对于一个超定系统 ${\bf A x}\cong {\bf b}$，我们通常寻找一个解 ${\bf x}$，使得残差向量 ${\bf r} = {\bf b} - {\bf A} {\bf x}$ 的欧几里得范数最小，

$$\min_{ {\bf x} } \|{\bf r}\|_2² = \min_{ {\bf x} } \|{\bf b} - {\bf A} {\bf x}\|_2².$$

这个问题 $A {\bf x} \cong {\bf b}$ 被称为 ***线性最小二乘问题***，其解 ${\bf x}$ 被称为 ***最小二乘解***。 ${\bf A}$ 是一个 ${m \times n}$ 矩阵，其中 ${m \ge n}$，${m}$ 是数据对点数，${n}$ 是“最佳拟合”函数的参数数。线性最小二乘问题 $A {\bf x} \cong {\bf b}$ ***总是*** 有解。当且仅当 ${rank({\bf A})= n}$ 时，这个解是唯一的。

## 正则方程

考虑最小二乘问题 ${\bf A} {\bf x} \cong {\bf b}$，其中 ${\bf A} $ 是 $m \times n$ 的实矩阵（$m > n$）。如上所述，最小二乘解最小化了残差的平方 2-范数。因此，我们想要找到使以下函数最小的 $\mathbf{x}$：

$$\phi(\mathbf{x}) = \|\mathbf{r}\|_2² = (\mathbf{b} - {\bf A} \mathbf{x})^T (\mathbf{b} - {\bf A} \mathbf{x}) = \mathbf{b}^T \mathbf{b} - 2\mathbf{x}^T {\bf A} ^T \mathbf{b} + \mathbf{x}^T {\bf A} ^T {\bf A} \mathbf{x}.$$

为了解决这个无约束最小化问题，我们需要满足一阶必要条件以获得驻点：

$$\nabla \phi(\mathbf{x}) = 0 \Rightarrow -2 {\bf A} ^T \mathbf{b} + 2 {\bf A} ^T {\bf A} \mathbf{x} = 0.$$

得到的平方（$n \times n$）线性系统

$${\bf A} ^T {\bf A} \mathbf{x} = {\bf A} ^T \mathbf{b}$$

被称为**正则方程组**。如果矩阵 ${\bf A}$ 是满秩的，则最小二乘解是唯一的，并且由以下给出：

$${\bf x} = ({\bf A} ^T {\bf A})^{-1} {\bf A} ^T \mathbf{b}$$

我们可以通过评估 $\phi$ 的 Hessian 来查看最小化问题的二阶充分条件：

$${\bf H} = 2 {\bf A} ^T {\bf A}$$

由于 Hessian 矩阵是对称和正定的，我们确认最小二乘解 ${\bf x}$ 确实是一个最小值点。

尽管对于满秩矩阵，可以通过正则方程解决最小二乘问题，但解往往会恶化问题的条件。具体来说，

$$\text{cond}({\bf A}^T {\bf A}) = (\text{cond}({\bf A}))².$$

由于这个原因，使用正则方程来找到最小二乘解通常不是一个好的选择（尽管实现起来很简单）。

解决线性最小二乘的另一种方法是找到 ${\bf y} = {\bf A} {\bf x}$，它是最接近向量 ${\bf b}$ 的。当残差 ${\bf r} = {\bf b} - {\bf y} = {\bf b} - {\bf A} {\bf x}$ 与 ${\bf A}$ 的所有列正交时，则 ${\bf y}$ 是最接近 ${\bf b}$ 的。

$${\bf A}^T{\bf r} = {\bf A^T}\left({\bf b} - {\bf A} {\bf x}\right) = 0 \implies {\bf A} ^T {\bf A} {\bf x} = {\bf A}^T {\bf b}$$

## 数据拟合与插值

重要的是要理解，插值和最小二乘数据拟合，尽管在某些方面相似，但它们的目的是根本不同的。在这两个问题中，我们都有一个数据点集 $(t_i, y_i)$，$i=1,\ldots,m$，并且我们试图确定基函数线性组合的系数。

通过插值，我们寻找基函数的线性组合，使得所得函数能够**精确地**通过每个数据点。因此，对于 $m$ 个独特的数据点，我们需要 $m$ 个线性无关的基函数（并且由此产生的线性系统将是方阵且满秩，因此它将有一个精确的解）。

相反，然而，在最小二乘数据拟合中，我们有一些模型，我们试图找到最佳拟合数据点的模型参数。例如，在线性最小二乘中，我们可能有 300 个有噪声的数据点，我们希望将其建模为二次函数。因此，我们试图将我们的数据表示为

$$y = x_0 + x_1 t + x_2 t²$$

其中 $x_0, x_1,$ 和 $x_2$ 是我们想要确定的未知数（基函数的系数）。由于数据点比参数多得多，我们并不期望函数会精确地通过数据点。对于这个例子，在有噪声的数据点上，我们不希望函数精确地通过数据点，因为我们正在试图模拟一般趋势而不是捕捉噪声。

## 计算复杂度

由于正则方程组产生一个平方对称矩阵，最小二乘解可以使用如 Cholesky 分解等有效方法来计算。请注意，分解的整体计算复杂度是 $\mathcal{O}(n³)$。然而，矩阵 ${\bf A} ^T {\bf A}$ 的构建复杂度是 $\mathcal{O}(mn²)$。

在典型的数据拟合问题中，$m >> n$，因此正则方程法的时间复杂度总体上是 ${\bf \mathcal{O}(mn²)}$.

## 使用奇异值分解（SVD）求解最小二乘问题

解决最小二乘问题 ${\bf A} {\bf x} \cong {\bf b}$（其中我们寻找 ${\bf x}$ 以最小化 $\|{\bf b} - {\bf A} {\bf x}\|_2²$）的另一种方法是使用 ${\bf A}$ 的奇异值分解（SVD）。

$${\bf A} = {\bf U \Sigma V}^T$$

其中残差的平方范数变为：

$$ \begin{align} \|{\bf b} - {\bf A} {\bf x}\|_2² &= \|{\bf b} - {\bf U \Sigma V}^T {\bf x}\|_2² & (1)\\ &= \|{\bf U}^T ({\bf b} - {\bf U \Sigma V}^T {\bf x})\|_2² & (2)\\ &= \|{\bf U}^T {\bf b} - {\bf \Sigma V}^T {\bf x}\|_2² \end{align} $$

我们可以从（1）到（2）进行转换，因为乘以一个正交矩阵不会改变向量的 2-范数。现在，让

$$ {\bf y} = {\bf V}^T {\bf x} $$$$ {\bf z} = {\bf U}^T {\bf b}, $$

我们现在正在寻找 ${\bf y}$ 以最小化

$$ \|{\bf z} - \Sigma {\bf y}\|_2²\. $$

注意到

$$ \Sigma {\bf y} = \begin{bmatrix} \sigma_1 y_1\\ \sigma_2 y_2\\ \vdots \\ \sigma_n y_n \end{bmatrix},(\sigma_i = \Sigma_{i,i}) $$

因此我们选择

$$ y_i = \begin{cases} \frac{z_i}{\sigma_i} & \sigma_i \neq 0\\ 0 & \sigma_i = 0 \end{cases} $$

这将最小化 $\|{\bf z} - {\bf \Sigma} {\bf y}\|_2²$. 最后，我们计算

$${\bf x} = {\bf V} {\bf y}$$

为了找到 ${\bf x}$。最小二乘解的表达式是

$${\bf x} = \sum_{\sigma_i \neq 0} \frac{ {\bf u}_i^T {\bf b} }{\sigma_i} {\bf v}_i$$

其中 ${\bf u}_i$ 表示 ${\bf U}$ 的第 $i$ 列，${\bf v}_i$ 表示 ${\bf V}$ 的第 $i$ 列。

在闭式表达中，我们可以将最小二乘解表示为：

$${\bf x} = {\bf V\Sigma}^{+}{\bf U}^T{\bf b}$$

其中 ${\bf \Sigma}^{+}$ 是通过取非零对角元素的倒数，保留零，并转置结果矩阵计算出的奇异矩阵的伪逆。例如：

$$\Sigma = \begin{bmatrix} \sigma_1 & & &\\ & \ddots & & \\& & \sigma_r &\\ & & & 0\\ 0 & ... & ... & 0 \\ \vdots & \ddots & \ddots & \vdots \\ 0 & ... & ... & 0 \end{bmatrix} \quad \implies \quad \Sigma^{+} = \begin{bmatrix} \frac{1}{\sigma_1} & & & & 0 & \dots & 0 \\ & \ddots & & & & \ddots &\\ & & \frac{1}{\sigma_r} & & 0 & \dots & 0 \\ & & & 0 & 0 & \dots & 0 \end{bmatrix}.$$

或者以简化的形式：

$${\bf x} = {\bf V\Sigma}_R^{+}{\bf U}_R^T{\bf b}$$

## 使用简化 SVD 的计算复杂度

使用**给定**的简化 SVD 求解最小二乘问题的时间复杂度为 $\mathcal{O}(mn)$。

假设我们事先知道 $\bf A$ 的简化奇异值分解（这意味着我们事先知道 $\bf V, \Sigma^{+}_{R}, U^{T}_{R}$ 的元素）。

然后，使用 $n \times m$ 矩阵 $\bf U^{T}_{R}$ 和 $m \times 1$ 向量 $\bf b$ 求解 $\bf z = U^{T}_{R}b$ 的复杂度为 $\mathcal{O}(mn)$。

使用 $n \times n$ 矩阵 $\bf \Sigma^{+}_{R}$ 和 $n \times 1$ 向量 $\bf z$ 求解 $\bf y = \Sigma^{+}_{R}z$ 的复杂度为 $\mathcal{O}(n)$，因为 $\bf \Sigma^{+}_{R}$ 是一个对角矩阵。

使用 $n \times n$ 矩阵 $\bf V$ 和 $n \times 1$ 向量 $\bf y$ 求解 $\bf x = Vy$ 的复杂度为 $\mathcal{O}(n²)$。

因此，时间复杂度为 $\mathcal{O}(n² + n + mn) = \mathcal{O}(mn)$，因为 $m > n$。我们只有在事先知道 $\bf A$ 的简化奇异值分解的情况下才能实现这一点。

## 使用 SVD 确定最小二乘问题中的残差

我们已经展示了如何使用 SVD 来找到最小二乘问题的最小二乘解（即最小化残差平方 2-范数的解）${\bf A} {\bf x} \cong {\bf b}$。我们还可以使用 SVD 来确定残差值的最小二乘解的精确表达式。

假设在 ${\bf A}$ 的奇异值分解中，${\bf A} = {\bf U \Sigma V}^T$，${\bf \Sigma}$ 的对角线元素按降序排列（$\sigma_1 \ge \sigma_2 \ge \dots $），并且 ${\bf \Sigma}$ 的前 $r$ 个对角线元素非零，其余为零，那么

$$\begin{align} \|{\bf b} - A {\bf x}\|_2² &= \|{\bf z} - \Sigma {\bf y}\|_2²\\ &= \sum_{i=1}^n (z_i - \sigma_i y_i)²\\ &= \sum_{i=1}^r (z_i - \sigma_i \frac{z_i}{\sigma_i})² + \sum_{i=r+1}^n (z_i - 0)²\\ &= \sum_{i=r+1}^n z_i² \end{align}$$

回想一下

$$ {\bf z} = {\bf U}^T {\bf b}, $$

我们得到

$$ \|{\bf b} - {\bf A} {\bf x}\|_2² = \sum_{i=r+1}^n ({\bf u}_i^T {\bf b})² $$

${\bf u}_i$ 表示 ${\bf U}$ 的第 $i$ 列。

（更多正式的证明请查看[这个视频](https://mediaspace.illinois.edu/media/t/1_w6u83js8/158464041)）

### 使用 SVD 求解最小二乘解的示例

假设我们有 $3$ 个数据点，${(t_i,y_i)}={(1,1.2),(2,1.9),(3,1)}$，我们想要找到最佳拟合这些数据点的直线，${y = x_0 + x_1 t}$ 的系数。使用 SVD 求解这个最小二乘问题的代码如下：

```py
import numpy as np
import numpy.linalg as la

A = np.array([[1,1],[2,1],[3,1]])
b = np.array([1.2,1.9,1])
U, s, V = la.svd(A)
V = V.T
y = np.zeros(len(A[0]))
z = np.dot(U.T,b)
k = 0
threshold = 0.01
# matrix multiplying A by pseudo-inverse of sigma while k < len(A[0]) and s[k] > threshold:
  y[k] = z[k]/s[k]
  k += 1

x = np.dot(V,y)
print("The function of the best line is: y = " + str(x[0]) + "x + " + str(x[1])) 
```

## 非线性最小二乘问题与线性最小二乘问题比较

上述线性最小二乘问题与一个超定线性系统 $A {\bf x} \cong {\bf b}$ 相关联。这个问题被称为“线性”，因为我们正在寻找的拟合函数在 ${\bf x}$ 的分量上是线性的。例如，如果我们正在寻找一个多项式拟合函数

$$ f(t,{\bf x}) = x_1 + x_2t + x_3t² + \dotsb + x_nt^{n-1} $$

来拟合数据点 ${(t_i,y_i), i = 1, …, m}$（其中 $m > n$），这个问题可以使用线性最小二乘法来解决，因为 $f(t,{\bf x})$ 在 ${\bf x}$ 的分量上是线性的（尽管 $f(t,{\bf x})$ 在 $t$ 上是非线性的）。

如果数据点 $(t_i,y_i), i = 1, ..., m$ 的拟合函数 $f(t,{\bf x})$ 在 ${\bf x}$ 的分量上是非线性的，那么这个问题就是一个非线性最小二乘问题。例如，拟合指数和

$$ f(t,{\bf x}) = x_1 e^{x_2 t} + x_2 e^{x_3 t} + \dotsb + x_{n-1} e^{x_n t} $$

是一个***非线性最小二乘问题***。

线性最小二乘问题有闭式解，而非线性最小二乘问题没有闭式解，需要使用数值方法来求解。

## 复习问题

1.  最小二乘解最小化什么值？

1.  对于给定的模型和给定的数据点，你能形成最小二乘问题 ${\bf A x} \cong {\bf b}$ 的系统吗？

1.  对于一个小问题，给定一些数据点和模型，你能确定最小二乘解吗？

1.  通常，我们可以对最小二乘解的残差值说些什么？

1.  最小二乘数据拟合和插值之间有什么区别？

1.  给定矩阵 ${\bf A}$ 的奇异值分解（SVD），我们如何使用 SVD 来计算最小二乘解的残差？

1.  给定矩阵 ${\bf A}$ 的奇异值分解（SVD），我们如何使用 SVD 来计算最小二乘解？对于一个小问题，能够做到这一点。

1.  给定一个矩阵 ${\bf A}$ 的已计算奇异值分解（SVD），使用 SVD 求解最小二乘问题的成本是多少？

1.  为什么你会使用奇异值分解（SVD）而不是正则方程来找到 ${\bf A x} \cong {\bf b}$ 的解？

1.  通过正则方程求解最小二乘问题或使用奇异值分解（SVD）求解最小二乘问题哪个成本更低？

1.  线性最小二乘问题和非线性最小二乘问题有什么区别？什么类型的模型使其成为非线性问题？对于数据点 ${\left(t_i, y_i\right)}$，如果我们尝试拟合 ${y = a*cos(t) + b}$（其中 ${a}$ 和 ${b}$ 是我们试图确定的系数），这是一个线性还是非线性最小二乘问题？

## 更新日志

+   2024 年 3 月 6 日：Bhargav Chandaka (bhargav9) — 对内容进行重大重组，以与幻灯片/视频中的内容相匹配

+   2023 年 4 月 28 日：Yuxuan Chen (yuxuan19) — 添加使用降秩 SVD 的计算复杂度

+   2022 年 4 月 9 日：Arnav Shah (arnavss2) — 在作业中添加了关于幻灯片的一些评论

+   

查看剩余条目



    +   2020 年 8 月 8 日：Jerry Yang (jiayiy7) — 添加了解决最小二乘法使用奇异值分解的正式证明链接

    +   2020 年 4 月 26 日：Mariana Silva (mfsilva) — 全面改进了文本；移除了非线性最小二乘法的理论

    +   2018 年 11 月 14 日：Erin Carrier (ecarrie2) — 修复了 lstsq 结果求和范围中的错误

    +   2018 年 1 月 14 日：Erin Carrier (ecarrie2) — 移除了演示链接

    +   2017 年 11 月 29 日：Erin Carrier (ecarrie2) — 修复了 lst-sq 代码中的错误，非线性 lst-sq 中的雅可比描述

    +   2017 年 11 月 17 日：Erin Carrier (ecarrie2) — 修复了错误的链接

    +   2017 年 11 月 16 日：Erin Carrier (ecarrie2) — 添加了复习问题，对全文进行了细微的格式调整以确保一致性，增加了正常方程和插值与列表平方法部分，从非线性最小二乘法中移除了高斯-牛顿法

    +   2017 年 11 月 12 日：Yu Meng (yumeng5) — 首次完整草案

    +   2017 年 10 月 17 日：Luke Olson (lukeo) — 概要

## 作者

+   CS 357 课程工作人员
