# 指数分布

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part2/exponential/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part2/exponential/)

* * *

指数分布衡量的是从下一个事件发生所需的时间**量**。它假设事件通过泊松过程发生。请注意，这与衡量固定时间段内事件数量的泊松随机变量不同。

**指数随机变量**

| 符号： | $X \sim \Exp(\lambda)$ |
| --- | --- |
| 描述： | 如果（a）事件以恒定的平均速率发生，并且（b）它们与上次事件发生的时间无关，则下一个事件发生的时间。 |
| 参数： | $\lambda \in \mathbb{R}^{+}$，恒定的平均速率。 |
| 支持集： | $x \in \mathbb{R}^+$ |
| PDF 方程： | $$f(x) = \lambda e^{-\lambda x}$$ |
| CDF 方程： | $$F(x) = 1 - e^{-\lambda x}$$ |
| 期望： | $\E[X] = 1/\lambda$ |
| 方差： | $\var(X) = 1/\lambda²$ |
| PDF 图： |

参数 $\lambda$：

<canvas id="exponentialPdf" style="max-height: 400px"></canvas>

指数分布是连续分布的一个很好的例子，其中累积分布函数（CDF）更容易处理，因为它允许你回答概率问题而不需要使用积分。

**示例：**根据美国地质调查局的历史数据，8.0+ 级别的地震在某个地点以每年 0.002 的速率发生。已知地震是通过泊松过程发生的。在接下来的 4 年内发生大地震的概率是多少？

设 $Y$ 为下一次大地震的年数。因为 $Y$ 衡量的是下一个事件发生的时间，所以它符合指数随机变量的描述：$Y \sim \Exp(\lambda = 0.002)$。问题是询问 $\p(Y < 4)$？ $$\begin{align*} \p(Y < 4) &= F_Y(4) && \text{CDF 衡量 $\p(Y < y)$} \\ &= 1 - e^{- \lambda \cdot y} && \text{指数的 CDF} \\ &= 1 - e^{- 0.002 \cdot 4} && \text{指数的 CDF} \\ &\approx 0.008 \end{align*}$$ 注意，使用 PDF 也可以回答这个问题，但需要求解一个积分。

## 指数分布是无记忆的

获取对“泊松过程”含义直观理解的一种方法是通过证明指数分布是["无记忆性"](https://en.wikipedia.org/wiki/Memorylessness)。这意味着过去事件的发生（或未发生）不会改变我们对下一次发生所需时间的信念。这可以正式表述如下。如果 $X \sim \Exp(\lambda)$，那么对于从开始到 $s$ 的时间间隔，以及随后的查询时间间隔 $t$：$$\p(X > s + t | X > s) = \p(X > t) $$ 这是我们能够证明的：$$\begin{align*} \p(X > s + t | X > s) &= \frac{\p(X > s + t \and X > s)}{\p(X > s)} && \text{条件概率的定义} \\ &= \frac{\p(X > s + t )}{\p(X > s)} && \text{因为 $X>s+t$ 意味着 $X>s$} \\ &= \frac{1 - F_X(s + t )}{1 - F_X(s)} && \text{累积分布函数的定义} \\ &= \frac{e^{-\lambda (s + t)}}{e^{-\lambda s}} && \text{通过指数分布的累积分布函数} \\ &= e^{-\lambda t} && \text{简化} \\ &= 1 - F_X(t) && \text{通过指数分布的累积分布函数} \\ &= \p(X > t) && \text{累积分布函数的定义} \\ \end{align*}$$
