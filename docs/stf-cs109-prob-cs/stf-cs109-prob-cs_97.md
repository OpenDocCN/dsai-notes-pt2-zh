# 高斯混合

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/mixture_models/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/mixture_models/)

* * *

数据 = [6.47, 5.82, 8.7, 4.76, 7.62, 6.95, 7.44, 6.73, 3.38, 5.89, 7.81, 6.93, 7.23, 6.25, 5.31, 7.71, 7.42, 5.81, 4.03, 7.09, 7.1, 7.62, 7.74, 6.19, 7.3, 7.37, 6.99, 2.97, 3.3, 7.08, 6.23, 3.67, 3.05, 6.67, 6.5, 6.08, 3.7, 6.76, 6.56, 3.61, 7.25, 7.34, 6.27, 6.54, 5.83, 6.44, 5.34, 7.7, 4.19, 7.34]参数 $t$: 参数 $\mu_a$: 参数 $\sigma_a$: 参数 $\mu_b$: 参数 $\sigma_b$:

<canvas id="mixturePdf" style="max-height: 400px">

似然：对数似然：最佳观察：

### 什么是高斯混合？

高斯混合描述了一个随机变量，其概率密度函数可能来自两个高斯分布（或更多，但在这个演示中我们只使用两个）。样本来自第一个高斯分布的概率是确定的，否则来自第二个。它有五个参数：四个用于描述两个高斯分布，一个用于描述两个高斯分布的相对权重。

#### 生成代码

```py
from scipy import stats
def sample():
   # choose group membership
   membership = stats.bernoulli.rvs(0.2)
   if membership == 1:
      # sample from gaussian 1
      return stats.norm.rvs(3.5,0.7)
   else:
      # sample from gaussian 2
      return stats.norm.rvs(6.8,0.7)
```

#### 概率密度函数

$$\begin{align*} f(X=x) = t \cdot f(A=x) + (1-t) \cdot f(B=x) \end{align*}$$ $\text{st}$ $A \sim N(\mu_a, \sigma_a²)$ $B \sim N(\mu_b, \sigma_b²)$

将所有这些放在一起，高斯混合的概率密度函数（PDF）为：

$$\begin{align*} f(x) = t \cdot \Big(\frac{1}{\sqrt{2\pi}\sigma_a} e^{-\frac{1}{2}(\frac{x-\mu_a}{\sigma_a})²}\Big) + (1-t) \cdot \Big(\frac{1}{\sqrt{2\pi}\sigma_b} e^{-\frac{1}{2}(\frac{x-\mu_b}{\sigma_b})²}\Big) \end{align*}$$

### 高斯混合的最大似然估计

特别说明：尽管生成故事有一个伯努利（组成员）属性，但它从未被观察到。MLE 最大化的是观察数据的似然。

令 $\vec{\theta} = [t, \mu_a,\mu_b,\sigma_a, \sigma_b]$ 为参数。因为数学表达式会变得很长，我将使用 $\theta$ 作为符号来代替 $\vec{\theta}$。只需记住它是一个向量。

最大似然估计（MLE）的想法是选择使对数似然最大的 $\theta$ 值。所有优化方法都需要我们计算我们想要优化的东西（对数似然）相对于我们可以改变的值（我们的参数）的偏导数。

#### 似然函数

$$\begin{align*} L(\theta) &= \prod_i^n f(x_i | \theta) \\ &= \prod_i^n \Big[t \cdot \Big(\frac{1}{\sqrt{2\pi}\sigma_a} e^{-\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²}\Big) + (1-t) \cdot \Big(\frac{1}{\sqrt{2\pi}\sigma_b} e^{-\frac{1}{2}(\frac{x_i-\mu_b}{\sigma_b})²}\Big) \Big] \end{align*}$$

#### 对数似然函数

$$\begin{align*} LL(\theta) &= \log L(\theta) \\ &= \log \prod_i^n f(x_i | \theta) \\ &= \sum_i^n \log f(x_i | \theta) \\ \end{align*}$$

现在已经足够了，但如果你想要扩展这个术语，你会得到：$$\begin{align*} LL(\theta) &= \sum_i^n \log \Big[t \cdot \Big(\frac{1}{\sqrt{2\pi}\sigma_a} e^{-\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²}\Big) + (1-t) \cdot \Big(\frac{1}{\sqrt{2\pi}\sigma_b} e^{-\frac{1}{2}(\frac{x_i-\mu_b}{\sigma_b})²}\Big) \Big] \end{align*}$$

#### 关于 $\theta$ 的 LL 的导数

这里是一个计算关于参数之一 $\mu_a$ 的偏导数的例子。你需要为所有参数都找到这样的导数。

**注意：**当我最初写这个演示时，我以为这只是一个简单的导数。它并不简单，因为对数中有一个和。因此，对数项不会减少。对数仍然用于将外层的 $\prod$ 转换为 $\sum$。因此，$LL$ 的偏导数是可解的，但证明使用了相当多的链式法则。**要点：**本节的主要要点（如果你想跳过导数证明）是，得到的导数足够复杂，我们希望有一种方法来计算 argmax，而无需将那个导数设为零并求解 $\mu_a$。梯度下降法登场！

在对对数似然函数进行大量求导时，一个好的第一步是考虑单个数据点的似然对数的导数。这是对数似然表达式中的内层求和：$ \frac{\d}{\d \mu_a} \log f(x_i|\theta) $

在开始之前：请注意，$\mu_a$ 在 $f(x_i|\theta) $ 这个项中不出现：$(1-t) \cdot \Big(\frac{1}{\sqrt{2\pi}\sigma_b} e^{-\frac{1}{2}(\frac{x_i-\mu_b}{\sigma_b})²}\Big) =K $ 在证明中，当我们遇到这个项时，我们将把它视为一个常数，我们称之为 $K$。好的，让我们开始吧！ $$\begin{align*} \frac{\d}{\d \mu_a} & \log f(x_i|\theta) \\ &= \frac{1}{f(x_i|\theta)} \frac{\d}{\d \mu_a} f(x_i|\theta) &&\text{链式法则在 }\log \\ &= \frac{1}{f(x_i|\theta)} \frac{\d}{\d \mu_a} \Big[t \cdot \Big(\frac{1}{\sqrt{2\pi}\sigma_a} e^{-\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²}\Big) + K\Big] &&\text{代入 }f(x_i|\theta)\\ &= \frac{1}{f(x_i|\theta)} \frac{\d}{\d \mu_a} \Big[t \cdot \Big(\frac{1}{\sqrt{2\pi}\sigma_a} e^{-\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²}\Big)\Big] &&\frac{\d}{\d \mu_a} K = 0\\ &= \frac{t}{f(x_i|\theta) \sqrt{2\pi}\sigma_a} \cdot \frac{\d}{\d \mu_a} e^{-\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²} &&\text{提取常数}\\ &= \frac{t}{f(x_i|\theta) \sqrt{2\pi}\sigma_a} \cdot e^{-\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²} \cdot \frac{\d}{\d \mu_a} -\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²&&\text{对 }e^x \text{ 求链式}\\ &= \frac{t}{f(x_i|\theta) \sqrt{2\pi}\sigma_a} \cdot e^{-\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²} \cdot \Big[-(\frac{x_i-\mu_a}{\sigma_a}) \frac{\d}{\d \mu_a} (\frac{x_i-\mu_a}{\sigma_a})\Big]&&\text{对 }x² \text{ 求链式}\\ &= \frac{t}{f(x_i|\theta) \sqrt{2\pi}\sigma_a} \cdot e^{-\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²} \cdot \Big[ -(\frac{x_i-\mu_a}{\sigma_a}) \cdot \frac{-1}{\sigma_a}\Big] &&\text{最终导数} \\ &= \frac{t}{f(x_i|\theta) \sqrt{2\pi}\sigma_a³} \cdot e^{-\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²} \cdot (x_i-\mu_a) &&\text{简化} \\ \end{align*}$$

那是针对单个数据点的。对于完整的数据集： $$\begin{align*} \frac{\d LL(\theta)}{\d \mu_a} &= \sum_i^n \frac{\d}{\d \mu_a} \log f(x_i|\theta)\\ &= \sum_i^n \frac{t}{f(x_i|\theta) \sqrt{2\pi}\sigma_a³} \cdot e^{-\frac{1}{2}(\frac{x_i-\mu_a}{\sigma_a})²} \cdot (x_i-\mu_a) \end{align*}$$

这个过程应该对所有五个参数重复进行！现在，我们应该如何找到一个 $\mu_a$ 的值，在存在其他参数设置和数据的情况下，使得这个导数为零？将导数设为 0 并求解 $\mu_a$ 是不会奏效的。

### 使用优化器估计参数

一旦我们有了 $LL$ 函数以及 $LL$ 对每个参数的导数，我们就可以使用优化器来计算 argmax。在这种情况下，最佳选择可能是梯度上升（或负对数似然梯度下降）。 $$\begin{align*} \nabla_{\theta} LL(\theta) &=\begin{bmatrix} \frac{\d LL(\theta)}{\d t}\\ \frac{\d LL(\theta)}{\d \mu_a}\\ \frac{\d LL(\theta)}{\d \mu_b}\\ \frac{\d LL(\theta)}{\d \sigma_a}\\ \frac{\d LL(\theta)}{\d \sigma_b}\\ \end{bmatrix} \end{align*}$$

</canvas>
