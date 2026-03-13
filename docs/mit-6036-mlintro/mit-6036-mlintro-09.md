# 9：L9- 状态机与马尔可夫决策过程 🚜

![](img/2220f93cadcaca2dfe0e327d8d583653_1.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_3.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_5.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_7.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_9.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_11.png)

在本节课中，我们将要学习状态机与马尔可夫决策过程。我们将从一个简单的农场管理例子出发，理解决策如何改变世界的状态，并学习如何通过数学模型来评估和选择最优的决策策略。

![](img/2220f93cadcaca2dfe0e327d8d583653_13.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_15.png)

---

![](img/2220f93cadcaca2dfe0e327d8d583653_17.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_19.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_21.png)

## 📝 概述

![](img/2220f93cadcaca2dfe0e327d8d583653_23.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_25.png)

到目前为止，我们主要讨论了监督学习，包括回归和分类。在这些情况下，我们每次针对一个独立的数据点做出决策，例如决定今天是否穿外套。然而，许多决策会改变世界的状态，从而影响未来的决策。本节课我们将探讨这类问题。

![](img/2220f93cadcaca2dfe0e327d8d583653_27.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_29.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_31.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_33.png)

首先，我们将介绍**状态机**，它描述了世界状态如何变化。然后，我们将引入**马尔可夫决策过程**，它扩展了状态机，加入了**奖励**和**随机性**的概念，使我们能够评估和选择最优的决策序列。

![](img/2220f93cadcaca2dfe0e327d8d583653_35.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_37.png)

---

![](img/2220f93cadcaca2dfe0e327d8d583653_39.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_41.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_43.png)

## 🏞️ 状态机：描述世界的变化

![](img/2220f93cadcaca2dfe0e327d8d583653_45.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_47.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_49.png)

我们从一个农场管理的例子开始。假设你租了一块田地，田地的土壤状态可以是**肥沃**或**贫瘠**。你的决策（**输入**）可以是**种植**或**休耕**。

![](img/2220f93cadcaca2dfe0e327d8d583653_51.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_53.png)

状态机由以下几个要素定义：
*   **状态集合 (S)**: {肥沃, 贫瘠}
*   **输入集合 (X)**: {种植, 休耕}
*   **初始状态 (s₀)**: 假设初始时土壤是肥沃的。
*   **转移函数 (f)**: 它定义了在当前状态和输入下，下一个状态是什么。

![](img/2220f93cadcaca2dfe0e327d8d583653_55.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_57.png)

以下是转移函数的一个确定性示例：
*   如果当前是**贫瘠**土壤，选择**休耕**，则下一季变为**肥沃**。
*   如果当前是**贫瘠**土壤，选择**种植**，则下一季保持**贫瘠**。
*   如果当前是**肥沃**土壤，选择**种植**，则下一季变为**贫瘠**。
*   如果当前是**肥沃**土壤，选择**休耕**，则下一季保持**肥沃**。

我们可以用状态转移图来表示这个过程。

有时，我们无法直接观察状态（例如土壤的肥沃程度），而是通过传感器测量一些指标（如土壤湿度）。这引入了**输出函数 (g)**，它将隐藏的状态映射到我们实际观察到的**输出**。在本课大部分内容中，我们假设可以直接观察状态，即输出函数是恒等函数。

![](img/2220f93cadcaca2dfe0e327d8d583653_59.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_61.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_63.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_65.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_67.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_69.png)

---

![](img/2220f93cadcaca2dfe0e327d8d583653_71.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_73.png)

## 🎯 引入奖励：评估决策的好坏

状态机描述了状态如何变化，但没有告诉我们哪些决策是“好”的。为了做出决策，我们需要一个衡量标准，即**奖励函数 (R)**。

在我们的农场例子中，奖励可以是收获的**蒲式耳**（一种计量单位）数量。我们期望收获越多越好。奖励函数通常输出一个实数。

![](img/2220f93cadcaca2dfe0e327d8d583653_75.png)

关键点在于，奖励不仅取决于你的**行动**（种植或休耕），还取决于你行动时的**状态**。
*   在**肥沃**土壤上**种植**，可能收获100蒲式耳。
*   在**贫瘠**土壤上**种植**，可能只收获10蒲式耳。
*   在任何土壤上**休耕**，收获为0蒲式耳。

![](img/2220f93cadcaca2dfe0e327d8d583653_77.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_79.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_81.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_83.png)

因此，奖励函数可以表示为：`R(状态, 行动)`。例如，`R(肥沃, 种植) = 100`。

![](img/2220f93cadcaca2dfe0e327d8d583653_85.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_87.png)

---

![](img/2220f93cadcaca2dfe0e327d8d583653_89.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_91.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_93.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_95.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_97.png)

## 🎲 引入随机性：更真实的转移模型

![](img/2220f93cadcaca2dfe0e327d8d583653_99.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_101.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_103.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_105.png)

现实世界充满不确定性。例如，即使你选择种植，由于天气等因素，土壤状态的变化也可能不是确定的。

![](img/2220f93cadcaca2dfe0e327d8d583653_107.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_109.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_111.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_113.png)

因此，我们需要将确定性的**转移函数**扩展为随机性的**转移模型 (T)**。转移模型给出了在特定状态和行动下，转移到下一个状态的概率。

![](img/2220f93cadcaca2dfe0e327d8d583653_115.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_117.png)

我们可以用三种方式表示转移模型：
1.  **概率转移图**：在状态转移箭头上标注概率。
2.  **转移矩阵**：为每个行动创建一个矩阵，其中行表示起始状态，列表示结束状态，矩阵元素 `T[s, s']` 表示从状态 `s` 转移到状态 `s'` 的概率。每一行的概率之和必须为1。
3.  **概率函数**：函数 `T(s, a, s')` 返回在状态 `s` 采取行动 `a` 后，转移到状态 `s'` 的概率。

例如，对于“种植”行动，转移矩阵可能如下（假设状态顺序为[肥沃, 贫瘠]）：
```
T_plant = [[0.1, 0.9],  # 从肥沃开始：0.1概率保持肥沃，0.9概率变贫瘠
           [0.01, 0.99]] # 从贫瘠开始：0.01概率变肥沃，0.99概率保持贫瘠
```
对于“休耕”行动，会有另一个不同的转移矩阵。

---

![](img/2220f93cadcaca2dfe0e327d8d583653_119.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_121.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_123.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_125.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_127.png)

## 🤖 马尔可夫决策过程：决策的完整框架

![](img/2220f93cadcaca2dfe0e327d8d583653_129.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_131.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_133.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_135.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_137.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_139.png)

结合状态、行动、随机转移模型和奖励函数，我们就得到了**马尔可夫决策过程** 的核心组成部分。

![](img/2220f93cadcaca2dfe0e327d8d583653_141.png)

一个MDP正式定义为以下五元组 `(S, A, T, R, γ)`：
*   **S**: 状态集合。
*   **A**: 行动集合（之前称为输入）。
*   **T**: 转移模型，`T(s, a, s') = P(s' | s, a)`。
*   **R**: 奖励函数，`R(s, a)`。
*   **γ**: **折扣因子** (0 ≤ γ ≤ 1)，用于衡量未来奖励的当前价值（稍后详述）。

![](img/2220f93cadcaca2dfe0e327d8d583653_143.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_145.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_147.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_149.png)

MDP与状态机的关键区别在于：1) 包含了奖励函数来评估决策优劣；2) 转移过程可以是随机的。

![](img/2220f93cadcaca2dfe0e327d8d583653_151.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_153.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_155.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_156.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_158.png)

---

![](img/2220f93cadcaca2dfe0e327d8d583653_160.png)

## 📜 策略与策略评估

![](img/2220f93cadcaca2dfe0e327d8d583653_162.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_164.png)

在MDP中，我们做出的决策序列称为**策略 (π)**。策略是一个函数，它根据当前状态告诉我们该采取什么行动，即 `行动 = π(状态)`。

![](img/2220f93cadcaca2dfe0e327d8d583653_166.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_168.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_170.png)

我们面临两个核心问题：
1.  **策略评估**：给定一个策略，它有多好？即它的期望总奖励是多少？
2.  **策略优化**：如何找到最好的策略？

![](img/2220f93cadcaca2dfe0e327d8d583653_172.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_174.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_176.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_178.png)

首先解决评估问题。策略的价值取决于你执行该策略的**时间步数**，我们称之为**规划期界 (H)**。例如，你的租约还剩H个生长季。

![](img/2220f93cadcaca2dfe0e327d8d583653_180.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_182.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_184.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_186.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_188.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_190.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_192.png)

定义 `V^H_π(s)` 为：从状态 `s` 开始，执行策略 `π` 恰好 `H` 步所获得的**期望总奖励**。

![](img/2220f93cadcaca2dfe0e327d8d583653_194.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_196.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_198.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_200.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_202.png)

我们可以递归地计算它：
*   **基础情况**：`V^0_π(s) = 0`。没有时间了，奖励为0。
*   **递归情况** (H ≥ 1):
    `V^H_π(s) = R(s, π(s)) + Σ_{s' in S} [ T(s, π(s), s') * V^{H-1}_π(s') ]`
    *   第一部分 `R(s, π(s))` 是当前步的即时奖励。
    *   第二部分是对所有可能的下一个状态 `s'` 求和，考虑转移到 `s'` 的概率 `T(...)`，以及从 `s'` 开始剩余 `H-1` 步的期望奖励 `V^{H-1}_π(s')`。

![](img/2220f93cadcaca2dfe0e327d8d583653_204.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_206.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_208.png)

**示例：两个农民的策略**
*   **农民A的策略 (π_A)**：总是种植。
*   **农民B的策略 (π_B)**：如果土壤肥沃就种植，如果贫瘠就休耕。

![](img/2220f93cadcaca2dfe0e327d8d583653_210.png)

通过上述公式计算不同期界H下，从不同状态开始的 `V^H_π`，我们发现：
*   当 `H=1`（只剩一季）时，`π_A` 优于 `π_B`（因为最后一季应贪婪地获取最大即时奖励）。
*   当 `H=3`（还剩三季）时，`π_B` 优于 `π_A`（因为 `π_B` 通过休耕来改善土壤，从而在长期获得更高总奖励）。
*   当 `H=2` 时，没有绝对优劣，取决于起始状态。

![](img/2220f93cadcaca2dfe0e327d8d583653_212.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_214.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_216.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_218.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_220.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_222.png)

这说明**最优策略可能依赖于剩余的决策步数（期界）**。允许策略随期界变化的策略称为**非平稳策略**。

---

![](img/2220f93cadcaca2dfe0e327d8d583653_224.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_226.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_228.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_230.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_232.png)

## 🏆 寻找最优策略：Q函数与值迭代

![](img/2220f93cadcaca2dfe0e327d8d583653_234.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_236.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_238.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_240.png)

我们不仅想评估给定策略，更想找到**最优策略** `π*`，即在所有可能策略中能获得最高期望总奖励的策略。

![](img/2220f93cadcaca2dfe0e327d8d583653_242.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_244.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_246.png)

为此，我们引入 **Q函数** `Q^H(s, a)`。它表示：从状态 `s` 开始，**立即采取行动 `a`**，然后在后续的 `H-1` 步中**遵循最优策略**所能获得的期望总奖励。

![](img/2220f93cadcaca2dfe0e327d8d583653_248.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_250.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_252.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_254.png)

Q函数也可以递归计算：
*   **基础情况** (H=1): `Q^1(s, a) = R(s, a)`。只剩一步，奖励就是即时奖励。
*   **递归情况** (H > 1):
    `Q^H(s, a) = R(s, a) + Σ_{s' in S} [ T(s, a, s') * max_{a'} Q^{H-1}(s', a') ]`
    *   第一部分是即时奖励。
    *   第二部分是考虑所有可能的下一个状态 `s'`，以及从 `s'` 开始剩余 `H-1` 步时，**选择能最大化未来奖励的最优行动 `a'`** 所对应的Q值。

![](img/2220f93cadcaca2dfe0e327d8d583653_256.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_258.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_260.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_262.png)

一旦我们计算出所有状态和行动在期界H下的Q值，**最优策略**就很容易得到：在当前状态 `s`，选择使 `Q^H(s, a)` 最大的行动 `a`。
`π*_H(s) = argmax_{a in A} Q^H(s, a)`

![](img/2220f93cadcaca2dfe0e327d8d583653_264.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_266.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_268.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_270.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_272.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_273.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_275.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_277.png)

这种从 `H=0` 开始，逐步计算 `H=1,2,3,...` 的Q值，并导出最优策略的方法，称为**有限期界值迭代**。

![](img/2220f93cadcaca2dfe0e327d8d583653_279.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_281.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_283.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_285.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_287.png)

在我们的农场例子中，计算 `H=2` 的Q值后发现：
*   起始状态为**肥沃**时，`Q^2(肥沃, 种植) > Q^2(肥沃, 休耕)`，所以应选择**种植**。
*   起始状态为**贫瘠**时，`Q^2(贫瘠, 休耕) > Q^2(贫瘠, 种植)`，所以应选择**休耕**。
这验证了最优策略确实依赖于状态和期界。

![](img/2220f93cadcaca2dfe0e327d8d583653_289.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_291.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_293.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_294.png)

---

![](img/2220f93cadcaca2dfe0e327d8d583653_296.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_298.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_300.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_302.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_304.png)

## ∞ 无限期界与折扣因子

![](img/2220f93cadcaca2dfe0e327d8d583653_306.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_308.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_310.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_312.png)

如果规划期界是无限的（例如，你永久拥有这块地），前述的递归公式会变成无限求和，可能导致总奖励无穷大。此外，经济学常识告诉我们，**当前获得的奖励比未来获得的等额奖励更有价值**。

![](img/2220f93cadcaca2dfe0e327d8d583653_314.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_316.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_318.png)

为此，我们引入**折扣因子 γ** (0 < γ < 1)。未来第 `t` 步获得的奖励 `r_t`，其当前价值为 `γ^t * r_t`。γ 越接近1，表示越重视未来奖励；越接近0，表示越重视即时奖励。

![](img/2220f93cadcaca2dfe0e327d8d583653_320.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_322.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_324.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_326.png)

在无限期界下，策略 `π` 的**值函数** `V_π(s)` 定义为从状态 `s` 开始，遵循 `π` 所获得的**折扣期望总奖励**。它满足**贝尔曼期望方程**：
`V_π(s) = R(s, π(s)) + γ * Σ_{s' in S} [ T(s, π(s), s') * V_π(s') ]`

![](img/2220f93cadcaca2dfe0e327d8d583653_328.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_330.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_332.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_334.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_336.png)

同样，我们可以定义无限期界的 **Q函数** 和 **贝尔曼最优方程**，并通过类似值迭代的算法（如**策略迭代**）来求解最优策略。折扣因子 γ 确保了这些方程有唯一解。

![](img/2220f93cadcaca2dfe0e327d8d583653_338.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_340.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_342.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_344.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_346.png)

---

![](img/2220f93cadcaca2dfe0e327d8d583653_348.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_350.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_352.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_354.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_356.png)

## 📚 总结

![](img/2220f93cadcaca2dfe0e327d8d583653_357.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_359.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_361.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_363.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_365.png)

本节课我们一起学习了：
1.  **状态机**：一个描述系统状态如何根据输入确定性变化的模型。
2.  **马尔可夫决策过程**：扩展了状态机，加入了**奖励函数**以评估决策优劣，以及**随机转移模型**以描述现实世界的不确定性。MDP是序列决策问题的基本框架。
3.  **策略与评估**：策略是状态到行动的映射。我们可以递归地计算一个策略在给定期界内的期望总奖励 `V^H_π(s)`。
4.  **寻找最优策略**：通过定义和计算 **Q函数** `Q^H(s, a)`，我们可以使用**有限期界值迭代**算法找到最优策略。最优策略可能依赖于剩余步数（非平稳）。
5.  **无限期界与折扣**：对于无限期界问题，我们引入**折扣因子 γ** 来比较不同时间点奖励的价值，并确保数学上的可解性。

![](img/2220f93cadcaca2dfe0e327d8d583653_367.png)

![](img/2220f93cadcaca2dfe0e327d8d583653_369.png)

通过农场管理的贯穿案例，我们看到了如何将实际问题建模为MDP，并利用这些工具来分析和优化长期的决策序列。