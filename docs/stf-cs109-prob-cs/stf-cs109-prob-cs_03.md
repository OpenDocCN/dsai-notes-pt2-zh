# 随机变量参考

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/intro/all_distributions/`](https://chrispiech.github.io/probabilityForComputerScientists/en/intro/all_distributions/)

* * *

### 离散随机变量

**伯努利随机变量**

| 符号: | $X \sim \Ber(p)$ |
| --- | --- |
| 描述: | 一个布尔变量，以概率 $p$ 为 1 |
| 参数: | $p$，$X=1$ 的概率。 |
| 支持集: | $x$ 要么是 0，要么是 1 |
| PMF 方程: | $\p(X=x) = \begin{cases} p && \text{if }x = 1\\ 1-p && \text{if }x = 0 \end{cases}$ |
| PMF (平滑): | $\p(X=x) = p^x(1-p)^{1-x}$ |
| 期望: | $\E[X] = p$ |
| 方差: | $\var(X) = p (1-p)$ |
| PMF 图: |

参数 $p$:

<canvas id="bernoulliPmf" style="max-height: 400px"></canvas>

**二项式随机变量**

| 符号: | $X \sim \Bin(n, p)$ |
| --- | --- |
| 描述: | 在 $n$ 个相同、独立的实验中成功的次数，每个实验成功的概率为 $p$。 |
| 参数: | $n \in \{0, 1, \dots\}$，实验次数。$p \in [0, 1]$，单个实验成功的概率。 |
| 支持集: | $x \in \{0, 1, \dots, n\}$ |
| PMF 方程: | $$\p(X=x) = {n \choose x}p^x(1-p)^{n-x}$$ |
| 期望: | $\E[X] = n \cdot p$ |
| 方差: | $\var(X) = n \cdot p \cdot (1-p)$ |
| PMF 图: |

参数 $n$: 参数 $p$:

<canvas id="binomialPmf" style="max-height: 400px"></canvas>

**泊松随机变量**

| 符号: | $X \sim \Poi(\lambda)$ |
| --- | --- |
| 描述: | 在固定时间段内发生的事件数量，如果 (a) 事件以恒定的平均速率发生，并且 (b) 事件的发生与上次事件的时间无关。 |
| 参数: | $\lambda \in \mathbb{R}^{+}$，恒定的平均速率。 |
| 支持集: | $x \in \{0, 1, \dots\}$ |
| PMF 方程: | $$\p(X=x) = \frac{\lambda^xe^{-\lambda}}{x!}$$ |
| 期望: | $\E[X] = \lambda$ |
| 方差: | $\var(X) = \lambda$ |
| PMF 图: |

参数 $\lambda$:

<canvas id="poissonPmf" style="max-height: 400px"></canvas>

**几何随机变量**

| 符号: | $X \sim \Geo(p)$ |
| --- | --- |
| 描述: | 达到成功所需的实验次数。假设每个实验是独立的，成功的概率为 $p$。 |
| 参数: | $p \in [0, 1]$, 单个实验成功的概率。 |
| 支持集: | $x \in \{1, \dots, \infty\}$ |
| PMF 方程: | $$\p(X=x) = (1-p)^{x-1} p$$ |
| 期望: | $\E[X] = \frac{1}{p}$ |
| 方差: | $\var(X) = \frac{1-p}{p²}$ |
| PMF 图: |

参数 $p$:

<canvas id="geometricPmf" style="max-height: 400px"></canvas>

**负二项式随机变量**

| 符号: | $X \sim \NegBin(r, p)$ |
| --- | --- |
| 描述: | 达到 $r$ 次成功所需的实验次数。假设每个实验是独立的，成功的概率为 $p$。 |
| 参数: | $r > 0$，我们等待的成功次数。$p \in [0, 1]$，单个实验成功的概率。 |
| 支持集: | $x \in \{r, \dots, \infty\}$ |
| PMF 方程： | $$\p(X=x) = {x - 1 \choose r - 1}p^r(1-p)^{x-r}$$ |
| 期望： | $\E[X] = \frac{r}{p}$ |
| 方差： | $\var(X) = \frac{r \cdot (1-p)}{p²}$ |
| PMF 图： |

参数 $r$：参数 $p$：

<canvas id="negBinomialPmf" style="max-height: 400px"></canvas>

### 连续随机变量

**均匀随机变量**

| 符号： | $X \sim \Uni(\alpha, \beta)$ |
| --- | --- |
| 描述： | 一个连续随机变量，其值在 $\alpha$ 和 $\beta$ 之间以相同的可能性取值。 |
| 参数： | $\alpha \in \R$，变量的最小值。$\beta \in \R$，$\beta > \alpha$，变量的最大值。 |
| 支持集： | $x \in [\alpha, \beta]$ |
| PDF 方程： | $$f(x) = \begin{cases} \frac{1}{\beta - \alpha} && \text{for }x \in [\alpha, \beta]\\ 0 && \text{else} \end{cases}$$ |
| CDF 方程： | $$F(x) = \begin{cases} \frac{x - \alpha}{\beta - \alpha} && \text{for }x \in [\alpha, \beta]\\ 0 && \text{for } x < \alpha \\ 1 && \text{for } x > \beta \end{cases}$$ |
| 期望： | $\E[X] = \frac{1}{2}(\alpha + \beta)$ |
| 方差： | $\var(X) = \frac{1}{12}(\beta - \alpha)²$ |
| PDF 图： |

参数 $\alpha$：参数 $\beta$：

<canvas id="uniPdf" style="max-height: 400px"></canvas>

**指数随机变量**

| 符号： | $X \sim \Exp(\lambda)$ |
| --- | --- |
| 描述： | 如果（a）事件以恒定的平均速率发生，并且（b）它们的发生与自上次事件以来经过的时间无关，则直到下一次事件的时间。 |
| 参数： | $\lambda \in \mathbb{R}^{+}$，恒定的平均速率。 |
| 支持集： | $x \in \mathbb{R}^+$ |
| PDF 方程： | $$f(x) = \lambda e^{-\lambda x}$$ |
| CDF 方程： | $$F(x) = 1 - e^{-\lambda x}$$ |
| 期望： | $\E[X] = 1/\lambda$ |
| 方差： | $\var(X) = 1/\lambda²$ |
| PDF 图： |

参数 $\lambda$:

<canvas id="exponentialPdf" style="max-height: 400px"></canvas>

**正态（又称高斯）随机变量**

| 符号： | $X \sim \N(\mu, \sigma²)$ |
| --- | --- |
| 描述： | 一种常见且自然发生的分布。 |

| 参数：| $\mu \in \mathbb{R}$，均值。$\sigma² \in \mathbb{R}$，方差。|

|

| 支持集： | $x \in \mathbb{R}$ |
| --- | --- |
| PDF 方程： | $$f(x) = \frac{1}{\sigma \sqrt{2 \pi}} e^{-\frac{1}{2}\Big(\frac{x-\mu}{\sigma}\Big)²}$$ |
| CDF 方程： | $$\begin{align} F(x) &= \phi(\frac{x-\mu}{\sigma}) && \text{Where $\phi$ is the CDF of the standard normal} \end{align}$$ |
| 期望： | $\E[X] = \mu$ |
| 方差： | $\var(X) = \sigma²$ |
| PDF 图： |

参数 $\mu$：参数 $\sigma$：

<canvas id="normalPdf" style="max-height: 400px"></canvas>

**贝塔随机变量**

| 符号： | $X \sim \Beta(a, b)$ |
| --- | --- |
| 描述： | 在观察到 $a-1$ 次成功和 $b- 1$ 次失败后，从二项分布中得到的概率 $p$ 的信念分布。 |
| 参数： | $a > 0$，成功次数 + 1 $b > 0$，失败次数 + 1 |
| 支持集： | $x \in [0, 1]$ |
| PDF 方程： | $f(x) = B(a,b) \cdot x^{a-1} \cdot (1-x)^{b-1}$ 其中 $B(a,b) = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a,b)}$ |
| CDF 方程： | 没有封闭形式 |
| 期望： | $\E[X] = \frac{a}{a+b}$ |
| 方差： | $\var(X) = \frac{ab}{(a+b)²(a+b+1)}$ |
| PDF 图： |

参数 $a$：参数 $b$：

<canvas id="betaPdf" style="max-height: 400px"></canvas>
