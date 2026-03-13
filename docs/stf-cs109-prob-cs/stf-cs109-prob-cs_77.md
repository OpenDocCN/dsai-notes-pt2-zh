# 自举法

> [原文链接](https://chrispiech.github.io/probabilityForComputerScientists/en/part4/bootstrapping/)

* * *

自举法是一种新发明的统计技术，用于理解统计量的分布和计算 $p$-值（$p$-值是一个科学主张错误的概率）。它是在 1979 年在这里斯坦福发明的，当时数学家们刚开始理解计算机和计算机模拟如何被用来更好地理解概率。

第一个关键洞见是：如果我们能访问基础分布（$F$），那么回答我们可能提出的关于我们的统计量准确性的任何问题都变得简单直接。例如，在前一节中，我们给出了如何从大小为 $n$ 的样本中计算样本方差的公式。我们知道在期望中，我们的样本方差等于真实方差。但如果我们想知道真实方差在计算出的数值的某个范围内，这个概率是多少？这个问题可能听起来很枯燥，但它对于评估科学主张是至关重要的！如果你知道基础分布 $F$，你可以简单地重复从 $F$ 中抽取大小为 $n$ 的样本的实验，从我们的新样本中计算样本方差，并测试有多少部分落在某个范围内。

自举法的下一个洞见是，我们能从样本本身得到对 $F$ 的最佳估计！估计 $F$ 的最简单方法（我们将在本课程中使用的方法）是假设 $P(X=k)$ 就是 $k$ 在样本中出现的频率的分数。请注意，这定义了我们估计 $F$ 的概率质量函数 $\hat{F}$。

```py
def bootstrap(sample):
   N = number of elements in sample
   pmf = estimate the underlying pmf from the sample
   stats = []
   repeat 10,000 times:
      resample = draw N new samples from the pmf
      stat = calculate your stat on the resample
      stats.append(stat)
   stats can now be used to estimate the distribution of the stat
```

自举法是合理的事情去做，因为你所拥有的样本是你关于基础总体分布实际看起来如何的最佳和唯一信息。此外，大多数样本如果它们是随机选择的，看起来会非常像它们所来自的总体。

要计算 $\text{Var}(S²)$，我们可以为每个重采样 $i$ 计算 $S_i²$，并在 10,000 次迭代后，我们可以计算所有 $S_i²$ 的样本方差。你可能想知道为什么重采样的大小与原始样本（$n$）相同。答案是，你所计算的统计量的变异性可能取决于样本的大小（或重采样的大小）。为了准确估计统计量的分布，我们必须使用相同大小的重采样。

自举法有强大的理论保证，并被科学界接受。当基础分布有一个“长尾”或者样本不是独立同分布时，它就会失效。

## $p$-值计算的例子

我们试图弄清楚人们在不丹还是尼泊尔更快乐。我们在不丹抽取了$n_1 = 200$个个体，在尼泊尔抽取了$n_2 = 300$个个体，并要求他们对他们的幸福感进行 1 到 10 的评分。我们测量了两个样本的样本均值，并观察到尼泊尔的人稍微快乐一些——尼泊尔样本均值与不丹样本均值在幸福感量表上的差异是 0.5 分。

如果你想要使这个主张科学化，你应该计算一个$p$-值。$p$-值是指在零假设为真的情况下，测量的统计量等于或大于你所报告的值的概率。零假设是两个测量的现象之间没有关系或两组之间没有差异的假设。

在比较尼泊尔和不丹的情况下，零假设是尼泊尔和不丹的幸福分布没有差异。零假设的论点是：尼泊尔和不丹的幸福分布没有差异。当你抽取样本时，尼泊尔的平均值偶然比不丹高 0.5 分。

我们可以使用自助法来计算$p$-值。首先，我们通过从尼泊尔的全部样本和不丹的全部样本中制作一个概率质量函数来估计零假设的潜在分布。

```py
def pvalue_bootstrap(bhutan_sample, nepal_sample):
   N = size of the bhutan_sample
   M = size of the nepal_sample
   universal_sample = combine bhutan_samples and nepal_samples
   universal_pmf = estimate the underlying pmf of the universalSample
   count = 0
   observed_difference = mean(nepal_sample) - mean(bhutan_sample)
   repeat 10,000 times:
      bhutan_resample = draw N new samples from the universalPmf
      nepal_resample = draw M new samples from the universalPmf
      mu_bhutan = sample mean of the bhutanResample
      mu_nepal = sample mean of the nepalResample
      mean_difference = |muNepal - muBhutan|
      if mean_difference > observed_difference:
         count += 1
   pvalue = count / 10,000
```

这尤其好，因为我们没有在任何地方对样本来自的参数分布做出假设（即我们从未声称幸福感是高斯分布）。你可能听说过 t 检验。这是计算$p$-值的另一种方法，但它假设两个样本都是高斯分布，并且它们都有相同的方差。在现在这个我们有合理计算能力的背景下，自助法是一个更正确、更通用的工具。
