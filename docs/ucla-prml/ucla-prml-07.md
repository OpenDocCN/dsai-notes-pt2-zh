# 7：模式识别与机器学习导论 - 偏差-方差分解与分区估计器分析 📊

![](img/c929f863fb1fcbd522f1e41b961f596d_0.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_2.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_4.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_6.png)

在本节课中，我们将学习回归分析中的一个核心概念：偏差-方差分解。我们将通过分析一个具体的非参数估计器——分区估计器，来理解其预测误差如何分解为偏差和方差两部分，并探讨带宽选择对估计性能的影响。

![](img/c929f863fb1fcbd522f1e41b961f596d_8.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_10.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_12.png)

---

![](img/c929f863fb1fcbd522f1e41b961f596d_14.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_16.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_18.png)

上一节我们介绍了回归分析的基本框架和最优回归函数。本节中，我们来看看如何分析一个具体估计器的性能。

![](img/c929f863fb1fcbd522f1e41b961f596d_20.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_22.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_24.png)

## 偏差-方差分解 🔍

![](img/c929f863fb1fcbd522f1e41b961f596d_26.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_28.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_30.png)

我们关心的核心量是估计回归函数 \(\hat{\eta}(x)\) 与真实回归函数 \(\eta(x)\) 之间的均方误差（MSE）。在给定训练数据 \(X_1, ..., X_n\) 的条件下，我们分析以下期望：

![](img/c929f863fb1fcbd522f1e41b961f596d_32.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_34.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_36.png)

\[
\mathbb{E} \left[ (\eta(x) - \hat{\eta}(x))^2 \mid X_1, ..., X_n \right]
\]

![](img/c929f863fb1fcbd522f1e41b961f596d_38.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_39.png)

为了分析这个量，我们使用一个经典的技巧：加减 \(\hat{\eta}(x)\) 的期望值 \(\mathbb{E}[\hat{\eta}(x)]\)。

![](img/c929f863fb1fcbd522f1e41b961f596d_41.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_43.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_45.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_47.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_49.png)

\[
\eta(x) - \hat{\eta}(x) = [\eta(x) - \mathbb{E}[\hat{\eta}(x)]] + [\mathbb{E}[\hat{\eta}(x)] - \hat{\eta}(x)]
\]

将上式平方并取期望，交叉项为零，最终得到分解：

![](img/c929f863fb1fcbd522f1e41b961f596d_51.png)

\[
\mathbb{E} \left[ (\eta(x) - \hat{\eta}(x))^2 \right] = \underbrace{(\eta(x) - \mathbb{E}[\hat{\eta}(x)])^2}_{\text{偏差平方}} + \underbrace{\mathbb{E} \left[ (\hat{\eta}(x) - \mathbb{E}[\hat{\eta}(x)])^2 \right]}_{\text{方差}}
\]

这个分解公式非常通用，它表明估计器的均方误差由两部分组成：
*   **偏差平方**：估计器期望值与真实值之间的差异。它衡量了估计器的系统性误差。
*   **方差**：估计器本身围绕其期望值的波动程度。它衡量了估计器对训练数据随机性的敏感度。

![](img/c929f863fb1fcbd522f1e41b961f596d_53.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_55.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_57.png)

通常，偏差和方差之间存在权衡。

![](img/c929f863fb1fcbd522f1e41b961f596d_59.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_61.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_63.png)

---

![](img/c929f863fb1fcbd522f1e41b961f596d_65.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_67.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_69.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_71.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_73.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_75.png)

理解了通用的偏差-方差分解后，我们将其应用到一个具体的估计器上。

## 分区估计器 📏

分区估计器是一种简单的局部平均方法。假设输入 \(X\) 是一维的，且定义在区间 \([0,1]\) 上。我们将该区间划分为若干个长度为 \(h\) 的小区间（或称“单元”）。

对于给定的预测点 \(x\)，令 \(A(x)\) 表示包含 \(x\) 的那个小区间。分区估计器的定义是，对落在 \(A(x)\) 内的所有训练样本的输出 \(Y_i\) 取平均：

![](img/c929f863fb1fcbd522f1e41b961f596d_77.png)

\[
\hat{\eta}(x) = \frac{\sum_{i=1}^{n} Y_i \cdot \mathbb{I}(X_i \in A(x))}{\sum_{i=1}^{n} \mathbb{I}(X_i \in A(x))}
\]

其中 \(\mathbb{I}(\cdot)\) 是指示函数。这个估计器可以重写为加权和的形式：

![](img/c929f863fb1fcbd522f1e41b961f596d_79.png)

\[
\hat{\eta}(x) = \sum_{i=1}^{n} w_i(x) Y_i, \quad \text{其中} \quad w_i(x) = \frac{\mathbb{I}(X_i \in A(x))}{n \cdot \hat{\nu}_n(A(x))}
\]

![](img/c929f863fb1fcbd522f1e41b961f596d_81.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_83.png)

这里，\(\hat{\nu}_n(A(x)) = \frac{1}{n} \sum_{i=1}^{n} \mathbb{I}(X_i \in A(x))\) 是经验测度，即训练样本落在区间 \(A(x)\) 中的比例。

---

![](img/c929f863fb1fcbd522f1e41b961f596d_85.png)

现在，我们利用偏差-方差分解公式来分析分区估计器的性能。

![](img/c929f863fb1fcbd522f1e41b961f596d_87.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_89.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_91.png)

### 方差分析

![](img/c929f863fb1fcbd522f1e41b961f596d_93.png)

首先计算估计器 \(\hat{\eta}(x)\) 的方差。在给定训练输入 \(X_1,...,X_n\) 的条件下，权重 \(w_i(x)\) 是常数，而 \(Y_i\) 是条件独立的。

![](img/c929f863fb1fcbd522f1e41b961f596d_95.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_97.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_99.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_101.png)

\[
\text{Var}(\hat{\eta}(x)) = \text{Var}\left( \sum_{i=1}^{n} w_i(x) Y_i \right) = \sum_{i=1}^{n} w_i(x)^2 \text{Var}(Y_i \mid X_i)
\]

![](img/c929f863fb1fcbd522f1e41b961f596d_103.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_105.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_107.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_109.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_111.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_113.png)

我们假设条件方差是常数，即 \(\text{Var}(Y \mid X) = \sigma^2\)。代入权重公式并进行化简：

![](img/c929f863fb1fcbd522f1e41b961f596d_115.png)

\[
\begin{aligned}
\text{Var}(\hat{\eta}(x)) &= \sigma^2 \sum_{i=1}^{n} \left( \frac{\mathbb{I}(X_i \in A(x))}{n \hat{\nu}_n(A(x))} \right)^2 \\
&= \frac{\sigma^2}{n} \cdot \frac{1}{\hat{\nu}_n(A(x))}
\end{aligned}
\]

![](img/c929f863fb1fcbd522f1e41b961f596d_117.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_119.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_120.png)

当样本量 \(n\) 很大时，经验测度 \(\hat{\nu}_n(A(x))\) 会收敛于真实概率 \(\nu(A(x)) = P(X \in A(x))\)。如果我们进一步假设 \(X\) 在 \([0,1]\) 上均匀分布，那么 \(\nu(A(x)) = h\)。因此，对于大的 \(n\)，方差近似为：

![](img/c929f863fb1fcbd522f1e41b961f596d_122.png)

\[
\text{Var}(\hat{\eta}(x)) \approx \frac{\sigma^2}{n h}
\]

**结论**：分区估计器的方差与带宽 \(h\) 成反比。\(h\) 越大（单元越宽），用于平均的样本越多，方差越小。

---

![](img/c929f863fb1fcbd522f1e41b961f596d_124.png)

分析完方差，我们接下来看看偏差部分。

![](img/c929f863fb1fcbd522f1e41b961f596d_126.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_128.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_130.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_132.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_134.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_136.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_137.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_138.png)

### 偏差分析

接下来计算估计器 \(\hat{\eta}(x)\) 的期望，即偏差部分。

\[
\mathbb{E}[\hat{\eta}(x)] = \mathbb{E}\left[ \sum_{i=1}^{n} w_i(x) Y_i \right] = \sum_{i=1}^{n} w_i(x) \mathbb{E}[Y_i \mid X_i] = \sum_{i=1}^{n} w_i(x) \eta(X_i)
\]

![](img/c929f863fb1fcbd522f1e41b961f596d_140.png)

代入权重表达式并利用大数定律，当 \(n\) 很大时：

![](img/c929f863fb1fcbd522f1e41b961f596d_142.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_144.png)

\[
\mathbb{E}[\hat{\eta}(x)] \approx \frac{1}{\nu(A(x))} \int_{u \in A(x)} \eta(u) d\nu(u)
\]

在 \(X\) 均匀分布的假设下，这简化为在区间 \(A(x)\) 上对真实回归函数 \(\eta(u)\) 取平均：

![](img/c929f863fb1fcbd522f1e41b961f596d_146.png)

\[
\mathbb{E}[\hat{\eta}(x)] \approx \frac{1}{h} \int_{u \in A(x)} \eta(u) du
\]

![](img/c929f863fb1fcbd522f1e41b961f596d_148.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_150.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_151.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_153.png)

因此，偏差为：

![](img/c929f863fb1fcbd522f1e41b961f596d_155.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_157.png)

\[
\text{Bias}(x) = \eta(x) - \mathbb{E}[\hat{\eta}(x)] \approx \eta(x) - \frac{1}{h} \int_{u \in A(x)} \eta(u) du
\]

![](img/c929f863fb1fcbd522f1e41b961f596d_159.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_161.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_163.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_165.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_167.png)

**直观理解**：分区估计器用整个区间 \(A(x)\) 上 \(\eta\) 的平均值，来近似该区间内某一点 \(x\) 的真实值 \(\eta(x)\)。只有当区间宽度 \(h \to 0\) 时，这个平均值才会趋近于 \(\eta(x)\)，从而使偏差趋近于零。

**结论**：分区估计器的偏差与带宽 \(h\) 正相关。\(h\) 越小（单元越窄），局部平均越接近点值，偏差越小。

![](img/c929f863fb1fcbd522f1e41b961f596d_169.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_171.png)

---

![](img/c929f863fb1fcbd522f1e41b961f596d_173.png)

## 权衡与总结 ⚖️

综合方差和偏差的分析，我们得到分区估计器均方误差（MSE）的近似表达式：

![](img/c929f863fb1fcbd522f1e41b961f596d_175.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_176.png)

\[
\text{MSE} \approx \underbrace{\left( \eta(x) - \frac{1}{h}\int_{A(x)} \eta(u) du \right)^2}_{\text{偏差平方，随 } h \text{ 减小而减小}} + \underbrace{\frac{\sigma^2}{n h}}_{\text{方差，随 } h \text{ 减小而增大}}
\]

![](img/c929f863fb1fcbd522f1e41b961f596d_178.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_180.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_182.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_184.png)

这揭示了一个根本性的**权衡（Bias-Variance Tradeoff）**：
*   选择**大的带宽 \(h\)**：方差小，但偏差大（估计过于平滑，可能欠拟合）。
*   选择**小的带宽 \(h\)**：偏差小，但方差大（估计波动剧烈，可能过拟合）。

![](img/c929f863fb1fcbd522f1e41b961f596d_186.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_188.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_190.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_192.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_194.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_196.png)

最优的带宽 \(h^*\) 需要平衡这两者，使得总的均方误差最小。偏差收敛到零的速度取决于真实回归函数 \(\eta(x)\) 的平滑度，这将在后续课程中讨论。

![](img/c929f863fb1fcbd522f1e41b961f596d_198.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_200.png)

---

![](img/c929f863fb1fcbd522f1e41b961f596d_202.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_204.png)

![](img/c929f863fb1fcbd522f1e41b961f596d_206.png)

本节课中我们一起学习了偏差-方差分解这一核心概念，并将其应用于分区估计器的分析。我们了解到，任何估计器的预测误差都可以分解为偏差和方差两部分，而带宽参数 \(h\) 的选择正是在偏差（要求 \(h\) 小）和方差（要求 \(h\) 大）之间进行权衡的关键。理解这一权衡对于选择和调整机器学习模型至关重要。