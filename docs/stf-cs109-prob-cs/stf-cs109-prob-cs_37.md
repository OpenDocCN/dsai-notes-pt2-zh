# 均匀分布

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part2/uniform/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part2/uniform/)

* * *

所有连续随机变量中最基本的是均匀随机变量，它在范围（$\alpha, \beta$）内以相同的可能性取任何值。$X$ 是一个 *均匀随机变量*（$X \sim \Uni(\alpha, \beta)$），如果它具有以下概率密度函数：$$\begin{align*} f(x) = \begin{cases} \frac{1}{\beta - \alpha} &\text{when } \alpha \leq x \leq \beta \\ 0 & \text{otherwise} \end{cases} \end{align*}$$

注意密度 $1/(\beta - \alpha$) 不论 $x$ 的值如何都是相同的。这使得密度均匀。那么为什么概率密度函数是 $1/(\beta - \alpha)$ 而不是 1 呢？这就是使得对所有可能输入的积分等于 1 的常数。

**均匀随机变量**

| 符号: | $X \sim \Uni(\alpha, \beta)$ |
| --- | --- |
| 描述: | 一个连续随机变量，其值在 $\alpha$ 和 $\beta$ 之间以相同的可能性出现 |
| 参数: | $\alpha \in \R$, 变量的最小值。$\beta \in \R$, $\beta > \alpha$, 变量的最大值。 |
| 支持集: | $x \in [\alpha, \beta]$ |
| 概率密度函数方程: | $$f(x) = \begin{cases} \frac{1}{\beta - \alpha} && \text{for }x \in [\alpha, \beta]\\ 0 && \text{else} \end{cases}$$ |
| 累积分布函数方程: | $$F(x) = \begin{cases} \frac{x - \alpha}{\beta - \alpha} && \text{for }x \in [\alpha, \beta]\\ 0 && \text{for } x < \alpha \\ 1 && \text{for } x > \beta \end{cases}$$ |
| 期望值: | $\E[X] = \frac{1}{2}(\alpha + \beta)$ |
| 方差: | $\var(X) = \frac{1}{12}(\beta - \alpha)²$ |
| 概率密度函数图: |

参数 $\alpha$: 参数 $\beta$:

<canvas id="uniPdf" style="max-height: 400px"></canvas>

**示例:** 你正在跑向公交车站。你不知道公交车确切什么时候到达。你认为 2 点到 2:30 之间的任何时间到达的可能性都是相同的。你在下午 2:15 到达。等待时间小于 5 分钟的概率是多少？

设 $T$ 为公交车在下午 2 点后到达的时间（以分钟计）。因为我们认为在这个范围内所有时间到达的可能性都是相同的，所以 $T \sim \Uni(\alpha = 0, \beta = 30)$。等待 5 分钟的概率等于公交车在 2:15 到 2:20 之间到达的概率。换句话说 $\p(15 < T < 20)$: $$\begin{align*} \p(\text{Wait under 5 mins}) &= \p(15 < T < 20) \\ &= \int_{15}^{20} f_T(x) \partial x \\ &= \int_{15}^{20} \frac{1}{\beta - \alpha} \partial x \\ \\ &= \frac{1}{30} \partial x \\ \\ &= \frac{x}{30}\bigg\rvert_{15}^{20} \\ &= \frac{20}{30} - \frac{15}{30} = \frac{5}{30} \end{align*}$$

我们可以求出均匀随机变量 $X$ 在范围 $a$ 到 $b$ 内的概率的封闭形式，假设 $\alpha \leq a \leq b \leq \beta$：$$\begin{align*} \P(a \leq X \leq b) &= \int_a^b f(x) \d x \\ &= \int_a^b \frac{1}{\beta - \alpha} \d x \\ &= \frac{ b - a }{ \beta - \alpha } \end{align*}$$
