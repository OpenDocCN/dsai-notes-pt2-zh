# 42： 轨迹优化与线性二次调节器 (LQR) 🚀

![](img/dca975c57ee7e31d5bbfb3959315f2dd_1.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_3.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_5.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_7.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_9.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_11.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_13.png)

在本节课中，我们将要学习如何利用动力学的导数进行轨迹优化。我们将从基本的优化问题出发，介绍两种主要方法：射击法和共轭点法，并重点深入讲解一种经典且高效的二阶方法——线性二次调节器 (LQR)。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_15.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_17.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_19.png)

---

![](img/dca975c57ee7e31d5bbfb3959315f2dd_21.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_23.png)

## 概述

![](img/dca975c57ee7e31d5bbfb3959315f2dd_25.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_27.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_29.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_31.png)

到目前为止，我们已经讨论了规划中的黑箱优化方法和蒙特卡洛树搜索。这些方法主要适用于离散动作和随机环境。接下来，我们将讨论带有导数的轨迹优化方法，这在许多已知动力学导数的连续环境中非常有用。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_33.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_35.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_37.png)

在强化学习和动态规划中，我们通常使用 `s_t` 和 `a_t` 表示状态和动作，用 `r` 表示奖励。而在最优控制领域，更常见的做法是使用 `x_t` 和 `u_t` 表示状态和动作，并使用**成本**（Cost）代替**奖励**（Reward）。本部分将讨论轨迹优化和最优控制方法，这些是最优控制社区最常研究的方法。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_39.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_41.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_43.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_45.png)

为了与教科书符号保持一致，我们将使用 `x` 表示状态，`u` 表示动作。请记住，这仅仅是符号上的差异，基本原理完全相同。你可以尝试在心理上将 `s` 替换为 `x`，将 `a` 替换为 `u`，并思考这些方法在最大化奖励（而非最小化成本）时的样子。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_47.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_49.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_51.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_53.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_55.png)

---

![](img/dca975c57ee7e31d5bbfb3959315f2dd_57.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_59.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_61.png)

## 利用导数进行规划

![](img/dca975c57ee7e31d5bbfb3959315f2dd_63.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_65.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_67.png)

现在，让我们思考如何利用导数进行规划。首先，回到最初的约束优化问题。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_69.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_71.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_73.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_75.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_77.png)

当我们定义基于模型的规划问题时，我们希望最小化总成本（或最大化总回报），但必须将系统动力学作为约束条件考虑进去。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_79.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_81.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_83.png)

**优化问题公式**：
最小化总成本，同时满足动力学约束 `x_t = f(x_{t-1}, u_{t-1})`。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_85.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_87.png)

带有等式约束的优化问题，总是可以通过将约束代入变量，转化为无约束优化问题。因此，上述约束优化问题等价于一个复杂的、但无约束的优化问题。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_89.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_91.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_93.png)

如果我们想使用导数来优化这个无约束问题，一个直接的想法是计算梯度并通过反向传播进行优化。具体来说，我们需要计算动力学 `f` 和成本函数 `c` 相对于其输入 `x_t` 和 `u_t` 的导数，即 `df/dx_t`, `df/du_t`, `dc/dx_t`, `dc/du_t`。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_95.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_97.png)

然而，在实践中，对于这种目标函数，仅使用一阶梯度下降法通常效果很差。因此，使用二阶方法（如牛顿法）来解决这种优化问题非常有帮助。幸运的是，这个问题具有特殊的结构，可以导出一个非常高效的算法，而无需计算庞大的海森矩阵。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_99.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_101.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_103.png)

---

![](img/dca975c57ee7e31d5bbfb3959315f2dd_105.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_107.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_109.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_111.png)

## 射击法 vs. 共轭点法

![](img/dca975c57ee7e31d5bbfb3959315f2dd_113.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_115.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_117.png)

在深入描述二阶方法之前，需要先了解轨迹优化中两个核心概念的差异：**射击法** (Shooting Methods) 和 **共轭点法** (Collocation Methods)。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_119.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_121.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_123.png)

**射击法** 是一种直接优化动作序列 `{u_1, ..., u_T}` 的方法。之所以称为“射击法”，是因为你可以想象初始动作的选择就像在状态空间中“射击”，其影响会贯穿整个轨迹，对最终结果产生重大影响。这也解释了为什么射击法在数值上可能不稳定：早期动作对目标的敏感性极高，导致优化问题的条件数很差，一阶梯度方法难以处理。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_125.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_127.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_129.png)

**共轭点法** 则同时优化状态序列 `{x_1, ..., x_T}` 和动作序列 `{u_1, ..., u_T}`，并附加动力学等式约束。在这种方法中，优化变量是轨迹上的所有点，只要满足约束即可移动。通常，共轭点法的数值条件更好，对一阶方法更友好，但实现起来通常更复杂。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_131.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_133.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_135.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_137.png)

本节课我们将重点讨论一种经典的、基于射击法的二阶方法。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_139.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_141.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_143.png)

---

![](img/dca975c57ee7e31d5bbfb3959315f2dd_145.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_147.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_149.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_151.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_153.png)

## 线性二次调节器 (LQR)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_155.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_157.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_159.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_161.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_163.png)

我们将要讨论的经典射击法是 **线性二次调节器**。首先，我们从线性控制问题的特例开始，然后再扩展到非线性情况。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_165.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_167.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_169.png)

### 问题设定

![](img/dca975c57ee7e31d5bbfb3959315f2dd_171.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_173.png)

我们的优化问题是最小化总成本，这对应于最初的约束优化问题，但通过代入约束，我们将其视为关于动作序列的无约束优化问题。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_175.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_177.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_179.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_181.png)

**线性情况** 指的是动力学 `f(x_t, u_t)` 是线性的，即可以表示为：
`f(x_t, u_t) = F_t * [x_t; u_t] + f_t`
其中 `F_t` 是矩阵，`f_t` 是常数向量。注意，我们目前讨论的是确定性动力学，稍后会扩展到随机情况。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_183.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_185.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_187.png)

我们假设**成本函数是二次的**。如果成本是线性的，无约束最小化的解可能在无穷远处，这没有意义。因此，成本至少是二次的，可以写成：
`c(x_t, u_t) = 1/2 * [x_t; u_t]^T C_t [x_t; u_t] + [c_{x,t}; c_{u,t}]^T [x_t; u_t]`

![](img/dca975c57ee7e31d5bbfb3959315f2dd_189.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_191.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_193.png)

**线性动力学 + 二次成本 = 线性二次调节器 (LQR)**。我们允许每个时间步的矩阵 `C_t`, `c_t`, `F_t`, `f_t` 都不同，这在扩展到非线性情况时会很重要。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_195.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_197.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_199.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_201.png)

### LQR 推导

![](img/dca975c57ee7e31d5bbfb3959315f2dd_203.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_205.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_207.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_209.png)

我们通过**动态规划**的思想来求解 LQR 问题，即从最后一个时间步开始，反向推导到第一个时间步。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_211.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_213.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_215.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_217.png)

**第一步：求解最后一步 (t=T)**
在最后一步，我们只关心最小化当前成本 `c(x_T, u_T)`。这是一个关于 `u_T` 的二次函数。
1.  将成本矩阵 `C_T` 按状态和动作分块：`C_T = [[C_{xx,T}, C_{xu,T}], [C_{ux,T}, C_{uu,T}]]`，其中 `C_{ux,T} = C_{xu,T}^T`。
2.  对 `u_T` 求导并令导数为零，可以得到最优动作 `u_T` 关于状态 `x_T` 的表达式：
    `u_T = K_T * x_T + k_T`
    其中，
    `K_T = -C_{uu,T}^{-1} * C_{ux,T}`
    `k_T = -C_{uu,T}^{-1} * c_{u,T}`
3.  将最优 `u_T` 代回成本函数，可以得到最后一步的**价值函数** `V(x_T)`，它表示从状态 `x_T` 开始执行最优动作后的总成本。可以证明，`V(x_T)` 仍然是 `x_T` 的二次函数：
    `V(x_T) = 1/2 * x_T^T * V_T * x_T + x_T^T * v_T + 常数`

![](img/dca975c57ee7e31d5bbfb3959315f2dd_219.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_221.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_223.png)

**第二步：反向递归 (t=T-1, ..., 1)**
现在考虑前一个时间步 `t`。此时的选择 `u_t` 不仅影响当前成本 `c(x_t, u_t)`，还会通过动力学影响下一个状态 `x_{t+1}`，从而影响未来的最优成本 `V(x_{t+1})`。
1.  定义 **Q-函数**：`Q(x_t, u_t) = c(x_t, u_t) + V(f(x_t, u_t))`。这表示在状态 `x_t` 执行动作 `u_t`，之后遵循最优策略的总成本。
2.  将线性动力学 `x_{t+1} = F_t * [x_t; u_t] + f_t` 和二次价值函数 `V(x_{t+1})` 代入 `Q(x_t, u_t)`。经过代数运算（主要是展开和合并同类项），可以发现 `Q(x_t, u_t)` 仍然是关于 `[x_t; u_t]` 的二次函数。
3.  再次对 `u_t` 求导并令导数为零，可以解出最优动作：
    `u_t = K_t * x_t + k_t`
    其中，`K_t` 和 `k_t` 的表达式与最后一步形式相同，但其中的矩阵 `Q_{uu,t}`, `Q_{ux,t}` 和向量 `q_{u,t}` 是由当前成本 `c_t`、动力学 `F_t, f_t` 以及下一步的价值函数参数 `V_{t+1}, v_{t+1}` 共同计算得出的。
4.  同样，将最优 `u_t` 代入 `Q(x_t, u_t)`，可以得到当前步的价值函数 `V(x_t)`，它仍然是 `x_t` 的二次函数，并可以更新参数 `V_t`, `v_t`。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_225.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_227.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_229.png)

**算法流程**：
1.  **反向过程**：从 `t=T` 到 `t=1`，递归地计算每个时间步的增益矩阵 `K_t`、偏移向量 `k_t` 以及价值函数参数 `V_t`, `v_t`。
2.  **正向过程**：从给定的初始状态 `x_1` 开始，对于 `t=1` 到 `T`：
    *   计算动作：`u_t = K_t * x_t + k_t`
    *   通过动力学计算下一个状态：`x_{t+1} = f(x_t, u_t)`
    这样就得到了最优的状态轨迹 `{x_1, ..., x_T}` 和动作轨迹 `{u_1, ..., u_T}`。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_231.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_233.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_235.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_237.png)

---

![](img/dca975c57ee7e31d5bbfb3959315f2dd_239.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_241.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_243.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_245.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_247.png)

## 总结

![](img/dca975c57ee7e31d5bbfb3959315f2dd_249.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_251.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_253.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_255.png)

本节课中，我们一起学习了如何利用导数进行轨迹优化。
*   我们首先比较了**射击法**和**共轭点法**这两种不同的优化思路。
*   然后，我们重点深入推导了**线性二次调节器 (LQR)** 这一经典算法。LQR 针对**线性动力学**和**二次成本**这一特殊问题，通过动态规划的思想，高效地计算出最优策略——该策略表现为一个随时间变化的线性反馈控制器 `u_t = K_t * x_t + k_t`。
*   LQR 的核心在于其反向递归计算增益矩阵 `K_t` 和偏移量 `k_t`，再通过正向模拟得到最优轨迹。虽然推导过程中的线性代数运算写起来繁琐，但每一步在数学上都是直接了当的。

![](img/dca975c57ee7e31d5bbfb3959315f2dd_257.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_259.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_261.png)

![](img/dca975c57ee7e31d5bbfb3959315f2dd_263.png)

理解 LQR 是学习更高级轨迹优化方法（如迭代 LQR、微分动态规划 DDP）的重要基础。对于非线性系统，我们通常在其局部线性化/二次近似后应用 LQR，并通过迭代来改进轨迹。