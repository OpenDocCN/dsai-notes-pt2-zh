# 概率和婴儿

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/prob_baby_delivery/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/prob_baby_delivery/)

* * *

这个演示曾经是实时的。我们现在知道，交付发生在 1 月 23 日。让我们回到 1 月 1 日，看看那时的概率是什么样的。

在劳拉今天分娩的概率（假设她今天之前还没有分娩）是多少？

今天的日期预产期

* * *

今天送达的概率：**未来 7 天内送达的概率：**逾期天数：**days

今天的无条件概率质量：******

********与预产期相比，人类分娩的可能性有多大？已经有数百万次分娩，这给我们提供了一个相对清晰的画面 [1]。人类怀孕的长度差异很大！你听说过怀孕是 9 个月吗？这是一个粗略的点估计。怀孕的平均持续时间为 278.6 天，怀孕长度有一个标准差（SD）为 12.5 天。这个分布不是正态分布，但大致符合"[偏态正态分布](https://en.wikipedia.org/wiki/Skew_normal_distribution)"。这是从数十万女性收集的第一胎的一般概率质量函数（这个 PMF 在人口统计学上非常相似，但根据女性是否分娩过而变化）：

<canvas id="unconditionalPMF" style="max-height: 400px"></canvas>

当然，我们还有更多信息。具体来说，我们知道劳拉**尚未**在今天之前分娩（当情况改变时，我们将更新这个例子）。我们还知道，超过 14 天晚期的婴儿会在第 14 天进行"[诱导](https://en.wikipedia.org/wiki/Labor_induction)"。如果我们今天还没有分娩，那么分娩的可能性有多大？请注意，y 轴的刻度不同：

<canvas id="conditionalPMF" style="max-height: 400px"></canvas>

让我们用推理的形式来解决这个问题。首先，我们引入一个随机变量$D$来表示婴儿出生后的天数。注意，如果婴儿在预产期之前出生，$D$可以是负数。我们可以使用推理来更新我们对$D$的信念，基于我们尚未分娩的观察：$$ \begin{align} \P(D = i | \text{No Baby Yet}) &= \frac{\P(\text{No Baby Yet} | D = i) \P(D = i)}{\P(\text{No Baby Yet})} \\ \end{align} $$

$\P(\text{No Baby Yet} | D = i)$始终是 1 或 0。注意，在$D=i$的条件下，我们被告知实际的分娩日期。如果分娩尚未发生（例如，今天是$i$之前），则“尚未分娩”的概率为 1。如果分娩已经发生（例如，今天是$i$之后），则“尚未分娩”的概率为 0。

$\P(D = i)$ 是我们的先验信念（基于历史数据的交货日期的概率）。$\P(\text{No Baby Yet})$ 是归一化常数。我们不必显式地计算它，而是可以计算每个 $i$ 值的分子。然后我们可以归一化分布（计算分子的总和，并将每个概率除以这个总和）以隐式地计算它。一个等效（但计算量更大的）解决方案是使用全概率公式展开 $\P(\text{No Baby Yet})$：$$ \P(\text{No Baby Yet}) = \sum_i \P(\text{No Baby Yet} | D = i) \P(D = i) $$

我们如何处理 $D = 14$ 后婴儿被催产的事实呢？我们可以调整我们的先验，使得所有 14 天及以后的概率都转移到第 14 天。这相当于以下计算：$$ \P(D = 14) = \sum_{i \geq 14} \P(D = i) $$

```py
def update_belief_baby(prior, today = -19):
	# pr_D[i] is P(D = i| No Baby Yet).
	pr_D = {}
	min_i = -50
	max_i = 14
	for i in range(min_i, max_i + 1):
		 # P(NoBaby | D = i)
		 likelihood = 0 if i < today else 1
		 pr_D[i] = likelihood * prior[i]
	# implicitly computes the LOTP
	normalize(pr_D)
	return pr_D

def normalize(unormalized_pmf):
	total_sum = sum(unormalized_pmf.values())
	normalized = {}
	for key, value in unormalized_pmf.items():
		normalized[key] = value / total_sum
	return normalized 
```

* * *

### 扩展问题

克里斯还有两个其他的好朋友，他们的婴儿与他的预产期完全相同（真的！这确实发生了）。三个婴儿都在同一天出生的概率是多少？

三对夫妇在同一天的概率：

**我们是如何得到这个数字的？设 $p_i$ 为一个婴儿在 $i$ 天出生的概率——这个数字可以从概率质量函数中读出。设 $D_i$ 为三个婴儿都在 $i$ 天出生的事件。注意事件 $D_i$ 与三个婴儿在另一天出生的事件是互斥的（例如，$D_1$ 与 $D_2$，$D_3$ 等等是互斥的）。设 $N=3$ 为所有婴儿在同一天出生的事件：$$ \begin{align} \p(N=3) &= \sum_i \p(D_i) && \text{因为天数是互斥的} \\ &= \sum_i p_i³ && \text{因为三对夫妇是独立的} \end{align} $$**  *** * *

[1] [通过超声波和末次月经预测早期妊娠的分娩日期](https://www.sciencedirect.com/science/article/pii/S0029784400011315?casa_token=yV-QZInYkl8AAAAA:0U_Z2dT-r0y1etlX8hRG5ulyrjtzoVXRXIlvJkcSyXhtllUlkhWPNr5f3MJL0LMFzHZv5TwsN4Q)

致谢：这个问题最初是由克里斯·格雷格提出给我的。**********
