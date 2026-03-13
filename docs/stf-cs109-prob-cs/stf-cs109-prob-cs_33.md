# 泊松分布

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part2/poisson/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part2/poisson/)

* * *

泊松随机变量给出在固定时间间隔（或空间）内发生特定数量事件的概率。它假设事件以已知的恒定平均速率发生，并且与上次事件发生的时间无关。

**泊松随机变量**

| 符号： | $X \sim \Poi(\lambda)$ |
| --- | --- |
| 描述： | 在固定时间段内发生的事件数量，如果（a）事件以恒定的平均速率发生，并且（b）它们与上次事件发生的时间无关。 |
| 参数： | $\lambda \in \mathbb{R}^{+}$，恒定的平均速率。 |
| 支持集： | $x \in \{0, 1, \dots\}$ |
| PMF 方程： | $$\p(X=x) = \frac{\lambda^xe^{-\lambda}}{x!}$$ |
| 期望： | $\E[X] = \lambda$ |
| 方差： | $\var(X) = \lambda$ |
| PMF 图： |

参数 $\lambda$:

<canvas id="poissonPmf" style="max-height: 400px"></canvas>

## 泊松直觉

在本节中，我们展示了泊松推导背后的直觉。这不仅是一种深入理解泊松分布的好方法，也是对二项分布的良好实践。

让我们来解决预测在固定时间段（下一分钟）内发生特定数量事件概率的问题。例如，假设你正在开发一个共享出行应用程序，你关心特定区域收到的请求数量的概率。根据历史数据，你知道每分钟的请求平均数为 $\lambda = 5$。在一分钟内收到 1 个、2 个、3 个等请求的概率是多少？

*：我们可以通过使用二项分布来近似解决这个问题！假设我们将一分钟分成 60 秒，并将每一秒作为一个指示伯努利变量——你要么收到请求，要么不收。如果你在一秒内收到请求，指示变量为 1。否则为 0。以下是我们的 60 个二元指示变量的可视化。在这个例子中，假设我们在 2.75 秒和 7.12 秒收到请求，相应的指示变量是蓝色填充的方框：*

*1 分钟

在一分钟内接收到的总请求数可以近似为六十个指示变量的和，这恰好符合二项分布——伯努利分布的和的描述。具体定义 $X$ 为一分钟内的请求数。$X$ 是一个有 $n=60$ 次试验的二项分布。在单次试验中成功的概率 $p$ 是多少？为了使 $X$ 的期望值等于观察到的历史平均值 $\lambda =5$，我们应该选择 $p$ 使得 $\lambda = \E[X]$。$$ \begin{align} \lambda &= \E[X] && \text{期望值与历史平均值匹配} \\ \lambda &= n \cdot p && \text{二项分布的期望值是 } n \cdot p \\ p &= \frac{\lambda}{n} && \text{求解 $p$} \end{align} $$ 在这个例子中，由于 $\lambda=5$ 且 $n=60$，我们应该选择 $p=5/60$ 并声明 $X \sim \Bin(n=60, p=5/60)$。现在我们有了 $X$ 的形式，我们可以通过使用二项分布的概率质量函数来回答关于请求数量的概率问题：$$\p(X = x) = {n \choose x} p^x (1-p)^{n-x}$$

例如：$$\p(X=1) = {60 \choose 1} (5/60)¹ (55/60)^{60-1} \approx 0.0295$$ $$\p(X=2) = {60 \choose 2} (5/60)² (55/60)^{60-2} \approx 0.0790$$ $$\p(X=3) = {60 \choose 3} (5/60)³ (55/60)^{60-3} \approx 0.1389$$ 很好！但别忘了这只是一个近似。我们没有考虑到在单个秒内可能发生多个事件的事实。解决这个问题的方法之一是将我们的分钟分割成更细的区间（将它们分割成 60 秒的选择相当随意）。相反，让我们将我们的分钟分割成 600 分秒，再次在 2.75 秒和 7.12 秒有请求：1 分钟

现在 $n=600$，$p=5/600$，且 $X \sim \Bin(n=600, p=6/600)$。我们可以使用这个更好的近似重复我们的示例计算：$$\p(X=1) = {600 \choose 1} (5/600)¹ (595/60)^{600-1} \approx 0.0333$$ $$\p(X=2) = {600 \choose 2} (5/600)² (595/600)^{600-2} \approx 0.0837$$ $$\p(X=3) = {600 \choose 3} (5/600)³ (595/600)^{600-3} \approx 0.1402$$

选择任何 $n$ 的值，这是我们分割分钟的桶的数量：

$n$ 越大，近似值越准确。那么当 $n$ 是无穷大时会发生什么？它变成了泊松分布！

## 泊松分布，二项分布的极限

或者，如果我们真的关心确保我们不会在同一个桶中出现两个事件，我们可以将我们的分钟分割成无限小的桶：

1 分钟

***证明***：泊松分布的推导

现在我们将我们的分钟无限分割，$X$ 的概率质量函数（PMF）看起来会是什么样子？我们可以写出方程，并随着 $n$ 趋向于无穷大来思考它。回想一下，$p$ 仍然等于 $\lambda/n$：

$$ \P(X=x) = \lim_{n \rightarrow \infty} {n \choose x} (\lambda / n)^x(1-\lambda/n)^{n-x} $$

虽然这个表达式看起来可能令人畏惧，但它简化得很好。这个证明使用了我们在这本书中没有介绍的一些特殊的极限规则：

$$ \begin{align} \P(X=x) &= \lim_{n \rightarrow \infty} {n \choose x} (\lambda / n)^x(1-\lambda/n)^{n-x} && \text{开始：极限中的二项式}\\ &= \lim_{n \rightarrow \infty} {n \choose x} \cdot \frac{\lambda^x}{n^x} \cdot \frac{(1-\lambda/n)^{n}}{(1-\lambda/n)^{x}} && \text{展开幂次项} \\ &= \lim_{n \rightarrow \infty} \frac{n!}{(n-x)!x!} \cdot \frac{\lambda^x}{n^x} \cdot \frac{(1-\lambda/n)^{n}}{(1-\lambda/n)^{x}} && \text{展开二项式项} \\ &= \lim_{n \rightarrow \infty} \frac{n!}{(n-x)!x!} \cdot \frac{\lambda^x}{n^x} \cdot \frac{e^{-\lambda}}{(1-\lambda/n)^{x}} && \href{http://www.sosmath.com/calculus/sequence/specialim/specialim.html}{\text{规则 }} \lim_{n \rightarrow \infty}(1-\lambda/n)^{n} = e^{-\lambda}\\ &= \lim_{n \rightarrow \infty} \frac{n!}{(n-x)!x!} \cdot \frac{\lambda^x}{n^x} \cdot \frac{e^{-\lambda}}{1} && \href{https://www.youtube.com/watch?v=x1WBTBtfvjM}{\text{规则 }} \lim_{n \rightarrow \infty}\lambda/n= 0\\ &= \lim_{n \rightarrow \infty} \frac{n!}{(n-x)!} \cdot \frac{1}{x!} \cdot \frac{\lambda^x}{n^x} \cdot \frac{e^{-\lambda}}{1} && \text{拆分第一项}\\ &= \lim_{n \rightarrow \infty} \frac{n^x}{1} \cdot \frac{1}{x!} \cdot \frac{\lambda^x}{n^x} \cdot \frac{e^{-\lambda}}{1} && \lim_{n \rightarrow \infty }\frac{n!}{(n-x)!} = n^x\\ &= \lim_{n \rightarrow \infty} \frac{\lambda^x}{x!} \cdot \frac{e^{-\lambda}}{1} && \text{消去 }n^x\\ &= \frac{\lambda^x \cdot e^{-\lambda}}{x!} && \text{简化}\\ \end{align} $$

这是一个美丽的表达式！现在我们可以计算每分钟请求数量的实际概率，如果历史平均值为 $\lambda=5$：

$$\p(X=1) = \frac{5¹ \cdot e^{-5}}{1!} = 0.03369$$ $$\p(X=2) = \frac{5² \cdot e^{-5}}{2!}= 0.08422$$ $$\p(X=3) = \frac{5³ \cdot e^{-5}}{3!} = 0.14037$$

这既更准确，也更容易计算！

## 改变时间框架

假设你被给出一个单位时间内的速率，但你想要知道另一个单位时间内的速率。例如，你可能被给出每分钟的网站点击率，但你想要知道 20 分钟内的概率。你只需将这个速率乘以 20，就可以从“每 1 分钟时间”的速率转换为“每 20 分钟时间”的速率。*
