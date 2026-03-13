# 机器学习

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part5/machine_learning/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part5/machine_learning/)

* * *

机器学习是计算机科学的一个子领域，它使计算机能够在没有明确编程的情况下执行任务。机器学习领域包含多个不同的任务，以及多种不同的“学习”算法。在本章中，我们将重点关注分类以及两种经典的分类算法：朴素贝叶斯和逻辑回归。

## 分类

在分类任务中，你的任务是使用带有特征/标签对 ($\mathbf{x}$, y) 的训练数据来估计一个函数 $\hat{y} = g(\mathbf{x})$。这个函数可以用来进行预测。在分类中，$y$ 的值取自一个 \textbf{离散} 的数值集合。因此，我们通常选择 $g(\mathbf{x}) = \underset{y}{\operatorname{argmax }}\text{ }\hat{P}(Y=y|\mathbf{X} = \mathbf{x})$。

在分类任务中，你将得到 $N$ 个训练对：$(\mathbf{x}^{(1)},y^{(1)}), (\mathbf{x}^{(2)},y^{(2)}), \dots , (\mathbf{x}^{(N)},y^{(N)})$ 其中 $\mathbf{x}^{(i)}$ 是第 $i$ 个训练示例的 $m$ 个离散特征向量，而 $y^{(i)}$ 是第 $i$ 个训练示例的离散标签。

在我们介绍机器学习时，我们将假设训练数据集中的所有值都是二元的。虽然这不是一个必要的假设，但它使得学习核心概念变得容易得多。具体来说，我们假设所有标签都是二元的 $y^{(i)} \in \{0, 1\} \text{ }\forall i$，并且所有特征都是二元的 $x^{(i)}_j \in \{0, 1\} \text{ }\forall i, j$。
