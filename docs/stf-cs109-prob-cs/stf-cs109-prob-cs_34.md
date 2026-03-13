# 更多离散分布

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part2/more_discrete/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part2/more_discrete/)

* * *

简介页：章节即将推出！

**几何随机变量**

| 符号： | $X \sim \Geo(p)$ |
| --- | --- |
| 描述： | 达到一次成功所需的实验次数。假设每个实验都是独立的，成功的概率为 $p$。 |
| 参数： | $p \in [0, 1]$，单个实验成功的概率。 |
| 支持集： | $x \in \{1, \dots, \infty\}$ |
| PMF 公式： | $$\p(X=x) = (1-p)^{x-1} p$$ |
| 期望： | $\E[X] = \frac{1}{p}$ |
| 方差： | $\var(X) = \frac{1-p}{p²}$ |
| PMF 图： |

参数 $p$：

<canvas id="geometricPmf" style="max-height: 400px"></canvas>

**负二项随机变量**

| 符号： | $X \sim \NegBin(r, p)$ |
| --- | --- |
| 描述： | 达到 $r$ 次成功所需的实验次数。假设每个实验都是独立的，成功的概率为 $p$。 |
| 参数： | $r > 0$，我们期望的成功次数。$p \in [0, 1]$，单个实验成功的概率。 |
| 支持集： | $x \in \{r, \dots, \infty\}$ |
| PMF 公式： | $$\p(X=x) = {x - 1 \choose r - 1}p^r(1-p)^{x-r}$$ |
| 期望： | $\E[X] = \frac{r}{p}$ |
| 方差： | $\var(X) = \frac{r \cdot (1-p)}{p²}$ |
| PMF 图： |

参数 $r$：参数 $p$：

<canvas id="negBinomialPmf" style="max-height: 400px"></canvas>
