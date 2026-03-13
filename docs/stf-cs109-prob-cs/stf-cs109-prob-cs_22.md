# 随机洗牌

> [原文链接](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/random_shuffles/)

* * *

这里有一个令人惊讶的声明。如果你将一副标准牌洗七次，几乎可以肯定地说，牌的确切排序从未被见过！哇！让我们来探索一下。我们可以正式地提出这个问题：在从时间开始以来的$n$次洗牌中，你的排序是独一无二的概率是多少？

### 52 张牌的排序

我们的冒险从一个简单的观察开始：有**非常**多的方式来排序 52 张牌。但标准牌组的确切独特排序有多少呢？

有$52!$种方式来排序一副标准牌。由于每张牌都是独一无二的（每张牌都有独特的花色和数值组合），因此我们可以应用不同对象的排列规则：$$\begin{align*} \text{Num. Unique Orderings} &= 52! \end{align*}$$ 这是一个巨大的数字。$52!$等于 80658175170943878571660636856403766975289505440883277824000000000000。

那超过了$8 \cdot 10^{67}$。回想一下，据估计，可观测宇宙中有大约$10^{82}$个原子。

### 已见洗牌次数

当然，我们不知道$n$的值是多少——没有人计算过人类洗牌的次数。我们可以提出一个合理的过高估计。假设$k$ = 70 亿人自从发明牌以来每秒洗一次牌。扑克牌可能最早在 9 世纪的唐朝被发明。据我所知，最古老的 52 张牌是伊斯坦布尔的[托普卡比牌组](https://cards.old.no/1500-mamluk/)，大约在公元 15 世纪。这样，我们的过高估计是$n = s \cdot k \approx 10^{20}$。

接下来，让我们计算那些$n$次历史洗牌中没有一次与你特定的 52 张牌排序相匹配的概率。有两种有效的方法：使用等可能结果和使用独立性。

### 等可能结果

一种计算你 52 张牌的排序在历史上独一无二概率的方法是使用等可能结果. 考虑所有可能排序的所有已发牌的样本空间。这个集合中的每个结果都将有$n$个牌组，每个牌组都有自己的排序。因此，样本空间的大小是$|S| = (52!)^{n}$。注意，样本空间中的所有结果都是等可能的——我们可以通过对称性来说服自己——没有任何排序比其他排序更有可能。从那个样本空间中，我们想要计算没有排序与你匹配的结果数量。有$52! - 1$种方式来排序 52 张不是你的牌。我们可以通过步骤构建事件空间：对于历史上的每次$n$次洗牌，选择那些$52! - 1$种排序中的任意一种。因此，$|E| = (52!-1)^n$。

设 $U$ 为你 52 张牌的特定排序是唯一的 $$\begin{align*} \P(U) &= \frac{|E|}{|S|} && \text{等可能的结果}\\ &= \frac{(52!-1)^n}{(52!)^n} \\ &= \frac{(52!-1)^{10^{20}}}{(52!)^{10^{20}}} && n = 10^{20} \\ &= \Big(\frac{52!-1}{52!}\Big) ^{10^{20}} \end{align*}$$ 理论上这是正确的答案，但这些数字如此之大，以至于不清楚如何评估它，即使使用计算机。一个好主意是首先计算对数概率：$$\begin{align*} \log \P(U) &= \log \Big[\Big(\frac{52!-1}{52!}\Big) ^{10^{20}}\Big] \\ &= 10^{20} \cdot \log \Big(\frac{52!-1}{52!}\Big) \\ &= 10^{20} \cdot \Big[ \log (52!-1) - \log(52!) \Big] \\ &= 10^{20} \cdot (-1.24 \times 10^{-68}) \\ &= -1.24 \times 10^{-48} \end{align*}$$ 现在如果我们取消对数（并使用 $e^{-x}$ 对于小的 $x$ 值非常接近 $1 - x$ 的这一事实）：$$\begin{align*} \P(U) &= e^{-1.24 \times 10^{-48}} \\ &\approx 1 - 1.24 \times 10^{-48} \end{align*}$$

因此，你特定排序是唯一的概率非常接近于 $1$，而其他人得到相同排序的概率，$1 - P(U)$，是一个小数点后有 47 个零的数字。可以肯定地说，你的排序是唯一的。

在 python 中，你可以使用一个名为 decimal 的特殊库来计算非常小的概率。以下是如何计算 $\log \frac{52!-1}{52!}$ 的一个例子：

```py
from decimal import *
import math

n = math.pow(10, 20)
card_perms = math.factorial(52)
denominator = card_perms
numerator = card_perms - 1

# decimal library because these are tiny numbers
getcontext().prec = 100 # increase precision
log_numer = Decimal(numerator).ln()
log_denom = Decimal(denominator).ln()
log_pr = log_numer - log_denom

# approximately -1.24E-68
print(log_pr)
```

我们还可以使用[二项式近似](https://en.wikipedia.org/wiki/Binomial_approximation)来检查我们的结果。

对于小的 $x$ 值，$(1 - x)^n$ 的值非常接近于 $1 - nx$，这为我们计算 $P(U)$ 提供了另一种方法：$$\begin{align*} \P(U) &= \frac{(52!-1)^n}{(52!)^n} \\ &= \Big(1 - \frac{1}{52!}\Big)^{10^{20}} && n = 10^{20} \\ &\approx 1 - \frac{10^{20}}{52!} \\ &\approx 1 - 1.24 \times 10^{-48} \end{align*}$$

这与使用 python 的 decimal 库得到的结果一致。

### 独立性

另一种方法是定义事件 $D_i$，即第 $i$ 张牌的洗牌不同于你的。因为我们假设每次洗牌都是独立的，所以 $P(U) = \prod_i P(D_i)$。$(D_i)$ 的概率是多少？如果你考虑 $D_i$ 的样本空间，它是以 52!种方式排序一副牌。事件空间是除了你的排序之外的 52! - 1 种结果。

$$\begin{align*} \P(U) &= \prod_{i=1}^n \P(D_i) \\ \log \P(U) &= \sum_{i=1}^n \log \P(D_i) \\ &= n \cdot \log \P(D_i) \\ &= 10^{20} \cdot \log \frac{52!-1}{52!}\\ &\approx 10^{20} \cdot -1.24 \times 10^{-68} \end{align*}$$ 这与另一种方法得到 $\log \P(U)$ 的答案相同

### 你的洗牌有多随机？

一个我们可以探讨的最终问题。如何得到一张真正随机的牌序？1992 年，Dave Bayer 和 Persi Diaconis 研究了这个问题，并在文章[追踪 dovetail shuffle 至其巢穴](https://www.projecteuclid.org/journals/annals-of-applied-probability/volume-2/issue-2/Trailing-the-Dovetail-Shuffle-to-its-Lair/10.1214/aoap/1177005705.full)中发表了他们的研究结果。他们展示了如果你使用[ riffle shuffle](https://en.wikipedia.org/wiki/Shuffling)（也称为 dovetail shuffle）的方式洗牌七次，几乎可以保证得到一张随机排序的牌。他们使用的方法为研究计算机产生的伪随机数铺平了道路。
