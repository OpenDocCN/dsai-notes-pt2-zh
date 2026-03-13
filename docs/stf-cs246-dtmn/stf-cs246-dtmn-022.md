#  022： 证明技巧与概率回顾

在本节课中，我们将学习几种常用的数学证明技巧，并对概率论的基础知识进行回顾。这些内容对于理解课程后续的算法和分析至关重要。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_1.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_2.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_3.png)

## 证明技巧

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_5.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_7.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_9.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_11.png)

上一节我们介绍了课程概述，本节中我们来看看几种核心的证明方法。

### 直接证明

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_13.png)

直接证明是最基础的证明方法。它通过逻辑推理，从已知条件或公理出发，直接推导出结论。

例如，证明“任何奇数的平方都是奇数”。
*   设任意奇数为 `2k + 1`，其中 `k` 为整数。
*   其平方为 `(2k + 1)^2 = 4k^2 + 4k + 1 = 2(2k^2 + 2k) + 1`。
*   由于 `2k^2 + 2k` 是整数，因此 `2(2k^2 + 2k) + 1` 是奇数。
*   因此，任何奇数的平方都是奇数。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_15.png)

### 逆否证明

有时直接证明一个命题“若A则B”比较困难，可以转而证明其等价的逆否命题“若非B则非A”。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_17.png)

例如，证明“若 `x^2` 是奇数，则 `x` 是奇数”。
*   其逆否命题为：“若 `x` 是偶数，则 `x^2` 是偶数”。
*   设 `x = 2k`，则 `x^2 = 4k^2 = 2(2k^2)`，显然是偶数。
*   由于逆否命题为真，原命题也为真。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_19.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_21.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_23.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_25.png)

**注意**：逆否命题（若非B则非A）与原命题等价，但逆命题（若B则A）则不一定。

### 反证法

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_27.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_29.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_31.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_33.png)

反证法通过假设结论不成立，推导出与已知事实或公理矛盾的结论，从而证明原结论必须成立。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_35.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_37.png)

例如，证明“√2 是无理数”。
*   假设 √2 是有理数，可表示为既约分数 `p/q`（`p` 和 `q` 互质）。
*   则 `2 = p^2 / q^2`，即 `2q^2 = p^2`。
*   因此 `p^2` 是偶数，`p` 也是偶数（因为奇数的平方是奇数）。设 `p = 2k`。
*   代入得 `2q^2 = (2k)^2 = 4k^2`，即 `q^2 = 2k^2`。
*   因此 `q^2` 是偶数，`q` 也是偶数。
*   这与 `p` 和 `q` 互质的假设矛盾。
*   因此，假设错误，√2 是无理数。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_39.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_41.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_43.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_45.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_47.png)

### 分情况证明

当一个问题可以自然地划分为有限个互斥的情况时，可以分别证明每种情况下结论都成立，从而证明结论普遍成立。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_49.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_51.png)

例如，证明“若整数 `n` 不能被3整除，则 `n^2` 可表示为 `3k + 1` 的形式”。
*   不能被3整除的整数有两种形式：`n = 3p + 1` 或 `n = 3p + 2`。
*   **情况1**：`n = 3p + 1`。则 `n^2 = 9p^2 + 6p + 1 = 3(3p^2 + 2p) + 1`，符合形式。
*   **情况2**：`n = 3p + 2`。则 `n^2 = 9p^2 + 12p + 4 = 3(3p^2 + 4p + 1) + 1`，符合形式。
*   所有情况均已涵盖，故命题得证。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_53.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_55.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_57.png)

### 数学归纳法

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_59.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_61.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_63.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_64.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_65.png)

数学归纳法用于证明与自然数 `n` 相关的命题。它包含两个步骤：
1.  **基础步骤**：证明当 `n = 1`（或某个起始值）时命题成立。
2.  **归纳步骤**：假设当 `n = k` 时命题成立（归纳假设），证明当 `n = k + 1` 时命题也成立。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_67.png)

例如，证明求和公式 `1 + 2 + ... + n = n(n+1)/2`。
*   **基础步骤**：`n=1` 时，左边=1，右边=`1*2/2=1`，成立。
*   **归纳步骤**：假设 `n=k` 时公式成立，即 `1+2+...+k = k(k+1)/2`。
*   则当 `n=k+1` 时，左边=`(1+2+...+k) + (k+1) = k(k+1)/2 + (k+1) = (k+1)(k/2 + 1) = (k+1)(k+2)/2`。
*   这正是 `n=k+1` 时的右边。因此，由归纳法可知公式对所有自然数 `n` 成立。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_69.png)

## 概率论基础

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_71.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_72.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_74.png)

上一节我们介绍了多种证明技巧，本节中我们来看看概率论的核心概念。

### 基本定义

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_76.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_78.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_80.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_82.png)

*   **样本空间 Ω**：一个实验所有可能结果的集合。例如，掷一个公平骰子，Ω = {1, 2, 3, 4, 5, 6}。
*   **事件**：样本空间 Ω 的任意子集。例如，事件 A = “掷出奇数” = {1, 3, 5}。
*   **概率函数 P**：为每个事件 A 分配一个介于 0 和 1 之间的数值 P(A)，表示该事件发生的可能性。它满足：
    *   `P(Ω) = 1`
    *   对于互斥事件（即 `A ∩ B = ∅`），有 `P(A ∪ B) = P(A) + P(B)`

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_84.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_86.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_88.png)

### 事件运算与概率

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_90.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_92.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_94.png)

*   **并集 A ∪ B**：事件 A **或** B 发生。
*   **交集 A ∩ B**：事件 A **且** B 同时发生。
*   **一般加法公式**：`P(A ∪ B) = P(A) + P(B) - P(A ∩ B)`。减去交集是为了避免重复计算。
*   **并集上界（Union Bound）**：对于任意事件集合 `A1, A2, ..., An`，有 `P(∪ Ai) ≤ Σ P(Ai)`。这是一个有用的上界估计工具。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_96.png)

### 条件概率与独立性

*   **条件概率 P(A|B)**：在事件 B 已发生的条件下，事件 A 发生的概率。公式为：
    `P(A|B) = P(A ∩ B) / P(B)`
*   **事件独立性**：如果 `P(A|B) = P(A)`，或等价地 `P(A ∩ B) = P(A)P(B)`，则称事件 A 和 B 相互独立。这意味着 B 的发生不影响 A 发生的概率。

### 贝叶斯定理

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_98.png)

贝叶斯定理描述了如何根据新证据（B 发生）更新对某个假设（A 发生）的概率估计。公式为：
`P(A|B) = [P(B|A) * P(A)] / P(B)`
其中 `P(B) = P(B|A)P(A) + P(B|¬A)P(¬A)`。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_100.png)

**应用示例（疾病检测）**：
*   已知某疾病在人群中的患病率 `P(病) = 0.01`。
*   检测的灵敏度（真有病且检测阳性）`P(阳|病) = 0.9`。
*   检测的假阳性率（真没病但检测阳性）`P(阳|无病) = 0.1`。
*   问：若某人检测呈阳性，其真实患病的概率 `P(病|阳)` 是多少？
*   根据贝叶斯定理：`P(病|阳) = (0.9 * 0.01) / (0.9*0.01 + 0.1*0.99) ≈ 0.083`。
*   结果显示，即使检测呈阳性，真实患病的概率也只有约 8.3%。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_102.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_104.png)

### 随机变量及其分布

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_106.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_108.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_110.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_112.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_114.png)

*   **随机变量 X**：将样本空间中的每个结果映射到一个实数的函数。
*   **概率质量函数（PMF）**：描述离散随机变量取每个特定值的概率。
*   **概率密度函数（PDF）**：描述连续随机变量在某个值附近的可能性密度。`X` 落在区间 `[a, b]` 的概率为 `∫_a^b f(x) dx`。PDF 满足 `f(x) ≥ 0` 且 `∫_{-∞}^{∞} f(x) dx = 1`。
*   **累积分布函数（CDF）**：`F(x) = P(X ≤ x)`。对于连续随机变量，`F(x) = ∫_{-∞}^{x} f(t) dt`。CDF 是单调非减且右连续的函数。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_116.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_118.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_120.png)

### 期望与方差

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_122.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_123.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_125.png)

*   **期望（均值）E[X]**：随机变量的加权平均值，衡量其中心趋势。
    *   离散：`E[X] = Σ x * P(X=x)`
    *   连续：`E[X] = ∫ x * f(x) dx`
*   **期望的线性性质**：`E[aX + b] = aE[X] + b`，且 `E[X+Y] = E[X] + E[Y]`（即使 X 和 Y 不独立也成立）。
*   **方差 Var(X)**：衡量随机变量取值与其均值的偏离程度。`Var(X) = E[(X - E[X])^2] = E[X^2] - (E[X])^2`。
*   **方差的性质**：`Var(aX + b) = a^2 Var(X)`。`Var(X+Y) = Var(X) + Var(Y)` 仅当 X 与 Y **不相关**时成立（独立必不相关，反之不必然）。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_127.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_129.png)

### 常见随机变量分布

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_131.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_133.png)

以下是几种重要的分布：

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_135.png)

**离散分布**：
*   **伯努利分布**：单次试验，成功概率为 `p`。`X ~ Bernoulli(p)`。
    *   `P(X=1)=p`, `P(X=0)=1-p`
    *   `E[X] = p`, `Var(X) = p(1-p)`
*   **几何分布**：进行一系列独立伯努利试验，直到第一次成功所需的试验次数。`X ~ Geometric(p)`。
    *   `P(X=k) = (1-p)^{k-1} p`
    *   `E[X] = 1/p`, `Var(X) = (1-p)/p^2`

**连续分布**：
*   **均匀分布**：在区间 `[a, b]` 上等可能取值。`X ~ Uniform(a, b)`。
    *   PDF: `f(x) = 1/(b-a)`, for `a ≤ x ≤ b`
    *   `E[X] = (a+b)/2`, `Var(X) = (b-a)^2/12`
*   **正态（高斯）分布**：最重要的连续分布之一，由均值 `μ` 和方差 `σ^2` 参数化。`X ~ N(μ, σ^2)`。
    *   PDF: `f(x) = (1/√(2πσ^2)) * exp(-(x-μ)^2/(2σ^2))`
    *   `E[X] = μ`, `Var(X) = σ^2`

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_137.png)

### 概率不等式

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_139.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_141.png)

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_142.png)

最后，我们介绍两个用于概率估计的有力不等式。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_144.png)

*   **马尔可夫不等式**：对于取非负值的随机变量 `X` 和任意 `a > 0`，有：
    `P(X ≥ a) ≤ E[X] / a`
    它给出了随机变量超过某个阈值的概率上界。

*   **切比雪夫不等式**：对于任意随机变量 `X`（期望为 `μ`，方差为 `σ^2`）和任意 `k > 0`，有：
    `P(|X - μ| ≥ k) ≤ σ^2 / k^2`
    它给出了随机变量偏离其均值超过 `k` 个单位的概率上界。它可以由马尔可夫不等式应用于 `(X-μ)^2` 推导出来。

![](img/c6cc9e29b1f3b48e2eabbd0d45f7edb7_146.png)

## 总结

本节课中我们一起学习了数学证明的几种核心技巧，包括直接证明、逆否证明、反证法、分情况证明和数学归纳法。随后，我们回顾了概率论的基础知识，涵盖了样本空间、事件、条件概率、贝叶斯定理、随机变量、期望、方差以及几个重要的概率分布（伯努利、几何、均匀、正态）。最后，我们介绍了马尔可夫不等式和切比雪夫不等式，它们是进行概率上界估计的有用工具。掌握这些内容将为学习海量数据集挖掘中的算法分析和概率模型打下坚实基础。