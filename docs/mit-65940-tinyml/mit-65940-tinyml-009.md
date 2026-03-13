# 009：知识蒸馏 🧠

在本节课中，我们将要学习知识蒸馏技术。这是一种与剪枝和量化正交的模型压缩方法，旨在利用一个大型“教师”模型来指导一个更小的“学生”模型进行训练，从而提升小模型的性能。

![](img/e11ae27be5160fd9cad659390fea888a_1.png)

![](img/e11ae27be5160fd9cad659390fea888a_3.png)

![](img/e11ae27be5160fd9cad659390fea888a_5.png)

![](img/e11ae27be5160fd9cad659390fea888a_6.png)

请确保您已完成作业一，并正在着手实验二。

![](img/e11ae27be5160fd9cad659390fea888a_8.png)

![](img/e11ae27be5160fd9cad659390fea888a_9.png)

![](img/e11ae27be5160fd9cad659390fea888a_11.png)

---

![](img/e11ae27be5160fd9cad659390fea888a_13.png)

![](img/e11ae27be5160fd9cad659390fea888a_15.png)

## 知识蒸馏的动机与概念 🤔

![](img/e11ae27be5160fd9cad659390fea888a_17.png)

![](img/e11ae27be5160fd9cad659390fea888a_18.png)

上一节我们介绍了剪枝和量化，本节中我们来看看另一种技术——知识蒸馏。其核心动机在于硬件资源的限制。无论是在云端还是移动设备上，计算和内存资源都是有限的。云端GPU成本高昂，内存容量有限；而移动设备和微控制器通常只有几百KB的内存。因此，我们需要训练能够适应极小内存预算的模型，同时尽可能匹配大型模型的精度。即使在云端，为了降低大语言模型的服务成本，知识蒸馏也至关重要，例如将一个700亿参数的模型蒸馏到70亿参数的模型，可以节省10倍的内存和带宽。

![](img/e11ae27be5160fd9cad659390fea888a_20.png)

![](img/e11ae27be5160fd9cad659390fea888a_21.png)

![](img/e11ae27be5160fd9cad659390fea888a_23.png)

![](img/e11ae27be5160fd9cad659390fea888a_25.png)

![](img/e11ae27be5160fd9cad659390fea888a_27.png)

核心问题是：**我们能否利用一个更大的模型来指导一个更小的模型？** 如下图所示，左侧是大型教师模型，右侧是小型学生模型。教师模型的精度可能高达82%，而未经指导的学生模型可能只有52%。知识蒸馏的目标就是借助教师模型来提升学生模型的训练效果。

![](img/e11ae27be5160fd9cad659390fea888a_29.png)

![](img/e11ae27be5160fd9cad659390fea888a_31.png)

![](img/e11ae27be5160fd9cad659390fea888a_33.png)

![](img/e11ae27be5160fd9cad659390fea888a_35.png)

![](img/e11ae27be5160fd9cad659390fea888a_8.png)

![](img/e11ae27be5160fd9cad659390fea888a_37.png)

![](img/e11ae27be5160fd9cad659390fea888a_39.png)

![](img/e11ae27be5160fd9cad659390fea888a_41.png)

![](img/e11ae27be5160fd9cad659390fea888a_43.png)

## 知识蒸馏的基本流程 🔄

![](img/e11ae27be5160fd9cad659390fea888a_45.png)

![](img/e11ae27be5160fd9cad659390fea888a_47.png)

![](img/e11ae27be5160fd9cad659390fea888a_49.png)

知识蒸馏的流程如下图所示。教师网络和学生网络接收相同的输入。教师网络通常更大，学生网络更小。它们都会产生预测逻辑值。

![](img/e11ae27be5160fd9cad659390fea888a_51.png)

![](img/e11ae27be5160fd9cad659390fea888a_52.png)

![](img/e11ae27be5160fd9cad659390fea888a_54.png)

![](img/e11ae27be5160fd9cad659390fea888a_56.png)

![](img/e11ae27be5160fd9cad659390fea888a_57.png)

![](img/e11ae27be5160fd9cad659390fea888a_58.png)

![](img/e11ae27be5160fd9cad659390fea888a_11.png)

![](img/e11ae27be5160fd9cad659390fea888a_60.png)

![](img/e11ae27be5160fd9cad659390fea888a_62.png)

![](img/e11ae27be5160fd9cad659390fea888a_64.png)

在训练学生网络时，我们不仅使用传统的分类损失，还会添加一个新的损失项——**蒸馏损失**。这个损失旨在匹配教师模型和学生模型的逻辑值输出。

![](img/e11ae27be5160fd9cad659390fea888a_66.png)

![](img/e11ae27be5160fd9cad659390fea888a_67.png)

![](img/e11ae27be5160fd9cad659390fea888a_68.png)

![](img/e11ae27be5160fd9cad659390fea888a_70.png)

![](img/e11ae27be5160fd9cad659390fea888a_71.png)

![](img/e11ae27be5160fd9cad659390fea888a_73.png)

![](img/e11ae27be5160fd9cad659390fea888a_13.png)

![](img/e11ae27be5160fd9cad659390fea888a_75.png)

![](img/e11ae27be5160fd9cad659390fea888a_76.png)

![](img/e11ae27be5160fd9cad659390fea888a_78.png)

添加蒸馏损失的直觉在于：即使学生模型的分类是正确的，其预测的“置信度”也可能与教师模型不同。例如，对于一张猫的图片，教师模型可能以98%的概率确信是猫，而学生模型可能只有73%的确信度。交叉熵损失无法捕捉这种置信度的差异，而蒸馏损失则试图让学生模型的输出概率分布向教师模型对齐。

## 温度与Softmax 🌡️

![](img/e11ae27be5160fd9cad659390fea888a_80.png)

![](img/e11ae27be5160fd9cad659390fea888a_82.png)

为了对齐概率分布，我们引入了**温度**的概念。标准的Softmax函数公式如下：

![](img/e11ae27be5160fd9cad659390fea888a_84.png)

![](img/e11ae27be5160fd9cad659390fea888a_86.png)

![](img/e11ae27be5160fd9cad659390fea888a_88.png)

**公式：** `P_i = exp(z_i) / Σ_j exp(z_j)`

![](img/e11ae27be5160fd9cad659390fea888a_90.png)

其中，`z_i` 是第i类的逻辑值。当温度 `T=1` 时，就是常规的Softmax。引入温度 `T` 后，公式变为：

![](img/e11ae27be5160fd9cad659390fea888a_92.png)

![](img/e11ae27be5160fd9cad659390fea888a_93.png)

![](img/e11ae27be5160fd9cad659390fea888a_95.png)

![](img/e11ae27be5160fd9cad659390fea888a_97.png)

![](img/e11ae27be5160fd9cad659390fea888a_99.png)

**公式：** `P_i = exp(z_i / T) / Σ_j exp(z_j / T)`

![](img/e11ae27be5160fd9cad659390fea888a_101.png)

![](img/e11ae27be5160fd9cad659390fea888a_103.png)

![](img/e11ae27be5160fd9cad659390fea888a_105.png)

![](img/e11ae27be5160fd9cad659390fea888a_107.png)

更高的温度会使输出的概率分布更加平滑。例如，原来的概率分布 `[0.98, 0.02]` 在 `T=10` 时可能变为 `[0.60, 0.40]`。在知识蒸馏中，我们通常使用较高的温度来计算教师模型的“软标签”，让学生模型去匹配这个更平滑、富含更多信息的分布。

![](img/e11ae27be5160fd9cad659390fea888a_35.png)

![](img/e11ae27be5160fd9cad659390fea888a_109.png)

![](img/e11ae27be5160fd9cad659390fea888a_111.png)

![](img/e11ae27be5160fd9cad659390fea888a_113.png)

## 匹配什么？——知识蒸馏的不同形式 🎯

![](img/e11ae27be5160fd9cad659390fea888a_115.png)

![](img/e11ae27be5160fd9cad659390fea888a_117.png)

![](img/e11ae27be5160fd9cad659390fea888a_118.png)

![](img/e11ae27be5160fd9cad659390fea888a_120.png)

![](img/e11ae27be5160fd9cad659390fea888a_121.png)

我们已经了解了匹配输出逻辑值的基本形式。实际上，我们可以匹配教师和学生模型之间多种不同的张量。以下是主要的匹配方式：

![](img/e11ae27be5160fd9cad659390fea888a_123.png)

### 1. 匹配输出逻辑值
这是最直接的方式，使用交叉熵损失或L2损失来匹配教师和学生模型的最终输出概率。

![](img/e11ae27be5160fd9cad659390fea888a_125.png)

![](img/e11ae27be5160fd9cad659390fea888a_126.png)

![](img/e11ae27be5160fd9cad659390fea888a_128.png)

**公式（交叉熵损失）：** `L_KD = - Σ P_T * log(P_S)`
**公式（L2损失）：** `L_KD = || P_T - P_S ||^2`

![](img/e11ae27be5160fd9cad659390fea888a_130.png)

![](img/e11ae27be5160fd9cad659390fea888a_131.png)

![](img/e11ae27be5160fd9cad659390fea888a_133.png)

### 2. 匹配中间权重
我们也可以尝试匹配中间层的权重。挑战在于教师和学生的权重张量维度不同。解决方案之一是使用一个可学习的投影矩阵（如1x1卷积），将学生的小维度权重映射到教师的大维度空间，然后进行匹配。

![](img/e11ae27be5160fd9cad659390fea888a_135.png)

![](img/e11ae27be5160fd9cad659390fea888a_66.png)

![](img/e11ae27be5160fd9cad659390fea888a_137.png)

![](img/e11ae27be5160fd9cad659390fea888a_139.png)

![](img/e11ae27be5160fd9cad659390fea888a_140.png)

### 3. 匹配中间特征/激活值
直觉是教师和学生网络不仅在最终输出，在中间层的特征分布上也应相似。我们可以匹配特定层的激活图。

![](img/e11ae27be5160fd9cad659390fea888a_142.png)

![](img/e11ae27be5160fd9cad659390fea888a_144.png)

![](img/e11ae27be5160fd9cad659390fea888a_146.png)

### 4. 匹配梯度
我们还可以尝试匹配梯度，特别是关于输入图像的梯度（即注意力图）。由于输入相同，教师和学生模型的输入梯度维度一致，易于匹配。梯度大的区域对模型决策更重要。

![](img/e11ae27be5160fd9cad659390fea888a_148.png)

![](img/e11ae27be5160fd9cad659390fea888a_150.png)

![](img/e11ae27be5160fd9cad659390fea888a_152.png)

![](img/e11ae27be5160fd9cad659390fea888a_154.png)

![](img/e11ae27be5160fd9cad659390fea888a_156.png)

![](img/e11ae27be5160fd9cad659390fea888a_80.png)

![](img/e11ae27be5160fd9cad659390fea888a_158.png)

![](img/e11ae27be5160fd9cad659390fea888a_160.png)

![](img/e11ae27be5160fd9cad659390fea888a_162.png)

### 5. 匹配稀疏模式
对于使用ReLU等激活函数的网络，我们可以匹配激活后的稀疏模式（即哪些神经元被激活）。

![](img/e11ae27be5160fd9cad659390fea888a_164.png)

![](img/e11ae27be5160fd9cad659390fea888a_166.png)

### 6. 匹配关系信息
这不再局限于单个张量，而是关注张量之间的关系。例如，匹配同一阶段内输入和输出特征之间的关系矩阵，或者匹配不同输入样本之间特征向量的相对距离（关系知识蒸馏）。

![](img/e11ae27be5160fd9cad659390fea888a_168.png)

![](img/e11ae27be5160fd9cad659390fea888a_170.png)

![](img/e11ae27be5160fd9cad659390fea888a_172.png)

![](img/e11ae27be5160fd9cad659390fea888a_173.png)

![](img/e11ae27be5160fd9cad659390fea888a_175.png)

![](img/e11ae27be5160fd9cad659390fea888a_120.png)

![](img/e11ae27be5160fd9cad659390fea888a_177.png)

![](img/e11ae27be5160fd9cad659390fea888a_179.png)

![](img/e11ae27be5160fd9cad659390fea888a_181.png)

![](img/e11ae27be5160fd9cad659390fea888a_183.png)

![](img/e11ae27be5160fd9cad659390fea888a_185.png)

关系知识蒸馏的损失函数涉及计算一个批次内所有样本对之间的特征距离，并匹配教师和学生模型对应的距离矩阵。

![](img/e11ae27be5160fd9cad659390fea888a_187.png)

![](img/e11ae27be5160fd9cad659390fea888a_189.png)

---

## 自蒸馏与在线蒸馏 🤝

传统的知识蒸馏需要预先训练一个大型教师模型，成本高昂。自蒸馏和在线蒸馏旨在解决这个问题。

![](img/e11ae27be5160fd9cad659390fea888a_191.png)

![](img/e11ae27be5160fd9cad659390fea888a_192.png)

### 自蒸馏
在自蒸馏中，教师和学生模型**架构相同、大小相同**。训练是迭代进行的：
1.  第一步，仅用交叉熵损失训练一个模型（作为教师0）。
2.  第二步，训练一个新模型（学生1），其损失结合了交叉熵和与教师0输出的蒸馏损失。
3.  重复此过程，用上一步的模型指导下一步。最后，可以集成所有步骤的模型以获得更好性能。

![](img/e11ae27be5160fd9cad659390fea888a_148.png)

![](img/e11ae27be5160fd9cad659390fea888a_194.png)

![](img/e11ae27be5160fd9cad659390fea888a_195.png)

![](img/e11ae27be5160fd9cad659390fea888a_197.png)

### 在线蒸馏（互学习）
在线蒸馏中，两个（或多个）相同大小的模型**从零开始共同训练**。每个模型同时作为其他模型的教师和学生。训练时，每个模型的损失包含其自身的分类损失和与其他模型输出的蒸馏损失。它们互相学习，共同进步。

![](img/e11ae27be5160fd9cad659390fea888a_198.png)

![](img/e11ae27be5160fd9cad659390fea888a_200.png)

![](img/e11ae27be5160fd9cad659390fea888a_202.png)

![](img/e11ae27be5160fd9cad659390fea888a_168.png)

![](img/e11ae27be5160fd9cad659390fea888a_204.png)

![](img/e11ae27be5160fd9cad659390fea888a_205.png)

![](img/e11ae27be5160fd9cad659390fea888a_207.png)

![](img/e11ae27be5160fd9cad659390fea888a_208.png)

### 成为你自己的老师
另一种思路是在单个模型内部进行蒸馏。使用深层分类器的输出作为“教师”，来监督较浅层分类器的训练。这样只需维护一套模型权重。

![](img/e11ae27be5160fd9cad659390fea888a_210.png)

![](img/e11ae27be5160fd9cad659390fea888a_211.png)

![](img/e11ae27be5160fd9cad659390fea888a_213.png)

![](img/e11ae27be5160fd9cad659390fea888a_214.png)

![](img/e11ae27be5160fd9cad659390fea888a_189.png)

![](img/e11ae27be5160fd9cad659390fea888a_216.png)

![](img/e11ae27be5160fd9cad659390fea888a_217.png)

![](img/e11ae27be5160fd9cad659390fea888a_219.png)

---

![](img/e11ae27be5160fd9cad659390fea888a_221.png)

![](img/e11ae27be5160fd9cad659390fea888a_222.png)

![](img/e11ae27be5160fd9cad659390fea888a_224.png)

![](img/e11ae27be5160fd9cad659390fea888a_226.png)

![](img/e11ae27be5160fd9cad659390fea888a_228.png)

## 知识蒸馏在不同任务中的应用 🛠️

知识蒸馏可应用于多种机器学习任务。

![](img/e11ae27be5160fd9cad659390fea888a_230.png)

![](img/e11ae27be5160fd9cad659390fea888a_232.png)

### 目标检测
在目标检测中，我们需要预测类别和边界框。蒸馏时，除了匹配特征图（通常使用1x1卷积对齐维度），还需要处理边界框回归损失。一种技巧是：仅当学生模型的预测误差大于教师模型加上一个阈值时，才应用蒸馏损失，确保教师提供的是有价值的指导。

![](img/e11ae27be5160fd9cad659390fea888a_234.png)

![](img/e11ae27be5160fd9cad659390fea888a_194.png)

![](img/e11ae27be5160fd9cad659390fea888a_235.png)

![](img/e11ae27be5160fd9cad659390fea888a_236.png)

![](img/e11ae27be5160fd9cad659390fea888a_238.png)

另一种方法是将连续的边界框坐标离散化为分类问题（分桶），然后使用交叉熵损失进行蒸馏。

![](img/e11ae27be5160fd9cad659390fea888a_240.png)

![](img/e11ae27be5160fd9cad659390fea888a_242.png)

![](img/e11ae27be5160fd9cad659390fea888a_244.png)

### 语义分割
对于像素级预测任务，可以引入一个判别器网络来提供对抗性损失。学生模型被训练以生成能够“欺骗”判别器的特征，使其无法区分特征来自教师还是学生，从而促使学生特征逼近教师特征。

![](img/e11ae27be5160fd9cad659390fea888a_246.png)

![](img/e11ae27be5160fd9cad659390fea888a_248.png)

![](img/e11ae27be5160fd9cad659390fea888a_249.png)

### 生成对抗网络压缩
知识蒸馏也可用于压缩GAN。损失函数通常结合：1) 中间特征图的蒸馏损失，2) 输出图像的重建损失，3) 对抗损失（确保生成质量）。这能显著提升小GAN模型在边缘设备上的推理速度。

![](img/e11ae27be5160fd9cad659390fea888a_251.png)

![](img/e11ae27be5160fd9cad659390fea888a_252.png)

![](img/e11ae27be5160fd9cad659390fea888a_253.png)

![](img/e11ae27be5160fd9cad659390fea888a_254.png)

![](img/e11ae27be5160fd9cad659390fea888a_228.png)

![](img/e11ae27be5160fd9cad659390fea888a_256.png)

### 自然语言处理/大语言模型
对于Transformer架构，除了匹配特征，匹配注意力图也非常有效。在大语言模型蒸馏中，通常使用剪枝后的模型作为学生，并匹配中间层的各种张量（如注意力输出、前馈网络输出等），以从超大教师模型向小型学生模型传递知识。

![](img/e11ae27be5160fd9cad659390fea888a_258.png)

![](img/e11ae27be5160fd9cad659390fea888a_260.png)

![](img/e11ae27be5160fd9cad659390fea888a_262.png)

![](img/e11ae27be5160fd9cad659390fea888a_264.png)

![](img/e11ae27be5160fd9cad659390fea888a_266.png)

---

![](img/e11ae27be5160fd9cad659390fea888a_268.png)

![](img/e11ae27be5160fd9cad659390fea888a_270.png)

![](img/e11ae27be5160fd9cad659390fea888a_272.png)

## 网络增广：另一种提升小模型性能的技术 🌱

![](img/e11ae27be5160fd9cad659390fea888a_274.png)

![](img/e11ae27be5160fd9cad659390fea888a_276.png)

除了知识蒸馏，**网络增广**是另一种提升小模型性能的正交技术。对于大模型，数据增广和Dropout能有效防止过拟合。但对于小模型，它们往往容量不足，容易欠拟合，这些技术可能反而有害。

![](img/e11ae27be5160fd9cad659390fea888a_278.png)

![](img/e11ae27be5160fd9cad659390fea888a_280.png)

网络增广的思路是：**在训练过程中，临时“增广”小模型，增加其宽度或深度，以提供额外的监督信号**。训练时，我们维护一个共享权重的小型基础模型。在每个训练步骤，我们随机采样一个增广后的更大网络（在基础模型上扩展），计算损失和梯度，并将梯度回传到共享的基础模型权重上。这相当于为基础模型提供了来自不同容量网络的辅助监督，有助于其逃离局部最优，提升性能。

![](img/e11ae27be5160fd9cad659390fea888a_282.png)

![](img/e11ae27be5160fd9cad659390fea888a_283.png)

![](img/e11ae27be5160fd9cad659390fea888a_284.png)

![](img/e11ae27be5160fd9cad659390fea888a_285.png)

![](img/e11ae27be5160fd9cad659390fea888a_287.png)

![](img/e11ae27be5160fd9cad659390fea888a_289.png)

![](img/e11ae27be5160fd9cad659390fea888a_304.png)

![](img/e11ae27be5160fd9cad659390fea888a_291.png)

![](img/e11ae27be5160fd9cad659390fea888a_293.png)

![](img/e11ae27be5160fd9cad659390fea888a_295.png)

![](img/e11ae27be5160fd9cad659390fea888a_296.png)

![](img/e11ae27be5160fd9cad659390fea888a_298.png)

实验表明，网络增广能有效提升小模型的精度，且可以与知识蒸馏结合使用，获得进一步增益。

![](img/e11ae27be5160fd9cad659390fea888a_300.png)

![](img/e11ae27be5160fd9cad659390fea888a_302.png)

---

![](img/e11ae27be5160fd9cad659390fea888a_304.png)

![](img/e11ae27be5160fd9cad659390fea888a_306.png)

![](img/e11ae27be5160fd9cad659390fea888a_308.png)

![](img/e11ae27be5160fd9cad659390fea888a_310.png)

## 总结 📚

![](img/e11ae27be5160fd9cad659390fea888a_312.png)

![](img/e11ae27be5160fd9cad659390fea888a_314.png)

![](img/e11ae27be5160fd9cad659390fea888a_316.png)

![](img/e11ae27be5160fd9cad659390fea888a_318.png)

本节课我们一起学习了知识蒸馏技术。我们首先了解了其动机：利用大型教师模型指导小型学生模型，以在有限资源下获得高性能。接着，我们深入探讨了其核心流程，包括温度Softmax的使用。

![](img/e11ae27be5160fd9cad659390fea888a_320.png)

![](img/e11ae27be5160fd9cad659390fea888a_322.png)

![](img/e11ae27be5160fd9cad659390fea888a_323.png)

![](img/e11ae27be5160fd9cad659390fea888a_325.png)

我们详细分析了可以匹配的多种对象：输出逻辑值、中间权重、特征、梯度、稀疏模式以及关系信息。然后，我们介绍了无需预训练大教师模型的自蒸馏和在线蒸馏方法。

![](img/e11ae27be5160fd9cad659390fea888a_327.png)

![](img/e11ae27be5160fd9cad659390fea888a_328.png)

此外，我们探索了知识蒸馏在目标检测、语义分割、GAN压缩以及大语言模型等不同任务中的应用。最后，我们介绍了另一种提升小模型性能的技术——网络增广，它通过临时增加模型容量来提供额外的训练监督。

![](img/e11ae27be5160fd9cad659390fea888a_330.png)

在下一讲中，我们将介绍算法-系统协同设计的MCUNet，探讨如何在微控制器上部署这些微型模型。