# 010：MCUNet与TinyML 🚀

在本节课中，我们将学习TinyML的概念、其面临的挑战、如何设计适用于微型设备的神经网络，以及其在视觉、音频、时间序列和异常检测等领域的应用。

## 概述 📋

![](img/6f1e7c1c906902af22669eda0ade29ef_1.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_3.png)

我们之前已经讨论了许多用于压缩和缩小神经网络的技术，包括剪枝、量化、知识蒸馏和神经架构搜索。现在，我们希望将这些不同的努力结合起来，构建一些酷炫的应用，并将它们真正部署在小型设备上。

![](img/6f1e7c1c906902af22669eda0ade29ef_5.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_6.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_8.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_10.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_12.png)

## 什么是TinyML？ 🤔

![](img/6f1e7c1c906902af22669eda0ade29ef_14.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_16.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_18.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_19.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_20.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_22.png)

当今的AI模型通常非常庞大，参数数量以数十亿计，并且增长迅速。然而，我们需要更高效的算法和硬件来进行推理和训练，而不是消耗大量的内存和计算资源。我们希望AI能够“微型化”，不仅运行在云端，也能运行在边缘设备上，这样我们就不必将个人数据（如图像、文本或语音）传输到云端，从而避免对抗性攻击和隐私泄露的风险。我们希望所有计算都在本地进行，例如在手机上，甚至在更小的设备上，如物联网设备。

![](img/6f1e7c1c906902af22669eda0ade29ef_24.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_26.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_28.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_29.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_30.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_32.png)

## TinyML的挑战 ⚠️

![](img/6f1e7c1c906902af22669eda0ade29ef_34.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_36.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_37.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_39.png)

TinyML面临的主要挑战是资源限制，尤其是内存资源。

![](img/6f1e7c1c906902af22669eda0ade29ef_41.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_43.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_45.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_47.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_49.png)

*   **云端AI**：可以轻松获得数十GB的内存和TB甚至PB级的存储。
*   **移动设备**：通常有几GB的内存和数百GB的存储。
*   **微控制器**：资源极其有限，通常只有几百KB的SRAM（用于存储激活值）和大约1MB的闪存（用于存储模型权重）。

![](img/6f1e7c1c906902af22669eda0ade29ef_51.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_52.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_54.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_56.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_57.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_59.png)

微控制器的资源比云端AI和移动AI小4到5个数量级。因此，我们需要同时减少权重和激活值的大小，以便将深度神经网络适配到这些微型设备中。

![](img/6f1e7c1c906902af22669eda0ade29ef_61.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_63.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_64.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_66.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_67.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_69.png)

## 内存瓶颈分析 🔍

![](img/6f1e7c1c906902af22669eda0ade29ef_71.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_73.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_74.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_75.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_77.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_79.png)

为了理解TinyML的内存挑战，我们需要分析权重内存和激活内存的瓶颈。

![](img/6f1e7c1c906902af22669eda0ade29ef_81.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_83.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_85.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_86.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_88.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_90.png)

一个卷积神经网络通常包含多个卷积层、池化层和全连接层。对于每一层，我们都有输入激活值，通过与卷积核（例如3x3）进行卷积运算，产生输出激活值。

![](img/6f1e7c1c906902af22669eda0ade29ef_92.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_93.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_95.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_97.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_98.png)

*   **SRAM**：用于存储输入和输出激活值，因为它需要被读取和写入。SRAM是易失性的，断电后数据会丢失。
*   **闪存**：用于存储模型权重。在推理阶段，权重是只读的，可以存储在非易失性的闪存中。

![](img/6f1e7c1c906902af22669eda0ade29ef_100.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_102.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_104.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_106.png)

**闪存使用量** 大致等于模型的大小，因为权重是静态的，需要存储在闪存中。
**SRAM使用量** 大致等于输入激活值加上输出激活值的大小。我们关心的是**峰值SRAM使用量**，即最大层的大小决定了峰值内存使用量。

与微控制器有限的内存（例如320KB SRAM）相比，即使是经过量化的MobileNetV2模型，其峰值激活内存也超出了限制。因此，我们需要找到方法来克服这个差距。

## 系统与算法协同设计 🤝

为了在微型设备上实现极致效率，我们需要协同设计神经网络架构和推理引擎。MCUNet就是这种思想的体现。

*   **算法侧**：设计定制化的、适合特定硬件和库的神经网络架构（例如，通过神经架构搜索）。
*   **系统侧**：开发新的高效库和运行时，以优化推理引擎。

![](img/6f1e7c1c906902af22669eda0ade29ef_108.png)

本节课我们将重点介绍第一部分：**TinyNAS（微型神经架构搜索）**。下一讲我们将介绍第二部分：**TinyEngine（微型引擎）**。

![](img/6f1e7c1c906902af22669eda0ade29ef_110.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_112.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_114.png)

## TinyNAS：两阶段神经架构搜索 🔬

![](img/6f1e7c1c906902af22669eda0ade29ef_116.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_118.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_120.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_122.png)

TinyNAS采用两阶段方法来搜索适合微型设备的神经网络架构。

![](img/6f1e7c1c906902af22669eda0ade29ef_124.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_126.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_128.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_130.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_132.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_134.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_135.png)

### 第一阶段：搜索空间优化

![](img/6f1e7c1c906902af22669eda0ade29ef_137.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_139.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_141.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_143.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_145.png)

搜索空间的质量在很大程度上决定了搜索结果的性能。对于微控制器，移动设备（如手机）的搜索空间并不适用，因为资源差距巨大。因此，我们需要针对物联网设备设计新的搜索空间。

![](img/6f1e7c1c906902af22669eda0ade29ef_147.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_149.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_150.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_152.png)

我们可以通过缩放现有搜索空间（如MobileNet的搜索空间）来创建新的搜索空间，主要调整两个参数：**输入图像分辨率** 和 **网络宽度乘子**。

![](img/6f1e7c1c906902af22669eda0ade29ef_154.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_156.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_158.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_160.png)

给定一个完整的设计空间，我们加入内存和存储约束，然后优化这个搜索空间。通过分析不同搜索空间下模型的**计算量分布**，我们可以发现，在相同内存约束下，能够容纳更高计算量的设计空间往往能产生更高精度的模型。这是一种无需训练模型即可评估设计空间质量的启发式方法。

![](img/6f1e7c1c906902af22669eda0ade29ef_162.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_163.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_165.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_167.png)

### 第二阶段：在优化后的搜索空间内进行架构搜索

![](img/6f1e7c1c906902af22669eda0ade29ef_169.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_171.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_173.png)

确定了有希望的设计空间后，我们就可以像在森林的特定区域寻找朋友一样，专注于这个区域进行搜索。这里我们使用之前学过的**权重共享**方法（如Once-for-All），在一个超网络中采样不同的子网络并进行联合微调，从而高效地生成许多不同的候选架构。

![](img/6f1e7c1c906902af22669eda0ade29ef_175.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_176.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_178.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_180.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_182.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_183.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_185.png)

TinyNAS搜索出的模型能更均衡地利用内存。与手工设计的MobileNetV2相比，TinyNAS模型的各层峰值内存差异更小，分布更均匀，从而允许在相同内存下容纳更大的模型。

![](img/6f1e7c1c906902af22669eda0ade29ef_187.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_189.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_190.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_192.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_194.png)

## 基于分块的推理 🧩

![](img/6f1e7c1c906902af22669eda0ade29ef_196.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_197.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_199.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_201.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_203.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_204.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_206.png)

为了解决早期层激活值过大的内存瓶颈，我们引入了**基于分块的推理**。

![](img/6f1e7c1c906902af22669eda0ade29ef_208.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_210.png)

传统的推理是**逐层进行**的：计算完某一层的所有输出后，再计算下一层。对于激活值很大的层，这会占用大量SRAM。

![](img/6f1e7c1c906902af22669eda0ade29ef_212.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_214.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_216.png)

基于分块的推理则是**逐块进行**的：将大的输入特征图分割成多个小块（例如2x2或3x3的网格）。我们一次只处理一个小块，计算该小块经过连续几层后的输出，然后再处理下一个小块。这就像把一个大披萨切成小块来吃。

![](img/6f1e7c1c906902af22669eda0ade29ef_218.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_219.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_220.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_222.png)

这种方法可以显著降低峰值内存使用量。理论上，内存节省的上限是分块数量的倍数（例如，分成4块最多可节省4倍内存）。虽然由于需要存储最终输出层等原因，实际节省会小于理论值，但效果仍然非常显著。

![](img/6f1e7c1c906902af22669eda0ade29ef_224.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_225.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_227.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_229.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_230.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_231.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_233.png)

然而，分块推理会带来计算开销，因为相邻分块在边界处存在重叠区域（“光环”），导致重复计算。这种开销源于卷积层的**感受野**。

![](img/6f1e7c1c906902af22669eda0ade29ef_235.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_236.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_238.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_239.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_241.png)

为了减少这种开销，我们可以进行**网络重分布**：在早期使用分块推理的阶段，使用更小的卷积核（如1x1）或减少层数来限制感受野；同时，在后期不使用分块推理的阶段，增加卷积层来补偿，保持模型的总感受野不变。这样可以在保持精度的同时，消除分块推理带来的额外计算开销。

![](img/6f1e7c1c906902af22669eda0ade29ef_243.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_244.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_245.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_247.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_249.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_250.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_251.png)

最后，我们可以将分块推理的调度策略（如使用多少块、在哪些层使用）也作为搜索空间的一部分，与神经架构一起进行联合搜索。

![](img/6f1e7c1c906902af22669eda0ade29ef_253.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_255.png)

## 应用领域 🌐

![](img/6f1e7c1c906902af22669eda0ade29ef_257.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_259.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_260.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_261.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_263.png)

设计出高效的微型模型后，我们可以将其应用于多个领域。

![](img/6f1e7c1c906902af22669eda0ade29ef_265.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_267.png)

### 微型视觉

![](img/6f1e7c1c906902af22669eda0ade29ef_269.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_271.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_273.png)

*   **图像分类**：从简单的水果分类扩展到大规模ImageNet级别的分类，在微控制器上达到超过70%的准确率。
*   **视觉唤醒词**：检测画面中是否有人，用于触发后续更复杂的处理流程（如人脸识别），以节省功耗和保护隐私。
*   **目标检测**：在微控制器上进行人脸、口罩、行人等目标检测。高分辨率对检测精度至关重要，而基于分块的推理使得在有限内存下使用高分辨率输入成为可能。
*   **设备端训练**：在微控制器上收集少量新数据，并进行在线学习，以适应新任务。

### 微型音频

将音频信号（如语音）转换为二维频谱图（时间 vs. 频率），然后将其视为图像处理问题，使用卷积神经网络进行关键词检测或语音识别。MCUNet在此类任务上也能提升效率。

![](img/6f1e7c1c906902af22669eda0ade29ef_275.png)

### 时间序列与异常检测

![](img/6f1e7c1c906902af22669eda0ade29ef_277.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_279.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_281.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_283.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_284.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_285.png)

广泛应用于制造业、视频监控、医疗保健等领域，用于检测异常事件或产品缺陷。

![](img/6f1e7c1c906902af22669eda0ade29ef_287.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_289.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_291.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_293.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_295.png)

**传统方法**：使用**自编码器**。它包含一个编码器（将输入压缩为低维编码向量）和一个解码器（试图从编码向量重建输入）。训练目标是最小化重建误差。对于训练数据分布内的“正常”数据，重建误差小；对于“异常”数据，重建误差大。通过设定阈值，即可检测异常。

![](img/6f1e7c1c906902af22669eda0ade29ef_297.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_299.png)

![](img/6f1e7c1c906902af22669eda0ade29ef_301.png)

**新趋势**：随着大语言模型和视觉语言模型的发展，现在可以使用这些强大的模型来理解和描述图像中的异常，为异常检测提供了新的可能性。

## 总结 📝

![](img/6f1e7c1c906902af22669eda0ade29ef_303.png)

本节课我们一起学习了TinyML的核心概念与挑战。我们了解到微控制器的资源极其有限，需要协同设计算法与系统来克服内存瓶颈。我们深入探讨了TinyNAS如何通过两阶段搜索自动设计出内存高效的微型网络架构，并介绍了基于分块的推理技术来进一步降低峰值内存消耗。最后，我们看到了这些技术在微型视觉、音频、时间序列分析及异常检测等领域的广泛应用。这些方法使得在成本仅几美元、功耗极低的微型设备上运行智能应用成为现实，真正实现了AI的民主化。