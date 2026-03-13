# 37：策略改进的近似边界 🔬

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_1.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_3.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_5.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_7.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_9.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_11.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_13.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_15.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_17.png)

在本节课中，我们将学习如何通过数学推导，证明在特定条件下，一个易于处理的目标函数可以很好地近似真实的强化学习目标。核心在于理解当新旧策略足够接近时，我们可以忽略状态分布的变化，从而得到一个有理论保证的策略改进方法。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_19.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_21.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_23.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_25.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_27.png)

---

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_29.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_31.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_33.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_35.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_36.png)

上一节我们讨论了策略梯度方法的基础。本节中，我们来看看如何为策略改进建立一个可靠的近似边界。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_38.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_40.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_42.png)

我们探讨在何种情况下，可以使用策略 $\pi_{\theta}$ 下的状态分布 $p_{\theta}(s_t)$ 来近似新策略 $\pi_{\theta‘}$ 下的分布 $p_{\theta’}(s_t)$，并仍然得到一个能准确近似新策略回报的合理目标。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_44.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_46.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_48.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_50.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_52.png)

具体做法是忽略分布不匹配的问题。我们使用 $p_{\theta}(s_t)$ 而非 $p_{\theta‘}(s_t)$，使得在整个方程中，$\theta’$ 的唯一依赖只出现在重要性权重上。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_54.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_56.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_58.png)

从之前的策略梯度讲座中我们知道，如果对等式右侧的表达式求导，我们恰好能得到策略梯度。我们希望这个性质成立，以便 $J(\theta‘) - J(\theta)$ 能被一个带横杠的近似量 $\bar{J}$ 很好地近似。这样，我们只需最大化 $\bar{J}$ 就能得到更好的新策略。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_60.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_62.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_64.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_66.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_68.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_70.png)

我们试图证明的是：当 $\pi_{\theta}$ 接近 $\pi_{\theta‘}$ 时，$p_{\theta}(s_t)$ 接近 $p_{\theta’}(s_t)$。当这种情况发生时，右侧近似左侧，意味着它们之间的差异可以被一个量所限制。这个量在 $\pi_{\theta}$ 和 $\pi_{\theta‘}$ 差异很小时也很小。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_72.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_74.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_76.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_78.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_80.png)

---

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_82.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_84.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_86.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_88.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_90.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_92.png)

### 确定性策略的情况 🎯

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_94.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_96.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_98.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_100.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_102.png)

首先，我们从简单情况开始分析，假设 $\pi_{\theta}$ 是一个确定性策略。这意味着我们可以将其表示为 $a_t = \pi_{\theta}(s_t)$。我们稍后会将其推广到随机策略。确定性策略的推导提供了一些直觉，使得随机情况更容易理解。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_104.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_106.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_108.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_110.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_112.png)

在这种情况下，我们试图证明：如果 $\pi_{\theta‘}$ 接近 $\pi_{\theta}$，那么 $\theta’$ 和 $\theta$ 的状态边缘分布也将接近。现在 $\pi_{\theta‘}$ 不一定是确定性的。我们定义“接近”的方式是：$\pi_{\theta’}$ 分配给任何不是 $\pi_{\theta}$ 所分配的动作的概率小于或等于 $\epsilon$。本质上，$\pi_{\theta‘}$ 做出不同决策的概率是有限的。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_114.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_116.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_118.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_120.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_122.png)

以下是基于此假设的推导步骤：
1.  时间步 $t$ 处 $\theta‘$ 的边缘状态分布可以写为两项之和。
2.  第一项描述了从初始时间步开始，新策略 $\pi_{\theta’}$ 在所有步骤中都与 $\pi_{\theta}$ 做相同事情的情况。
3.  由于每一步都做相同事情的概率是 $(1-\epsilon)$，这个项前面有一个乘数 $(1-\epsilon)^t$，并且其状态分布等于 $p_{\theta}(s_t)$。
4.  第二项包含了所有其他情况（即至少犯了一次错误），其概率为 $1 - (1-\epsilon)^t$，对应某个我们一无所知的其他状态分布 $p_{\text{error}}$。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_124.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_126.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_127.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_129.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_131.png)

这个方程与我们之前在分析行为克隆时遇到的方程完全相同。它暗示了 $p_{\theta‘}(s_t)$ 与 $p_{\theta}(s_t)$ 之间的总变分距离（Total Variation Distance）主要由第二部分贡献。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_133.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_135.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_137.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_139.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_141.png)

因此，状态边缘分布的总变分距离满足以下不等式：
$$ TV(p_{\theta‘}, p_{\theta}) \leq 2[1 - (1-\epsilon)^t] $$
利用不等式 $(1-\epsilon)^t \geq 1 - \epsilon t$（对于 $\epsilon \in [0,1]$），我们可以得到一个更简洁的界限：
$$ TV(p_{\theta‘}, p_{\theta}) \leq 2 \epsilon t $$
这个界限表明，随着 $\epsilon$ 减小（即策略越接近），状态分布也越相似。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_142.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_144.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_146.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_148.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_150.png)

---

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_152.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_154.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_156.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_158.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_160.png)

上一节我们分析了确定性策略的情况。本节中，我们将其推广到更一般的随机策略。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_162.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_164.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_166.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_168.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_170.png)

### 随机策略的一般情况 🎲

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_172.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_174.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_176.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_178.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_180.png)

这个证明遵循信任区域策略优化（Trust Region Policy Optimization, TRPO）论文中的方法。这里，我们说 $\pi_{\theta‘}$ 接近 $\pi_{\theta}$，如果对于所有状态 $s$，它们的总变分距离被 $\epsilon$ 所限制。实际上，我们甚至可以使用一个期望上的界限，但逐点的界限更容易解释。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_182.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_184.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_186.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_188.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_190.png)

分析中需要使用一个有用的引理（来自TRPO论文）：
> 如果两个分布 $p(x)$ 和 $q(x)$ 的总变分距离 $TV(p, q) = \epsilon$，那么存在一个联合分布 $p(x, y)$，其边缘分布 $p(x)$ 和 $p(y)$ 就是原始的 $p$ 和 $q$，并且满足 $P(x = y) = 1 - \epsilon$。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_192.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_194.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_196.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_197.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_199.png)

这个引理的直观理解是：如果两个分布的总变分距离是 $\epsilon$，那么它们“不一致”的概率最多就是 $\epsilon$。这允许我们将确定性策略情况下的结果推广到随机策略。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_201.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_203.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_205.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_207.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_209.png)

因此，即使 $\pi_{\theta}$ 是随机的，只要 $\pi_{\theta‘}$ 和 $\pi_{\theta}$ 的总变分距离被 $\epsilon$ 限制，我们同样可以写出状态分布的界限：
$$ TV(p_{\theta‘}(s_t), p_{\theta}(s_t)) \leq 2 \epsilon t $$

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_211.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_213.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_215.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_217.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_219.png)

---

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_221.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_223.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_225.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_227.png)

### 目标函数期望值的界限 📊

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_229.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_231.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_233.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_235.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_237.png)

我们最终关心的是目标函数本身。我们想要将用优势函数表达的两个目标联系起来。为此，我们推导一个关于在两个不同分布下函数期望值的界限。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_239.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_241.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_243.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_245.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_247.png)

设 $f(s_t)$ 是一个关于状态的函数（在我们的案例中，它是一个涉及优势函数和重要性权重的复杂表达式）。我们可以将其在两个分布下的期望值联系起来。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_248.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_250.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_252.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_254.png)

以下是推导的核心不等式：
$$ \mathbb{E}_{s_t \sim p_{\theta‘}}[f(s_t)] \geq \mathbb{E}_{s_t \sim p_{\theta}}[f(s_t)] - TV(p_{\theta‘}, p_{\theta}) \cdot \max_{s_t} |f(s_t)| $$
这个不等式的推导方法是：将 $p_{\theta‘}$ 写成 $p_{\theta} + (p_{\theta’} - p_{\theta})$，然后利用总变分距离的定义进行放缩。理解这个推导对掌握后续内容很重要。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_256.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_258.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_260.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_262.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_264.png)

将我们对总变分距离的界限 $TV(p_{\theta‘}, p_{\theta}) \leq 2 \epsilon t$ 代入，我们得到：
$$ \mathbb{E}_{s_t \sim p_{\theta‘}}[f(s_t)] \geq \mathbb{E}_{s_t \sim p_{\theta}}[f(s_t)] - 2 \epsilon t \cdot C $$
其中 $C = \max_{s_t} |f(s_t)|$ 是一个常数。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_266.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_268.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_269.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_271.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_273.png)

在我们的具体问题中，$f(s_t)$ 是重要性采样估计器对优势函数的期望。优势函数 $A^{\pi}(s_t, a_t)$ 是未来累积奖励的期望，其最大值与时间步长 $T$（或折扣因子下的有效步长 $1/(1-\gamma)$）乘以最大单步奖励 $R_{\text{max}}$ 同阶。因此，常数 $C$ 的量级是 $O(T \cdot R_{\text{max}})$ 或 $O(R_{\text{max}}/(1-\gamma))$。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_275.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_277.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_279.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_281.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_283.png)

---

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_285.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_287.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_289.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_291.png)

### 结论与算法启示 💡

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_293.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_295.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_297.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_299.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_301.png)

综上所述，我们证明了以下结论：
最大化这个可处理的目标函数 $\bar{J}(\theta‘)$：
$$ \bar{J}(\theta’) = \mathbb{E}_{s_t \sim p_{\theta}} \left[ \mathbb{E}_{a_t \sim \pi_{\theta}} \left[ \frac{\pi_{\theta‘}(a_t|s_t)}{\pi_{\theta}(a_t|s_t)} A^{\pi_{\theta}}(s_t, a_t) \right] \right] $$
是最大化真实强化学习目标 $J(\theta‘)$ 的一个好方法，前提是新策略 $\pi_{\theta’}$ 在总变分距离上足够接近旧策略 $\pi_{\theta}$。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_303.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_304.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_306.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_308.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_310.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_312.png)

这个推导直接启示了我们应该使用哪种强化学习算法：**在每一步更新中，我们必须约束新策略不要偏离旧策略太远**。这样，通过梯度上升最大化 $\bar{J}(\theta‘)$（其梯度恰好是策略梯度），我们就能保证真实目标 $J(\theta’)$ 得到改进。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_314.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_316.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_318.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_320.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_322.png)

这为诸如**信任区域策略优化（TRPO）**和**近端策略优化（PPO）**等算法提供了核心的理论基础。这些算法通过不同的方式（如KL散度约束或裁剪目标函数）来实施“策略不要变化太大”这一约束，从而实现稳定、单调的策略改进。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_324.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_326.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_328.png)

---

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_330.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_332.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_334.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_336.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_338.png)

本节课中我们一起学习了如何为策略改进建立近似的理论边界。我们首先在确定性策略的设定下进行了推导，然后利用一个关键的联合分布引理将其推广到一般的随机策略。最后，我们得到了一个关键的不等式，表明只要新旧策略足够接近，一个易于优化的替代目标就能保证提升真实的策略性能。这为现代策略梯度算法中的核心约束提供了坚实的数学依据。