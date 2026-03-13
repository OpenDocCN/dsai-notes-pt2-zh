# 相关系数

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part3/correlation/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part3/correlation/)

* * *

## 协方差

协方差是衡量一个变量的偏差与其均值匹配程度与另一个变量的偏差与其均值匹配程度之间关系的定量度量。它是一个定义为：$$\begin{align*} \text{Cov}(X,Y) = E[(X-E[X])(Y-E[Y])] \end{align*}$$

这一点有点难以理解（但值得稍微深入探讨）。外层期望将是内层函数在特定 $(x,y)$ 处的加权求和，权重为 $(x,y)$ 的概率。如果 $x$ 和 $y$ 都高于各自的均值，或者如果 $x$ 和 $y$ 都低于各自的均值，那么这个项将是正的。如果一个高于其均值而另一个低于，这个项将是负的。如果项的加权求和是正的，那么两个随机变量将具有正相关。我们可以重写上面的方程以得到一个等价的方程：$$\begin{align*} \text{Cov}(X,Y) = E[XY] - E[Y]E[X] \end{align*}$$

***引理：独立随机变量的相关系数***:

如果两个随机变量 $X$ 和 $Y$ 是独立的，那么它们的协方差必须为 0. $$\begin{align*} \text{Cov}(X,Y) &= E[XY] - E[Y]E[X] && \text{协方差的定义} \\ &= E[X]E[Y] - E[Y]E[X] && \text{期望的乘积引理} \\ &= 0 \end{align*}$$ 注意，逆命题并不成立。协方差为 0 并不能证明独立性。使用这个方程（以及乘积引理）可以很容易地看出，如果两个随机变量是独立的，它们的协方差为 0。在一般情况下，逆命题是不成立的。

## 协方差性质

假设 $X$ 和 $Y$ 是任意随机变量：$$\begin{align*} &\text{Cov}(X,Y) = \text{Cov}(Y,X) \\ &\text{Cov}(X,X) = E[X²] - E[X]E[X] = \text{Var}(X) \\ &\text{Cov}(aX +b,Y) = a\text{Cov}(X,Y) \end{align*}$$

设 $X = X_1 + X_2 + \dots + X_n$，设 $Y = Y_1 + Y_2 + \dots + Y_m$。$X$ 和 $Y$ 的协方差为：$$\begin{align*} &\text{Cov}(X,Y) = \sum_{i=1}^n \sum_{j=1}^m\text{Cov}(X_i,Y_j) \\ &\text{Cov}(X,X) = \text{Var}(X) = \sum_{i=1}^n \sum_{j=1}^n\text{Cov}(X_i,X_j) \end{align*}$$

最后一个属性给我们提供了计算方差的第三种方法。我们可以用它再次展示如何得到二项分布的方差。

## 相关系数

在上一节课中，我们讨论了协方差。协方差很有趣，因为它是对两个变量之间关系的定量测量。今天我们将扩展这个概念到相关系数。两个随机变量 $X$ 和 $Y$ 的相关系数 $\rho(X, Y)$ 是这两个变量的协方差除以每个变量的方差。这种归一化消除了单位：$$\begin{align*} \rho(X,Y) = \frac{\text{Cov}(X,Y)}{\sqrt{\text{Var}(X)Var(Y)}} \end{align*}$$

相关性衡量 $X$ 和 $Y$ 之间的线性关系。 $$\begin{align*} &\rho(X,Y) = 1 && Y = aX + b \text{ 其中 } a = \sigma_y / \sigma_x \\ &\rho(X,Y) = -1 && Y = aX + b \text{ 其中 } a = -\sigma_y / \sigma_x \\ &\rho(X,Y) = 0 && \text{ 没有线性关系} \\ \end{align*}$$

如果 $\rho(X, Y) = 0$，我们说 $X$ 和 $Y$ 是“不相关的”。

当人们使用“相关性”这个术语时，他们实际上是在指一种特定的相关性，称为“皮尔逊相关性”。它衡量两个变量之间线性关系的程度。另一种衡量方法是“斯皮尔曼相关性”，其公式几乎与常规的相关性评分相同，只是将基础随机变量首先转换为它们的秩。斯皮尔曼相关性不属于 CS109 的范畴。
