# 帕累托分布的最大似然估计

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/mle_pareto/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/mle_pareto/)

* * *

你正在创建不同大小的圆形艺术作品，这些圆形遵循帕累托分布：

$X \sim \text{Pareto}(\alpha)$

帕累托分布由单个参数 $\alpha$ 定义，并具有概率密度函数

$$\begin{align*} f(x) = \frac{\alpha}{x^{\alpha + 1}} \end{align*}$$

你希望你的艺术作品中的 $\alpha$ 与你当地海滩的沙子中的 $\alpha$ 相匹配。你去了海滩，收集了 100 粒沙子并测量了它们的大小。将测量的半径称为 $x_1 , \dots, x_{100}$：

```py
 observations = [1.677, 3.812, 1.463, 2.641, 1.256, 1.678, 1.157, 
1.146, 1.323, 1.029, 1.238, 1.018, 1.171, 1.123, 1.074, 1.652, 
1.873, 1.314, 1.309, 3.325, 1.045, 2.271, 1.305, 1.277, 1.114, 
1.391, 3.728, 1.405, 1.054, 2.789, 1.019, 1.218, 1.033, 1.362, 
1.058, 2.037, 1.171, 1.457, 1.518, 1.117, 1.153, 2.257, 1.022, 
1.839, 1.706, 1.139, 1.501, 1.238, 2.53 , 1.414, 1.064, 1.097, 
1.261, 1.784, 1.196, 1.169, 2.101, 1.132, 1.193, 1.239, 1.518, 
2.764, 1.053, 1.267, 1.015, 1.789, 1.099, 1.25 , 1.253, 1.418, 
1.494, 1.015, 1.459, 2.175, 2.044, 1.551, 4.095, 1.396, 1.262, 
1.351, 1.121, 1.196, 1.391, 1.305, 1.141, 1.157, 1.155, 1.103, 
1.048, 1.918, 1.889, 1.068, 1.811, 1.198, 1.361, 1.261, 4.093, 
2.925, 1.133, 1.573]
```

根据你收集的数据，推导出 $\alpha$ 的最大似然估计公式。

### 编写对数似然函数

在最大似然估计（MLE）中，第一个主要目标是为我们数据构造一个对数似然表达式。为此，我们首先写出如果我们被告知 $\alpha$ 的值，我们的数据集看起来有多可能：\begin{aligned} L(\alpha) = f(x_1\dots x_n) = \prod_{i=1}^n\frac{\alpha}{x_i^{\alpha+1}} \end{aligned}

如果我们尝试优化对数似然，优化将变得容易得多：\begin{aligned} LL(\alpha) &= \log L(\alpha) = \log \prod_{i=1}^n\frac{\alpha}{x_i^{\alpha+1}} \\ &= \sum_{i=1}^n \log \frac{\alpha}{x_i^{\alpha+1}} \\ &= \sum_{i=1}^n \log \alpha - (\alpha +1)\log x_i \\ &= n \log \alpha - (\alpha +1) \sum_{i=1}^n\log x_i \\ \end{aligned}

### 选择 $\alpha$

我们将选择 $\alpha$ 以最大化对数似然。为此，我们需要 $\alpha$ 对 LL 的导数 \begin{aligned} \frac{\partial LL(\alpha)}{\partial \alpha} &= \frac{\partial LL(\alpha)}{\partial \alpha} \Big( n \log \alpha - (\alpha +1) \sum_{i=1}^n\log x_i \Big) \\ &= \frac{n}{\alpha} - \sum_{i=1}^n\log x_i \end{aligned}

一种优化方法是求导数并将其设为零：\begin{aligned} 0=\frac{n}{\alpha} - \sum_{i=1}^n\log x_i\\ \sum_{i=1}^n\log x_i = \frac{n}{\alpha} \\ \alpha = \frac{n}{ \sum\limits_{i=1}^n\log x_i} \end{aligned}

到目前为止，我们有一个可以用来计算 $\alpha$ 的公式！哇哦

### 将其放入代码

```py
import math

def estimate_alpha(observations):
    # This code computes the MLE estimate of alpha
    log_sum = 0
    for x_i in observations:
        log_sum += math.log(x_i)
    n = len(observations)
    return n / log_sum

def main():
    observations = [1.677, 3.812, 1.463, 2.641, 1.256, 1.678, 1.157, 1.146, 
    1.323, 1.029, 1.238, 1.018, 1.171, 1.123, 1.074, 1.652, 1.873, 1.314, 
    1.309, 3.325, 1.045, 2.271, 1.305, 1.277, 1.114, 1.391, 3.728, 1.405, 
    1.054, 2.789, 1.019, 1.218, 1.033, 1.362, 1.058, 2.037, 1.171, 1.457, 
    1.518, 1.117, 1.153, 2.257, 1.022, 1.839, 1.706, 1.139, 1.501, 1.238, 
    2.53 , 1.414, 1.064, 1.097, 1.261, 1.784, 1.196, 1.169, 2.101, 1.132, 
    1.193, 1.239, 1.518, 2.764, 1.053, 1.267, 1.015, 1.789, 1.099, 1.25 , 
    1.253, 1.418, 1.494, 1.015, 1.459, 2.175, 2.044, 1.551, 4.095, 1.396, 
    1.262, 1.351, 1.121, 1.196, 1.391, 1.305, 1.141, 1.157, 1.155, 1.103, 
    1.048, 1.918, 1.889, 1.068, 1.811, 1.198, 1.361, 1.261, 4.093, 2.925, 
    1.133, 1.573]
    alpha = estimate_alpha(observations)
    print(alpha)

if __name__ == '__main__':
    main()
```
