# 分布之间的距离

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part4/divergence/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part4/divergence/)

* * *

这里有一个重要的问题！你如何量化两个分布之间的差异？换句话说，如果我有两个概率质量函数，我能计算出一个数字来表示它们彼此之间有多大的差异？这里有三种合理的方式来量化分布之间的距离：

### 总变差距离

遍历所有可能的值并计算概率的绝对差异。

***定义：*** 总变差距离

设 $X$ 和 $Y$ 为离散随机变量

$$\begin{align*} \text{TV}(X, Y) = \frac{1}{2} \sum_{i} |\P(X = i) - \P(Y = i)| \end{align*}$$

### 地球迁移距离

想象一个分布是一堆泥土。要让它看起来和另一个分布一样，需要做多少工作？也称为 Wasserstein 度量。

这个值非常有意义，但它没有封闭形式的方程。相反，它通过求解线性规划来计算。如果随机变量可以取的值的范围大小为 $n$，线性规划的计算时间为 $O(n³ \cdot \log n)$，这非常慢。

### 库尔巴克-莱布勒散度

设 $X$ 和 $Y$ 为离散随机变量。计算当实际概率质量函数为 $X$ 时，使用 $Y$ 作为概率质量函数带来的“额外惊喜”的期望值。

***定义：*** 库尔巴克-莱布勒散度

设 $X$ 和 $Y$ 为离散随机变量

$$\begin{align*} \text{KL}(X, Y) &= \sum_{x \in X} \text{ExcessSurprise}(x) \cdot P(X=x) \\ &= \sum_{x \in X} \Big[\text{Surprise}_X(x) - \text{Surprise}_Y(x)\Big] \cdot P(X=x) \\ &= \sum_{x \in X} \Big[\log_2\frac{1}{P(Y=x)} - \log_2 \frac{1}{P(X=x)}\Big] \cdot P(X=x) \\ &= \sum_{x \in X} - \log_2 P(Y=x) + \log_2 P(X=x) \cdot P(X=x) \\ &= \sum_{x \in X} \log_2 \frac{P(X=x)}{P(Y=x) } \cdot P(X=x) \\ \end{align*}$$

这里是计算每年观察到的飓风概率质量函数与预测的泊松分布差异的示例代码

```py
from scipy import stats
import math

def kl_divergence(predicted_lambda, observed_pmf):
    """
    We predicted that the number of hurricanes would be 
    X ~ Poisson(predicted_lambda) and observed a real world
    number of hurricanes Y ~ observed_pmf
    """
    X = stats.poisson(predicted_lambda)
    divergence = 0
    # loop over all the values of hurricanes
    for i in range(0, 40):
      pr_X_i = X.pmf(i)
      pr_Y_i = observed_pmf[i]
      excess_surprise_i = math.log(pr_X_i / pr_Y_i)
      divergence += excess_surprise_i * pr_X_i
    return divergence 
```
