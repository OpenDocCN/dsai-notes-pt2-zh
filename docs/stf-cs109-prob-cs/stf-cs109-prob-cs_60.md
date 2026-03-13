# 维度灾难

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/curse_of_dimensionality/#part3_examples/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/curse_of_dimensionality/#part3_examples/)

* * *

在机器学习中，就像计算机科学的许多领域一样，经常涉及高维点，高维空间具有一些令人惊讶的概率特性。

一个随机 *值* $X_i$ 是一个均匀分布（Uni(0, 1)）。

一个维度为 $d$ 的随机 *点* 是 $d$ 个随机值的列表：$[X_1 \dots X_d]$.

![图片](img/5dff7474c3d062d91ad5577d290f5e5f.png)

一个随机 *值* $X_i$ 如果 $X_i$ 小于 0.01 **或者** $X_i$ 大于 0.99，则认为它接近边缘。一个随机值接近边缘的概率是多少？

设 $E$ 为随机值接近边缘的事件。$P(E) = P(X_i < 0.01) + P(X_i > 0.99) = 0.02$

一个维度为 $3$ 的随机 *点* $[X_1, X_2, X_3]$ 如果其 *任何* 值接近边缘，则认为它接近边缘。一个三维点接近边缘的概率是多少？

该事件等价于点的 *任何* 维度都不接近边缘的补事件，即：$1 - (1 - P(E))³ = 1 - 0.98³ \approx 0.058$

一个维度为 $100$ 的随机 *点* $[X_1, \dots X_{100}]$ 如果其 *任何* 值接近边缘，则认为它接近边缘。一个 100 维点接近边缘的概率是多少？

同样地，它是：$1 - (1 - P(E))^{100} = 1 - 0.98^{100} \approx 0.867$。高维点有许多其他现象：例如，点之间的欧几里得距离开始收敛。
