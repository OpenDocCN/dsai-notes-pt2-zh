# 特征值和特征向量

> 原文：[`cs357.cs.illinois.edu/textbook/notes/eigen.html`](https://cs357.cs.illinois.edu/textbook/notes/eigen.html)

## 学习目标

+   为各种应用计算特征值/特征向量。

+   使用幂方法找到特征向量。

+   特征值/特征向量的定义。

+   获取特征值的方法。

+   为各种应用计算特征值/特征向量。

+   使用幂方法找到特征向量。

## 特征值和特征向量

一个 $n \times n$ 矩阵 $\mathbf{A}$ 的**特征值**是一个标量 $\lambda$，使得对于某个非零向量 ${\bf x}$，有 $\mathbf{A} {\bf x} = \lambda {\bf x}$。特征值 $\lambda$ 可以是任何实数或复数标量（我们写作 $\lambda \in \mathbb{R}\ \text{或 } \lambda \in \mathbb{C}$）。即使矩阵 $\mathbf{A}$ 的所有项都是实数，特征值也可以是复数。在这种情况下，相应的向量 ${\bf x}$ 必须具有复数值分量（我们写作 ${\bf x}\in \mathbb{C}^n$)。方程 $\mathbf{A}\mathbf{x}=\lambda\mathbf{x}$ 被称为**特征值方程**，任何这样的非零向量 ${\bf x}$ 被称为 $\mathbf{A}$ 对应于 $\lambda$ 的**特征向量**。

可以将特征值方程重新排列为 $(\mathbf{A} - \lambda {\bf I}) {\bf x} = 0$，由于 ${\bf x}$ 不为零，因此当且仅当 $\lambda$ 是**特征方程**的解时，才有解：

$$\operatorname{det}(\mathbf{A} - \lambda {\bf I}) = 0.$$

表达式 $p(\lambda) = \operatorname{det}(\mathbf{A} - \lambda {\bf I})$ 被称为**特征多项式**，是一个 $n$ 次的多项式。

虽然可以通过求解特征方程找到所有特征值，但对于 $n \ge 5$ 的多项式的根没有一般形式的封闭形式的解析解，这也不是寻找特征值的好数值方法。

除非另有说明，我们按大小顺序写出特征值，即

$$|\lambda_1| \geq |\lambda_2| \geq \cdots \geq |\lambda_n|,$$

我们对特征向量进行归一化，使得 $\|{\bf x}\| = 1$。

我们定义 $A$ 的零空间为 $\mathbf {Ax}= \mathbf{0}$ 的解的线性组合的生成空间，或所有线性组合的集合。

#### 示例：求解小矩阵以找到特征值

如果矩阵相对较小，我们可以高效地找到行列式并求解特征多项式。

$$\bf{A}=\begin{bmatrix} 2 & 1 \\ 4 & 2 \end{bmatrix} \qquad \text{det}(\bf{A}- \bf{I}\lambda)=p(\lambda)=(2-\lambda)²-4 \rightarrow \lambda_1=0, \lambda_2=4$$

第二，我们通过求解 $\bf A-\bf I\lambda$ 的平凡解（零空间）来找到每个特征值对应的特征向量。**注意**以下任何 $\bf x$ 的倍数都是其特征值的有效特征向量。

$$\lambda_1: \begin{bmatrix} 2 & 1 \\ 4 & 2 \end{bmatrix}\bf x=0 \rightarrow \bf{x}=\begin{bmatrix} 1 \\ -2 \end{bmatrix} \qquad \lambda_2: \begin{bmatrix} -2 & 1 \\ 4 & -2 \end{bmatrix}\bf{x}=0 \rightarrow \bf{x}=\begin{bmatrix} 1 \\ 2 \end{bmatrix}$$

## 对角化性

一个 $n \times n$ 矩阵，如果它有 $n$ 个线性无关的特征向量，可以表示为其特征值和特征向量的形式：

$$\mathbf{A}\mathbf{X} = \begin{bmatrix} \vert & & \vert \\ \lambda_1 {\bf x}_1 & \dots & \lambda_n {\bf x}_n \\ \vert & & \vert \end{bmatrix} = \begin{bmatrix} \vert & & \vert \\ {\bf x}_1 & \dots & {\bf x}_n \\ \vert & & \vert \end{bmatrix} \begin{bmatrix}\lambda_1 & & \\ & \ddots & \\ & & \lambda_n \end{bmatrix} = \mathbf{X}\mathbf{D}$$

特征向量矩阵可以求逆以获得 $\mathbf{A}$ 的以下 **相似变换**：

$$\mathbf{AX} = \mathbf{XD} \iff \mathbf{A} = \mathbf{XDX}^{-1} \iff \mathbf{X}^{-1}\mathbf{A}\mathbf{X} = \mathbf{D}$$

将矩阵 $\mathbf{A}$ 左乘以 $\mathbf{X}^{-1}$ 和右乘以 $\mathbf{X}$ 将其转换为对角矩阵；它已经被“对角化”。

#### 示例：可对角化的矩阵

一个 $n \times n$ 矩阵是可对角化的当且仅当它有 $n$ 个线性无关的特征向量。例如：

$$\overbrace{\begin{bmatrix} 1/6 & -1/3 & 1/6 \\ -1/2 & 0 & 1/2 \\ 1/3 & 1/3 & 1/3 \end{bmatrix}}^{\mathbf{X}^{-1}} \overbrace{\begin{bmatrix} 1 & 1 & 0 \\ 1 & 0 & 1 \\ 0 & 1 & 1 \end{bmatrix}}^{\mathbf{A}} \overbrace{\begin{bmatrix} 1 & -1 & 1 \\ -2 & 0 & 1 \\ 1 & 1 & 1 \end{bmatrix}}^{\mathbf{X}} = \overbrace{\begin{bmatrix} -1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 2 \end{bmatrix}}^{\mathbf{D}}$$

#### 示例：不可对角化的矩阵

一个具有线性相关特征向量的矩阵 $\mathbf{A}$ 是不可对角化的。例如，虽然以下说法是正确的：

$$\overbrace{\begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}}^{\mathbf{A}} \overbrace{\begin{bmatrix} 1 & 1 \\ 0 & 0 \end{bmatrix}}^{\mathbf{X}} = \overbrace{\begin{bmatrix} 1 & 1 \\ 0 & 0 \end{bmatrix}}^{\mathbf{X}} \overbrace{\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}}^{\mathbf{D}},$$

矩阵 $\mathbf{X}$ 没有逆矩阵，所以我们不能通过应用逆矩阵来对 $\mathbf{A}$ 进行对角化。事实上，对于任何非奇异矩阵 $\mathbf{P}$，乘积 $\mathbf{P}^{-1}\mathbf{AP}$ 也不是对角矩阵。

#### 示例：对角化矩阵（代码片段）

以下代码片段在可能的情况下对角化一个方阵，请注意，特征向量作为二维 numpy 数组的列存储。

```py
import numpy as np
import numpy.linalg as la
def diagonalize(A):
    # A: nxn matrix
    m, n = np.shape(A)
    if (m != n):
      return None

    evals, evecs = la.eig(A) # eigenvectors as columns
    if (la.matrix_rank(evecs) != n):
      return None

    D = np.diag(evals)
    X = evecs
    return (D, X) 
```

#### 关于特征值需要记住的事项

+   特征值可以取零值。

+   特征值可以是负数。

+   特征值可以是实数或复数。

+   一个 $n \times n$ 的实矩阵可以具有复特征值。

+   $n \times n$ 矩阵的特征值不一定唯一。实际上，我们可以定义特征值的重数。特征向量 $\lambda$ 的几何重数对应于 $\lambda$ 的线性无关特征向量的数量。

+   如果一个 $n \times n$ 矩阵有 $n$ 个线性无关的特征向量，那么该矩阵是可对角化的。因此，秩亏矩阵仍然可能是可对角化的。

#### 可对角化的条件

+   如果一个 $n \times n$ 矩阵 $\mathbf A$ 有 $n$ 个线性无关的特征向量 $\mathbf x$，那么 $\mathbf A$ 是可对角化的。

+   如果一个 $n \times n$ 矩阵的特征向量少于 $n$ 个，那么该矩阵被称为病态的（因此不可对角化）。

+   如果一个 $n \times n$ 矩阵有 $n$ 个不同的特征值，那么 A 是可对角化的。

## 平移矩阵的特征值

给定一个矩阵 $\mathbf{A}$，对于任何常数标量 $\sigma$，我们定义 ***平移矩阵*** 是 $\mathbf{A} - \sigma {\bf I}$。如果 $\lambda$ 是 $\mathbf{A}$ 的一个特征值，其特征向量为 ${\bf x}$，那么 $\lambda - \sigma$ 是平移矩阵的一个特征值，其特征向量相同。这可以通过以下方式推导出来：

$$\begin{aligned} (\mathbf{A} - \sigma {\bf I}) {\bf x} &= \mathbf{A} {\bf x} - \sigma {\bf I} {\bf x} \\ &= \lambda {\bf x} - \sigma {\bf x} \\ &= (\lambda - \sigma) {\bf x}. \end{aligned}$$

## 逆矩阵的特征值

可逆矩阵不能有等于零的特征值。等于零的特征值将意味着 $\mathbf{Ax}=\mathbf{b}$ 的平凡解，一个非零维数的零空间，因此一个不可逆矩阵。此外，逆矩阵的特征值等于原矩阵特征值的倒数：

$$\mathbf{A} {\bf x} = \lambda {\bf x}\implies \\ \mathbf{A}^{-1} \mathbf{A} {\bf x} = \lambda \mathbf{A}^{-1} {\bf x} \implies \\ {\bf x} = \lambda \mathbf{A}^{-1} {\bf x}\implies \\ \mathbf{A}^{-1} {\bf x} = \frac{1}{\lambda} {\bf x}.$$

## 平移逆矩阵的特征值

同样，我们可以描述平移逆矩阵的特征值：

$$(\mathbf{A} - \sigma {\bf I})^{-1} {\bf x} = \frac{1}{\lambda - \sigma} {\bf x}.$$

在这里需要注意的是，对于平移或/和逆矩阵，特征向量保持不变。

## 将任意向量表示为特征向量的线性组合

如果一个 $n\times n$ 矩阵 $\mathbf{A}$ 是可对角化的，那么我们可以将任意向量表示为 $\mathbf{A}$ 的特征向量的线性组合。设 ${\bf u}_1,{\bf u}_2,\dots,{\bf u}_n$ 是 $\mathbf{A}$ 的 $n$ 个线性无关的特征向量；那么任意向量 $\mathbf{x}_0$ 可以表示为：

$${\bf x}_0 = \alpha_1 {\bf u}_1 + \alpha_2 {\bf u}_2 + \dots + \alpha_n {\bf u}_n.$$

如果我们将矩阵 $\mathbf{A}$ 应用于 $\mathbf{x}_0$：

$$\begin{align} \mathbf{A}{\bf x}_0 &= \alpha_1 \mathbf{A}{\bf u}_1 + \alpha_2\mathbf{A}{\bf u}_2 + \dots + \alpha_n \mathbf{A}{\bf u}_n, \\ &= \alpha_1 \lambda_1 {\bf u}_1 + \alpha_2\lambda_2 {\bf u}_2 + \dots + \alpha_n \lambda_n {\bf u}_n, \\ &= \lambda_1 \left(\alpha_1 {\bf u}_1 + \alpha_2\frac{\lambda_2}{\lambda_1}{\bf u}_2 + \dots + \alpha_n \frac{\lambda_n}{\lambda_1} {\bf u}_n\right). \\ \end{align}$$

如果我们反复应用 $\mathbf{A}$，则有

$$\mathbf{A}^k{\bf x}_0= \lambda_1^k \left(\alpha_1 {\bf u}_1 + \alpha_2\left(\frac{\lambda_2}{\lambda_1}\right)^k{\bf u}_2 + \dots + \alpha_n \left(\frac{\lambda_n}{\lambda_1}\right)^k {\bf u}_n\right).$$

在一个特征值的模严格大于其他所有特征值的情况下，即

$\vert\lambda_1\vert > \vert\lambda_2\vert\geq \vert\lambda_3\vert \geq \dots \geq\vert\lambda_n\vert$,

这意味着

$$\lim_{k\to\infty}\frac{\mathbf{A}^k {\bf x}_0}{\lambda_1^{k}} = \alpha_1 {\bf u}_1.$$

显然，当我们反复将 $\mathbf{A}$ 应用到一个任意向量上——这个向量总是可以由 $n$ 个线性无关的特征向量组成，这些特征向量张成 $\mathbb{R}^n$ ——结果收敛到 $\mathbf{A}$ 的主导特征向量的一个倍数：$\bf{u_1}$。这一观察启发了一种称为**幂迭代**的算法，这是下一节的主题。

## 幂迭代算法

对于一个矩阵 ${\bf A}$，幂迭代将找到一个特征向量 ${\bf u}_1$ 的标量倍，对应于主导特征值（模最大的）$\lambda_1$，前提是 $\vert\lambda_1\vert$ 严格大于其他特征值的模，即 $\vert\lambda_1\vert > \vert\lambda_2\vert \ge \dots \ge \vert\lambda_n\vert$.

假设

$$\mathbf{x}_0 = \alpha_1 \mathbf{u}_1 + \alpha_2\mathbf{u}_2 + \dots \alpha_n\mathbf{u}_n,\text{ with }\alpha_1 \neq 0.$$

从上一节，迭代序列

$$\mathbf{x}_k = \mathbf{A}\mathbf{x}_{k-1}\text{ for }k=1,2,3,\dots$$

满足

$$\mathbf{x}_k = \mathbf{A}^k\mathbf{x}_0 \implies \lim_{k\to\infty}\frac{\mathbf{x}_k}{\lambda_1^k} = \alpha_1\mathbf{u}_1.$$

因此，对于大的 $k$，我们有 $\mathbf{x}_k\approx \lambda_1^k \alpha_1\mathbf{u}_1$。不幸的是，这意味着 $\|\mathbf{x}_k\| \approx |\lambda_1|^k\cdot\|\alpha_1\mathbf{u}_1\|,$ 如果 $|\lambda_1| > 1$，这将非常大，如果 $|\lambda_1| < 1$，这将非常小。因此，我们使用**归一化**幂迭代。

归一化幂迭代，由以下给出。设 $\mathbf{x}_0$ 是一个单位范数的向量：$\|\mathbf{x}_0\| = 1$（任何范数都行），且 $\mathbf{x}_0 = \alpha_1 \mathbf{u}_1 + \alpha_2\mathbf{u}_2 + \dots \alpha_n\mathbf{u}_n,\text{ and }\alpha_1 \neq 0$.

**归一化幂迭代**定义为以下迭代序列，对于 $k=1,2,3,\dots$:

$$\begin{align} &\mathbf{y}_k = \mathbf{A}\mathbf{x}_{k-1} \\ &\mathbf{x}_k = \frac{\mathbf{y}_k}{\|\mathbf{y}_k\|} \end{align}$$

其中范数 $\|\cdot\|$ 与我们假设 $\|\mathbf{x}_0\| = 1$ 时使用的范数相同。

可以证明这个序列满足

$$\mathbf{x}_k = \frac{\mathbf{A}^k\mathbf{x}_0}{\|\mathbf{A}^k\mathbf{x}_0\|}.$$

这意味着对于大的 $k$ 值，我们有

$$\mathbf{x}_k \approx \left(\frac{\lambda_1}{|\lambda_1|}\right)^k\cdot\frac{\alpha_1\mathbf{u}_1}{\|\alpha_1\mathbf{u}_1\|}.$$

最大的特征值可能是正数、负数或复数。在每种情况下，我们都会有：

$$\begin{align} \lambda_1 > 0 \implies &\mathbf{x}_k \approx \frac{\alpha_1\mathbf{u}_1}{\|\alpha_1\mathbf{u}_1\|}\hspace{22.5mm} \mathbf{x}_k\text{ 收敛} \\ \lambda_1 < 0 \implies &\mathbf{x}_k \approx (-1)^k \frac{\alpha_1\mathbf{u}_1}{\|\alpha_1\mathbf{u}_1\|}\hspace{11.5mm} \text{在极限情况下，}\mathbf{x}_k\text{ 在 } \pm\frac{\alpha_1\mathbf{u}_1}{\|\alpha_1\mathbf{u}_1\|} \text{ 之间交替} \\ \lambda_1 = re^{i\theta} \implies & \mathbf{x}_k \approx e^{ik\theta} \frac{\alpha_1\mathbf{u}_1}{\|\alpha_1\mathbf{u}_1\|} \hspace{16mm} \text{在极限情况下，}\mathbf{x}_k \text{ 是 } \mathbf{u}_1 \text{ 的一个标量倍，其系数在单位圆上旋转}. \end{align}$$

严格来说，归一化幂迭代只有在 $\lambda_1 > 0$ 时才收敛到单个向量，但无论主导特征值是正数、负数还是复数，$\mathbf{x}_k$ 都会接近特征向量 $\mathbf{u}_1$ 的一个标量倍，对于大的 $k$ 值。因此，归一化幂迭代对于任何 $\lambda_1$ 值都有效，只要它的绝对值比其他特征值大。

## 幂迭代代码

以下代码片段执行幂迭代：

```py
import numpy as np
def power_iter(A, x_0, p):
  # A: nxn matrix, x_0: initial guess, p: type of norm
  x_0 = x_0/np.linalg.norm(x_0,p)
  x_k = x_0
  for i in range(max_iterations):
    y_k = A @ x_k
    x_k = y_k/np.linalg.norm(y_k,p)
  return x_k 
```

#### **示例：幂迭代的两步**

我们将使用归一化幂迭代（使用无穷范数）来逼近以下矩阵的特征向量：$\mathbf{A} = \begin{bmatrix} 1 & -2 \\ -1 & 1 \end{bmatrix}$，以及以下初始猜测：$\mathbf{x}_0 = \begin{bmatrix} -1 \\ 0 \end{bmatrix}$

**第一次迭代**:

$$\begin{align} &\mathbf{y}_1 = \mathbf{A}\mathbf{x}_0 = \begin{bmatrix} 1 & -2 \\ -1 & 1 \end{bmatrix} \begin{bmatrix} -1 \\ 0 \end{bmatrix} = \begin{bmatrix} -1 \\ 1 \end{bmatrix},\$$15pt] &\mathbf{x}_1 = \frac{\mathbf{y}_1}{\|\mathbf{y}_1\|_{\infty}} = \mathbf{y}_1 = \begin{bmatrix} -1 \\ 1\end{bmatrix}. \end{align}$$

**第二次迭代**:

$$\begin{align} &\mathbf{y}_2 = \mathbf{A}\mathbf{x}_1 = \begin{bmatrix} 1 & -2 \\ -1 & 1 \end{bmatrix} \begin{bmatrix} -1 \\ 1 \end{bmatrix} = \begin{bmatrix} -3 \\ 2 \end{bmatrix},\$$15pt] &\mathbf{x}_2 = \frac{\mathbf{y}_2}{\|\mathbf{y}_2\|_{\infty}} = \frac{1}{3}\mathbf{y}_2= \begin{bmatrix} -1 \\ \frac{2}{3}\end{bmatrix} = \begin{bmatrix} -1 \\ 0.6666\dots\end{bmatrix}. \end{align}$$

即使只有两次迭代，我们也在接近相应的特征向量：

$$\mathbf{u}_1 = \begin{bmatrix} -1 \\ \frac{1}{\sqrt{2}} \end{bmatrix} \approx \begin{bmatrix} -1 \\ 0.7071 \end{bmatrix}$$

当用无穷范数测量时，相对误差约为 4%。

## 从特征向量计算特征值

力迭代允许我们找到对应于最大特征值（模）的近似特征向量。我们如何从这个近似特征向量计算实际的特征值呢？

如果 $\lambda$ 是 $\mathbf{A}$ 的一个特征值，对应的特征向量为 $\mathbf{u}$，那么我们可以使用 ***瑞利商*** 来计算 $\lambda$ 的值：

$$\lambda = \frac{\mathbf{u}^T\mathbf{A}\mathbf{u}}{\mathbf{u}^T\mathbf{u}}.$$

因此，可以使用在幂迭代过程中找到的近似特征向量来计算一个近似特征值。

## 力迭代与浮点运算

回想一下，我们假设初始猜测满足

$$\mathbf{x}_0 = \alpha_1 \mathbf{u}_1 + \alpha_2\mathbf{u}_2 + \dots \alpha_n\mathbf{u}_n,\text{ 其中 }\alpha_1 \neq 0.$$

如果我们选择的初始猜测中 $\alpha_1 = 0$ 会发生什么？如果我们进一步假设 $\vert\lambda_2\vert > \vert\lambda_3\vert\geq \vert\lambda_4\vert \geq \dots \geq\vert\lambda_n\vert$，那么在理论上

$$\mathbf{A}^k\boldsymbol{x}_0= \lambda_2^k \left(\alpha_2 {\bf u}_2 + \alpha_3\left(\frac{\lambda_3}{\lambda_2}\right)^k{\bf u}_3 + \dots + \alpha_n \left(\frac{\lambda_n}{\lambda_2}\right)^k {\bf u}_n\right),$$

我们预计

$$\lim_{k\to\infty}\frac{\mathbf{A}^k \boldsymbol{x}_0}{\lambda_2^{k}} = \alpha_2 {\bf u}_2.$$

实际上，这种情况不会发生。一方面，如果我们对特征向量 $\mathbf{u}_1$ 没有先验知识，选择一个 $\alpha_1 = 0$ 的初始猜测几乎是不可能的。由于幂迭代是数值上进行的，使用有限精度算术，我们将在每次迭代中遇到舍入误差的存在。这意味着在每次迭代 $k$（包括 $k = 0$），我们实际上将会有

$$\mathbf{A}^k\hat{\boldsymbol{x}}_0= \lambda_1^k \left(\hat{\alpha}_1 \boldsymbol{u}_1 + \hat{\alpha}_2\left(\frac{\lambda_2}{\lambda_1}\right)^k\boldsymbol{u}_2 + \dots + \hat{\alpha}_n \left(\frac{\lambda_n}{\lambda_1}\right)^k \boldsymbol{u}_n\right),$$

其中 $\hat{\alpha}_k$ 是舍入结果的近似展开系数。即使 $\alpha_1 = 0$，有限精度的表示 $\hat{\mathbf{x}}_0$，很可能具有展开系数 $\hat{\alpha}_1 \neq 0$。即使在舍入初始猜测不会引入非零 $\hat{\alpha}_1$ 的情况下，在足够多的迭代后，舍入应用矩阵 $\mathbf{A}$ 后几乎肯定会在主导特征向量中引入一个非零分量。得到一个起始猜测 $\mathbf{x}_0$，使得所有迭代中 $\hat{\alpha}_1 = 0$ 的概率非常非常低，如果不是不可能的话。

## 没有主特征值的幂迭代

在上面，我们假设一个特征值的模严格大于所有其他特征值：$\vert\lambda_1\vert > \vert\lambda_2\vert\geq \vert\lambda_3\vert \geq \dots \geq\vert\lambda_n\vert$。如果 $\vert\lambda_1\vert = \vert\lambda_2\vert$ 会发生什么？

如果 $\lambda_1 = \lambda_2 = \lambda \in \mathbb{R}$，那么：

$$\mathbf{x}_k = \mathbf{A}^k\mathbf{x}_0 \approx \alpha_1\lambda^k\mathbf{u}_1 + \alpha_2\lambda^k\mathbf{u}_2 = \lambda^k\left(\alpha_1\mathbf{u}_1 + \alpha_2\mathbf{u}_2\right),$$

因此

$$\lim_{k\to\infty}\lambda^{-k}\mathbf{A}^k\mathbf{x}_0 = \alpha_1\mathbf{u}_1 + \alpha_2\mathbf{u}_2.$$

量 $\alpha_1\mathbf{u}_1 + \alpha_2\mathbf{u}_2$ 仍然是对应于 $\lambda$ 的特征向量，因此幂迭代仍然会趋近于主特征向量。

如果主特征值具有相反的符号，即 $\lambda_1 = -\lambda_2 = \lambda \in \mathbb{R}$，那么

$$\mathbf{x}_k = \mathbf{A}^k\mathbf{x}_0 \approx \alpha_1\lambda^k\mathbf{u}_1 + \alpha_2(-\lambda)^k\mathbf{u}_2 = \lambda^k\left(\alpha_1\mathbf{u}_1 + (-1)^k\alpha_2\mathbf{u}_2\right).$$

对于大的 $k$，我们将有 $\lambda^{-k}\mathbf{A}\mathbf{x}_0 \approx \alpha_1\mathbf{u}_1 + (-1)^k\alpha_2\mathbf{u}_2$，尽管它是两个特征向量的线性组合，但它本身 ***不是*** $\mathbf{A}$ 的特征向量。

最后，如果两个主特征值是复共轭对 $\lambda_1 = re^{i\theta},\ \lambda_2 = re^{-i\theta}$，那么 $\mathbf{x}_k = \mathbf{A}^k\mathbf{x}_0 \approx \alpha_1\lambda^k\mathbf{u}_1 + \alpha_2(\overline{\lambda})^k\mathbf{u}_2 = \lambda^k\left(\alpha_1\mathbf{u}_1 + \left(\frac{\overline{\lambda}}{\lambda}\right)^k\alpha_2\mathbf{u}_2\right) = \lambda^k(\alpha_1\mathbf{u}_1 + \alpha_2 e^{-i2k\theta}\mathbf{u}_2).$

对于大的 $k$，$\lambda^{-k}\mathbf{A}\mathbf{x}_0$ 近似为两个特征向量的线性组合，但这种线性组合本身 ***不是*** 特征向量。

## 逆迭代

为了获得对应于非奇异矩阵的 ***最小*** 特征值 $\lambda_n$ 的特征向量，我们可以对 $\mathbf{A}^{-1}$ 应用幂迭代。以下递推关系描述了逆迭代算法：$\boldsymbol{x}_{k+1} = \frac{\mathbf{A}^{-1} \boldsymbol{x}_k}{\|\mathbf{A}^{-1} \boldsymbol{x}_k\|}.$ 不要忘记对每个 $\boldsymbol{x}_{k+1}$ 进行归一化。

在实践中，我们不是取逆并用于幂迭代，而是对 $\mathbf{A}$ 进行 LU 分解，并对每次迭代进行 LU 解，将每次迭代的运行时间从 $O(n³)$ 降低到 $O(n²)$，预处理仍然是 $O(n³)$。

## 带平移的逆迭代

为了获得与某个值 $\sigma$ 最接近的特征值对应的特征向量，可以将 $\mathbf{A}$ 平移 $\sigma$ 并求逆，以便类似于幂迭代算法来求解。以下递推关系描述了逆迭代算法：$\boldsymbol{x}_{k+1} = \frac{(\mathbf{A} - \sigma \mathbf{I})^{-1} \boldsymbol{x}_k}{\|(\mathbf{A} - \sigma \mathbf{I})^{-1} \boldsymbol{x}_k\|}$。注意，如果平移为零，则这与逆迭代相同。

## 瑞利商迭代

可以根据当前特征值的估计值更新平移 $\sigma$ 以提高收敛速度。这种估计可以通过瑞利商得到。瑞利商迭代由以下递推关系给出：

$$\sigma_k = \frac{\boldsymbol{x}_k^T \mathbf{A} \boldsymbol{x}_k}{\boldsymbol{x}_k^T\boldsymbol{x}_k}$$ $$\boldsymbol{x}_{k+1} = \frac{(\mathbf{A} - \sigma_k \mathbf{I})^{-1} \boldsymbol{x}_k}{\|(\mathbf{A} - \sigma_k \mathbf{I})^{-1} \boldsymbol{x}_k\|}.$$

## 收敛性质

功迭代法的收敛率是**线性**的，当前迭代与主特征向量之间误差的递推关系为：$\mathbf{e}_{k+1} \approx \frac{|\lambda_2|}{|\lambda_1|}\mathbf{e}_k$。

（平移的）逆迭代法的收敛率也是线性的，但现在取决于与平移 $\sigma$ 最接近的两个特征值。（记住，标准逆迭代对应于平移 $\sigma = 0$。）误差的递推关系为：$\mathbf{e}_{k+1} \approx \frac{|\lambda_\text{closest} - \sigma|}{|\lambda_\text{second-closest} - \sigma|}\mathbf{e}_k$。

## 成本和收敛性摘要

| 方法 | 描述 | 成本 | 收敛性 |
| --- | --- | --- | --- |
| 功方法 | $\boldsymbol{x}_{k+1} = \mathbf{A} \boldsymbol{x}_{k}$ | $kn²$ | $\left | \frac{\lambda_2}{\lambda_1}\right | $ |
| 逆幂方法 | $\mathbf{A} \boldsymbol{x}_{k+1} = \boldsymbol{x}_{k}$ | $n^{3} + kn²$ | $\left | \frac{\lambda_n}{\lambda_{n-1}}\right | $ |
| 平移逆幂方法 | $(\mathbf{A} - \sigma \mathbf{I}) \boldsymbol{x}_{k+1} = \boldsymbol{x}_{k}$ | $n^{3} + kn²$ | $\left | \frac{\lambda_c-\sigma}{\lambda_{c2}-\sigma}\right | $ |

$\lambda_1$: 最大的特征值（按大小）

$\lambda_2$: 第二大的特征值（按大小）

$\lambda_n$: 最小的特征值（按大小）

$\lambda_{n-1}$: 第二小的特征值（按大小）

$\lambda_c$: 最接近 $\sigma$ 的特征值

$\lambda_{c2}$: 最接近 $\sigma$ 的第二个特征值

## 正交矩阵

方阵被称为***正交的***，当且仅当其列向量彼此正交且范数为 $1$（这样的向量集形式上称为***正交归一***集），即：$\boldsymbol{c}_i^T \boldsymbol{c}_j = 0 \quad \forall \ i \neq j, \quad \|\boldsymbol{c}_i\| = 1 \quad \forall \ i \iff \mathbf{A} \in \mathcal{O}(n),$ 或者 $\langle\boldsymbol{c}_i,\boldsymbol{c}_j \rangle = \begin{cases} 0 \quad \mathrm{if} \ i \neq j, \\ 1 \quad \mathrm{if} \ i = j \end{cases} \iff \mathbf{A} \in \mathcal{O}(n),$ 其中 $\mathcal{O}(n)$ 是所有 $n \times n$ 的正交矩阵的集合，称为正交群，$\boldsymbol{c}_i$, $i=1, \dots, n$ 是 $\mathbf{A}$ 的列向量，$\langle \cdot, \cdot \rangle$ 是内积算子。正交矩阵具有许多理想的性质：

(a) $\mathbf{A}^T \in \mathcal{O}(n)$

(b) $\mathbf{A}^T \mathbf{A} = \mathbf{A} \mathbf{A}^T = \mathbf{I} \implies \mathbf{A}^{-1} = \mathbf{A}^T$

(c) $\det{\mathbf{A}} = \pm 1$

(d) $\kappa_2(\mathbf{A}) = 1$

## Gram-Schmidt

从一组线性无关的向量构造正交基的算法称为 Gram-Schmidt 过程。对于一个基集 $\{x_1, x_2, \dots x_n\}$，我们可以通过以下变换形成一个正交集 $\{v_1, v_2, \dots v_n\}$：

$\begin{align} \boldsymbol{v}_1 &= \boldsymbol{x}_1, \\ \boldsymbol{v}_2 &= \boldsymbol{x}_2 - \frac{\langle\boldsymbol{v}_1,\boldsymbol{x}_2\rangle}{\|\boldsymbol{v}_1\|²}\boldsymbol{v}_1,\\ \boldsymbol{v}_3 &= \boldsymbol{x}_3 - \frac{\langle\boldsymbol{v}_1,\boldsymbol{x}_3\rangle}{\|\boldsymbol{v}_1\|²}\boldsymbol{v}_1 - \frac{\langle\boldsymbol{v}_2,\boldsymbol{x}_3\rangle}{\|\boldsymbol{v}_2\|²}\boldsymbol{v}_2,\\ \vdots &= \vdots\\ \boldsymbol{v}_n &= \boldsymbol{x}_n - \sum_{i=1}^{n-1}\frac{\langle\boldsymbol{v}_i,\boldsymbol{x}_n\rangle}{\|\boldsymbol{v}_i\|²}\boldsymbol{v}_i, \end{align}$

其中 $\langle \cdot, \cdot \rangle$ 是内积算子。新正交集 $\{v_1, v_2, \dots v_n\}$ 中的每个向量都可以独立地**归一化**，以获得**正交归一基**。

## 复习问题

1.  自主值/特征向量对的定义是什么？

1.  如果 $\mathbf{v}$ 是 $\mathbf{A}$ 的一个特征向量，对于任何非零标量 $c$，我们可以说关于 $c\mathbf{v}$ 什么？

1.  $\mathbf{A}$ 的特征值与以下特征值之间的关系是什么？1) 对于某个标量 $c$，$c\mathbf{A}$ 的特征值，2) 对于某个标量 $\sigma$，$(\mathbf{A} - \sigma \mathbf{I})$ 的特征值，3) $\mathbf{A}^{-1}$ 的特征值？

1.  $\mathbf{A}$ 的特征向量与以下特征向量之间的关系是什么？1) 对于某个标量 $c$，$c\mathbf{A}$ 的特征向量，2) 对于某个标量 $\sigma$，$(\mathbf{A} - \sigma \mathbf{I})$ 的特征向量，3) $\mathbf{A}^{-1}$ 的特征向量？

1.  能够运行归一化幂迭代的一步或几步。

1.  力迭代收敛到 $\mathbf{A}$ 的哪个特征向量？

1.  逆幂迭代收敛到 $\mathbf{A}$ 的哪个特征向量？

1.  带位移的逆幂迭代收敛到 $\mathbf{A}$ 的哪个特征向量？

1.  描述逆迭代法的成本。

1.  如果我们给定 $(\mathbf{A} - \sigma \mathbf{I})$ 的 LU 分解，描述逆迭代法的成本。

1.  在什么情况下幂迭代（或归一化幂迭代）会失败？

1.  给定一个近似特征向量，我们如何近似 $\mathbf{A}$ 的特征值？

1.  如果我们在幂迭代过程中不对迭代进行归一化，会发生什么？

1.  什么是雷利商？

1.  如果初始猜测没有主特征向量的任何分量，幂迭代的结果会发生什么？这取决于我们使用的是有限精度还是无限精度吗？

1.  幂迭代的收敛速度是多少？

1.  幂迭代的收敛如何依赖于特征值？

1.  我们如何找到矩阵的其他特征值，而不仅仅是主特征值？

1.  矩阵可对角化意味着什么？

1.  所有矩阵都可以对角化吗？

## 更新日志

+   2025 年 10 月 28 日：Dev Singh（dsingh14）— 修复特征向量计算

+   2024 年 2 月 13 日：Pascal Adhikary（pascala2）— 添加来自幻灯片的信息/示例，重新组织

+   2022 年 2 月 28 日：陈宇轩（yuxuan19）— 添加学习目标，成本摘要

+   

查看剩余条目



    +   2020 年 3 月 1 日：Peter Sentz（）— 添加文本以包含幻灯片内容

    +   2018 年 10 月 14 日：Erin Carrier（ecarrie2）— 删除正交/GS 部分

    +   2018 年 1 月 14 日：Erin Carrier（ecarrie2）— 删除演示链接

    +   2017 年 11 月 10 日：Erin Carrier（ecarrie2）— 添加方法成本

    +   2017 年 10 月 26 日：Matthew West（mwest）— 重写 eval/evec 定义

    +   2017 年 10 月 25 日：Erin Carrier（ecarrie2）— 进行小修，添加复习问题

    +   2017 年 10 月 16 日：Luke Olson（lukeo）— 概述

    +   2017 年 10 月 14 日：Arun Lakshmanan（lakshma2）— 首次完整草案

## 作者

+   CS 357 课程工作人员
