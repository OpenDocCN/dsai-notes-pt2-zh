# 算法分析

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part4/algorithmic_analysis/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part4/algorithmic_analysis/)

* * *

在本节中，我们将使用概率来分析代码。具体来说，我们将计算代码的期望：期望运行时间、期望结果值等。我们将关注期望的原因是它有几个很好的性质。我们迄今为止看到的最有用的性质之一是，期望的和是期望的和，*无论*随机变量之间是否相互独立。在本节中，我们将看到更多有用的性质，包括总期望定律，这在分析代码时也非常有用：

**总期望定律**

总期望定律为你提供了一种在计算 $\E[X|Y=y]$（其中 $Y$ 是另一个随机变量）更容易的情况下计算 $\E[X]$ 的方法：$$\begin{align*} \E[X] &= \sum_y \E[X|Y=y] \p(Y=y) \end{align*}$$

## 分布式文件系统

想象一下从斯坦福的电脑上加载一个大型文件的任务，通过互联网。你的文件存储在一个分布式文件系统中。在分布式文件系统中，你的文件最接近的实例可能在世界各地不同位置的几台电脑之一。想象你知道文件位于几个位置 $l$ 之一的概率：$\P(L=l)$，以及对于每个位置，获取文件所需的期望时间 $T$，$\E[T|L=l]$，假设文件就在那个位置：

| 位置 | $P(L = l)$ | $\E[T | L = l]$ |
| --- | --- | --- | --- |
| 南加州 | 0.5 | 0.3 秒 |
| 纽约 | 0.2 | 20.7 秒 |
| 日本 | 0.3 | 96.3 秒 |

总期望定律为计算 $\E[T]$ 提供了一种直接的方法：

$$\begin{align*} \E[T] &= \sum_l \E[T|L=l] \p(L=l)\\ &= 0.5 \cdot 0.3 + 0.2 \cdot 20.7 + 0.3 \cdot 96.7\\ &= 33.3 \text{ 秒} \end{align*}$$

## 递归代码的玩具示例

在理论计算机科学中，有很多时候你想分析算法的期望运行时间。为了练习这种技术，让我们尝试解决一个简单的递归函数。设 Y 为 `recurse()` 返回的值。$E[Y]$ 是什么？

```py
def recurse():
    x = random.choice([1, 2, 3])  # Equally likely values
	if x == 1: 
		return 3;
	else if (x == 2):
		return 5 + recurse()
	else:
		return 7 + recurse()
```

为了解决这个问题，我们需要使用总期望定律，将 $X$ 作为背景变量。

$$\begin{align*} \E[Y] = &\sum_{i \in \{1,2,3\}} \E[Y|X=i] \P(X=i)\\ =&\E[Y|X=1] \P(X=1) \\& + \E[Y|X=2] \P(X=2) \\&+ \E[Y|X=3] \P(X=3) \end{align*}$$ 我们知道对于 $x \in \{1,2,3\}$，概率 $\P(X=x) = \frac{1}{3}$。我们如何计算像 $\E[Y|X=2]$ 这样的值呢？嗯，那是在 $X=2$ 的世界里你的期望回报。在这种情况下，你将返回 5 + recurse()。这个期望是 $5 + \E[Y]$。将每个情况下的类似结果代入，我们可以继续我们的解决方案：$$\begin{align*} E[Y|X=1] &= 3\\ E[Y|X=2] &= 5 + \E[Y]\\ E[Y|X=3] &= 7 + \E[Y]\\ \end{align*}$$ 现在我们可以将值代入总期望定律：$$\begin{align*} \E[Y] = &\sum_{i \in \{1,2,3\}} \E[Y|X=i] \P(X=i)\\ =&\E[Y|X=1] \P(X=1) \\& + \E[Y|X=2] \P(X=2) \\&+ \E[Y|X=3] \P(X=3) \\ =&3 \cdot 1/3 \\ &+ (5 + \E[Y]) \cdot 1/3\\ &+ (7 + \E[Y]) \cdot 1/3\\ = &(15 + 2\E[Y]) \cdot 1/3 \\ 1/3 \cdot \E[Y] = &5 \\ \E[Y] = &15 \end{align*}$$

## 总期望定律的证明

让我们来证明总期望定律。在这个证明中，我们将从 $\sum_y E[X|Y=y]P(Y=y)$ 开始，并展示它等于 $E[X]$。我们的第一步将是展开 $E[X|Y=y]$。证明的其余部分将只是代数运算：

$$\begin{align*}\sum_y& E[X|Y=y]P(Y=y) \\ &= \sum_y\sum_x x P(X =x | Y = y) P(Y = y) \\ &= \sum_y\sum_x x P(X =x , Y = y)  \\ &= \sum_x\sum_y x P(X =x , Y = y)  \\ &= \sum_x x \sum_y  P(X =x , Y = y)  \\ &= \sum_x x P(X =x)  \\ &= E[X]\end{align*}$$
