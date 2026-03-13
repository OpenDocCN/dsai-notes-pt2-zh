# 13：概率分布、抽样与统计推断 📊

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_1.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_3.png)

在本节课中，我们将学习概率分布与经验分布的区别，了解抽样在数据科学中的核心作用，并探索如何利用样本数据推断总体特征。我们将通过掷骰子和航班延误数据的例子，直观地理解大数定律以及样本统计量如何逼近总体参数。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_5.png)

---

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_7.png)

## 🎲 概率分布与经验分布

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_9.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_11.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_13.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_15.png)

上一节我们介绍了模拟的基本概念，本节中我们来看看如何描述随机事件的可能性。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_17.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_19.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_21.png)

概率分布描述了一个随机变量所有可能取值及其对应的理论概率。例如，掷一枚均匀骰子时，每个面（1到6）出现的概率都是1/6。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_23.png)

**公式表示**：
对于一个均匀骰子，其概率分布可以表示为：
`P(X = x) = 1/6`，其中 `x ∈ {1, 2, 3, 4, 5, 6}`。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_25.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_27.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_29.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_31.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_33.png)

经验分布则基于实际观察到的数据。它描述了在多次实验中，每个观测值出现的比例。例如，如果你实际掷骰子25次，记录每个数字出现的次数，由此计算出的比例就构成了一个经验分布。经验分布会因实验者和实验次数不同而变化，而概率分布是固定不变的理论值。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_35.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_37.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_39.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_41.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_42.png)

---

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_44.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_46.png)

## 🔄 大数定律

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_48.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_50.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_52.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_54.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_56.png)

从掷骰子的经验中，我们观察到随着实验次数增加，经验分布会越来越接近理论上的概率分布。这一现象由大数定律所描述。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_58.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_59.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_61.png)

大数定律指出：在相同条件下独立重复进行一个随机试验，某个事件发生的频率会随着试验次数的增加而逐渐稳定，并趋近于该事件的理论概率。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_63.png)

这意味着，当我们进行大量模拟（如上一节课所做）时，用频率来估计概率是合理且可靠的。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_65.png)

---

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_67.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_68.png)

## 📋 总体与样本

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_70.png)

在数据科学中，我们常常无法获取研究对象的全部数据（即总体），这时就需要进行抽样。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_72.png)

*   **总体**：我们想要研究的全部个体或观测值的集合。例如，所有UCSD学生的身高。
*   **样本**：从总体中选取的一个子集。例如，随机调查的100名UCSD学生的身高。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_74.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_76.png)

我们的目标是通过分析样本数据来推断总体的特征。样本的选取方式至关重要，糟糕的抽样方法（如只调查篮球队成员）会导致结论存在偏差。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_78.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_80.png)

---

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_82.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_84.png)

## 🎯 简单随机抽样

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_86.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_88.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_90.png)

为了获得对总体有代表性的样本，黄金标准是进行**简单随机抽样**。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_92.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_94.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_96.png)

简单随机抽样满足两个条件：
1.  **均匀性**：总体中的每个个体被选中的概率相同。
2.  **无放回**：同一个个体不会被重复选中。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_98.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_99.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_101.png)

在代码中，我们可以使用 `np.random.choice(..., replace=False)` 或DataFrame的 `.sample()` 方法（默认无放回）来实现简单随机抽样。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_103.png)

---

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_105.png)

## ✈️ 实例分析：航班延误数据

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_107.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_109.png)

让我们通过一个真实数据集来理解这些概念。我们有一个包含2015年夏季从旧金山机场起飞的近14,000个联合航空公司航班的总体数据，其中包含“延误时间”这一数值变量。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_111.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_113.png)

首先，我们查看总体中延误时间的分布直方图。我们发现大部分航班基本准点，但存在一个长长的右尾，意味着有少数航班延误非常严重。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_115.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_117.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_119.png)

**核心操作代码**：
```python
# 从总体数据框中抽取一个简单随机样本
sample_of_100 = flights.sample(100)
# 绘制样本中延误时间的分布
sample_of_100.get('Delay').plot(kind='hist')
```

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_121.png)

当我们只有样本（例如100个航班）时，其延误分布直方图与总体分布相似，但不会完全一致。随着样本量增大（如1000个、10000个航班），样本的分布会越来越接近总体分布。这再次印证了大数定律的思想：更大的样本能提供关于总体更准确的信息。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_123.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_125.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_126.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_128.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_129.png)

---

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_131.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_133.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_135.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_137.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_139.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_140.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_142.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_143.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_145.png)

## 📐 参数与统计量

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_147.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_149.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_151.png)

为了进行定量推断，我们引入两个关键概念：

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_153.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_154.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_156.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_157.png)

*   **参数**：描述总体特征的固定数值。例如，所有航班的平均延误时间。参数通常未知，是我们希望通过样本去推断的目标。
*   **统计量**：基于样本数据计算得出的数值。例如，样本中100个航班的平均延误时间。统计量是随机的，因为不同的样本会计算出不同的值。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_159.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_161.png)

一个常用的记忆法是：**P**arameter（参数）对应 **P**opulation（总体），**S**tatistic（统计量）对应 **S**ample（样本）。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_163.png)

我们的目标是：使用样本统计量（如样本均值）来估计总体参数（如总体均值）。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_165.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_167.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_169.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_171.png)

---

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_173.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_174.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_176.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_178.png)

## 🎰 统计量的经验分布

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_180.png)

由于抽样具有随机性，基于不同样本计算出的统计量（如样本均值）会有所不同。为了理解这种变异性，我们可以通过模拟来研究统计量的经验分布。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_182.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_184.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_186.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_188.png)

以下是研究样本均值经验分布的方法：
1.  从总体中重复抽取大量相同大小的样本（例如，抽取2000次，每次抽100个航班）。
2.  对每个样本计算其统计量（例如，计算2000个样本各自的平均延误时间）。
3.  将这些统计量的值收集起来，绘制直方图。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_190.png)

这个直方图展示了样本均值可能取值的分布情况。我们发现：
*   当样本量较大（如1000）时，样本均值的分布非常集中，紧密围绕在总体均值（约17分钟）周围，形状对称且规则。
*   当样本量较小（如100）时，样本均值的分布则分散得多，这意味着基于小样本的估计结果可能很不稳定，有时会严重偏离真实值。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_192.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_194.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_196.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_197.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_199.png)

这直观地说明了：**更大的样本能产生更精确、更可靠的估计**。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_201.png)

---

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_203.png)

## 📝 总结

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_205.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_207.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_209.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_210.png)

本节课中我们一起学习了：
1.  **概率分布**（理论）与**经验分布**（观测）的区别。
2.  **大数定律**如何保证频率趋近于概率。
3.  数据科学中通过**样本**推断**总体**的基本框架。
4.  获得代表性样本的关键方法——**简单随机抽样**。
5.  **参数**（总体特征）与**统计量**（样本特征）的核心概念。
6.  通过模拟理解**统计量的经验分布**，并认识到**样本量越大，统计量作为估计量通常越优**。

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_212.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_214.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_216.png)

![](img/e31ed0999edea45ca2ac7d5bab9b42cf_218.png)

理解这些概念是进行统计推断的基石，能帮助我们在只有部分数据的情况下，对更广阔的世界做出合理的结论。