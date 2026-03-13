# 013：大语言模型高效部署技术 🚀

![](img/badc5f90e9fe4250bd201b5025a023b0_1.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_3.png)

在本节课中，我们将要学习大语言模型的高效部署技术。我们将从量化技术开始，探讨如何通过降低模型权重和激活值的精度来减少内存占用和计算开销。接着，我们会了解稀疏化技术，通过剪枝来减少模型的计算量。最后，我们将介绍支持大模型推理的系统级优化方法，如分页注意力、闪存注意力等，这些技术对于提升推理效率至关重要。

![](img/badc5f90e9fe4250bd201b5025a023b0_5.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_7.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_9.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_11.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_13.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_15.png)

---

![](img/badc5f90e9fe4250bd201b5025a023b0_17.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_19.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_21.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_23.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_25.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_26.png)

## 量化技术：8位权重与激活值量化

![](img/badc5f90e9fe4250bd201b5025a023b0_28.png)

上一节我们介绍了课程概述，本节中我们来看看量化技术。量化是将浮点数转换为低精度整数（如8位、4位）的过程，旨在减少模型的内存占用和计算成本。

![](img/badc5f90e9fe4250bd201b5025a023b0_30.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_31.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_33.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_35.png)

然而，传统的量化方法并不完全适用于大语言模型。随着模型规模从13亿参数增长到1750亿参数，8位量化的准确率会显著下降。这主要是因为大语言模型的激活值中存在“离群值”。

![](img/badc5f90e9fe4250bd201b5025a023b0_37.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_39.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_41.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_42.png)

### 离群值问题

![](img/badc5f90e9fe4250bd201b5025a023b0_44.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_46.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_47.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_49.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_51.png)

离群值是指某些通道的激活值异常巨大，远超过其他通道的值。如果直接量化，这些巨大的值会占据动态范围的大部分，导致其他较小的激活值在量化后被“挤压”为零，从而严重损害模型精度。

![](img/badc5f90e9fe4250bd201b5025a023b0_53.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_55.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_57.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_58.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_60.png)

**公式**：假设激活矩阵为 `X`，权重矩阵为 `W`。量化过程可以表示为：
`Q(X) = round(X / scale) * scale`
其中，离群值过大会导致 `scale` 过大，使得 `Q(X)` 中许多值变为零。

![](img/badc5f90e9fe4250bd201b5025a023b0_62.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_64.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_65.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_66.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_68.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_70.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_72.png)

### 平滑量化

![](img/badc5f90e9fe4250bd201b5025a023b0_74.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_76.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_78.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_79.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_80.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_81.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_82.png)

为了解决离群值问题，我们可以采用“平滑量化”技术。其核心思想是，由于矩阵乘法是线性的，我们可以通过缩放来平衡权重和激活值的量化难度。

![](img/badc5f90e9fe4250bd201b5025a023b0_84.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_85.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_87.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_89.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_90.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_91.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_92.png)

具体方法是：将激活值较大的通道缩小，同时将对应权重通道放大。这样，乘积结果保持不变，但激活值变得更容易量化，而权重虽然变得更难量化，但其本身分布相对均匀，仍能较好地承受量化。

![](img/badc5f90e9fe4250bd201b5025a023b0_93.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_95.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_97.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_99.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_101.png)

**公式**：寻找缩放因子 `s`，使得变换后的计算 `(X / s) * (W * s) = X * W` 结果不变。缩放因子 `s` 通常基于权重和激活值的统计量（如最大值）计算得出，例如取平方根：`s = sqrt(max(|X|) / max(|W|))`。

![](img/badc5f90e9fe4250bd201b5025a023b0_103.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_105.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_106.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_108.png)

通过这种方法，我们可以将量化的难度从激活值迁移到权重上，从而在保持数学等价性的前提下，实现更有效的低精度量化。

![](img/badc5f90e9fe4250bd201b5025a023b0_110.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_112.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_114.png)

---

![](img/badc5f90e9fe4250bd201b5025a023b0_116.png)

## 仅权重量化与AWQ算法

![](img/badc5f90e9fe4250bd201b5025a023b0_118.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_120.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_122.png)

上一节我们介绍了同时量化权重和激活值的方法，本节中我们来看看一种更极端的量化策略：仅权重量化。这种方法特别适用于单批次、单用户的设备端推理场景。

![](img/badc5f90e9fe4250bd201b5025a023b0_124.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_126.png)

在设备端推理中，计算强度较低，内存带宽（尤其是权重加载）成为主要瓶颈。因此，将权重量化到极低的位数（如4位），同时保持激活值为较高精度（如16位），可以显著减少内存占用，从而提升推理速度。

### 传统方法的局限性

![](img/badc5f90e9fe4250bd201b5025a023b0_128.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_129.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_130.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_132.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_134.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_135.png)

如果简单地使用四舍五入法对权重进行4位量化，会导致模型困惑度大幅上升，性能严重下降。这表明需要更智能的量化策略。

![](img/badc5f90e9fe4250bd201b5025a023b0_137.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_139.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_141.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_142.png)

### 激活感知权重量化

![](img/badc5f90e9fe4250bd201b5025a023b0_144.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_146.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_148.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_150.png)

AWQ算法的关键洞见是：在量化权重时，不应只关注权重本身的值，而应关注与之相乘的激活值。

![](img/badc5f90e9fe4250bd201b5025a023b0_152.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_154.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_156.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_158.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_160.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_162.png)

**原因**：激活值中存在离群通道。如果某个权重通道需要与一个巨大的激活值相乘，那么即使对该权重进行微小的量化扰动，也会对最终结果产生巨大影响。因此，我们需要“保护”这些重要的权重通道。

![](img/badc5f90e9fe4250bd201b5025a023b0_164.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_166.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_168.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_170.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_171.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_173.png)

以下是AWQ算法的核心步骤：

![](img/badc5f90e9fe4250bd201b5025a023b0_175.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_177.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_179.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_181.png)

1.  **识别重要通道**：通过分析校准数据集的激活值，找出那些具有较大幅度的通道。
2.  **缩放保护**：对于重要的权重通道，我们不是将其保留为浮点数（引入混合精度），而是将其按比例放大。同时，在推理时，将对应的激活值按相同比例缩小。这样，在数学上等价，但避免了复杂的混合精度计算。
3.  **优化缩放因子**：缩放因子 `s` 需要精心选择。`s` 过小保护不足，`s` 过大会损害其他通道。AWQ通过搜索一个超参数 `α` 来优化缩放因子：`s = (avg_activation_magnitude)^α`。

![](img/badc5f90e9fe4250bd201b5025a023b0_183.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_185.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_187.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_189.png)

**代码示意**：
```python
# 假设 W 是权重，X 是激活值，s 是计算出的缩放因子向量
W_scaled = W * s  # 放大重要权重
X_scaled = X / s  # 缩小对应激活值
# 量化 W_scaled 到4位
W_quant = quantize_to_4bit(W_scaled)
# 推理时使用： dequantize(W_quant) * X_scaled ≈ W * X
```

AWQ算法仅需少量校准数据，无需微调，就能在将权重量化到4位的同时，很好地保持模型在各种任务上的准确性。

![](img/badc5f90e9fe4250bd201b5025a023b0_191.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_193.png)

---

![](img/badc5f90e9fe4250bd201b5025a023b0_195.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_197.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_198.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_200.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_202.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_204.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_205.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_207.png)

## 结合二者优势：Q-Serve与W4A8量化

![](img/badc5f90e9fe4250bd201b5025a023b0_209.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_211.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_213.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_215.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_217.png)

上一节我们分别学习了面向云服务的平滑量化（W8A8）和面向边缘设备的AWQ（W4A16）。本节中我们来看看如何结合两者的优势，实现权重4位、激活值8位的量化（W4A8）。

![](img/badc5f90e9fe4250bd201b5025a023b0_219.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_221.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_223.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_225.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_227.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_229.png)

W4A8量化的目标是同时在低批次（内存带宽受限）和高批次（计算受限）场景下都获得性能提升。然而，实现高效的W4A8推理面临工程挑战。

### 工程实现挑战

关键在于如何高效地在GPU上执行4位权重与8位激活值的矩阵乘法。低效的实现（如在核心计算循环中进行反量化或缩放操作）会带来巨大开销，甚至导致速度比高精度版本更慢。

Q-Serve的解决方案是：
1.  **核心计算保持低精度**：在Tensor Core中进行计算时，先将4位权重解包为8位整数，然后与8位激活值进行整数矩阵乘法。
2.  **缩放操作外移**：将乘以缩放因子的操作移到核心计算循环之外，在CUDA Core中执行。这最大限度地减少了核心循环中的额外操作和寄存器压力。
3.  **KV缓存量化**：对注意力机制中的Key-Value缓存也进行4位量化，并应用类似平滑注意力的技术来处理Key中的离群值。

![](img/badc5f90e9fe4250bd201b5025a023b0_231.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_233.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_235.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_237.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_238.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_239.png)

通过这些系统级的优化，Q-Serve能够在保持高精度的前提下，实现比现有方案更高的吞吐量，成功结合了低权重精度和高激活值精度的优势。

![](img/badc5f90e9fe4250bd201b5025a023b0_241.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_242.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_243.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_245.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_247.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_249.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_250.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_251.png)

---

![](img/badc5f90e9fe4250bd201b5025a023b0_253.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_255.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_257.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_258.png)

## 应用于大语言模型的稀疏化技术

![](img/badc5f90e9fe4250bd201b5025a023b0_260.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_261.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_262.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_263.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_264.png)

上一节我们深入探讨了量化，本节我们转向另一种模型压缩技术：稀疏化。稀疏化通过将模型中的部分权重或激活值设为零来减少计算量。

### 权重稀疏化

![](img/badc5f90e9fe4250bd201b5025a023b0_266.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_268.png)

传统的权重剪枝基于权重幅度（magnitude），即剪掉值较小的权重。然而，对于大语言模型，更好的方法是基于“权重乘以输入激活值”的结果来剪枝。因为一个权重的重要性不仅取决于其本身大小，还取决于它需要处理的输入信号强度。

![](img/badc5f90e9fe4250bd201b5025a023b0_270.png)

### 上下文稀疏化

![](img/badc5f90e9fe4250bd201b5025a023b0_272.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_274.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_275.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_277.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_279.png)

静态稀疏化会损害模型灵活性。上下文稀疏化是一种动态方法，它根据当前输入文本来预测并跳过当前计算中不重要的注意力头或前馈网络维度。这需要训练一个轻量级预测器，但能更智能地减少计算，同时保持准确性。

![](img/badc5f90e9fe4250bd201b5025a023b0_281.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_283.png)

### 注意力稀疏化

自然语言存在冗余。注意力稀疏化通过分析注意力图，识别并剪除那些对当前输出贡献极小的输入token。例如，可以计算每个token收到的注意力分数总和，并剪除分数最低的token。类似地，也可以对KV缓存进行动态剪枝，以节省内存。

这些稀疏化技术可以与量化结合使用，进一步压缩和加速大语言模型。

![](img/badc5f90e9fe4250bd201b5025a023b0_285.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_287.png)

---

## 大语言模型推理的系统支持

上一节我们讨论了算法层面的优化，本节我们来看看支持高效推理的系统级技术与评估指标。

### 推理服务指标

![](img/badc5f90e9fe4250bd201b5025a023b0_289.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_291.png)

1.  **首词延迟**：用户提交查询后，模型产生第一个响应词所需的时间。这对交互体验至关重要。
2.  **每词延迟**：生成每个输出词所需的时间，其倒数即“每秒生成词数”。
3.  **吞吐量**：推理服务器每秒为所有请求生成的词数总和。
系统优化的目标是**最小化延迟**（尤其是首词延迟）并**最大化吞吐量**，这二者通常需要权衡。

![](img/badc5f90e9fe4250bd201b5025a023b0_293.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_294.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_296.png)

### 关键技术

![](img/badc5f90e9fe4250bd201b5025a023b0_298.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_300.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_301.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_303.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_305.png)

以下是提升推理效率的关键系统技术：

![](img/badc5f90e9fe4250bd201b5025a023b0_306.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_307.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_308.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_310.png)

**分页注意力**
KV缓存会随序列增长而膨胀，导致内存碎片化。分页注意力借鉴操作系统虚拟内存的思想，将KV缓存划分为固定大小的“块”，并通过块表管理。不同请求可以共享提示词的KV块，并能高效利用内存，减少浪费。

![](img/badc5f90e9fe4250bd201b5025a023b0_312.png)

**闪存注意力**
计算注意力矩阵（O(N²)）是内存密集型操作。闪存注意力通过“平铺”技术，将计算分解为小块，在计算QK^T后立即与V相乘，避免将整个巨大的注意力矩阵 materialize 到内存中，从而大幅降低内存占用和加速计算。

![](img/badc5f90e9fe4250bd201b5025a023b0_314.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_315.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_317.png)

**推测解码**
使用一个快速的小模型（草稿模型）自回归地生成多个候选词，然后一次性将这些候选词输入给大型、精确的模型（验证模型）进行并行验证和修正。由于大模型的并行计算特性，验证K个词的耗时接近于验证1个词，从而能用大模型的单次前向传播成本换取多个词的生成，显著提升解码速度。

![](img/badc5f90e9fe4250bd201b5025a023b0_319.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_320.png)

**动态与连续批处理**
*   **静态批处理**：等待一批请求满后再处理，吞吐量高但延迟大。
*   **动态批处理**：设置超时时间，批满或超时即处理，平衡吞吐与延迟。
*   **连续批处理**：以词为粒度进行调度。当一个请求生成完一个词后，可以立即插入另一个请求的词进行计算，实现GPU的持续饱和利用，特别适合输出长度不一的流式场景。

![](img/badc5f90e9fe4250bd201b5025a023b0_322.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_324.png)

---

![](img/badc5f90e9fe4250bd201b5025a023b0_326.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_328.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_329.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_330.png)

![](img/badc5f90e9fe4250bd201b5025a023b0_332.png)

本节课中我们一起学习了大语言模型高效部署的核心技术。我们从**量化**开始，了解了如何通过平滑量化和AWQ算法，在降低模型精度（至8位、4位）的同时保持准确性。接着，我们探讨了**稀疏化**技术，包括权重、上下文和注意力稀疏化，以动态减少计算量。最后，我们介绍了关键的**系统级优化**，如分页注意力、闪存注意力、推测解码和先进批处理策略，这些对于构建高性能、低延迟的推理服务至关重要。掌握这些技术，是高效部署大语言模型并将其应用于实际场景的关键。