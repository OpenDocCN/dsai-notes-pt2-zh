# 贝叶斯碳定年

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/bayesian_carbon_dating/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/bayesian_carbon_dating/)

* * *

我们可以使用被称为碳定年法的过程来确定古代文物的年龄。这个过程涉及很多不确定性！你观察到样本中 90%的自然 C14 分子的测量值。你对样本年龄的信念分布是什么？这项任务需要概率模型，因为我们必须同时考虑两个随机变量：样本的年龄$A$和剩余的 C14 分子数$M$。

### 碳定年演示

想象你刚刚从你的文物中取了一个样本。对于你取的样本大小，一个活体生物会有 1000 个 C14 分子。使用这个演示来探索剩余的 C14 量和你对文物年龄的信念分布之间的关系。
