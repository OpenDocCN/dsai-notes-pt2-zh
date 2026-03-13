# 最大后验概率

> [`chrispiech.github.io/probabilityForComputerScientists/en/part5/map/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part5/map/)

* * *

MLE（最大似然估计）很棒，但它并不是估计参数的唯一方法！本节介绍另一种算法，最大后验概率（Maximum A Posteriori，MAP）。MAP 的范式是我们应该选择最有可能的数据对应的参数值。乍一看，这似乎与 MLE 相同，然而请注意，MLE 选择的是使数据最有可能的参数值。形式上，对于独立同分布（IID）的随机变量 $X_1, \dots, X_n$：$$\begin{align*} \theta_{\text{MAP}} =& \underset{\theta}{\operatorname{argmax }} \text{ } f(\Theta = \theta | X_1=x_1, X_2=x_2, \dots X_n=x_n) \end{align*}$$在上面的方程中，我们试图计算给定观测随机变量的未观测随机变量的条件概率。当这种情况发生时，想想贝叶斯定理！使用贝叶斯定理的连续版本展开函数 $f$。$$\begin{align*} \theta_{\text{MAP}} =& \underset{\theta}{\operatorname{argmax }} \text{ } f(\Theta = \theta | X_1=x_1, X_2=x_2, \dots X_n=x_n) \\ =& \underset{\theta}{\operatorname{argmax }} \text{ } \frac{f(X_1=x_1, X_2=x_2, \dots, X_n=x_n |\Theta = \theta) f(\Theta = \theta)}{f(X_1=x_1, X_2=x_2, \dots X_n=x_n)} && \text{贝叶斯定理} \end{align*}$$请注意，$f$ 都是概率密度函数或概率质量函数。现在我们将利用两个观察结果。首先，假设数据是 IID 的，因此我们可以分解给定 $\theta$ 的数据密度。其次，分母相对于 $\theta$ 是常数。因此，它的值不影响 argmax，我们可以省略这一项。数学上：$$\begin{align*} \theta_{\text{MAP}} =& \underset{\theta}{\operatorname{argmax }} \text{ } \frac{f(\Theta = \theta) \cdot \prod_{i=1}^n f(X_i =x_i| \Theta = \theta) }{f(X_1 = x_1, X_2 = x_2, \dots X_n = x_n)} && \text{由于样本是 IID 的}\\ =& \underset{\theta}{\operatorname{argmax }} \text{ } f(\Theta = \theta) \cdot\prod_{i=1}^n f(X_i =x_i |\Theta = \theta) && \text{分母相对于 $\theta$ 是常数} \end{align*}$$与之前一样，找到 MAP 函数的对数的 argmax 将更方便，这给出了参数 MAP 估计的最终形式。 $$\begin{align*} \theta_{\text{MAP}} =& \underset{\theta}{\operatorname{argmax }} \text{ } \left( \log f(\Theta = \theta) + \sum_{i=1}^n \log(f(X_i =x_i|\Theta = \theta)) \right) \end{align*}$$使用贝叶斯术语，MAP 估计是 $\theta$ 的“后验”分布的众数。如果你将这个方程与 MLE 方程并排放置，你会注意到 MAP 是相同函数的 argmax 加上一个对数先验项。

## 参数先验

为了准备好 MAP 估计的世界，我们需要复习我们的分布。我们需要为我们的不同参数中的每一个找到一个合理的分布。例如，如果你正在预测泊松分布，$\lambda$ 的先验分布应该选择哪种合适的随机变量类型？

对于先验分布的一个期望是，得到的后验分布具有相同的函数形式。我们称这些为“共轭”先验。在你多次更新你的信念的情况下，共轭先验使得在数学方程中进行编程变得容易得多。

这里是一个不同参数及其通常用于其先验分布的分布列表：$$\begin{align*} &\text{参数 }&& \text{分布}\\ &\text{伯努利 } p && \text{Beta}\\ &\text{二项式 } p && \text{Beta}\\ &\text{泊松 } \lambda && \text{Gamma}\\ &\text{指数 } \lambda && \text{Gamma}\\ &\text{多项式 } p_i && \text{Dirichlet}\\ &\text{正态 } \mu && \text{Normal}\\ &\text{正态 } \sigma² && \text{Inverse Gamma} \end{align*}$$ 你只需要对新的分布有一个高层次的理解。你不需要了解逆伽马分布。我包括它是为了完整性。

用于表示你对随机变量“先验”信念的分布通常会具有自己的参数。例如，Beta 分布使用两个参数 $(a, b)$ 定义。我们是否必须使用参数估计来评估 $a$ 和 $b$？不。这些参数被称为“超参数”。这是一个我们保留用于在运行参数估计之前固定的模型参数的术语。在你运行 MAP 之前，你将决定 $(a, b)$ 的值。

## Dirichlet

Dirichlet 分布以与多项式分布推广伯努利分布相同的方式推广了 Beta 分布。一个服从 Dirichlet 分布的随机变量 $X$ 被参数化为 $X \sim \text{Dirichlet}(a_1, a_2, \dots, a_m)$。该分布的 PDF 为：$$\begin{align*} f(X_1 = x_1, X_2 = x_2, \dots, X_m = x_m) = K \prod_{i=1}^m x_i^{a_i - 1} \end{align*}$$ 其中 $K$ 是归一化常数。

你可以直观地理解 Dirichlet 分布的超参数：想象你已经看到了 $\sum_{i=1}^m a_i - m$ 个虚拟试验。在这些试验中，你有 $(a_i - 1)$ 个值为 $i$ 的结果。作为一个例子，考虑估计一个六面偏斜骰子（每个面是不同形状）得到不同数字的概率。我们将通过反复掷骰子 $n$ 次来估计掷出每个面的概率。这将产生 $n$ 个独立同分布的样本。对于 MAP 模式，我们需要为每个参数 $p_1 \dots p_6$ 的信念设定一个先验。我们希望表达出我们轻信每次掷骰子的概率是相等的。

在你掷骰子之前，让我们想象你已经掷了六次骰子，并且得到了每种可能值的一个。因此，“先验”分布将是 Dirichlet($2, 2, 2, 2, 2, 2$)。在观察到 $n_1 + n_2 + \dots + n_6$ 个新的试验结果，其中 $n_i$ 是结果 $i$ 的次数后，“后验”分布是 Dirichlet($2 + n_1, \dots 2 + n_6$)。使用代表每个结果的一个想象观察的先验称为“拉普拉斯平滑”，并且它保证了你的概率不会是 0 或 1。

## Gamma

Gamma($k, \theta$) 分布是泊松分布 $\lambda$ 参数的共轭先验分布（它也是指数分布的共轭分布，但我们将不会深入探讨这一点）。

超参数可以被解释为：你在 $\theta$ 个想象的时间段内观察到了 $k$ 个总想象事件。在接下来的 $t$ 个时间段内观察到 $n$ 个事件后，后验分布是 Gamma($k + n, \theta + t$)。

例如，Gamma(10, 5) 将代表在 5 个时间段内观察到 10 个想象事件。这就像想象一个有某种置信度的 2 的速率。如果我们以那个 Gamma 作为先验，然后在接下来的 2 个时间段内观察到 11 个事件，我们的后验是 Gamma(21,7)，这相当于一个更新的速率为 3。
