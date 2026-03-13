# 维度诅咒

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/curse_of_dimensionality/#part2_examples/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/curse_of_dimensionality/#part2_examples/)

* * *

在机器学习中，就像计算机科学的许多领域一样，经常涉及高维点，高维空间具有一些令人惊讶的概率特性。

随机 *值* $X_i$ 是一个均匀分布（Uni(0, 1))。

维度为 $d$ 的随机 *点* 是 $d$ 个随机值的列表：$[X_1 \dots X_d]$。

![](img/5dff7474c3d062d91ad5577d290f5e5f.png)

当 $X_i$ 小于 0.01 **或者** $X_i$ 大于 0.99 时，随机 *值* $X_i$ 就接近边缘。随机值接近边缘的概率是多少？

设 $E$ 为随机值接近边缘的事件。$P(E) = P(X_i < 0.01) + P(X_i > 0.99) = 0.02$

维度为 $3$ 的随机 *点* $[X_1, X_2, X_3]$ 如果其 **任何** 值接近边缘，则该点接近边缘。一个三维点接近边缘的概率是多少？

事件相当于没有任何一个点的维度接近边缘的补集，即：$1 - (1 - P(E))³ = 1 - 0.98³ \approx 0.058$

维度为 $100$ 的随机 *点* $[X_1, \dots X_{100}]$ 如果其 **任何** 值接近边缘，则该点接近边缘。一个 100 维点接近边缘的概率是多少？

同样，它也是：$1 - (1 - P(E))^{100} = 1 - 0.98^{100} \approx 0.867$有许多其他高维点的现象：例如，点之间的欧几里得距离开始收敛。
