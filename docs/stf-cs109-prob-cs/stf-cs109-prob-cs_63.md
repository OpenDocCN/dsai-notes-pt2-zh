# 名字到年龄

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/name2age/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/name2age/)

***

由于名字流行趋势的变化，一个人的名字可以暗示他们的年龄。美国发布了一份数据，其中包含了在特定年份出生并使用特定名字的美国居民数量，这些数据基于社会保障申请。我们可以使用推理来计算逆概率分布：根据他们的名字更新对一个人年龄的信念。提醒一下，如果我知道某人的出生年份，我可以在一年内计算出他们的年龄。

查询名字：

`<canvas id="babyNamePMF" style="max-height: 400px;display:none">`

带有该名字的记录：

这个演示基于 1914 年至 2014 年美国社会保障申请的真实数据。感谢[`www.kaggle.com/kaggle/us-baby-names`](https://www.kaggle.com/kaggle/us-baby-names)整理数据。下载数据。

### 计算

美国社会保障申请数据为你提供了一个函数：`count(year, name)`，该函数返回在特定年份出生并使用特定名字的美国公民数量。你还可以访问一个包含美国所有曾经使用过的名字的列表`names`和一个包含所有年份的列表`years`。这个函数隐式地给出了关于名字和出生年份的联合概率。名字和出生年份的联合分配的概率可以估计为具有该名字并在该年出生的人数与数据集中总人数的比例。设$B$为某人的出生年份，$N$为他们的名字。我们将使用$k$表示数据集中的条目数：$ P(B = b,N = n) \approx \frac{\text{count}(b, n)} {k} $

我们真正想回答的问题是：在知道居民的名字是 Gary 的情况下，你认为他们出生于 1950 年的信念是什么？

我们可以通过应用随机变量的条件概率定义开始：$\P( B = 1950 | N = \text{Gary} ) = \frac{\P(N = \text{Gary} , B = 1950)}{\P(N = \text{Gary})}$ 注意：贝叶斯定理是此类推理任务的一个更典型选择。然而，在这种情况下，由于计算$P(B = b, N=n)$比计算$P(N=n | B=b)$更容易，因此它是必要的。这就是为什么我们使用了条件概率的定义。这种方法留下一个需要计算的项：$\P(N = \text{Gary})$，我们可以通过边际化来计算：$\P( N = \text{Gary}) = \sum_{y \in \text{years}} P(B = y,N = \text{Gary}) \approx \sum\limits_{y \in \text{years}} \frac{\text{count}(y, \text{Gary})}{k}$

将这些信息综合起来，我们得到：$$\begin{align*} \P( B = 1950 | N = \text{Gary} ) &= \frac{\P(N = \text{Gary} , B = 1950)}{\P(N = \text{Gary})} \\ &\approx \frac { \Big( \frac{\text{count}(1950, \text{Gary})} {k} \Big) } { \Big( \frac{ \sum\limits_{y \in \text{years}} \text{count}(y, \text{Gary})}{k} \Big) } \\ &\approx \frac { \text{count}(1950, \text{Gary}) } { \sum\limits_{y \in \text{years}} \text{count}(y, \text{Gary}) } \end{align*}$$

更普遍地，对于任何名字，我们可以计算出生年份的条件的概率质量函数：$$\begin{align*} \P( B = b | N = n ) &\approx \frac { \text{count}(b, n) } { \sum\limits_{y \in \text{years}} \text{count}(y, n) } \end{align*}$$

### 从出生年份到年龄

当然，如果$B$是一个人的出生年份，那么他们的年龄$A$大约是当前年份减去$B$。如果某人的生日在年底较晚，可能会相差一年，但我们现在忽略这个小的偏差。所以例如，如果我们认为一个人是在 1988 年出生的，那么当前年份就是他们的年龄 - 1988 =

### 假设

这个问题有很多假设，值得强调。事实上，每次我们根据稀少的信息进行概括（尤其是关于人口统计数据）时，我们都应该谨慎行事。以下是我能想到的假设：

1.  这份数据仅适用于美国人的名字。在其他国家，根据名字给出的年龄概率可能会有很大差异。

1.  美国人口普查并不完美。它没有捕捉到所有居住在美国的人，而且有一些人口统计数据没有得到充分代表。这也会影响我们的结果。

### 揭示年龄的名字

一些名字在特定年份特别流行，这些名字提供了关于出生年份的大量信息。让我们看看一些具有最高最大概率的名字。

**中等流行度（>10,000 人使用该名字）**

| 姓名 | 最大概率年龄 | 最可能年龄的概率 |
| --- | --- | --- |
| Katina | 49 | 0.245 |
| Marquita | 38 | 0.233 |
| Ashanti | 19 | 0.250 |
| Miley | 13 | 0.250 |  |
| Aria | 7 | 0.247 |

**高流行度（>100,000 人使用该名字）**

| 姓名 | 最大概率年龄 | 最可能年龄的概率 |
| --- | --- | --- |
| Debbie | 62 | 0.104 |
| Whitney | 35 | 0.098 |
| Chelsea | 29 | 0.103 |
| Aidan | 18 | 0.098 |
| Addison | 14 | 0.112 |

搜索“Katina 1972”显示了一篇关于 1972 年一个名叫 Katina 的婴儿的有趣文章，这篇文章来自[CBS 肥皂剧](http://www.nancy.cc/2012/01/25/baby-name-katina/)。[Marquita](https://www.youtube.com/watch?v=K2LcWa4G0W4)的流行可能源于 1983 年的一个[牙膏广告](https://www.youtube.com/watch?v=K2LcWa4G0W4)。[Ashanti Douglas](https://en.wikipedia.org/wiki/Ashanti_(singer))和[Miley Cirus](https://en.wikipedia.org/wiki/Miley_Cyrus)分别在 2002 年和 2008 年成为了流行的歌手。

### 进一步阅读

一些名字似乎没有足够的数据来做出良好的概率估计。我们能否量化这种概率估计的不确定性？例如，如果一个名字在数据库中只有 10,000 条记录，其中只有 100 人在 1950 年出生，我们对于 1950 年真实概率为$\frac{100}{10000} = 0.01$的信心有多大？表达我们不确定性的方法之一是通过贝塔分布。在这种情况下，我们可以将我们对 1950 年概率的信念表示为$X \sim \Beta(a=101, b=9901)$，这反映了我们看到了 100 个在 1950 年出生的人，以及 9900 个不是在 1950 年出生的人。我们可以绘制这种信念，并聚焦于范围[0, 0.03]：

<canvas id="betaPdfnameBeta" style="max-height: 400px"></canvas>

现在，我们可以提出一些问题，例如，$X$在 0.01 附近 0.002 的概率是多少？

$$\begin{align*} P(&0.008 < X < 0.012) \\ &= P(X < 0.012) - P(X < 0.008) \\ &= F_X(0.012) - F_X(0.008) \\ &= 0.966 - 0.013 \\ &= 0.953 \end{align*}$$

从语义上讲，这导致了一个断言：在观察了 100 个在 1950 年出生的名字后，在整个数据集中，该名字有 10,000 个出生记录，有 95%的把握认为某人在 1950 年出生的概率是 0.010 $\pm$ 0.002。

</canvas>
