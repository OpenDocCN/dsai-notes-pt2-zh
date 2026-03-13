# 预期值

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part2/expectation/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part2/expectation/)

* * *

一个随机变量完全由其概率质量函数（PMF）表示，该函数表示随机变量可以取的每个值及其对应的概率。PMF 可以包含大量信息。有时总结随机变量是有用的！一个随机变量最常见、也许也是最有用的总结是其“**预期值**”。

***定义***：预期值

随机变量 X 的预期值，记作$\E[X]$，是随机变量可以取的所有值的平均值，每个值都按照随机变量取该值的概率进行加权。$$ \E[X] = \sum_x x \cdot \p(X=x) $$

预期值还有许多其他名称：均值、加权平均、质心、一阶矩。所有这些都是使用相同的公式计算的。

回想一下，$\p(X=x)$，也写作$\p(x)$，是随机变量$X$的概率质量函数。以下是根据概率质量函数计算两个骰子之和的预期值的代码：

```py
def expectation_sum_two_dice():
    exp_sum_two_dice = 0
    # sum of dice can take on the values 2 through 12
    for x in range(2, 12 + 1):
        pr_x = pmf_sum_two_dice(x) # pmf gives Pr sum is x
        exp_sum_two_dice += x * pr_x
    return exp_sum_two_dice

def pmf_sum_two_dice(x):
    # Return the probability that two dice sum to x
    count = 0
    # Loop through all possible combinations of two dice
    for dice1 in range(1, 6 + 1):
        for dice2 in range(1, 6 + 1):
            if dice1 + dice2 == x:
                count += 1
    return count / 36  # There are 36 possible outcomes (6x6) 
```

如果我们手动计算，我们会得到如果$X$是两个骰子的和，$\E[X] = 7$：$$ \E[X] = \sum_x x \cdot \p(X=x) = 2 \cdot \frac{1}{36} + 3 \cdot \frac{2}{36} + \dots + 12 \frac{1}{36} = 7 $$ 7 是如果你无限次地取两个骰子的和所期望得到的“平均”数。在这种情况下，它也恰好是众数，即两个骰子之和的最可能值，但这并不总是如此！

## 预期值的属性

***属性***：预期值的线性

$$E[aX + b] = a\E[X]+b$$ 其中$a$和$b$是常数，不是随机变量。

***属性***：随机变量和的预期值

$$E[X+Y] = E[X] +E[Y]$$ 这对于$X$和$Y$之间的关系是成立的。它们可以是相关的，也可以有不同的分布。这也适用于超过两个随机变量的情况。$$E\Big[\sum_{i=1}^n X_i\Big] = \sum_{i=1}^n E[X_i]$$

***属性***：无意识统计学家定律 (LOTUS)

$$E[g(X)] = \sum_x g(x)\p(X=x)$$

当已知随机变量 X 的概率分布，但不知道 g(X)的分布时，也可以计算随机变量 X 的函数 g(X)的预期值。这个定理有一个幽默的名字“无意识统计学家定律”(LOTUS)，因为它非常有用，以至于你应该能够无意识地使用它。

***属性***：常数的预期值

$$E[a] = a$$

有时在证明中，你可能会得到常数的预期值（而不是随机变量的预期值）。例如，$\E[5]$代表什么？由于 5 不是一个随机变量，它不会改变，并且始终是 5，$\E[5] = 5$。

## 预期值和的证明

期望值的一个非常有用的性质是，随机变量期望值的总和可以通过对每个随机变量自身的期望值求和来计算。在[随机变量相加](https://example.org/part4/summation_vars/)的学习中，我们将会了解到，在相加随机变量时计算完整的概率质量函数（或概率密度函数）相当困难，尤其是在随机变量相互依赖的情况下。然而，期望值的总和总是可以分解的：$$E[X+Y] = E[X] + E[Y]$$ 这个非常有用的结果有些令人惊讶。我相信，理解这个结果的最佳方式是通过证明。然而，这个证明将使用课程阅读材料中下一节的一些概念，即概率模型。一旦你学会了如何联合思考随机变量，你将能够理解这个证明。阅读材料中有一个部分详细介绍了这个证明，并给出了为什么它是正确的可视化解释！[随机变量和的期望值证明](https://example.org/examples/expectation_of_sums/)。

## 无意识统计学家定律的例子

期望值的性质：$$E[g(X)] = \sum_x g(x)\p(X=x)$$ 仅通过阅读方程式就既有用又难以理解。它允许我们计算任何函数应用于随机变量后的函数的期望值！在计算[方差](https://example.org/part2/variance)时，一个将证明非常有用的函数是 $E[X²]$。根据无意识统计学家定律：$$E[X²] = \sum_x x² \p(X=x)$$ 在这种情况下，$g$ 是平方函数。为了计算 $E[X²]$，我们以类似于 $E[X]$ 的方式计算期望值，只是在将值乘以概率质量函数之前，我们先对 $x$ 的值进行平方。以下是一段代码，用于计算两个骰子之和的 $E[X²]$：

```py
def expectation_sum_two_dice_squared():
    exp_sum_two_dice_squared = 0
    # sum of dice can take on the values 2 through 12
    for x in range(2, 12 + 1):
        pr_x = pmf_sum_two_dice(x) # pmf gives Pr(x)
        exp_sum_two_dice_squared += x**2 * pr_x
    return exp_sum_two_dice_squared
```

### 连续随机变量的期望值

在课程阅读材料后面的部分，我们将学习关于连续随机变量的知识。对于这些类型的随机变量，期望值非常相似。详见[连续随机变量](https://example.org/pathToLang/part2/continuous#ex_continuous)。
