# 19：中心极限定理与置信区间 📊

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_1.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_3.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_5.png)

在本节课中，我们将要学习中心极限定理，并了解它如何帮助我们理解样本均值的分布，以及如何利用它来构建置信区间，而无需进行大量的自助法重采样计算。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_7.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_9.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_11.png)

## 回顾：标准单位

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_13.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_15.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_17.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_19.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_21.png)

上一节我们介绍了标准单位的概念。标准单位用于衡量一个数值相对于其数据集的平均值有多少个标准差。其公式为：

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_23.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_25.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_27.png)

**标准单位 = (数值 - 平均值) / 标准差**

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_29.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_31.png)

对于任何数值型数据集，标准单位计算的是该数值高于平均值多少个标准差。我们可以将其可视化：平均值是中心点，一个标准单位对应一个标准差的跳跃。标准单位也可以是负值，表示数值低于平均值。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_33.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_35.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_37.png)

## 中心极限定理介绍

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_39.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_41.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_42.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_44.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_46.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_48.png)

现在，我们来看一个重要的定理——中心极限定理。为了理解它，我们使用之前分析过的航班延误分布数据。这个分布本身并非正态分布（例如，呈右偏态），但当我们从中抽取大量随机样本并计算每个样本的均值时，这些样本均值的分布会呈现出有趣的规律。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_50.png)

### 样本均值的分布

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_52.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_53.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_55.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_57.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_59.png)

如果我们从一个总体（如所有航班延误数据）中反复抽取相同大小的随机样本（例如，每次抽取500个航班），并计算每个样本的均值，那么这些样本均值的分布会如何？

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_61.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_63.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_64.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_66.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_68.png)

通过模拟这个过程（抽取2000个样本，每个样本大小为500），我们得到了样本均值的分布直方图。这个分布呈现出明显的钟形曲线形状，即近似正态分布。有趣的是，尽管原始总体分布（航班延误）不是正态的，但样本均值的分布却是正态的。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_70.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_72.png)

这个现象就是**中心极限定理**的核心内容。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_74.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_76.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_78.png)

### 中心极限定理的表述

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_79.png)

中心极限定理指出：当从总体中抽取**大样本**（样本量足够大）并计算其**均值**（或总和）时，这些样本均值的分布将近似服从**正态分布**。无论原始总体本身的分布形状如何，这个结论都成立。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_81.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_83.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_85.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_86.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_87.png)

在我们的例子中，总体是严重右偏的航班延误分布，但样本均值的分布却变成了漂亮的钟形曲线。

### 分布的中心与展布

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_89.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_91.png)

这个正态分布（样本均值的分布）有两个关键特征：
1.  **中心**：它**以总体均值**为中心。这是因为随机抽样是无偏的，样本均值有时会偏高，有时会偏低，但平均而言会集中在总体均值附近。
2.  **展布（标准差）**：其**展布（标准差）** 由以下公式决定，这被称为**平方根法则**：

    **样本均值分布的标准差 = 总体标准差 / √样本量**

    这意味着，样本量越大，样本均值分布就越狭窄，样本均值作为总体均值的估计就越精确。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_93.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_95.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_97.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_99.png)

**重要区分**：这里讨论的“标准差”是指**样本均值这个统计量的分布**的标准差，而不是单个样本内部数值的标准差。单个大样本本身可能包含更多极端值，其内部标准差可能更大。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_101.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_103.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_104.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_106.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_107.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_108.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_110.png)

## 从理论到实践：利用单一样本

上述理论很完美，但依赖于我们知道总体参数（总体均值、总体标准差）。在实践中，我们通常只有一个样本。如何应用中心极限定理呢？

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_112.png)

思路与自助法类似：我们假设**一个大的随机样本可以很好地代表总体**。因此，我们可以用**样本统计量**来近似替代未知的**总体参数**。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_114.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_116.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_118.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_119.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_120.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_122.png)

具体来说：
*   用**样本均值** (`sample_mean`) 来估计中心极限定理分布的中心（即总体均值）。
*   用**样本标准差** (`sample_sd`) 来替代平方根法则中的总体标准差。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_124.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_126.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_128.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_129.png)

由此，我们可以预测，如果对原始样本进行多次自助重采样，这些重采样样本的均值分布将近似服从以下正态分布：
*   **中心**：`sample_mean`
*   **标准差**：`sample_sd / √n` （其中 `n` 是原始样本量）

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_131.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_133.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_135.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_136.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_137.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_138.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_140.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_142.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_143.png)

通过对比可以发现，根据这个公式绘制的正态曲线与通过实际自助法重采样5000次得到的样本均值分布直方图几乎完全重合。这证明了中心极限定理为我们提供了一种无需大量计算即可估计样本均值分布的有效捷径。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_145.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_147.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_149.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_150.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_152.png)

## 构建置信区间

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_154.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_156.png)

我们研究样本均值分布的主要目的之一是构建总体均值的置信区间。之前我们使用自助法：通过重采样得到统计量的分布，然后取中间95%的范围作为置信区间。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_158.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_160.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_162.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_164.png)

利用中心极限定理，我们可以更直接地计算置信区间。我们知道样本均值的分布近似为正态分布 `N(sample_mean, sample_sd/√n)`。对于正态分布，约有95%的数据落在“均值 ± 2个标准差”的范围内。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_166.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_168.png)

因此，总体均值的一个**近似95%置信区间**可以通过以下公式计算：

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_170.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_172.png)

**置信区间 = [ sample_mean - 2 * (sample_sd / √n), sample_mean + 2 * (sample_sd / √n) ]**

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_174.png)

### 对比自助法与中心极限定理

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_176.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_178.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_179.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_180.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_182.png)

以下是两种方法的对比：
*   **自助法**：通过模拟重采样得到经验分布，通用性强（也适用于中位数等），但结果略有随机性，计算量较大。
*   **中心极限定理法**：利用公式直接计算，仅适用于样本均值（或总和），结果确定且计算快捷。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_184.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_186.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_187.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_189.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_191.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_192.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_194.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_195.png)

在实践中，对于均值问题，推荐使用中心极限定理法；对于其他统计量（如中位数），则需使用自助法。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_197.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_199.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_201.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_203.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_205.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_206.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_208.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_209.png)

### 调整置信水平

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_211.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_213.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_215.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_217.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_219.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_221.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_223.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_224.png)

上述公式中的数字“2”对应95%的置信水平。如果需要不同置信水平（例如80%或99%）的区间，需要调整这个乘数（通常记为`z`）。置信水平越低，所需的`z`值越小（区间越窄）；置信水平越高，所需的`z`值越大（区间越宽）。可以通过标准正态分布表来查找特定置信水平对应的`z`值。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_226.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_227.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_229.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_231.png)

## 总结

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_233.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_235.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_236.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_237.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_239.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_241.png)

本节课我们一起学习了中心极限定理及其在推断统计学中的应用。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_243.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_244.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_246.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_248.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_250.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_252.png)

1.  **中心极限定理**：无论总体分布如何，大样本均值的分布近似服从正态分布。
2.  **定理的关键**：该正态分布以总体均值为中心，其标准差为 `总体标准差 / √样本量`。
3.  **实践应用**：通过单一样本，我们可以用样本均值和样本标准差来估计上述分布，从而绕过复杂的自助法模拟。
4.  **构建置信区间**：利用该正态分布的性质，我们可以使用公式 `样本均值 ± z * (样本标准差 / √样本量)` 来快速计算总体均值的置信区间。

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_254.png)

![](img/b74f79e3ebbcf4ac12a1ada6927bc3b7_256.png)

中心极限定理是统计学中一个强大而实用的工具，它使我们对样本均值的变异性有了深刻的理解，并提供了进行统计推断的坚实理论基础。