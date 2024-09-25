# 【深度强化学习 CS285 2023】伯克利—中英字幕 - P38：p38 CS 285： Lecture 9, Part 3 - 加加zero - BV1NjH4eYEyZ

好的，让我们讨论如何实际实现带有约束的政策梯度。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_1.png)

为了实例化我们在前一节中导出的算法，所以，我们有一个声称，即p theta of st接近p theta prime of st，当pi theta接近pi theta prime时。

这里'接近'被定义为总变分距离，现在，对我们来说，得到一个稍微更方便的界限将有所帮助，因为对于某些政策类。



![](img/d9f6aced9bfaaf8419cdefab2d169d39_3.png)

强制实施总变分距离约束实际上是相当困难的。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_5.png)

一，因此，我们可以从以下更方便的边界中推导出来。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_7.png)

你可以使用总变分距离实际上与KL距离相关的事实。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_9.png)

通过不等式，所以，如果你对πθ'和πθ之间的KL距离进行边界，这也根据这个方程对总变分距离进行了边界。



![](img/d9f6aced9bfaaf8419cdefab2d169d39_11.png)

所以嗯，这意味着πθ'和πθ之间的KL距离。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_13.png)

限制了状态边缘差异，但对于那些不熟悉KL距离的人，这基本上是分布之间的最广泛使用的离散度度量类型。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_15.png)

而且它可以非常方便，因为它有可求解的表达式，基本上表示为对对数概率的期望值。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_17.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_18.png)

而且许多连续值分布有可求解的封闭形式解决方案对于KL散度，所以这使KL散度非常方便使用。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_20.png)

嗯，所以，KL散度的表达式是期望值对比度的对数，之间的分布。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_22.png)

一种获取直觉的方法，为什么这种类型的差异稍微更容易管理。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_24.png)

是因为总变异差异以绝对值表达，这意味着它通常不是全部可微的。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_26.png)

而KL差异只要两个分布有相同的支持就是可微的。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_28.png)

所以，KL差异有一些非常方便的属性。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_30.png)

这使得它更容易近似，并且在实际的强化学习算法中更容易使用。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_32.png)

正如我们在本讲座的其余部分所看到的，所以实际上，如果我们实际上想要一个有约束的政策梯度方法，我们将把我们的约束表达为KL散度，而不是作为总变分散度，但由于KL散度限制了总变分散度，这是一件合法的事情。

并且它保留了我们的界限。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_34.png)

好的，所以然后，我们要优化的目标是我们的通常重要采样目标。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_36.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_37.png)

与约束条件KL散度之间pi theta，Prime和pi theta不超过epsilon，如果ε足够小，这确保jθ'减去jθ将得到改善，因为嗯。



![](img/d9f6aced9bfaaf8419cdefab2d169d39_39.png)

误差项将被限制，那么我们如何强制执行这个约束。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_41.png)

嗯，有许多不同的方法可以做到这一点，嗯和嗯。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_43.png)

你知道，一个非常简单的方法是实际上写出一个目标函数u，以这个受限优化问题的拉格朗日函数来表示。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_45.png)

"所以，对于你们中的每个人，拉格朗日量是"。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_47.png)

"那些不记得的"，"你的二次凸优化是由简单地取约束形成的"。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_49.png)

"取约束的左边减去右边"，并将其乘以拉格朗日乘数，"并且我们有一个约束和一个拉格朗日乘子"，我称之为"lambda"的。



![](img/d9f6aced9bfaaf8419cdefab2d169d39_51.png)

"如果你想解决一个约束优化问题"，"你可以做的事情之一是"。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_53.png)

"你可以交替地以原始变量theta为参数以最大化拉格朗日函数。"。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_55.png)

然后，在双变量上迈一步。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_57.png)

梯度下降步，所以，直觉是如果你对约束的违反太多，你就提高lambda。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_59.png)

否则，你就立即降低它，因为如果KL散度远大于epsilon。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_61.png)

他们将添加dk l减去epsilon，这是一个正数到lambda。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_63.png)

所以lambda会变得更大，如果约束远低于epsilon。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_65.png)

你会让一个负数，lambda会变得更小，所以你基本上交替解决一个无约束问题。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_67.png)

并调整你的拉格朗日乘数，以更严格或不严格的方式强制执行约束。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_69.png)

取决于它是否被违反。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_71.png)

这个程序被称为嗯，对偶梯度下降，我们实际上将在后续的讲座中详细讨论对偶梯度下降。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_73.png)

![](img/d9f6aced9bfaaf8419cdefab2d169d39_74.png)

但现在你可以大致相信我，这个程序将渐近找到正确的拉格朗日乘数。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_76.png)

这意味着它将实际上解决你的约束优化问题，现在，这是一种理论上的原则性解决方案，你可以想象一个更直观的解决方案。



![](img/d9f6aced9bfaaf8419cdefab2d169d39_78.png)

也许你可以手动选择一个lambda的值，并将这种KL散度视为一种正则化。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_80.png)

直觉上这也很有道理，你基本上在惩罚你的策略偏离旧策略太多。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_82.png)

因为你可以在几个梯度步骤中不完全地进行这个最大化，因为。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_84.png)

当然，在实际中运行优化到收敛可能非常昂贵或不实际。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_86.png)

所以，这是一个完成优化你策略的约束算法。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_88.png)

你可以计算目标函数的梯度，然后你会得到看起来基本像重要采样策略梯度的东西。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_90.png)

你可以计算KL散度。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_92.png)

这也是非常直接的事情，你会得到一个导数，你可以用它来最大化这个。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_94.png)

这会让你有一个强化学习算法，实际上，这个算法强制执行一个约束。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_96.png)

并且有许多算法使用这个想法的变体。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_98.png)

包括实际上的原始引导策略搜索方法和ppo。

![](img/d9f6aced9bfaaf8419cdefab2d169d39_100.png)