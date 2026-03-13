# 正态分布

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part2/normal/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part2/normal/)

* * *

最重要的随机变量类型是正态（又称高斯）随机变量，它由均值（$\mu$）和方差（$\sigma²$）参数化，有时也可以等价地写成均值和方差（$\sigma²$）。如果 $X$ 是一个正态变量，我们写成 $X \sim N(\mu, \sigma²)$。正态分布之所以重要，是因为它是由独立随机变量的和生成的，因此它在自然界中很常见。世界上许多事物并非呈正态分布，但数据科学家和计算机科学家仍然将它们建模为正态分布。为什么？因为它是在匹配特定期望（平均值）和方差（分散度）的同时，我们能为随机变量做出的最熵（保守）的建模决策。

正态分布的概率密度函数（PDF）对于 $X \sim N(\mu, \sigma²)$ 是：$$\begin{align*} f_X(x) = \frac{1}{\sigma \sqrt{2\pi} } e ^{\frac{-(x-\mu)²}{2\sigma²}} \end{align*}$$ 注意 PDF 函数指数中的 $x$。当 $x$ 等于均值 ($\mu$) 时，e 的指数为 $0$，PDF 达到最大值。

根据定义，正态分布有 $\E[X] = \mu$ 和 $\var(X) = \sigma²$。

正态 PDF 的积分没有封闭形式，因此也没有封闭形式的 CDF。然而，我们可以将任何正态分布转换为具有预计算 CDF 的正态分布。这种数学技巧的结果是，正态分布 $X \sim N(\mu, \sigma²)$ 的 CDF 为：$$\begin{align*} F_X(x) = \Phi\left(\frac{x - \mu}{\sigma}\right) \end{align*}$$

其中 $\Phi$ 是一个预计算的函数，表示标准正态的 CDF。

**正态（又称高斯）随机变量**

| 符号： | $X \sim \N(\mu, \sigma²)$ |
| --- | --- |
| 描述： | 一种常见且自然发生的分布。 |

| 参数：| $\mu \in \mathbb{R}$，均值。$\sigma² \in \mathbb{R}$，方差。

|

| 支持集： | $x \in \mathbb{R}$ |
| --- | --- |
| PDF 方程： | $$f(x) = \frac{1}{\sigma \sqrt{2 \pi}} e^{-\frac{1}{2}\Big(\frac{x-\mu}{\sigma}\Big)²}$$ |
| CDF 方程： | $$\begin{align} F(x) &= \phi(\frac{x-\mu}{\sigma}) && \text{其中 $\phi$ 是标准正态的 CDF} \end{align}$$ |
| 期望： | $\E[X] = \mu$ |
| 方差： | $\var(X) = \sigma²$ |
| PDF 图： |

参数 $\mu$：参数 $\sigma$：

<canvas id="normalPdf" style="max-height: 400px"></canvas>

## 线性变换

如果 $X$ 是一个正态分布，即 $X \sim N(\mu, \sigma²)$，且 $Y$ 是 $X$ 的线性变换，即 $Y = aX + b$，那么 $Y$ 也是一个正态分布，其中：$$\begin{align*} Y \sim N(a\mu + b, a²\sigma²) \end{align*}$$

## 投影到标准正态

对于任何正态变量 $X$，我们可以找到一个从 $X$ 到标准正态变量 $Z \sim N(0, 1)$ 的线性变换。注意，$Z$ 是标准正态的典型表示法。对于任何正态变量，如果你从正态变量中减去均值（$\mu$）并除以标准差（$\sigma$），结果总是标准正态。我们可以用数学方法证明这一点。设 $W = \frac{X - \mu}{\sigma}$：$$\begin{align*} W &= \frac{X -\mu}{\sigma} && \text{ 对 $X$ 进行变换：减去 $\mu$ 并除以 $\sigma$} \\ & = \frac{1}{\sigma}X - \frac{\mu}{\sigma} && \text{ 使用代数重写方程}\\ & = aX + b && \text{ 线性变换，其中 $a = \frac{1}{\sigma}$，$b = - \frac{\mu}{\sigma}$ }\\ &\sim N(a\mu + b, a²\sigma²) && \text{ 正态变量的线性变换是另一个正态}\\ &\sim N(\frac{\mu}{\sigma} - \frac{\mu}{\sigma}, \frac{\sigma²}{\sigma²}) && \text{ 代入 $a$ 和 $b$ 的值}\\ &\sim N(0, 1) && \text{ 标准正态} \end{align*}$$

使用这个变换，我们可以用已知的 $Z$ 的累积分布函数 $F_Z(x)$ 来表示 $X$ 的累积分布函数 $F_X(x)$。由于 $Z$ 的累积分布函数非常常见，它得到了自己的希腊符号：$\Phi(x)$ $$\begin{align*} F_X(x) &= P(X \leq x) \\ &= P\left(\frac{X - \mu}{\sigma} \leq \frac{x - \mu}{\sigma}\right) \\ &= P\left(Z \leq \frac{x - \mu}{\sigma}\right)\\ &= \Phi\left(\frac{x - \mu}{\sigma}\right) \end{align*}$$

可以在表中查找 $\Phi(x)$ 的值。每种现代编程语言也都有计算正态随机变量累积分布函数（CDF）的能力！

***示例***：设 $X\sim \mathcal{N}(3, 16)$，$P(X > 0)$ 是多少？$$\begin{align*} P(X > 0) &= P\left(\frac{X-3}{4} > \frac{0-3}{4}\right) = P\left(Z > -\frac{3}{4}\right) = 1 - P\left(Z \leq -\frac{3}{4}\right)\\ &= 1 - \Phi(-\frac{3}{4}) = 1 - (1- \Phi(\frac{3}{4})) = \Phi(\frac{3}{4}) = 0.7734 \end{align*}$$ $P(2 < X < 5)$ 是多少？$$\begin{align*} P(2 < X < 5) &= P\left(\frac{2 - 3}{4} < \frac{X-3}{4} < \frac{5-3}{4}\right) = P\left(-\frac{1}{4} < Z < \frac{2}{4}\right)\\ &= \Phi(\frac{2}{4})-\Phi(-\frac{1}{4}) = \Phi(\frac{1}{2})-(1 - \Phi(\frac{1}{4})) = 0.2902 \end{align*}$$

***示例***：你可以在导线上发送 2 或-2 伏特的电压来表示 1 或 0。设 $X$ = 发送的电压，设 $R$ = 接收到的电压。$R = X + Y$，其中 $Y \sim \mathcal{N}(0, 1)$ 是噪声。在解码时，如果 $R \geq 0.5$，我们解释电压为 1，否则为 0。解码后原比特为 1 的情况下发生错误的概率 $P(\text{error after decoding}|\text{original bit} = 1)$ 是多少？$$\begin{align*} P(X + Y < 0.5) &= P(2 + Y < 0.5) \\ &= P(Y < -1.5) \\ &= \Phi(-1.5) \\ &\approx 0.0668 \end{align*}$$

***示例***：在标准差内的 67%规则。一个正态变量 $X \sim \N(\mu, \sigma)$ 的值在其均值的一个标准差内的概率是多少？

$$ \begin{align} \text{在} \mu \text{的一个} \sigma \text{范围内} \text{的概率} &= \p(\mu - \sigma < X < \mu + \sigma) \\ &= \p(X < \mu + \sigma) - \p(X < \mu - \sigma) && \text{范围的概率} \\ &= \Phi\Big(\frac{(\mu + \sigma)-\mu}{\sigma}\Big) - \Phi\Big(\frac{(\mu - \sigma)-\mu}{\sigma}\Big) && \text{正态分布的 CDF} \\ &= \Phi\Big(\frac{\sigma}{\sigma}\Big) - \Phi\Big(\frac{- \sigma}{\sigma}\Big) && \text{消去} \mu \text{项} \\ &= \Phi(1) - \Phi(-1) && \text{消去} \sigma \text{项} \\ &\approx 0.8413 - 0.1587 \approx 0.683 && \text{代入} \Phi \text{函数} \end{align} $$ 我们没有对 $\mu$ 或 $\sigma$ 的值做出任何假设，因此这适用于每一个正态随机变量。由于它使用了正态 CDF，所以这不适用于其他类型的随机变量。

## CDF 计算器

要计算正态分布（也称为高斯分布）随机变量在值 $x$ 处的累积密度函数（CDF），也写作 $F(x)$，你可以将你的分布转换为“标准正态分布”并在标准正态 CDF 中查找相应的值。然而，大多数编程库都会提供一个正态 CDF 函数：

**正态分布累积密度函数计算器**

| x |  |
| --- | --- |
| μ |  |
| std |  |

在 Python 中，你可以使用`scipy`库来计算这些值

```py
from scipy import stats

# get the input values
mean = 1.0
std_dev = 0.5
query = 0.1 # aka x

# calc the CDF in two lines
X = stats.norm(mean, std_dev)
p = X.cdf(query)

# calc the CDF in one line
p = stats.norm.cdf(query, mean, std_dev) 
```

重要的是要注意，在 Python 库中，正态分布的第二个参数是标准差**而不是**方差，正如它在数学符号中通常定义的那样。回想一下，标准差是方差的平方根。
