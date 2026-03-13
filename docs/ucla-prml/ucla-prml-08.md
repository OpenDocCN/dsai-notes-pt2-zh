# 8：模式识别与机器学习导论 - 偏差-方差分解与性能评估 📊

![](img/56a72def89d5e70ffc3df8cea2a67035_0.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_2.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_4.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_6.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_8.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_10.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_12.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_14.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_16.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_18.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_20.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_22.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_24.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_26.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_28.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_30.png)

在本节课中，我们将深入分析回归问题中的偏差-方差分解，并探讨分类器性能评估的常用方法。我们将从上一节引入的均方误差分解开始，理解其组成部分，并学习如何通过权衡偏差与方差来优化模型。最后，我们将回到分类问题，介绍ROC曲线等评估工具。

![](img/56a72def89d5e70ffc3df8cea2a67035_32.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_34.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_36.png)

## 偏差-方差分解回顾 🔍

上一节我们分析了条件均方误差，这是一个衡量回归函数估计器性能的重要指标。我们论证了该指标可以分解为偏差平方与方差之和。

![](img/56a72def89d5e70ffc3df8cea2a67035_38.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_40.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_42.png)

具体公式如下：
\[
\text{MSE} = \text{Bias}^2 + \text{Variance}
\]

![](img/56a72def89d5e70ffc3df8cea2a67035_44.png)

这个分解被称为偏差-方差分解或权衡。当我们尝试优化估计器时，需要同时考虑这两个部分。

![](img/56a72def89d5e70ffc3df8cea2a67035_46.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_48.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_50.png)

## 分区估计器的分析 📐

![](img/56a72def89d5e70ffc3df8cea2a67035_52.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_54.png)

我们以分区估计器为例进行计算。首先引入一些符号：经验分布或经验测度表示训练数据中X的分布。根据大数定律，经验分布会收敛于真实分布。

![](img/56a72def89d5e70ffc3df8cea2a67035_56.png)

分区估计器可以写为Y值的加权平均，权重由特定的质量函数决定。我们计算了其方差，并做了一个简化假设：给定X的条件方差是常数。在此假设下，方差最终近似为：
\[
\text{Variance} \approx \frac{\sigma^2}{n \cdot \mu(A_x)}
\]
其中，\(\mu(A_x)\) 是包含点x的单元格在真实分布下的测度。

![](img/56a72def89d5e70ffc3df8cea2a67035_58.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_60.png)

以一维空间[0,1]划分为长度为h的区间为例。一个随机点落在任一区间的概率约为h。因此，对于大的n，方差近似为 \(\sigma^2 / (n h)\)。当带宽h变小时，落入该区间的点变少，方差会增大。

![](img/56a72def89d5e70ffc3df8cea2a67035_62.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_63.png)

## 偏差的分析与利普希茨条件 📈

![](img/56a72def89d5e70ffc3df8cea2a67035_65.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_67.png)

接下来我们分析偏差。分区估计器的期望行为类似于分段常数函数。偏差源于用单元格内的平均值来近似真实回归函数在点x的值。

![](img/56a72def89d5e70ffc3df8cea2a67035_69.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_71.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_73.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_75.png)

为了使偏差趋于零，我们需要让带宽h趋于零。偏差收敛到零的速度取决于真实回归函数 \(\eta(x)\) 的平滑度。我们引入利普希茨连续性来量化函数的平滑度。

![](img/56a72def89d5e70ffc3df8cea2a67035_77.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_79.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_80.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_82.png)

**利普希茨条件定义**：如果存在常数L，使得对于定义域内任意两点x和z，函数 \(\eta\) 满足：
\[
|\eta(x) - \eta(z)| \le L \cdot |x - z|
\]
则称函数 \(\eta\) 是L-利普希茨连续的。这等价于说函数的导数（几乎处处存在）的绝对值有界于L。

![](img/56a72def89d5e70ffc3df8cea2a67035_84.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_86.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_88.png)

以下是一些例子：
*   **常数函数**：是利普希茨连续的（L=0）。
*   **线性函数**：\(\eta(x) = ax + b\) 是利普希茨连续的，L等于斜率a的绝对值。
*   **函数 \(x^2\)**：在整个实数域上不是利普希茨连续，因为其导数 \(2x\) 无界；但在任何有界区间（如[0,1]）上是利普希茨连续的。
*   **Sigmoid函数**：是利普希茨连续的。

![](img/56a72def89d5e70ffc3df8cea2a67035_90.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_92.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_94.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_95.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_97.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_99.png)

在利普希茨假设下，我们可以控制偏差的大小。通过分析可得，偏差满足：
\[
|\text{Bias}| \le L \cdot h
\]
这意味着偏差以线性速度随h减小。

## 偏差-方差的权衡与维度灾难 ⚖️

现在，我们将偏差和方差的结果结合起来。均方误差的上界近似为：
\[
\text{MSE} \lesssim L^2 h^2 + \frac{\sigma^2}{n h}
\]

![](img/56a72def89d5e70ffc3df8cea2a67035_101.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_103.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_105.png)

*   **偏差项** \(L^2 h^2\)：随h减小而改善。
*   **方差项** \(\sigma^2 / (n h)\)：随h减小而恶化。

如果绘制MSE随h变化的曲线，会呈现一个U形，存在一个最优的h值使得MSE最小。通过令两项相等，可以近似求解最优带宽 \(h^*\) 及其对应的最小MSE：
\[
h^* \sim \left( \frac{\sigma^2}{L^2 n} \right)^{1/3}, \quad \text{MSE}^* \sim \frac{\sigma^2}{n^{2/3}}
\]

这个收敛速率 \(n^{-2/3}\) 比参数化模型（如线性回归）的典型速率 \(n^{-1}\) 要慢，这是因为我们假设的函数类（利普希茨连续）非常广泛，属于非参数估计。

![](img/56a72def89d5e70ffc3df8cea2a67035_107.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_109.png)

**维度灾难**：在高维（D维）情况下，问题变得更加严峻。方差项会变为 \(\sigma^2 / (n h^D)\)。最优MSE速率会恶化到大约 \(n^{-2/(2+D)}\)。当维度D很高时，这个速率变得极慢，意味着需要海量的样本才能准确估计一个一般的平滑函数。这解释了为什么在高维问题中，我们常常需要转向参数化模型或低维假设来避免这个问题。

![](img/56a72def89d5e70ffc3df8cea2a67035_111.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_113.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_115.png)

## 分类器性能评估：ROC曲线 📉

![](img/56a72def89d5e70ffc3df8cea2a67035_117.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_119.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_121.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_122.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_124.png)

现在，让我们切换话题，回到分类问题，讨论如何更细致地评估分类器的性能。

除了整体的分类错误率，我们经常需要分别考察模型在不同类别上的表现。特别是对于通过估计回归函数并设置阈值 \(\tau\) 来决策的分类器（即 \(\hat{f}(x) = \mathbb{I}(\hat{\eta}(x) > \tau)\)），其性能强烈依赖于 \(\tau\)。

以下是两个关键指标：
*   **假正率**：真实类别为0时，被预测为1的概率。\( \text{FPR}(\tau) = P(\hat{Y}=1 | Y=0) \)
*   **真正率**：真实类别为1时，被预测为1的概率。\( \text{TPR}(\tau) = P(\hat{Y}=1 | Y=1) \)

![](img/56a72def89d5e70ffc3df8cea2a67035_126.png)

通过让阈值 \(\tau\) 从 \(+\infty\) 变化到 \(-\infty\)，我们可以得到一系列（FPR, TPR）点，将它们连接起来形成的曲线称为**接收者操作特征曲线**。

![](img/56a72def89d5e70ffc3df8cea2a67035_128.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_130.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_132.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_134.png)

ROC曲线提供了分类器性能的完整图像：
*   曲线从左下角(0,0)（总是预测为0）延伸到右上角(1,1)（总是预测为1）。
*   对角线（FPR = TPR）表示随机猜测的性能。
*   曲线越向左上角凸起，分类器性能越好。完美的分类器对应的ROC曲线经过点(0,1)。

**曲线下面积**是另一个汇总性指标，表示随机选取一个正样本和一个负样本，分类器对正样本给出更高分数的概率。完美分类器的AUC为1，随机分类器的AUC为0.5。

![](img/56a72def89d5e70ffc3df8cea2a67035_136.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_138.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_140.png)

ROC曲线的优势在于它不依赖于类别的先验分布，并且能让我们根据实际应用中对假正率和真正率的不同容忍度来选择合适的决策阈值。

![](img/56a72def89d5e70ffc3df8cea2a67035_142.png)

## 总结 🎯

![](img/56a72def89d5e70ffc3df8cea2a67035_144.png)

本节课我们一起学习了以下核心内容：

1.  **偏差-方差分解**：深入理解了回归问题中均方误差如何分解为偏差平方和方差，并分析了分区估计器在这两方面的表现。
2.  **利普希茨连续性**：作为衡量函数平滑度的工具，它帮助我们量化了非参数估计中偏差项的收敛速度。
3.  **维度灾难**：认识到在高维空间中，非参数估计的方差会急剧增大，导致所需样本量指数级增长，这为使用参数化模型提供了动机。
4.  **分类器评估**：学习了超越简单准确率的评估方法，特别是ROC曲线和AUC，它们能更全面地反映分类器在不同决策阈值下的性能，尤其在类别不平衡时非常有用。

![](img/56a72def89d5e70ffc3df8cea2a67035_146.png)

![](img/56a72def89d5e70ffc3df8cea2a67035_148.png)

这些概念是理解模型复杂度、泛化能力以及选择合适评估指标的基础。