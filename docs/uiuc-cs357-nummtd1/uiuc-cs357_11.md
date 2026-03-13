# 条件数

> [`cs357.cs.illinois.edu/textbook/notes/condition.html`](https://cs357.cs.illinois.edu/textbook/notes/condition.html)

## 学习目标

+   计算条件数

+   量化高条件数的影响

## 数值实验

**输入**存在不确定性：

+   由于有限精度表示引起的错误

+   采样误差

一旦你选择了你的数值方法，你应该期望在输出中看到多少误差？

*你的方法对输入中的误差（扰动）敏感吗？*

## 线性系统解的敏感性和误差界限

### 动机

假设我们从非奇异线性方程组 ${\bf A} \boldsymbol{x} = \boldsymbol{b}$ 开始。如果我们通过一个小量 $\Delta \boldsymbol{b}$ 改变右侧向量 $\boldsymbol{b}$（输入），解 $\boldsymbol{x}$（输出）将改变多少，即 $\Delta \boldsymbol{x}$ 有多大？

让我们探索这个问题！

### 推导

设 $\boldsymbol{x}$ 是 ${\bf A} \boldsymbol{x} = \boldsymbol{b}$ 的解，$\hat{\boldsymbol{x}}$ 是扰动问题 ${\bf A} \hat{\boldsymbol{x}} = \boldsymbol{b} + \Delta \boldsymbol{b}$ 的解。

此外，设 $\Delta \boldsymbol{x} = \hat{\boldsymbol{x}} - \boldsymbol{x}$ 为输出中的绝对误差。

然后，我们有 ${\bf A} \boldsymbol{x} + {\bf A} \Delta \boldsymbol{x} = \boldsymbol{b} + \Delta \boldsymbol{b},$ 因此 ${\bf A} \Delta \boldsymbol{x} = \Delta \boldsymbol{b}.$

使用上述方程，我们将看到输出中的相对误差 $\left(\frac{\|\Delta \boldsymbol{x}\|}{\|\boldsymbol{x}\|}\right)$ 与输入中的相对误差 $\left(\frac{\|\Delta \boldsymbol{b}\|}{\|\boldsymbol{b}\|}\right)$ 之间的关系：

$$\begin{align} \frac{\|\Delta \boldsymbol{x}\| / \|\boldsymbol{x}\|}{\|\Delta \boldsymbol{b}\| / \|\boldsymbol{b}\|} &= \frac{\|\Delta \boldsymbol{x}\| \|\boldsymbol{b}\|}{\|\boldsymbol{x}\| \|\Delta \boldsymbol{b}\|}\\ &= \frac{\|{\bf A}^{-1} \Delta \boldsymbol{b}\| \|{\bf A} \boldsymbol{x}\|}{\|\boldsymbol{x}\| \|\Delta \boldsymbol{b}\|}\\ &\le \frac{\|{\bf A}^{-1}\| \|\Delta \boldsymbol{b}\| \|{\bf A}\| \|\boldsymbol{x}\|}{\|\boldsymbol{x}\| \|\Delta \boldsymbol{b}\|} \\ &= \|{\bf A}^{-1}\| \|{\bf A}\|\\ &= \text{cond}({\bf A}) \end{align}$$

其中我们使用了 $\|{\bf A}\boldsymbol{x}\| \le \|{\bf A}\| \|\boldsymbol{x}\|, \forall \boldsymbol{x}.$

#### 矩阵扰动和误差界限

然后

$$\frac{\|\Delta \boldsymbol{x}\|}{\|\boldsymbol{x}\|} \le \text{cond}({\bf A})\frac{\|\Delta \boldsymbol{b}\|}{\|\boldsymbol{b}\|} \qquad (1)$$

我们也可以通过一个小量 $\boldsymbol{E}$ 对矩阵 $\boldsymbol{A}$（输入）进行扰动，使得

$$\begin{align} (\boldsymbol{A} + \boldsymbol{E}) \hat{\boldsymbol{x}} = \boldsymbol{b} \end{align}$$

以类似的方式获得：

$$\frac{\|\Delta \boldsymbol{x}\|}{\|\boldsymbol{x}\|} \le \text{cond}({\bf A})\frac{\| \boldsymbol{E}\|}{\|\boldsymbol{A}\|}$$

因此，如果我们知道输入的相对误差，那么我们可以使用系统的条件数来获得我们计算解（输出）的相对误差的上界。

### 示例

给出一个条件非常好的矩阵的例子（即，具有适合计算的好的条件数）。选择矩阵可能的最优条件数？

$$\begin{flalign} & \text{A) } \text{cond}({\bf A}) < 0 \\ & \text{B) } \text{cond}({\bf A}) = 0 \\ & \text{C) } 0 < \text{cond}({\bf A}) < 1 \\ & \text{D) } \text{cond}({\bf A}) = 1 \\ & \text{E) } \text{cond}({\bf A}) = \text{large numbers} \\ && \end{flalign}$$ 

**答案**



$\bf D$

矩阵 ${\bf A}$ 的条件数不能小于 1，较小的条件数将最小化输出 $\left(\frac{\|\Delta \boldsymbol{x}\|}{\|\boldsymbol{x}\|}\right)$ 的相对误差。由于我们希望最小化计算误差，选择 $ \text{D} $ 是正确答案。

## 条件数

### 条件数定义

***条件数***：衡量求解线性方程组对输入变化的敏感度的度量。

一个平方非奇异矩阵 ${\bf A}$ 的 ***条件数*** 定义为 $\text{cond}({\bf A}) = \kappa({\bf A}) = \|{\bf A}\| \|{\bf A}^{-1}\|$。这也是与求解线性系统 ${\bf A} \boldsymbol{x} = \boldsymbol{b}$ 相关的条件数。具有大条件数的矩阵被称为 ***病态的***，而具有小条件的矩阵被称为 ***良态的***。

单位矩阵是良态的。我们通过以下方式证明这一点：

假设 $\|{\bf A}\|$ 的逆存在，$\text{cond}({\bf A}) = \|{\bf A}\| \|{\bf A}^{-1}\| \geq \|{\bf A}{\bf A}^{-1}\| = \|{\bf I}\| = 1.$

这是可能的最小条件数。小的条件数对应于小的误差放大。记住，小的条件数是好的！

如果 ${\bf A}$ 是奇异的 (${\bf A}^{-1}$ 不存在)，我们可以按照惯例定义 $\text{cond}({\bf A}) = \infty$。

### 诱导矩阵范数

回想一下，诱导矩阵范数由以下给出：

$$\begin{align} \|{\bf A}\|_p := \max_{\|\mathbf{x}\|=1} \|{\bf A}\mathbf{x}\|_p \end{align}$$

条件数可以用任何 $p$-范数来衡量，因此为了精确起见，我们通常指定所使用的范数，即 $\text{cond}_2$，$\text{cond}_1$，$\text{cond}_{\infty}$。

对于 1-范数，我们取矩阵 $\boldsymbol{A}$ 的最大绝对列和。

$$\|{\bf A}\|_1 = \max_j \sum_{i=1}^n \vert a_{ij} \vert.$$

对于 $\infty$-范数，我们取矩阵 $\boldsymbol{A}$ 的最大绝对行和。

$$\|{\bf A}\|_{\infty} = \max_i \sum_{j=1}^n \vert a_{ij} \vert.$$

对于 2-范数，$\sigma_k$ 是矩阵 $\boldsymbol{A}$ 的奇异值。

$$\|{\bf A}\|_{2} = \max_k \sigma_k$$

### 正交矩阵的条件数

正交矩阵 $\boldsymbol{A}$ 的 2-范数条件数是多少？

$$\begin{align} \text{cond}({\bf A}) = \|{\bf A}\|_2 \|{\bf A}^{-1}\|_2 = \|{\bf A}\|_2 \|{\bf A}^{T}\|_2 = 1 \end{align}$$

因此，这意味着正交矩阵具有最优的条件数。

### 关于条件数需要记住的事情

+   对于任何矩阵 ${\bf A}$，$\text{cond}({\bf A}) \geq 1.$

+   对于单位矩阵 ${\bf I}$，$\text{cond}({\bf I}) = 1.$

+   对于任何矩阵 ${\bf A}$ 和一个非零标量 $\gamma$，$\text{cond}(\gamma {\bf A}) = \text{cond}({\bf A}).$

+   对于任何对角矩阵 ${\bf D}$，$\text{cond}({\bf D})$ = $\frac{\text{max}\mid d_{i} \mid}{\text{min}\mid d_{i} \mid}.$

+   条件数是衡量矩阵接近奇异性程度的一个指标：条件数大的矩阵几乎奇异，而条件数接近 1 的矩阵远非奇异。

+   矩阵的行列式并不是检查矩阵是否接近奇异性好的指标。

### 示例

对角矩阵的 2-范数条件数是多少？

$$\mathbf{A} = \begin{bmatrix} 100 & 0 & 0 \\ 0 & 13 & 0 \\ 0 & 0 & 0.5 \end{bmatrix}?$$ $$\begin{flalign} & \text{A) } 1 \\ & \text{B) } 50 \\ & \text{C) } 100 \\ & \text{D) } 200 \\ && \end{flalign}$$ 

**答案**



$\bf D$

如上所述，对于任何对角矩阵 ${\bf D}$，$\text{cond}({\bf D}) $ = $\frac{\text{max}\mid d_{i} \mid}{\text{min}\mid d_{i} \mid}.$ 因此，答案是 $ 100 / 0.5 = 200\. $

另一种处理这个问题的方法是求对角矩阵 ${\bf A}$ 的逆：

$ \mathbf{A^{-1}} = \begin{bmatrix} 1/100 & 0 & 0 \\ 0 & 1/13 & 0 \\ 0 & 0 & 2 \end{bmatrix}? $

$ \begin{align} \text{cond}({\bf A}) = \|{\bf A}\|_2 \|{\bf A}^{-1}\|_2 = 100 * 2 = 200 \end{align} $

## 残差与误差

近似解 $\hat{\boldsymbol{x}}$ 对于线性系统 ${\bf A} \boldsymbol{x} = \boldsymbol{b}$ 的残差向量 $\boldsymbol{r}$ 定义为 $\boldsymbol{r} = \boldsymbol{b} - {\bf A} \hat{\boldsymbol{x}}$. 由于 ${\bf A} \hat{\boldsymbol{x}} = \boldsymbol{b} + \Delta \boldsymbol{b}$，我们有

$$\boldsymbol{r} = \boldsymbol{b} - (\boldsymbol{b} + \Delta \boldsymbol{b}) = -\Delta \boldsymbol{b}$$

因此，方程（1）也可以写成

$$\frac{\|\Delta \boldsymbol{x}\|}{\|\boldsymbol{x}\|} \le \text{cond}({\bf A})\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{b}\|}$$

如果我们定义相对残差为 $\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{b}\|}$，我们可以看到，只有当 ${\bf A}$ 是良态的（$\text{cond}({\bf A})$ 小）时，小的相对残差才意味着近似解中的小的相对误差。

此外，重要的是要注意相对残差和相对误差之间的区别。相对残差 $\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{b}\|}$ 告诉我们近似解 $\hat{\boldsymbol{x}}$ 满足线性系统 ${\bf A} \boldsymbol{x} = \boldsymbol{b}$ 的程度。相对误差 $\frac{\|\Delta \boldsymbol{x}\|}{\|\boldsymbol{x}\|}$ 告诉我们近似解 $\hat{\boldsymbol{x}}$ 与精确解 $\boldsymbol{x}$ 的接近程度。记住，我们不知道精确解 $\boldsymbol{x}$，这就是为什么我们开始使用残差向量 $\boldsymbol{r}$ 的原因。

### 示例

$$\mathbf{A} = \begin{bmatrix} 13 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 15 \end{bmatrix}$$

假设我们有一个 ${\boldsymbol{x}}$ 是 ${\bf A} \boldsymbol{x} = \boldsymbol{b}$ 的解，$\hat {\boldsymbol{x}}$ 是 ${\bf A} \hat{\boldsymbol{x}} = \boldsymbol{b} + \Delta \boldsymbol{b}$ 的解。我们定义 ${\bf r} = {\bf A} \hat{\boldsymbol{x}} - \boldsymbol{b}$。如果我们知道相对残差 $\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{b}\|}$ 是 $10^{-4}$，确定输出相对误差的上限。假设 2-范数。



**答案**



$\frac{\|\Delta \boldsymbol{x}\|}{\|\boldsymbol{x}\|} \le \text{cond}({\bf A})\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{b}\|} = \mathbf{15 * 10^{-4}} $

## 相对残差的替代定义

作为提醒，相对残差 $\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{b}\|}$ 告诉我们近似解 $\hat{\boldsymbol{x}}$ 满足线性系统 ${\bf A} \boldsymbol{x} = \boldsymbol{b}$ 的程度。

还有其他一些与“相对残差”密切相关的量，也具有相同的名称。请注意，

$$\begin{align} \|\Delta \boldsymbol{x}\| &= \|\hat{\boldsymbol{x}} - \boldsymbol{x}\| \\ &= \|\boldsymbol{A}^{-1}\boldsymbol{A}\hat{\boldsymbol{x}} - \boldsymbol{A}^{-1}\boldsymbol{b}\| \\ &= \|\boldsymbol{A}^{-1}(\boldsymbol{A}\hat{\boldsymbol{x}} - \boldsymbol{b})\| \\ &= \|\boldsymbol{A}^{-1}\boldsymbol{r}\|\\ &\leq \|\boldsymbol{A}^{-1}\|\cdot \| \boldsymbol{r}\| \\ &= \|\boldsymbol{A}^{-1}\|\cdot \|\boldsymbol{A}\| \frac{\|\boldsymbol{r}\|}{\|\boldsymbol{A}\|} \\ &= \text{cond}(\boldsymbol{A})\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{A}\|}. \end{align}$$

总结来说，

$$\|\Delta \boldsymbol{x}\| \leq \text{cond}(\boldsymbol{A})\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{A}\|}\qquad (2)$$

我们可以将这个不等式除以 $\|\boldsymbol{x}\|$ 来得到

$$\frac{\|\Delta \boldsymbol{x}\|}{\|\boldsymbol{x}\|} \le \text{cond}({\bf A})\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{A}\|\cdot\|\boldsymbol{x}\|}.$$

量 $\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{A}\|\cdot\|\boldsymbol{x}\|}$ 也被称为相对残差。这个不等式在数学上是有用的，但它涉及到未知解的范数 $\|\mathbf{x}\|$，因此它不是限制相对误差的实际方法。由于 $\|\boldsymbol{b}\| = \|\boldsymbol{A}\boldsymbol{x}\| \leq \|\boldsymbol{A}\|\cdot \|\boldsymbol{x}\|$，我们有

$$\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{A}\|\cdot\|\boldsymbol{x}\|} \leq \frac{\|\boldsymbol{r}\|}{\|\boldsymbol{b}\|}$$

*请注意，在某些选择 $\boldsymbol{b}$ 的情况下，两边有时是相等的。*

我们还可以将 方程 (2) 除以 $\|\hat{\boldsymbol{x}}\|$ 来得到

$$\frac{\|\Delta \boldsymbol{x}\|}{\|\hat{\boldsymbol{x}}\|} \le \text{cond}({\bf A})\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{A}\|\cdot\|\hat{\boldsymbol{x}}\|}.$$

左边不再是相对误差（分母现在是近似解的范数，而不是精确解），但右边仍然可以提供一个合理的相对误差估计。它也是可计算的，因为真解的范数没有出现在右边。

因此，量 $\frac{\|\boldsymbol{r}\|}{\|\boldsymbol{A}\|\cdot\|\hat{\boldsymbol{x}}\|}$ 也被称为相对残差。这在下一节中用来描述残差与矩阵 $\boldsymbol{A}$ 中的误差之间的关系。

虽然 3 个不同的量都被称为“相对残差”可能会令人困惑，但你应该能够通过上下文确定正在讨论的是哪一个。

## 带部分主元的高斯消元法保证产生小的残差

当我们使用带部分主元的高斯消元法来计算线性方程组 ${\bf A} \boldsymbol{x} = \boldsymbol{b}$ 的解并得到一个近似解 $\hat{\boldsymbol{x}}$ 时，残差向量 $\boldsymbol{r}$ 满足：

$$\frac{\|\boldsymbol{r}\|}{\|{\bf A}\| \|\hat{\boldsymbol{x}}\|} \le \frac{\|E\|}{\|{\bf A}\|} \le c \epsilon_{mach}$$

其中 $E$ 是 ${\bf A}$ 中的向后误差（定义为 $({\bf A}+E)\hat{\boldsymbol{x}} = \boldsymbol{b}$），$c$ 是与 ${\bf A}$ 和 $\epsilon_{mach}$ 相关的系数，而 $\epsilon_{mach}$ 是机器精度。

通常情况下，带部分主元时 $c$ 较小，但无主元时 $c$ 可以任意大。

因此，无论系统的条件数如何，带部分主元的高斯消元法都会产生**小的相对残差**。****

更多细节，请参阅 [高斯消元与舍入误差](https://math.la.asu.edu/~gardner/lu-round.pdf)。

## 条件数估计的经验法则

假设我们对线性方程组 ${\bf A} \boldsymbol{x} = \boldsymbol{b}$ 应用部分选主元的高斯消元法和回代，并得到一个计算出的解 $\hat{\boldsymbol{x}}$。如果 ${\bf A}$ 和 $\boldsymbol{b}$ 中的项精确到 $s$ 位小数，且 $\text{cond}({\bf A}) \approx 10^w$，那么解向量 $\hat{\boldsymbol{x}}$ 的元素将精确到大约 $s-w$ 位小数。

关于这个经验法则的证明，请参阅 [David S. Watkins 的《矩阵计算基础》](https://books.google.com/books?id=xi5omWiQ-3kC&pg=PA165&lpg=PA165&dq=gaussian+elimination+rule+of+thumb&source=bl&ots=KlQVax3zja&sig=o4SHiYPAXodkk39u9yw0NYZe1Zo&hl=en&sa=X&ved=0ahUKEwiopPykkvjWAhWjzIMKHYGpDIsQ6AEIXzAK#v=onepage&q=gaussian%20elimination%20rule%20of%20thumb&f=false)。

### 示例

如果我们使用部分选主元的高斯消元法来解决条件数为 $10^{10}$ 的线性方程组 ${\bf A} \boldsymbol{x} = \boldsymbol{b}$，并且假设我们使用 IEEE 双精度且输入精确到机器精度，我们期望在解中能得到多少位准确的小数？



**答案**

在 IEEE 双精度中，$\epsilon_{mach} \approx 2.2\times 10^{-16}$，这意味着 ${\bf A}$ 和 $\boldsymbol{b}$ 中的项精确到 $\vert\log_{10}(2.2\times 10^{-16})\vert \approx 16$ 位小数。

然后，使用这个经验法则，我们知道 $\hat{\boldsymbol{x}}$ 中的项将精确到大约 $16-10 = 6$ 位小数。

## 复习问题

1.  条件数的定义是什么？

1.  解方程 ${\bf A}\mathbf{x} = \mathbf{b}$ 的条件数是多少？

1.  矩阵-向量乘法的条件数是多少？

1.  计算给定 $p$ 的矩阵的 $p$-范数条件数。

1.  你想要一个小的条件数还是大的条件数？

1.  正交矩阵的条件数是多少？

1.  如果你 ${\bf A}$ 和 $\mathbf{b}$ 有 $p$ 位准确数字，那么当 ${\bf A}$ 的条件数为 $\kappa$ 时，你在 ${\bf A}\mathbf{x} = \mathbf{b}$ 的解中会有多少位准确数字？

1.  在解线性方程组 ${\bf A}\mathbf{x} = \mathbf{b}$ 时，小的残差是否保证结果准确？

1.  考虑解线性方程组 ${\bf A}\mathbf{x} = \mathbf{b}$。何时使用部分选主元的高斯消元法会产生小的残差？

1.  矩阵 ${\bf A}$ 的条件数与 ${\bf A}^{-1}$ 的条件数有何关系？

## 更新日志

+   2024 年 2 月 12 日：Arnav Aggarwal (arnava4) — 将笔记与幻灯片对齐并添加了额外的示例

+   2022 年 3 月 19 日：Yuxuan Chen (yuxuan19) — 添加了条件数要点，进行了一些小的修正

+   2017 年 10 月 27 日：Yu Meng (yumeng5) — 首次完整草案

+   

查看剩余条目



    +   2017 年 10 月 27 日：Erin Carrier (ecarrie2) — 添加复习问题，全文小修，修订了经验法则措辞

    +   2017 年 10 月 17 日：Luke Olson (lukeo) — 概要

## 作者

+   CS 357 课程工作人员
