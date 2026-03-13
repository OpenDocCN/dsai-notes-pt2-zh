# Thompson 采样

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/thompson/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/thompson/)

* * *

![](img/45877de51a46765b5fd6227b88a79024.png)

想象一下你必须做出以下一系列决定。你有两种药物可以给药，药物 1 或药物 2。最初你不知道哪种药物更好。你想要知道哪种药物最有效，但与此同时，探索的成本很高。

这里有一个例子：

```py
Welcome to the drug simulator. 
There are two drugs: 1 and 2.

Next patient. Which drug? (1 or 2): 1
Failure. Yikes!

Next patient. Which drug? (1 or 2): 2
Success. Patient lives!

Next patient. Which drug? (1 or 2): 2
Failure. Yikes!

Next patient. Which drug? (1 or 2): 1
Failure. Yikes!

Next patient. Which drug? (1 or 2): 1
Success. Patient lives!

Next patient. Which drug? (1 or 2): 1
Failure. Yikes!

Next patient. Which drug? (1 or 2): 2
Success. Patient lives!

Next patient. Which drug? (1 or 2): 2
Failure. Yikes!

Next patient. Which drug? (1 or 2): 
```

这个问题出奇地复杂。有时它被称为“[多臂老虎机问题](https://en.wikipedia.org/wiki/Multi-armed_bandit)！”事实上，对这个问题的完美答案可能非常难以计算。有许多近似解，并且这是一个活跃的研究领域。

一种解决方案已经变得相当受欢迎：Thompson 采样。它易于实现，易于理解，有可证明的保证 [[1](https://www.jmlr.org/papers/volume17/14-087/14-087.pdf)]，并且在实践中表现良好 [[2](https://proceedings.neurips.cc/paper/2011/file/e53a0a2978c28872a4505bdb51db06dc-Paper.pdf)]。

### 你对选择的了解

Thompson 采样的第一步是表达你对选择（以及你不知道的）的了解。让我们回顾一下上一节中提到的两种药物。到结束时，我们测试了药物 1 四次（1 次成功）和药物 2 四次（2 次成功）。一种复杂的方式来表示我们对药物 1 和药物 2 后面隐藏的概率的信念是使用 Beta 分布。让 $X_1$ 表示对药物 1 概率的信念，让 $X_2$ 表示对药物 2 概率的信念。$$ $$\begin{align*} X_1 \sim \Beta(a = 2, b = 4)\\ X_2 \sim \Beta(a = 3, b = 3) \end{align*}$$ $$

回想一下，在具有均匀先验的 Beta 分布中，第一个参数 $a$ 是观察到的成功次数 + 1。第二个参数 $b$ 是观察到的失败次数 + 1。从图形上观察这两个分布是有帮助的：

<canvas id="betaExamplePdf" style="max-height: 400px"></canvas>

如果我们不得不猜测，药物 2 看起来更好，但仍然有很多不确定性，这体现在这些信念的高方差中。这是一个有用的表示。但我们如何利用这些信息来做出下一个药物的好决定。

### 做出选择

确定正确的选择很难！如果你只有一个更多的病人，那么你该做什么就很明确了。你应该计算 $X_2 > X_1$ 的概率，如果这个概率超过 0.5，那么你应该选择 $a$。然而，如果你需要持续给药，那么正确的选择就不那么明确了。如果你选择 1，你将错过了解 2 的机会。我们该怎么办？我们需要平衡“探索”的需求和利用已知信息的需要。

汤普森采样的简单思想是随机地根据其成为最优选择的概率来做出选择。在这种情况下，我们应该选择药物 1，其选择的概率是 1 大于 2。人们在实践中是如何做到这一点的呢？他们有一个非常简单的公式。从每个 Beta 分布中随机采样。选择其采样值较大的选项。

```py
sample_a = sample_beta(2, 4)
sample_b = sample_beta(3, 3)
if sample_a > sample_b:
    choose choice a 
else:
    choose choice b 
```

采样意味着什么？这意味着根据概率密度函数（或概率质量函数）选择一个值。所以在我们上面的例子中，我们可能会为药物 1 采样 0.4，为药物 2 采样 0.35。在这种情况下，我们会选择药物 1。

在开始时，汤普森采样“探索”了相当长的时间。随着它越来越确信一种药物比另一种药物更好，它将开始大多数时候选择那种药物。最终，它将收敛到知道哪种药物最好，并且它将始终选择那种药物。
