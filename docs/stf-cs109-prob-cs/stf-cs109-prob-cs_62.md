# 联邦党人文集作者身份

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/federalist/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/federalist/)

* * *

让我们编写一个程序来决定詹姆斯·麦迪逊或亚历山大·汉密尔顿是否写了联邦党人文集第 49 篇。这两个人都声称自己写了它，因此作者身份存在争议。首先，我们使用历史论文来估计 $p_i$，即汉密尔顿生成单词 $i$ 的概率（独立于所有先前和未来的单词选择）。同样，我们估计了 $q_i$，即麦迪逊生成单词 $i$ 的概率。对于每个单词 $i$，我们观察到该单词在联邦党人文集第 49 篇中出现的次数（我们称该次数为 $c_i$）。我们假设，在没有证据的情况下，该论文被麦迪逊或汉密尔顿写的可能性是相等的。

定义三个事件：$H$ 是汉密尔顿写了该论文的事件，$M$ 是麦迪逊写了该论文的事件，$D$ 是一个包含在联邦党人文集第 49 篇中观察到的单词集合的论文的事件。我们想知道 $P(H|D)$ 是否大于 $P(M|D)$。这相当于试图决定 $P(H|D)/P(M|D)$ 是否大于 1。

事件 $D|H$ 是一个由值 $p$ 多项式参数化的事件。事件 $D|M$ 也是一个多项式事件，这次由值 $q$ 参数化。

使用贝叶斯定理，我们可以简化所需的概率。 $$\begin{align*} \frac{P(H|D)}{P(M|D)} &= \frac{ \frac{P(D|H)P(H)}{P(D)} }{ \frac{P(D|M)P(M)}{P(D)}} = \frac{ P(D|H)P(H) }{ P(D|M)P(M)} = \frac{ P(D|H) }{ P(D|M)} \\ &= \frac{ { {n} \choose {c_1,c_2,\dots , c_m}} \prod_i p_i^{c_i} }{ { {n} \choose {c_1,c_2,\dots , c_m}}\prod_i q_i^{c_i}} = \frac{ \prod_i p_i^{c_i} }{ \prod_i q_i^{c_i}} \end{align*}$$

这听起来很棒！我们已经用我们已经估计的值的乘积来表示所需的概率陈述。然而，当我们将其输入到计算机中时，分子和分母都变成了零。许多接近零的数的乘积对于计算机来说太难表示了。为了解决这个问题，我们使用计算概率中的标准技巧：我们对两边应用对数并应用一些基本的对数规则。 $$\begin{align*} \text{log}\Big(\frac{P(H|D)}{P(M|D)}\Big) &= \text{log}\Big(\frac{ \prod_i p_i^{c_i} }{ \prod_i q_i^{c_i}} \Big) \\ &= \text{log}(\prod_i p_i^{c_i}) - \text{log}( \prod_i q_i^{c_i}) \\ &= \sum_i \text{log}(p_i^{c_i}) - \sum_i \text{log}(q_i^{c_i}) \\ &= \sum_i c_i\text{log}(p_i) - \sum_i c_i \text{log}(q_i) \end{align*}$$ 这个表达式是“数值稳定的”，我的计算机返回的结果是一个负数。我们可以使用指数来解决 $P(H|D)/P(M|D)$。由于负数的指数是一个小于 1 的数，这意味着 $P(H|D)/P(M|D)$ 小于 1。因此，我们得出结论，麦迪逊更有可能写了联邦党人文集第 49 篇。这是历史学家目前所持有的假设！
