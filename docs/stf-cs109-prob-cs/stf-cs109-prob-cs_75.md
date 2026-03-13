# 中心极限定理

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part4/clt/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part4/clt/)

* * *

中心极限定理有两种表述方式。要么是独立同分布随机变量的和是正态分布，要么是独立同分布随机变量的平均值是正态分布。

**中心极限定理（和版本**）

设 $X_1, X_2, \dots, X_n$ 为独立同分布的随机变量。当 $n \rightarrow \infty$ 时，这些随机变量的**和**趋近于正态分布：$$\begin{align*} \sum_{i=1}^{n}X_i \sim N(n \cdot \mu, n \cdot \sigma²) \end{align*}$$ 其中 $\mu = \E[X_i]$ 和 $\sigma² = \Var(X_i)$。注意，由于每个 $X_i$ 都是同分布的，它们共享相同的期望和方差。

到目前为止，你可能认为中心极限定理很棒。但它还有更好的。通过一些代数操作，我们可以证明，如果独立同分布随机变量的样本均值是正态分布，那么等权重的独立同分布随机变量的和也必须是正态分布：

**中心极限定理（平均值版本**）

设 $X_1, X_2, \dots, X_n$ 为独立同分布的随机变量。当 $n \rightarrow \infty$ 时，这些随机变量的**平均值**趋近于正态分布：$$\begin{align*} \frac{1}{n}\sum_{i=1}^{n}X_i \sim N(\mu, \frac{\sigma²}{n}) \end{align*}$$ 其中 $\mu = \E[X_i]$ 和 $\sigma² = \Var(X_i)$。

## 中心极限定理直觉

在上一节中，我们探讨了当你添加两个随机变量时会发生什么。当你添加超过两个随机变量时会发生什么？例如，如果我想要将 100 个不同的均匀随机变量相加：

```py
from random import random 

def add_100_uniforms():
   total = 0
   for i in range(100):
       # returns a sample from uniform(0, 1)
       x_i = random()    
       total += x_i
   return total
```

这个函数返回的`total`值将是一个随机变量。点击下面的按钮运行函数并观察`total`的结果值：

`total:`

``总分布看起来像什么？让我们多次计算`total`并可视化它产生的值的直方图。      <canvas id="cltHistogram" style="max-height: 400px"></canvas>      这很有趣！`total`是 100 个独立均匀分布的和，看起来是正态的。这是均匀分布的特殊性质吗？不！实际上，这适用于几乎任何类型的分布（只要你要加的东西有有限的均值和有限的方差，这是我们在这个阅读器中涵盖的所有内容）。    *   40 个$X_i$的和，其中$X_i \sim \Beta(a = 5, b = 4)$？正态分布。 *   90 个$X_i$的和，其中$X_i \sim \Poi(\lambda = 4)$？正态分布。 *   50 次骰子投掷的和？正态分布。 *   10000 个$X_i$的平均值，其中$X_i \sim \Exp(\lambda = 8)$？正态分布。    对于任何分布，从该分布中抽取的$n$个独立等权样本的和或平均值将是正态分布。    ## 连续性校正    现在我们可以看到，使用正态分布的二项式近似实际上源于中心极限定理。回想一下，当我们计算正态近似的概率时，我们必须使用连续性校正。这是因为我们正在用连续随机变量（正态分布）来近似离散随机变量（二项分布）。每次你的正态分布近似离散随机变量时，都应该使用连续性校正。一般连续性校正的规则与二项式近似连续性校正的规则相同。    在上面的激励示例中，我们添加了 100 个均匀分布，不需要连续性校正，因为均匀分布的和是连续的。在下面的骰子投掷和示例中，需要连续性校正，因为骰子结果是离散的。    ## 示例    ***示例：***    你将掷一个 6 面的骰子 10 次。设$X$为 10 个骰子的总和 = $X_1 + X_2 + \dots + X_{10}$。如果你掷出的总和$X \leq 25$或$X \geq 45$，你就赢了游戏。使用中心极限定理计算你赢的概率。回想一下$E[X_i] = 3.5$和$\text{Var}(X_i) = \frac{35}{12}$。    设$Y$为近似正态分布。根据中心极限定理$Y \sim N(10 \cdot E[X_i], 10 \cdot \Var(X_i))$。代入已知的期望和方差值：$Y \sim N(35, 29.2)$ $$\begin{align*} \P(&X \leq 25 \text{ 或 } X \geq 45) \\ &= \P(X \leq 25) + \P(X \geq 45) \\ &\approx \P(Y < 25.5) + \P(Y > 44.5) &&\text{连续性校正} \\ &\approx \P(Y < 25.5) + [1 -\P(Y < 44.5)]\\ &\approx \Phi(\frac{25.5 - 35}{\sqrt{29.2} }) + \Big[1 -\Phi(\frac{44.5- 35}{\sqrt{29.2} })\Big] &&\text{正态 CDF}\\ &\approx \Phi(-1.76) + [1 - \Phi(1.76)]\\ &\approx 0.039 + (1-0.961) \approx 0.078 \end{align*}$$    ***示例：***    假设你有一个新的算法，你想测试它的运行时间。你对算法运行时间的方差有一个想法：$\sigma² = 4\text{sec}²$，但你想要估计均值：$\mu = t$sec。你可以重复运行该算法（独立同分布试验）。你需要运行多少次试验，才能以 95%的置信度估计运行时间 = $t \pm 0.5$？设$X_i$为第$i$次运行的时间（对于$1 \leq i \leq n$）。 $$\begin{align*} 0.95 = P(-0.5 \leq \frac{\sum_{i=1}^nX_i}{n} - t \leq 0.5) \end{align*}$$ 根据中心极限定理，标准正态分布$Z$必须等于： $$\begin{align*} Z &= \frac{\left(\sum_{i=1}^n X_i\right) - n\mu}{\sigma \sqrt{n}} \\ &= \frac{\left(\sum_{i=1}^n X_i\right) - nt}{2 \sqrt{n}} \end{align*}$$ 现在，我们重新写我们的概率不等式，使得中心项是$Z$： $$\begin{align*} 0.95&= P(-0.5 \leq \frac{\sum_{i=1}^nX_i}{n} - t \leq 0.5)=P(\frac{-0.5\sqrt{n}}{2} \leq \frac{\sum_{i=1}^nX_i}{n} - t \leq \frac{0.5\sqrt{n}}{2})\\ &=P(\frac{-0.5\sqrt{n}}{2} \leq \frac{\sum_{i=1}^nX_i}{n} - t \leq \frac{0.5\sqrt{n}}{2})=P(\frac{-0.5\sqrt{n}}{2} \leq \frac{\sum_{i=1}^nX_i}{n} - t \leq \frac{0.5\sqrt{n}}{2})\\ &=P(\frac{-0.5\sqrt{n}}{2} \leq \frac{\sum_{i=1}^nX_i}{n} - t \leq \frac{0.5\sqrt{n}}{2})\\ &=P(\frac{-0.5\sqrt{n}}{2} \leq Z \leq \frac{0.5\sqrt{n}}{2}) \end{align*}$$ 现在我们可以找到使这个等式成立的$n$的值。 $$\begin{align*} 0.95&= \phi(\frac{\sqrt{n}}{4}) - \phi(-\frac{\sqrt{n}}{4}) = \phi(\frac{\sqrt{n}}{4}) - (1- \phi(\frac{\sqrt{n}}{4})) \\ &= 2\phi(\frac{\sqrt{n}}{4}) - 1\\ 0.975 &= \phi(\frac{\sqrt{n}}{4})\\ \phi^{-1}(0.975) &= \frac{\sqrt{n}}{4} \\ 1.96 &= \frac{\sqrt{n}}{4}\\ n &= 61.4 \end{align*}$$ 因此，需要运行 62 次。如果你对在方差未知的情况下如何扩展这种情况感兴趣，可以查看学生 t 检验的变体。``
