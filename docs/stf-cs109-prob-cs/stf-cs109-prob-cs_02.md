# 核心概率参考

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/intro/core_probability_ref/`](https://chrispiech.github.io/probabilityForComputerScientists/en/intro/core_probability_ref/)

* * *

***定义***：概率的经验定义

任何事件 $E$ 的概率可以这样定义：

$$ \p(E) = \lim_{n \rightarrow \infty} \frac {\text{count}(E)} {n} $$

其中 $\text{count}(E)$ 是 $E$ 在 $n$ 次实验中发生的次数。

***定义：*** 核心恒等式

对于事件 $E$ 和样本空间 $S$

| $0 ≤ \p(E) ≤ 1$ | 所有概率都是介于 0 和 1 之间的数字。 |
| --- | --- |
| **$\p(S) = 1$** | 所有结果必须来自样本空间。 |
| $\P(E) = 1 - \P(E^\c)$ | 从事件的补集中计算事件发生的概率。 |

***定义***：等可能结果的概率

如果 $S$ 是一个具有等可能结果的样本空间，对于 $S$ 中结果的一个子集事件 $E$：$$ \begin{align} \p(E) &= \frac{\text{在 $E$ 中的结果数量}}{\text{在 $S$ 中的结果数量}} = \frac{|E|}{|S|} \end{align} $$***定义***：条件概率。

在事件 $F$ 已经发生的情况下（即条件为）事件 $E$ 的概率：$$ \p(E |F) = \frac{\p(E \and F)}{\p(F)} $$

***定义***：相互独立事件的**或**的概率

如果两个事件 $E$ 和 $F$ 是互斥的，那么 $E$ 或 $F$ 发生的概率是：$$ \p(E \or F) = \p(E) + \p(F) $$

对于 $n$ 个事件 $E_1, E_2, \dots E_n$，其中每个事件都是相互独立的（换句话说，没有结果在多个事件中）。那么：$$ \p(E_1 \or E_2 \or \dots \or E_n) = \p(E_1) + \p(E_2) + \dots + \p(E_n) = \sum_{i=1}^n \p(E_i) $$

***定义***：**或**的通用概率（包含-排除法则）

对于任意两个事件 $E$ 和 $F$：$$ \p(E \or F) = \p(E) + \p(F) − \p(E \and F) $$

对于三个事件，$E$、$F$ 和 $G$，公式如下：$$ \begin{align} \p(E \or F \or G) =& \text{ }\p(E) + \p(F) + \p(G) \\ & −\p(E \and F) − \p(E \and G)−\p(F \and G) \\ & +\p(E \and F \and G) \end{align} $$

对于超过三个事件，请参阅概率或章节。***定义***：独立事件的**和**的概率。

如果两个事件：$E$、$F$ 是独立的，那么 $E$ 和 $F$ 同时发生的概率是：$$ \p(E \and F) = \p(E) \cdot \p(F) $$

对于 $n$ 个相互独立的事件 $E_1, E_2, \dots E_n$：$$ \p(E_1 \and E_2 \and \dots \and E_n) = \prod_{i=1}^n \p(E_i) $$

***定义***：**和**的通用概率（链式法则）

对于任意两个事件 $E$ 和 $F$：$$ \p(E \and F) = \p(E | F) \cdot \p(F) $$

对于 $n$ 个事件 $E_1, E_2, \dots E_n$：$$ \begin{align} \p(E_1 \and E_2 \and \dots \and E_n) = &\p(E_1) \cdot \p(E_2|E_1) \cdot \p(E_3 |E_1 \and E_2) \dots \\ &\p(E_n|E_1 \dots E_{n−1}) \end{align} $$

***定义***：全概率公式

对于任意两个事件 $E$ 和 $F$：$$ \begin{align} \p(E) &= \p(E \and F) + \p(E \and F\c)\\ &=\p(E | F) \p(F) + \p(E | F\c) \p(F\c) \end{align} $$

对于互斥事件：$B_1, B_2, \dots B_n$，其中样本空间中的每个结果都落在这些事件之一中：$$ \begin{align} \p(E) &= \sum_{i=1}^n \p(E \and B_i) && \text{扩展我们的观察}\\ &= \sum_{i=1}^n \p(E | B_i) \p(B_i) && \text{对每个项使用链式法则} \end{align} $$

***定义***：贝叶斯定理

贝叶斯定理最常见的形式是**贝叶斯定理经典版**：$$ \p(B|E) = \frac{\p(E | B) \cdot \p(B)}{\p(E)} $$

贝叶斯定理与全概率定律相结合：$$ \p(B|E) = \frac{\p(E | B) \cdot \p(B)}{\p(E|B)\cdot \p(B) + \p(E|B\c) \cdot \p(B\c)} $$
