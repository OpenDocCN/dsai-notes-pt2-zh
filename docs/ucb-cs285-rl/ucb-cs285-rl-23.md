# 23：演员-评论家算法的实现与离策略扩展 🎓

![](img/d842ad3eeced91a1e3bc013e2f9751d2_1.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_3.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_5.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_7.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_9.png)

在本节课中，我们将学习如何将演员-评论家算法实现为深度强化学习算法，并探讨其离策略扩展。我们将讨论神经网络架构的设计选择、并行化以提高样本效率，以及如何修改算法以利用历史经验数据（回放缓冲区）。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_11.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_13.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_15.png)

---

![](img/d842ad3eeced91a1e3bc013e2f9751d2_17.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_19.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_21.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_23.png)

## 🏗️ 神经网络架构设计

![](img/d842ad3eeced91a1e3bc013e2f9751d2_25.png)

在上一节中，我们讨论了策略梯度。本节中，我们将看看如何表示价值函数和策略。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_27.png)

为了将算法实例化为深度强化学习算法，我们必须决定如何表示价值函数和策略。我们有几个选择。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_29.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_31.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_33.png)

以下是两种主要的网络设计选择：

![](img/d842ad3eeced91a1e3bc013e2f9751d2_35.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_37.png)

1.  **完全分离的网络**
    *   一个网络将状态映射到价值。
    *   另一个完全独立的网络将同一个状态映射到动作的分布。
    *   这两个网络不共享任何参数。
    *   **优点**：实现相对简单，训练通常更稳定。
    *   **缺点**：演员和评论家之间没有特征共享，可能效率较低，尤其是在从图像等原始输入学习时。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_39.png)

2.  **共享网络设计**
    *   一个共享的“主干”网络（例如卷积层）处理输入状态，提取特征。
    *   然后，有两个独立的“头”网络：
        *   一个用于输出价值。
        *   一个用于输出策略的动作分布。
    *   **优点**：允许特征共享，可能更高效。
    *   **缺点**：训练更具挑战性，可能不稳定，因为共享层同时被价值回归和策略梯度这两个不同分量更新，可能需要更多的超参数调整。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_41.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_43.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_45.png)

---

![](img/d842ad3eeced91a1e3bc013e2f9751d2_47.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_49.png)

## 🔄 并行化与批次处理

![](img/d842ad3eeced91a1e3bc013e2f9751d2_51.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_53.png)

上一节我们介绍了网络架构，本节中我们来看看如何提高数据效率。基本的演员-评论家算法是在线的，一次只用一个样本更新，这会导致高方差的更新。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_55.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_57.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_59.png)

从深度学习原理可知，使用随机梯度下降更新深度神经网络时，仅使用一个样本效果不佳。因此，最好使用一个批次的样本进行更新。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_61.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_63.png)

获取批次的一种方式是通过使用并行工作者。以下是两种并行化方法：

![](img/d842ad3eeced91a1e3bc013e2f9751d2_65.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_67.png)

*   **同步并行演员-评论家**
    *   运行多个模拟器（工作者线程），每个使用不同的随机种子。
    *   每个线程执行一步，收集一个转移样本。
    *   然后，同步地收集所有线程的数据，形成一个批次，用于统一更新价值函数和策略。
    *   批次大小等于工作者线程的数量。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_69.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_71.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_73.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_75.png)

*   **异步并行演员-评论家**
    *   移除同步点，各个线程以自己的速度独立运行。
    *   每个线程在更新时，会拉取最新的网络参数，使用自己收集的转移样本进行更新。
    *   更新时可能使用一个由多个线程收集的、固定大小的转移池（例如32个转移）。
    *   **潜在问题**：转移样本可能由略微过时的策略生成，因为线程进度不同。但只要延迟不大，在实践中，异步带来的速度提升通常能抵消由此产生的微小偏差。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_77.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_79.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_81.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_83.png)

---

![](img/d842ad3eeced91a1e3bc013e2f9751d2_84.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_86.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_88.png)

## 📦 离策略演员-评论家与回放缓冲区

![](img/d842ad3eeced91a1e3bc013e2f9751d2_90.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_92.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_94.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_96.png)

异步方法让我们思考：如果能使用由旧策略生成的转移，或许我们甚至不需要多个线程，可以直接复用历史数据。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_98.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_100.png)

这就是**离策略演员-评论家**的核心思想。我们引入一个**回放缓冲区**（通常实现为先进先出的环形缓冲区），用于存储历史转移经验。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_102.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_104.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_106.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_108.png)

以下是离策略算法的基本流程：

![](img/d842ad3eeced91a1e3bc013e2f9751d2_110.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_112.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_114.png)

1.  使用当前策略与环境交互，收集转移 `(s, a, r, s')`。
2.  将该转移存入回放缓冲区。
3.  从回放缓冲区中随机采样一个批次的转移（例如32个）。
4.  使用这个批次来更新评论家（价值函数）和演员（策略）。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_116.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_118.png)

然而，直接应用之前的算法会出问题，因为缓冲区中的动作 `a` 是由旧策略 `π_old` 生成的，而不是当前策略 `π_θ`。这导致两个主要问题：
1.  计算价值目标时，使用的不是当前策略下的预期回报。
2.  计算策略梯度时，采样的动作并非来自当前策略，破坏了策略梯度定理的前提。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_120.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_122.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_124.png)

---

![](img/d842ad3eeced91a1e3bc013e2f9751d2_126.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_128.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_130.png)

## 🛠️ 离策略修正：从 V 到 Q

![](img/d842ad3eeced91a1e3bc013e2f9751d2_132.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_134.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_136.png)

为了解决上述问题，我们需要修改算法。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_138.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_139.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_141.png)

首先，我们不再学习状态价值函数 `V(s)`，而是学习**状态-动作价值函数 Q(s, a)**。Q 函数评估在状态 `s` 下执行任意动作 `a`，然后遵循策略 `π` 所能获得的预期回报。这样，即使动作 `a` 来自旧策略，我们也能有效地训练 Q 函数。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_143.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_145.png)

**Q 函数的更新目标**变为：
`y_i = r_i + γ * Q_φ(s‘_i, a‘_i)`
其中 `a‘_i` 是**当前策略 `π_θ`** 在状态 `s‘_i` 下会采取的动作。我们可以通过查询当前策略网络来获得这个动作，而无需与环境交互。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_147.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_149.png)

---

![](img/d842ad3eeced91a1e3bc013e2f9751d2_151.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_153.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_155.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_157.png)

## 🎯 离策略策略梯度

![](img/d842ad3eeced91a1e3bc013e2f9751d2_159.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_161.png)

接下来，我们修正策略梯度。对于缓冲区中的每个状态 `s_i`，我们询问当前策略会采取什么动作，记作 `a_i^π`。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_163.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_165.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_167.png)

然后，我们使用 Q 值来构建策略梯度估计。在实践中，为了简便，我们常直接使用 Q 值而非优势函数：
`∇_θ J(θ) ≈ (1/N) * Σ_i [ ∇_θ log π_θ(a_i^π | s_i) * Q_φ(s_i, a_i^π) ]`
这样做方差较高（因为没有基线），但由于我们可以低成本地从策略中采样多个 `a_i^π` 来平均（只需运行网络，无需模拟），因此可以接受。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_169.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_171.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_173.png)

---

![](img/d842ad3eeced91a1e3bc013e2f9751d2_175.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_177.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_179.png)

## ⚠️ 注意事项与总结

![](img/d842ad3eeced91a1e3bc013e2f9751d2_181.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_183.png)

本节课中，我们一起学习了演员-评论家算法的深度实现与离策略扩展。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_185.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_187.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_189.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_191.png)

*   **架构选择**：分离网络简单稳定，共享网络可能更高效但难调。
*   **并行化**：同步和异步并行可以提高数据利用率和学习速度。
*   **离策略学习**：通过引入回放缓冲区和学习 Q 函数，我们可以复用历史数据，但需要仔细修正价值目标和策略梯度计算。
*   **剩余偏差**：即使进行了上述修正，状态 `s` 本身的分布仍然来自旧策略，这引入了偏差。但直觉上，回放缓冲区包含了更广泛的状态分布，这通常有助于学习，且不会错过当前策略访问的重要状态。

![](img/d842ad3eeced91a1e3bc013e2f9751d2_193.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_195.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_197.png)

![](img/d842ad3eeced91a1e3bc013e2f9751d2_198.png)

一个基于这些思想的著名实用算法是**软演员-评论家**。在后续关于 Q 学习的课程中，我们将深入探讨更复杂的离策略方法。