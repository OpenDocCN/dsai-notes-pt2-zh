# 79：控制即推断（第三部分）🎯

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_1.png)

在本节课中，我们将学习如何将控制问题视为概率推断问题，并利用变分推断工具来解决精确推断在复杂场景中不可行的问题。我们将重点探讨如何通过变分推断来修正之前提到的“乐观偏差”问题，并推导出与强化学习目标相似的算法。

---

## 概述

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_3.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_5.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_7.png)

在前面的课程中，我们看到了如何将控制框架视为特定图形模型中的推断。我们讨论了如何在该图形模型中进行精确推断，并理解了三种可能的推断问题：计算反向消息、计算策略以及计算向前消息。这些推断程序都是精确的。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_9.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_11.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_13.png)

然而，在状态空间复杂、高维、连续或动态未知（只能通过模拟采样）的设置中，我们需要进行**近似推断**。本节将使用变分推断工具来展示如何近似模型，并在此过程中解决“乐观偏差”问题。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_15.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_17.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_19.png)

---

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_21.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_23.png)

## 精确推断的局限性与乐观偏差

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_25.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_27.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_29.png)

上一节我们介绍了精确推断方法。本节中，我们来看看精确推断方法存在的一个核心问题：**乐观偏差**。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_31.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_33.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_35.png)

在精确推断中，状态向后消息和状态-动作向后消息的对数，可以被解释为类似于价值函数和Q函数。在对数空间下，我们得到了一个与价值迭代非常相似的算法，但其中动作的最大值被替换为**软最大值**，并且贝尔曼备份方程中有一个“期望值的指数对数”项。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_37.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_39.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_41.png)

这个备份方式的问题在于：**“期望值的指数对数”项会导致值函数被最幸运（即回报极高但概率极低）的状态所主导**。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_43.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_45.png)

**公式示例**：
考虑一个购买彩票的行动：有千分之一的机会获得巨额回报，其余机会回报为零。其期望值不高，但“期望值的指数对数”值会很高，因为计算过程会放大那个极低概率的积极结果的影响。这导致算法变得“乐观”，倾向于选择这种高风险、低期望值的行动。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_47.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_49.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_51.png)

这种现象发生的原因是，我们正在解决的推断问题是：**“在已知获得了高奖励（即轨迹最优）的条件下，最可能的轨迹是什么？”**。这相当于问：“假设你已经很成功（例如中了一百万），那么你更可能采取了什么行动？”。但这并不等同于“为了达到成功，最优的行动是什么？”。推断过程实际上会改变我们对动态（状态转移）的信念以符合“已获得高奖励”的证据，而在现实中，动态（环境规则）是不应改变的。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_52.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_54.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_56.png)

---

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_58.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_60.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_62.png)

## 使用变分推断修正乐观偏差

为了解决乐观偏差问题，我们希望找到一个近似分布，它接近后验分布，但**保持原始的状态转移动态不变**，只改变行动概率。这正是**变分推断**可以解决的问题。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_64.png)

我们将定义一个特殊的变分分布族 **q**：
*   它保持与原始问题相同的初始状态分布 `p(s1)` 和状态转移概率 `p(s_{t+1} | s_t, a_t)`。
*   它只学习一个新的部分：给定状态下的行动分布 `q(a_t | s_t)`。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_66.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_68.png)

**公式定义**：
```
q(τ) = q(s1, a1, ..., sT, aT) = p(s1) ∏_{t=1}^{T} p(s_{t+1} | s_t, a_t) q(a_t | s_t)
```
其中 `τ` 表示轨迹 `(s1, a1, ..., sT, aT)`。

我们的目标是让这个分布 `q(τ)` 去近似真实的后验分布 `p(τ | o_{1:T}=1)`，即已知整个轨迹最优的条件分布。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_70.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_72.png)

---

## 推导变分下界与强化学习目标

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_74.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_76.png)

根据变分推断原理，我们优化变分下界（ELBO）。将我们的定义代入ELBO公式后，一个关键的好处是：由于 `q` 中定义的初始状态和转移概率与真实模型 `p` 相同，它们在ELBO中相互抵消。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_78.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_80.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_82.png)

最终，我们得到的变分下界简化如下：

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_84.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_86.png)

**公式**：
```
log p(o_{1:T}=1) ≥ E_{(s_{1:T}, a_{1:T}) ~ q} [ ∑_{t=1}^{T} r(s_t, a_t) ] + ∑_{t=1}^{T} H(q(· | s_t))
```
其中 `H` 表示熵。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_88.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_90.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_92.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_94.png)

这个表达式具有清晰的物理意义：它等于**在策略 `q` 下的期望总奖励**，加上**策略在每个状态下的熵**。这正是**最大熵强化学习**的目标函数：既最大化累积奖励，又鼓励策略具有一定的随机性（探索性）。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_96.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_98.png)

通过变分推断，我们自然地推导出了这个目标，它修正了乐观偏差，因为变分分布 `q` 固定了真实的环境动态。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_100.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_102.png)

---

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_104.png)

## 优化方法：软价值迭代

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_106.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_108.png)

现在，我们有了一个需要最大化的目标（变分下界）。如何优化它呢？我们可以采用动态规划的思想，从最后一个时间步开始递归求解。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_110.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_112.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_114.png)

以下是求解过程的核心步骤：

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_116.png)

1.  **最后一个时间步（t=T）**：
    *   目标是在状态 `s_T` 下选择行动 `a_T`，最大化 `r(s_T, a_T) - log q(a_T | s_T)`。
    *   可以证明，该优化问题的最优解具有指数形式：
        ```
        q*(a_T | s_T) ∝ exp(r(s_T, a_T))
        ```
    *   此时，最优值函数为 `V_T(s_T) = log ∫ exp(r(s_T, a_T)) da_T`。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_118.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_120.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_122.png)

2.  **递归步骤（t < T）**：
    *   在时间步 `t`，我们需要考虑当前奖励和未来价值。
    *   定义软Q函数：`Q_t(s_t, a_t) = r(s_t, a_t) + E_{s_{t+1} ~ p} [V_{t+1}(s_{t+1})]`。这是一个常规的贝尔曼备份，没有乐观偏差。
    *   同样地，优化 `Q_t(s_t, a_t) - log q(a_t | s_t)` 得到最优策略：
        ```
        q*(a_t | s_t) ∝ exp(Q_t(s_t, a_t))
        ```
    *   对应的软价值函数为：`V_t(s_t) = log ∫ exp(Q_t(s_t, a_t)) da_t`。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_124.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_126.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_128.png)

这个过程可以总结为一个算法：**软价值迭代**。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_130.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_132.png)

**算法描述（软价值迭代）**：
```
初始化 V_{T+1}(s) = 0
for t = T to 1:
    # 贝尔曼备份（计算软Q值）
    Q_t(s, a) = r(s, a) + E_{s' ~ p(·|s,a)}[V_{t+1}(s')]
    # 软最大值（计算软V值）
    V_t(s) = log ∫_a exp(Q_t(s, a)) da
    # 提取最优策略
    π_t*(a | s) = exp(Q_t(s, a) - V_t(s))
```

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_134.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_136.png)

这个算法与经典的价值迭代非常相似，主要区别在于将“取最大值”操作替换为了“log-sum-exp”（即软最大值）操作。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_138.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_140.png)

---

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_142.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_144.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_146.png)

## 扩展与总结

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_148.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_150.png)

本节课中，我们一起学习了如何利用变分推断框架来解决控制即推断中的乐观偏差问题。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_152.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_154.png)

*   **核心思想**：通过定义一个保持环境动态不变的变分分布，我们将控制问题转化为一个最大化变分下界的优化问题。
*   **关键结果**：该下界恰好对应于**最大熵强化学习**目标：期望奖励加上策略熵。
*   **推导的算法**：通过动态规划优化该目标，我们得到了**软价值迭代**算法，它提供了计算最优软策略的方法。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_156.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_158.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_160.png)

此外，这个框架可以灵活扩展：
*   可以引入折扣因子 `γ`。
*   可以添加温度参数 `α` 来控制策略的随机性程度（`α → 0` 时接近确定性策略）。
*   可以推广到无限时域问题。

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_162.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_164.png)

![](img/2ccabd0b5daa7dec84d4c547f1bd89ad_166.png)

在下一部分，我们将讨论如何在实际中实例化这些想法，并介绍基于此框架的具体算法设计。