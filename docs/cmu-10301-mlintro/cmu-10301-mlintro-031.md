# 31：第三次考试复习教程

![](img/74f78ddb043deb17b7f3fc9a435697a6_1.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_2.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_4.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_5.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_6.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_7.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_9.png)

在本节课中，我们将一起复习第三次考试的核心内容，涵盖卷积神经网络、循环神经网络、Transformer、强化学习、主成分分析、K-Means聚类以及集成方法。我们将以简单直白的方式解释每个概念，并确保初学者能够理解。

![](img/74f78ddb043deb17b7f3fc9a435697a6_11.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_12.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_13.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_15.png)

## 卷积神经网络 (CNN) 基础

![](img/74f78ddb043deb17b7f3fc9a435697a6_17.png)

上一节我们介绍了本次复习的总体安排，本节中我们来看看卷积神经网络的基础概念。

![](img/74f78ddb043deb17b7f3fc9a435697a6_19.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_21.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_23.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_25.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_27.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_29.png)

### 什么是卷积核？

![](img/74f78ddb043deb17b7f3fc9a435697a6_31.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_32.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_33.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_35.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_36.png)

卷积核是一组权重或过滤器，它会与超参数（如填充、步幅和过滤器大小）一起在图像上滑动。

![](img/74f78ddb043deb17b7f3fc9a435697a6_38.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_40.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_42.png)

### 步幅的作用与权衡

![](img/74f78ddb043deb17b7f3fc9a435697a6_44.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_46.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_48.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_50.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_52.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_54.png)

步幅决定了每次卷积操作中过滤器移动的距离。它控制着过滤器在行和列上移动的速度。

![](img/74f78ddb043deb17b7f3fc9a435697a6_56.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_57.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_59.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_61.png)

以下是步幅不同取值的影响：
*   **较大的步幅值**：会减小输出维度，有助于对抗过拟合，但可能会丢失原始图像中的细节信息。
*   **较小的步幅值**：能更好地保持输出尺寸与输入尺寸相近。

![](img/74f78ddb043deb17b7f3fc9a435697a6_62.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_64.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_66.png)

### 填充的功能

![](img/74f78ddb043deb17b7f3fc9a435697a6_68.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_70.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_72.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_74.png)

填充是在输入图像边缘添加空白区域。它的主要作用有两个：
1.  防止过滤器在滑动时“滑出”图像边界，确保图像边缘的像素能被充分处理。
2.  帮助保持输出形状与输入形状相同。

![](img/74f78ddb043deb17b7f3fc9a435697a6_76.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_78.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_80.png)

### 输出尺寸计算公式

![](img/74f78ddb043deb17b7f3fc9a435697a6_82.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_84.png)

假设输入形状为 `A x A`，过滤器大小为 `K x K`，填充为 `P`，步幅为 `S`，则输出形状 `B x B` 可以通过以下公式计算：

![](img/74f78ddb043deb17b7f3fc9a435697a6_86.png)

`B = floor((A + 2P - K) / S) + 1`

![](img/74f78ddb043deb17b7f3fc9a435697a6_88.png)

**示例**：要将一个 `4x4` 的输入通过 `3x3` 的卷积核转换为 `3x3` 的输出，最小的步幅和填充组合是：**步幅=2，填充=1**。

![](img/74f78ddb043deb17b7f3fc9a435697a6_90.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_92.png)

### 下采样与上采样

![](img/74f78ddb043deb17b7f3fc9a435697a6_94.png)

*   **下采样**：用于降低输出维度，压缩图像，去除噪声，有助于对抗过拟合。
*   **上采样**：用于增加输出维度，例如将特征图尺寸恢复至原始输入大小。

![](img/74f78ddb043deb17b7f3fc9a435697a6_96.png)

### 参数共享

![](img/74f78ddb043deb17b7f3fc9a435697a6_98.png)

参数共享意味着在卷积过程中使用相同的过滤器。

![](img/74f78ddb043deb17b7f3fc9a435697a6_100.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_102.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_104.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_106.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_107.png)

*   **使用参数共享时**：学习的参数数量等于过滤器的大小，即 `K^2`。
*   **不使用参数共享时**：学习的参数数量等于过滤器大小乘以输出特征图的大小，即 `K^2 * B^2`。

**场景思考**：在已知所有汽车图片都是右侧视角的侧视图且汽车大致相同的情况下，参数共享可能不是最合适的，因为我们可以为车轮、车灯等不同部位创建不同的专用过滤器。

![](img/74f78ddb043deb17b7f3fc9a435697a6_109.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_110.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_112.png)

---

![](img/74f78ddb043deb17b7f3fc9a435697a6_114.png)

## 循环神经网络 (RNN) 与 Transformer

![](img/74f78ddb043deb17b7f3fc9a435697a6_116.png)

上一节我们探讨了CNN，本节中我们来看看处理序列数据的模型。

![](img/74f78ddb043deb17b7f3fc9a435697a6_118.png)

### RNN vs. CNN 适用场景

![](img/74f78ddb043deb17b7f3fc9a435697a6_120.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_122.png)

RNN 在处理具有时间或顺序依赖性的数据时更具优势。

![](img/74f78ddb043deb17b7f3fc9a435697a6_124.png)

以下是更适合使用 RNN 的场景：
*   **语音识别**：当前发音可能依赖于之前的音节。
*   **音乐作曲**：下一个音符的选择依赖于之前的旋律。
*   **自动驾驶系统**：当前的决策需要基于之前观察到的路况。

![](img/74f78ddb043deb17b7f3fc9a435697a6_126.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_128.png)

而**人脸识别**这类任务通常没有强烈的时序依赖，因此 CNN 更为常用。

### RNN 分析时间序列数据

![](img/74f78ddb043deb17b7f3fc9a435697a6_130.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_131.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_133.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_134.png)

RNN 能够将先前时间步的信息整合到当前时间步的计算中，并且可以处理可变长度的输入序列，这使其非常适合分析时间序列数据，用于趋势预测和异常检测等任务。

![](img/74f78ddb043deb17b7f3fc9a435697a6_136.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_138.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_140.png)

### Transformer 与掩码

![](img/74f78ddb043deb17b7f3fc9a435697a6_142.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_144.png)

Transformer 也是一种序列模型，但它允许模型同时关注序列中的所有位置。为了防止模型在预测时“偷看”未来的信息（即作弊），我们需要使用**掩码**。

![](img/74f78ddb043deb17b7f3fc9a435697a6_146.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_147.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_148.png)

**掩码的作用**：在训练时，掩码会遮挡住当前时间步之后的所有输入，确保模型只能基于当前及之前的信息进行预测。

![](img/74f78ddb043deb17b7f3fc9a435697a6_150.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_152.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_153.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_154.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_156.png)

### 填充与截断

![](img/74f78ddb043deb17b7f3fc9a435697a6_158.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_160.png)

为了利用Transformer的并行计算能力，我们通常将多个序列组成批次同时处理。这就要求批次内的所有序列长度必须相同。

*   **填充**：在较短序列的末尾添加特殊符号（如`[PAD]`），使其长度与批次中最长的序列一致。
*   **截断**：当序列过长时，将其截断至一个预设的最大长度，以适应内存和计算资源的限制。

![](img/74f78ddb043deb17b7f3fc9a435697a6_162.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_163.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_164.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_165.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_167.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_168.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_169.png)

### RNN 的梯度消失问题

![](img/74f78ddb043deb17b7f3fc9a435697a6_171.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_173.png)

在经典RNN架构中，梯度需要通过很长的链式路径反向传播。如果梯度值本身很小，在连续相乘（尤其是权重矩阵连乘）后可能会变得极其微小，甚至消失。这导致网络难以学习长距离的依赖关系，即“遗忘”较早的信息。

![](img/74f78ddb043deb17b7f3fc9a435697a6_175.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_177.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_178.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_180.png)

### 层归一化

![](img/74f78ddb043deb17b7f3fc9a435697a6_182.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_183.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_184.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_186.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_187.png)

在训练神经网络时，网络各层激活值的分布可能会发生变化，这被称为内部协变量偏移，会使训练变得困难。层归一化通过对每一层的输入进行标准化，使其保持稳定的分布，从而加速和稳定训练过程。

![](img/74f78ddb043deb17b7f3fc9a435697a6_189.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_191.png)

### 多头注意力机制

![](img/74f78ddb043deb17b7f3fc9a435697a6_193.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_195.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_197.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_198.png)

使用多头注意力机制类似于在CNN中使用多个过滤器。每个“头”可以学习关注序列中不同类型的关系或特征，从而让模型获得更丰富、更强大的表示能力。由于多个头的计算可以并行进行，增加头数通常不会显著增加训练时间。

### 微调 vs. 上下文学习

![](img/74f78ddb043deb17b7f3fc9a435697a6_200.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_202.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_203.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_205.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_207.png)

对于一个预训练的语言模型，针对不同任务选择合适的适应策略：
*   **法律文档分析**：更适合**微调**。因为该领域专业性强、规则固定，使用少量高质量的领域特定数据进行微调，能让模型快速适应特定任务。
*   **诗歌生成**：更适合**上下文学习**。因为诗歌风格多样，富有创造性。通过提供示例（上下文），让模型利用其已有的广泛知识来生成符合要求的文本，可能比微调到某一种固定风格更有效。

![](img/74f78ddb043deb17b7f3fc9a435697a6_209.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_210.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_212.png)

---

![](img/74f78ddb043deb17b7f3fc9a435697a6_214.png)

## 强化学习 (RL) 核心概念

![](img/74f78ddb043deb17b7f3fc9a435697a6_216.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_218.png)

上一节我们讨论了序列模型，本节中我们进入决策领域，学习强化学习。

![](img/74f78ddb043deb17b7f3fc9a435697a6_220.png)

### 马尔可夫决策过程 (MDP)

![](img/74f78ddb043deb17b7f3fc9a435697a6_222.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_223.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_225.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_227.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_228.png)

MDP 是强化学习的经典框架，它包含状态空间 `S`、动作空间 `A`、转移概率 `P` 和奖励函数 `R`。

![](img/74f78ddb043deb17b7f3fc9a435697a6_230.png)

**马尔可夫性假设**：下一个状态 `s‘` 的概率仅取决于当前状态 `s` 和当前采取的动作 `a`，而与之前的历史状态和动作无关。

![](img/74f78ddb043deb17b7f3fc9a435697a6_232.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_233.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_235.png)

**示例：状态与动作空间大小**
*   状态由 `(行, 列, 方向)` 三元组表示。在一个 `4x4` 的网格中，有 `4*4=16` 个位置，每个位置有4个方向（东、南、西、北）。因此，状态空间大小为 `16 * 4 = 64`。
*   动作空间为 `{左转， 右转， 前进}`，因此大小为 `3`。

![](img/74f78ddb043deb17b7f3fc9a435697a6_237.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_238.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_239.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_240.png)

### 价值迭代算法

![](img/74f78ddb043deb17b7f3fc9a435697a6_242.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_244.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_245.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_247.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_248.png)

价值迭代是一种求解MDP最优策略的动态规划方法。

![](img/74f78ddb043deb17b7f3fc9a435697a6_250.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_252.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_253.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_254.png)

**计算复杂度**：每次迭代的复杂度为 `O(|A| * |S|^2)`。因此，**状态空间大小**和**动作空间大小**会增加其计算复杂度，而转移函数是否随机、奖励函数是否已知则不影响单次迭代的复杂度。

![](img/74f78ddb043deb17b7f3fc9a435697a6_256.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_257.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_259.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_261.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_262.png)

**异步价值迭代示例**：在一个网格世界中，智能体需要计算到达目标状态所能获得的总奖励（即时奖励 + 未来奖励的折扣总和）。通过迭代更新每个状态的价值函数，最终可以收敛并找到最优策略（例如，在某个状态下选择向右走比向上走的总奖励更高）。

![](img/74f78ddb043deb17b7f3fc9a435697a6_264.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_266.png)

### Q学习

Q学习是一种无模型的强化学习方法，它不需要知道环境的转移概率和奖励函数。

![](img/74f78ddb043deb17b7f3fc9a435697a6_268.png)

**Q学习 vs. 价值/策略迭代**：
*   Q学习的主要优势在于它能应用于**模型未知**的环境。
*   因此，并非所有Q学习能解决的问题都能用价值/策略迭代解决。

**收敛性**：Q学习只有在**每个状态-动作对被无限次访问**的条件下，才保证收敛到最优Q值 `Q*`。

![](img/74f78ddb043deb17b7f3fc9a435697a6_270.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_272.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_274.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_275.png)

**Q值更新**：在收到奖励并到达新状态 `s‘` 后，但在更新Q值之前，旧的 `Q(s, a)` 与新估计值 `R + γ * max(Q(s‘, a‘))` 之间没有确定的数学关系（因为 `R` 和 `γ` 未知），因此无法判断其大小。

![](img/74f78ddb043deb17b7f3fc9a435697a6_277.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_278.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_279.png)

---

## 主成分分析 (PCA) 与 K-Means 聚类

![](img/74f78ddb043deb17b7f3fc9a435697a6_281.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_282.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_284.png)

上一节我们学习了如何让智能体通过试错进行学习，本节中我们来看看两种重要的无监督学习方法。

![](img/74f78ddb043deb17b7f3fc9a435697a6_286.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_288.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_290.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_291.png)

### 主成分分析 (PCA)

![](img/74f78ddb043deb17b7f3fc9a435697a6_293.png)

PCA的目标是找到数据中方差最大的方向（主成分），并将数据投影到这些方向上，以实现降维或特征提取。

![](img/74f78ddb043deb17b7f3fc9a435697a6_295.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_296.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_298.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_299.png)

**核心思想**：第一主成分是数据投影后方差最大的方向；第二主成分是与第一主成分正交且方差次大的方向，依此类推。

![](img/74f78ddb043deb17b7f3fc9a435697a6_301.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_303.png)

**注意点**：
*   PCA的目标是**最小化重构误差**或保留数据的主要变异，而不是直接优化对某个输出变量的预测性能。
*   PCA的输出可以是任意维度，不一定是更低维的。

![](img/74f78ddb043deb17b7f3fc9a435697a6_305.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_307.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_309.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_311.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_313.png)

### K-Means 聚类

![](img/74f78ddb043deb17b7f3fc9a435697a6_315.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_316.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_318.png)

K-Means 是一种将数据划分为K个簇的迭代算法。

![](img/74f78ddb043deb17b7f3fc9a435697a6_320.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_322.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_323.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_325.png)

**特性**：
*   **确定性**：给定相同的初始聚类中心，K-Means 每次都会产生相同的结果。
*   **局部最优**：K-Means 不能保证收敛到全局最优解，结果依赖于初始中心点的选择。
*   **对异常值敏感**：因为聚类中心是簇内所有点的均值，异常值会显著拉偏中心的位置。
*   **与KNN的区别**：K-Means 是无监督聚类算法（`K` 指簇数）；K近邻是有监督分类算法（`K` 指邻居数）。

![](img/74f78ddb043deb17b7f3fc9a435697a6_327.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_328.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_330.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_332.png)

### K-Means++ 初始化

![](img/74f78ddb043deb17b7f3fc9a435697a6_334.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_336.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_338.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_340.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_341.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_342.png)

K-Means++ 是一种改进的初始化方法，旨在选择彼此距离较远的点作为初始中心，以增加找到更好解的概率。

![](img/74f78ddb043deb17b7f3fc9a435697a6_344.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_345.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_346.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_348.png)

**步骤**：
1.  随机选择第一个中心点。
2.  对于每个非中心点，计算其与**最近中心点**的**距离的平方**。
3.  依据这个平方距离的比例作为概率，随机选择下一个中心点（距离越远的点被选中的概率越大）。
4.  重复步骤2-3，直到选出K个中心点。

![](img/74f78ddb043deb17b7f3fc9a435697a6_350.png)

**示例**：给定点 `(0,0)`, `(1,2)`, `(2,3)`, `(3,1)`, `(4,1)`。第一个中心是 `(0,0)`。
*   选择第二个中心时，各点概率与到 `(0,0)` 距离平方成正比。`(4,1)` 最远，概率最大，被选中。
*   选择第三个中心时，需计算各点到最近中心（`(0,0)` 或 `(4,1)`）的距离平方。`(2,3)` 到 `(4,1)` 的距离平方为8，在所有剩余点中最大，因此被选中。

![](img/74f78ddb043deb17b7f3fc9a435697a6_352.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_354.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_355.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_356.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_358.png)

---

![](img/74f78ddb043deb17b7f3fc9a435697a6_360.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_362.png)

## 集成方法：AdaBoost 与随机森林

![](img/74f78ddb043deb17b7f3fc9a435697a6_364.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_366.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_368.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_370.png)

上一节我们介绍了两种无监督学习技术，本节中我们来看看如何组合多个模型以获得更好的性能。

![](img/74f78ddb043deb17b7f3fc9a435697a6_372.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_374.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_375.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_376.png)

### AdaBoost (自适应提升)

![](img/74f78ddb043deb17b7f3fc9a435697a6_378.png)

AdaBoost 是一种 boosting 算法，它顺序地训练一系列弱分类器，并调整数据权重，使后续分类器更关注之前被错误分类的样本。

**关键特性**：
*   **最终假设**：即使最终的集成模型在训练集上达到零错误，也不意味着其中的每个弱分类器都是完美的。
*   **持续训练**：继续增加弱分类器（即使训练误差已为0）可能有助于降低在未见数据上的误差，提升泛化能力，防止过拟合。
*   **权重更新**：被错误分类的样本权重会以**相同的乘法因子**增加。

![](img/74f78ddb043deb17b7f3fc9a435697a6_380.png)

### 随机森林

![](img/74f78ddb043deb17b7f3fc9a435697a6_382.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_384.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_385.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_387.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_389.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_390.png)

随机森林是一种 bagging 算法，它构建多棵决策树，并通过投票（分类）或平均（回归）来做出最终预测。

![](img/74f78ddb043deb17b7f3fc9a435697a6_392.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_394.png)

**关键特性**：
*   **构建过程**：每棵树使用训练集的一个自助采样集进行训练，并且在每个节点分裂时，只考虑特征的一个随机子集。
*   **袋外误差**：对于每棵树，未参与其训练的数据（袋外数据）可以用来评估该树的性能。所有树的袋外误差的平均值可以作为随机森林泛化误差的估计。
*   **特征使用**：如果让每棵树使用所有特征进行训练，会降低树之间的多样性，可能导致模型相关性增强，从而可能**增加**集成模型的泛化误差。

![](img/74f78ddb043deb17b7f3fc9a435697a6_396.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_398.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_400.png)

---

![](img/74f78ddb043deb17b7f3fc9a435697a6_402.png)

![](img/74f78ddb043deb17b7f3fc9a435697a6_404.png)

本节课中我们一起学习了第三次考试涵盖的多个核心机器学习主题。我们从CNN的基本操作（卷积核、步幅、填充）和RNN/Transformer的序列建模能力开始，然后探讨了强化学习中的MDP、价值迭代和Q学习，接着复习了无监督学习中的PCA和K-Means聚类，最后总结了集成学习中的AdaBoost和随机森林。希望这份教程能帮助你巩固理解，为考试做好充分准备。