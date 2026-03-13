# 参数估计

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part5/parameter_estimation/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part5/parameter_estimation/)

* * *

我们已经学习了多种随机变量的分布，所有这些分布都有参数：当你定义随机变量时作为输入提供的数字。到目前为止，当我们处理随机变量时，要么明确告知参数的值，要么通过理解生成随机变量的过程来推断这些值。

如果我们不知道参数的值，也无法从自己的专业知识中估计它们，那会怎样？如果我们知道的不是随机变量，而是大量使用相同潜在分布生成的数据示例，那又会怎样？在本章中，我们将学习从数据中估计参数的正式方法。

这些思想对于人工智能至关重要。几乎所有现代机器学习算法都是这样工作的：(1)指定一个具有参数的概率模型。(2)从数据中学习这些参数的值。

## 参数

在我们深入参数估计之前，首先让我们回顾一下参数的概念。给定一个模型，参数是产生实际分布的数字。在伯努利随机变量的情况下，单个参数是值 $p$。在均匀随机变量的情况下，参数是定义最小值和最大值的 $a$ 和 $b$ 值。以下是随机变量及其对应参数的列表。从现在开始，我们将使用符号 $\theta$ 来表示所有参数的向量：

| Distribution | Parameters |
| --- | --- |
| Bernoulli($p$) | $\theta = p$ |
| Poisson($\lambda$) | $\theta = \lambda$ |
| Uniform($a, b$) | $\theta = [a, b]$ |
| Normal($\mu, \sigma²$) | $\theta = [\mu, \sigma²]$ |

在现实世界中，通常你不知道“真实”的参数，但你能够观察到数据。接下来，我们将探讨如何使用数据来估计模型参数。

估计参数值的方法不止一种。主要有两种思想流派：最大似然估计（MLE）和最大后验估计（MAP）。这两种思想流派都假设你的数据是独立同分布（IID）的样本：$X_1, X_2, \dots X_n$。
