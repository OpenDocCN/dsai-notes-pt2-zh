# Naïve Bayes

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part5/naive_bayes/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part5/naive_bayes/)

* * *

Naive Bayes 是一种用于“分类任务”的机器学习算法。它做出了一个实质性的假设（称为朴素贝叶斯假设），即所有特征在给定分类标签的情况下彼此独立。这个假设是错误的，但它允许算法快速且高效，通常很有用。为了实现朴素贝叶斯，你需要学习如何训练你的模型以及如何使用它进行预测，一旦模型训练完成。

## 训练（又称参数估计）

训练的目标是估计所有 $0 < i \leq m$ 个特征的概率 $P(Y)$ 和 $P(X_i | Y)$。我们使用符号 $\hat{p}$ 来明确表示概率是一个估计值。

使用 MLE 估计：$$\begin{align*} \hat{p}(X_i = x_i | Y = y) = \frac{ (\text{训练样本中 $X_i = x_i$ 且 $Y = y$ 的数量})}{(\text{训练样本中 $Y = y$ 的数量})} \end{align*}$$

使用拉普拉斯 MAP 估计：$$\begin{align*} \hat{p}(X_i = x_i | Y = y) = \frac{ (\text{训练样本中 $X_i = x_i$ 且 $Y = y$ 的数量}) + 1 }{(\text{训练样本中 $Y = y$ 的数量}) + 2} \end{align*}$$

使用 MLE 估计训练 $Y$ 的先验概率：$$\begin{align*} \hat{p}(Y = y) = \frac{ (\text{训练样本中 $Y = y$ 的数量})}{(\text{训练样本数量})} \end{align*}$$

## 预测

对于 $\mathbf{x} = [x_1, x_2, \dots , x_m]$ 的例子，估计 $y$ 的值如下：$$\begin{align*} \hat{y} &= \argmax_{y = \{0, 1\}} \text{ } \log \hat{p}(Y = y) + \sum_{i=1}^m \log \hat{p}(X_i = x_i | Y = y) \end{align*}$$ 注意，对于足够小的数据集，你可能不需要使用 argmax 的对数版本。

## 理论

在分类的世界里，当我们做出预测时，我们希望选择 $y$ 的值，使其最大化 $P(Y=y|\mathbf{X})$。 $$\begin{align*} \hat{y} &= \argmax_{y = \{0, 1\}} P(Y = y|\mathbf{X} = \mathbf{X}) && \text{我们的目标}\\ &= \argmax_{y = \{0, 1\}} \frac{P(Y=y)P(\mathbf{X} =\mathbf{x}| Y = y)}{P(\mathbf{X} =\mathbf{x})} && \text{根据贝叶斯定理}\\ &= \argmax_{y = \{0, 1\}} P(Y=y)P(\mathbf{X} =\mathbf{x}| Y = y)) && \text{因为 $P(\mathbf{X} =\mathbf{x})$ 与 $Y$ 无关} \end{align*}$$

使用我们的训练数据，我们可以将 $\mathbf{X}$ 和 $Y$ 的联合分布解释为一个巨大的多项式分布，每个 $\mathbf{X}=\mathbf{x}$ 和 $Y=y$ 的组合都有一个不同的参数。例如，如果输入向量只有长度为 1。换句话说 $|\mathbf{x}| = 1$，$x$ 和 $y$ 可以取的值数量很少，比如二进制，这是一个完全合理的做法。我们可以使用 MLE 或 MAP 估计器来估计多项式分布，然后在我们的表中进行几次查找来计算 argmax。

当特征数量变得很大时，糟糕的情况就会出现。回想一下，我们的多项式分布需要为向量 $\mathbf{x}$ 和值 $y$ 的每个唯一组合估计一个参数。如果存在 $|\mathbf{x}| = n$ 个二进制特征，那么这种策略将需要 $\mathcal{O}(2^n)$ 的空间，并且可能有许多参数在没有与相应赋值匹配的训练数据的情况下被估计。

**朴素贝叶斯假设**

朴素贝叶斯假设是，给定 $y$，$\mathbf{x}$ 的每个特征都是相互独立的。朴素贝叶斯假设是错误的，但很有用。这个假设允许我们使用与特征大小成线性关系的空间和数据来做出预测：如果 $|\mathbf{x}| = n$，则为 $\mathcal{O}(n)$。这使我们能够训练和预测具有巨大特征空间的数据，例如具有互联网上每个单词指示符的特征空间。使用这个假设，预测算法可以被简化。 $$\begin{align*} \hat{y} &= \argmax\limits_{y = \{0, 1\}} \text{ }P(Y = y)P(\mathbf{X} = \mathbf{x}| Y = y) && \text{正如我们上次留下的}\\ &= \argmax\limits_{y = \{0, 1\}} \text{ } P(Y= y)\prod_i P(X_i = x_i| Y = y) &&\text{朴素贝叶斯假设}\\ &= \argmax\limits_{y = \{0, 1\}} \text{ } \log P(Y = y) + \sum_i \log P(X_i = x_i| Y = y) && \text{为了数值稳定性}\\ \end{align*}$$

在最后一步，我们利用了函数的 argmax 等于函数的 log 的 argmax 的性质。这个算法在训练和预测时都既快又稳定。
