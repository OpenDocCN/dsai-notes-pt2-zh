# 008：神经架构搜索（第二部分）🚀

![](img/71796c0b5afbbca61fdeb798c7bdd401_1.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_3.png)

在本节课中，我们将继续学习神经架构搜索（NAS），重点关注如何高效地评估架构性能、实现硬件感知的搜索，以及“一次训练，处处部署”的One-Shot NAS方法。我们还将探讨NAS在多种应用场景下的实践。

![](img/71796c0b5afbbca61fdeb798c7bdd401_5.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_7.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_8.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_10.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_12.png)

---

![](img/71796c0b5afbbca61fdeb798c7bdd401_14.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_16.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_18.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_20.png)

## 概述：神经架构搜索流程回顾

![](img/71796c0b5afbbca61fdeb798c7bdd401_22.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_23.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_24.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_26.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_27.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_29.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_31.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_33.png)

上一节我们介绍了神经架构搜索的基本概念，包括搜索空间、搜索策略（如强化学习、进化算法）等。本节中，我们将深入探讨如何高效地评估候选架构的性能，以及如何让搜索过程对目标硬件平台更加敏感。

![](img/71796c0b5afbbca61fdeb798c7bdd401_35.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_37.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_39.png)

神经架构搜索的完整流程通常包含三个核心部分：
1.  **搜索空间**：定义候选神经网络架构的集合。
2.  **搜索策略**：用于在搜索空间中探索和选择架构的算法。
3.  **性能评估策略**：快速且高效地估计所选架构性能（如精度、延迟）的方法。

![](img/71796c0b5afbbca61fdeb798c7bdd401_41.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_43.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_44.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_45.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_47.png)

本节课，我们将聚焦于**性能评估策略**，目标是找到在不过度消耗计算资源的前提下，准确预测架构表现的方法。

![](img/71796c0b5afbbca61fdeb798c7bdd401_49.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_50.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_52.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_53.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_55.png)

---

![](img/71796c0b5afbbca61fdeb798c7bdd401_57.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_59.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_60.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_62.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_63.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_65.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_66.png)

## 性能评估策略 🔍

![](img/71796c0b5afbbca61fdeb798c7bdd401_68.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_70.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_72.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_74.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_76.png)

评估一个神经网络架构的性能（如分类精度）最直接的方法是**从头开始训练**它直到收敛，然后在验证集上测试。然而，这种方法成本极高。例如，在CIFAR-10这样的小数据集上搜索，也可能需要数万GPU小时。

![](img/71796c0b5afbbca61fdeb798c7bdd401_78.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_79.png)

因此，我们需要更高效的替代方案。以下是三种主要策略：

![](img/71796c0b5afbbca61fdeb798c7bdd401_81.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_83.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_85.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_87.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_89.png)

### 1. 从头训练
这是最基础但最昂贵的方法。给定一个模型架构，在训练集 `X` 上从头开始训练至收敛，然后在验证集上评估得到精度 `R`。公式上，这相当于最小化损失函数 `L` 以找到最优权重 `W*`：
`W* = argmin_W L(f(X; W), Y)`
其中 `f` 是模型，`Y` 是标签。

![](img/71796c0b5afbbca61fdeb798c7bdd401_91.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_93.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_95.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_97.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_99.png)

### 2. 权重继承
为了降低训练成本，我们可以从一个预训练模型继承权重，并在此基础上修改架构，而无需完全重新训练。两种经典操作是：
*   **Net2WiderNet**：通过复制神经元并平均权重来增加网络宽度。
*   **Net2DeeperNet**：通过添加恒等映射层来增加网络深度。
这些操作能保持修改前后模型的数学等价性，从而在改变架构的同时，重用已有权重。

![](img/71796c0b5afbbca61fdeb798c7bdd401_101.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_103.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_105.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_107.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_109.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_111.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_113.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_115.png)

### 3. 超网络
超网络是一个用于预测目标网络权重的神经网络。其输入是目标网络架构的图表示（节点嵌入和连接关系），输出则是该架构各层的权重。通过训练这个超网络，我们可以根据给定的架构描述快速生成其权重，从而避免为每个候选架构单独训练。
核心思想是学习一个映射函数 `H`：
`W = H(G)`
其中 `G` 是描述目标架构的图，`W` 是预测的权重。

![](img/71796c0b5afbbca61fdeb798c7bdd401_117.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_119.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_121.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_123.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_125.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_127.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_129.png)

---

![](img/71796c0b5afbbca61fdeb798c7bdd401_131.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_133.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_135.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_136.png)

## 硬件感知的神经架构搜索 🖥️

![](img/71796c0b5afbbca61fdeb798c7bdd401_138.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_139.png)

通用的神经网络模型在不同硬件平台（如手机CPU、服务器GPU、嵌入式设备）上可能效率低下。理想情况下，我们希望为每个平台自动搜索出**专用模型**，在保证精度的同时最大化硬件效率。

![](img/71796c0b5afbbca61fdeb798c7bdd401_141.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_142.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_144.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_146.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_148.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_150.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_152.png)

### 传统方法的挑战与代理任务
早期的NAS方法计算成本巨大，因此常使用**代理任务**来降低开销，例如：
*   在小数据集（如CIFAR-10）上搜索，而非目标数据集（如ImageNet）。
*   在小的架构空间搜索。
*   仅训练少量周期来评估潜力。
*   使用理论计算量（FLOPs）或参数量作为硬件效率的代理指标。

![](img/71796c0b5afbbca61fdeb798c7bdd401_154.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_156.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_158.png)

然而，这些代理方法存在明显问题：在小数据集上表现好的架构可能无法迁移到大数据集；FLOPs与实际延迟（Latency）关联性弱，不能准确反映真实硬件性能。

![](img/71796c0b5afbbca61fdeb798c7bdd401_160.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_161.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_163.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_165.png)

### 解决方案：ProxylessNAS
为了直接在目标任务和目标硬件上进行高效搜索，我们引入了**ProxylessNAS**。其核心是为网络中的每一层引入**架构参数** `α`，它表示选择不同操作（如3x3卷积、5x5卷积）的概率。

![](img/71796c0b5afbbca61fdeb798c7bdd401_167.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_169.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_171.png)

在训练时，我们同时优化：
1.  网络权重 `W`。
2.  架构参数 `α`。
通过使用Gumbel-Softmax等技术，在训练中仅采样一条路径进行前向和反向传播，从而将内存开销控制在 `O(1)`，而非 `O(N)`（N为候选操作数）。

![](img/71796c0b5afbbca61fdeb798c7bdd401_173.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_174.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_175.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_177.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_179.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_181.png)

训练完成后，我们选择概率最高的操作，二值化架构参数，得到最终的、高效的网络架构。这种方法消除了对代理任务的依赖，实现了端到端的硬件感知搜索。

![](img/71796c0b5afbbca61fdeb798c7bdd401_183.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_185.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_186.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_187.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_189.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_191.png)

### 延迟预测器
直接测量模型在硬件上的延迟非常耗时。一个高效的解决方案是构建一个**延迟预测模型**。
1.  **收集数据集**：在目标硬件上测量大量不同架构的延迟，形成 `(架构特征，延迟)` 数据对。
2.  **训练预测器**：使用简单的模型（如查找表或线性回归器）学习从架构特征（如输入维度、卷积核大小、通道数）到延迟的映射。
3.  **集成到搜索中**：在NAS过程中，使用这个预测器快速估计候选架构的延迟，并将其作为优化目标的一部分。

![](img/71796c0b5afbbca61fdeb798c7bdd401_193.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_195.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_197.png)

研究表明，为不同硬件平台（GPU、CPU、移动设备）搜索出的专用架构存在显著差异。例如，GPU偏好更宽、层数较少、使用大卷积核的网络；而CPU则偏好更窄、层数较多、避免大卷积核的网络。

![](img/71796c0b5afbbca61fdeb798c7bdd401_199.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_201.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_203.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_205.png)

---

![](img/71796c0b5afbbca61fdeb798c7bdd401_207.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_209.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_211.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_213.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_215.png)

## 一次训练，处处部署：One-Shot NAS 🎯

![](img/71796c0b5afbbca61fdeb798c7bdd401_217.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_219.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_221.png)

为每个硬件平台单独搜索模型仍然成本高昂。One-Shot NAS（以Once-for-All为代表）提出了一个更高效的范式：**训练一个包含无数子网络的大型超网络，然后从中直接提取适合不同平台的子模型，而无需重新训练**。

![](img/71796c0b5afbbca61fdeb798c7bdd401_223.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_225.png)

### 核心思想：弹性维度
超网络在多个维度上具备弹性，支持动态缩放：
1.  **弹性深度**：可以选择使用网络中的哪些层。
2.  **弹性宽度**：可以选择每个卷积层使用多少通道（按权重重要性排序后选择最重要的子集）。
3.  **弹性卷积核大小**：通过变换矩阵，从大卷积核中提取出中小卷积核，实现权重共享。
4.  **弹性输入分辨率**：训练时随机采样不同分辨率的输入图像。

![](img/71796c0b5afbbca61fdeb798c7bdd401_227.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_228.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_230.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_232.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_234.png)

### 训练与搜索过程
1.  **训练超网络**：通过交替采样不同配置（深度、宽度、核大小、分辨率）的子网络进行训练，使超网络的权重能够被所有子网络良好共享。
2.  **搜索子网络**：训练完成后，给定目标硬件和延迟约束，我们可以快速地从超网络中采样不同的子网络，用延迟预测器评估其性能，并通过进化搜索等算法找到满足约束的最佳子网络。

![](img/71796c0b5afbbca61fdeb798c7bdd401_236.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_238.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_239.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_241.png)

这种方法将巨大的训练成本**摊销**到一次超网络训练中，后续为任何平台搜索模型都变得极其高效，特别适合大模型场景。

![](img/71796c0b5afbbca61fdeb798c7bdd401_243.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_245.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_246.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_248.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_250.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_252.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_253.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_255.png)

---

![](img/71796c0b5afbbca61fdeb798c7bdd401_257.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_259.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_261.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_262.png)

## 零样本架构评估 🧐

![](img/71796c0b5afbbca61fdeb798c7bdd401_264.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_265.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_267.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_269.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_270.png)

我们能否在不进行任何训练的情况下，快速评估一个神经网络架构的潜力？零样本评估方法试图回答这个问题。

![](img/71796c0b5afbbca61fdeb798c7bdd401_272.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_274.png)

*   **Zen-NAS**：使用随机初始化的权重，通过分析网络对输入微小扰动的输出变化（敏感性），或批归一化层统计量的方差，来评估架构的潜在表达能力。其启发式思想是：一个好的架构应对输入变化更敏感，且内部激活应具有丰富的方差。
*   **Grad Sign**：通过检查不同输入样本下，网络权重梯度符号的一致性来评估。在损失函数平滑、局部最小值密集的区域，梯度符号更可能一致。因此，梯度符号一致性的比例越高，架构可能越好。

![](img/71796c0b5afbbca61fdeb798c7bdd401_276.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_278.png)

这些方法虽然粗糙，但能在毫秒级内提供架构潜力的初步排序，用于在昂贵训练开始前进行快速筛选。

![](img/71796c0b5afbbca61fdeb798c7bdd401_280.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_281.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_283.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_285.png)

---

![](img/71796c0b5afbbca61fdeb798c7bdd401_287.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_289.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_291.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_293.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_295.png)

## 神经架构与硬件加速器协同搜索 🤖

![](img/71796c0b5afbbca61fdeb798c7bdd401_297.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_299.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_300.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_301.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_302.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_304.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_306.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_308.png)

更进一步，我们不仅可以搜索神经网络架构，还可以同时搜索运行它的**硬件加速器架构**，即协同设计。

![](img/71796c0b5afbbca61fdeb798c7bdd401_310.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_311.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_313.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_315.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_317.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_318.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_320.png)

### 设计空间
协同搜索的设计空间非常庞大，包括三部分：
1.  **神经网络架构**：层数、通道数、卷积核大小、量化精度等。
2.  **硬件加速器架构**：缓存大小、处理单元数量与连接方式等。
3.  **编译映射策略**：如何将神经网络计算映射到硬件上（循环次序、分块大小、数据流）。

![](img/71796c0b5afbbca61fdeb798c7bdd401_322.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_324.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_326.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_327.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_329.png)

### 编码与搜索
挑战在于如何将非数值的设计选择（如循环次序、并行维度）编码为可优化的数值向量。一种方法是为每个循环维度分配一个“重要性”分数，然后根据分数排序来决定并行策略和循环次序。

![](img/71796c0b5afbbca61fdeb798c7bdd401_331.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_333.png)

搜索算法（如进化策略）在一个统一的循环中，同时优化神经网络、硬件架构和编译映射，以最小化**能量延迟积**等综合指标为目标。实验表明，协同设计能比单独优化神经网络或硬件带来显著的能效提升。

![](img/71796c0b5afbbca61fdeb798c7bdd401_335.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_337.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_338.png)

---

![](img/71796c0b5afbbca61fdeb798c7bdd401_340.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_341.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_343.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_344.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_346.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_348.png)

## NAS的应用领域 🌐

神经架构搜索技术已广泛应用于各类任务：

1.  **自然语言处理**：用于设计高效的Transformer模型，在保持精度的同时大幅降低延迟和模型大小。
2.  **3D视觉与点云处理**：为激光雷达点云分割等任务搜索快速准确的架构，显著提升自动驾驶系统的实时性。
3.  **生成式模型**：为图像编辑、风格迁移等GAN模型设计轻量子网络，实现移动设备上的实时交互。
4.  **姿态估计**：为人体关键点检测模型进行硬件感知搜索，在移动CPU上获得数倍加速。
5.  **量子机器学习**：将One-Shot思想应用于量子电路搜索，在存在噪声的真实量子设备上找到更鲁棒的电路结构。
6.  **大语言模型**：最新的工作将弹性深度/宽度技术应用于LLM，实现单一模型支持从云端到移动端的不同推理配置，满足多样化的部署需求。

![](img/71796c0b5afbbca61fdeb798c7bdd401_350.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_352.png)

---

![](img/71796c0b5afbbca61fdeb798c7bdd401_354.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_356.png)

## 总结 📚

本节课我们一起深入学习了神经架构搜索的第二部分。我们探讨了如何通过权重继承、超网络等方法高效评估架构性能；重点介绍了硬件感知的ProxylessNAS和“一次训练，处处部署”的One-Shot NAS范式，后者将在实验三中亲手实践；我们还了解了零样本评估和神经-硬件协同搜索的前沿方向；最后，看到了NAS在从NLP、CV到量子计算和大语言模型等多个领域的强大应用潜力。

![](img/71796c0b5afbbca61fdeb798c7bdd401_358.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_360.png)

![](img/71796c0b5afbbca61fdeb798c7bdd401_362.png)

通过本节课，你应该对如何自动化、高效地设计兼具高精度和硬件效率的神经网络有了更全面的认识。