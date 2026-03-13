# 陪审团选择

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/jury/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/jury/)

* * *

在最高法院案件：Berghuis 诉 Smith 中，最高法院（美国）讨论了以下问题：“如果陪审团池中某个群体代表性不足，你如何判断？”

法官 Breyer（斯坦福校友）通过引用二项式定理开始了提问。他假设了一个场景，涉及“一个装有千个球的花瓶，其中六十个是红色，九百四十个是绿色，然后你随机选择它们……每次十二个。”根据法官 Breyer 和二项式定理，如果红球代表黑人陪审员，那么“你预计……大约三分之一的陪审团至少会有一个黑人陪审员。”

注意：在这场对话中缺失的是在做出艰难决定时，多元背景所具有的力量。

* * *

## 模拟：

<canvas style="width:770px; height:100px;" id="simCanvas"></canvas>

* * *

## 说明：

从技术上讲，由于陪审员是随机选择的，你应该将代表性不足的陪审员数量表示为超几何随机变量（在 CS109 中我们不明确考虑的随机变量）。

$$\begin{align*}X \sim \text{HypGeo}(n=12, N = 1000, m = 60)\end{align*}$$

$$\begin{align*} P(X \geq 1) &= 1 - P(X = 0) \\ &= 1 - \frac{ {60 \choose 0}{940 \choose 12} }{1000 \choose 12} \\ &\approx 0.5261 \end{align*}$$

然而，法官 Breyer 通过引用二项式分布来论证。这不是二项式分布的完美应用，因为二项式分布假设每个实验成功的可能性（$p$）是相等的。由于陪审员是随机选择的，每次选择后得到少数族裔陪审员的可能性都会略有变化（并取决于选择的结果）。然而，正如我们将看到的，由于概率变化不大，二项式分布并不太偏离。

$$\begin{align*} X \sim \text{Binomial}(n=12, p = 60/1000) \end{align*}$$

$$\begin{align*} P(X \geq 1) &= 1 - P(X = 0) \\ &= 1 - {60 \choose 0}(1- 0.06)^{12} \\ &\approx 0.5241 \end{align*}$$

* * *

致谢：问题由 Mehran Sahami 提出并解决
