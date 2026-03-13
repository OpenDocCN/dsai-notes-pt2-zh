# 16：长上下文模型 📚

![](img/028f9f4bbddc87ababd7402d0c31c158_0.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_2.png)

在本节课中，我们将要学习如何处理长序列建模或长上下文模型。这是一个非常活跃的研究领域，涉及从系统优化到新架构设计的多种方法。我们将首先探讨传统Transformer模型在处理长序列时面临的挑战，然后介绍一系列改进技术，最后了解一种全新的架构——状态空间模型。

![](img/028f9f4bbddc87ababd7402d0c31c158_4.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_6.png)

## 问题动机与挑战 🤔

![](img/028f9f4bbddc87ababd7402d0c31c158_8.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_10.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_12.png)

上一节我们介绍了模型并行化的不同方式。本节中，我们来看看与处理超长序列相关的另一种并行化思路。

为什么长序列建模是一个难题？主要原因有以下几点：

![](img/028f9f4bbddc87ababd7402d0c31c158_14.png)

*   **内存复杂度**：Transformer模型的内存需求随序列长度呈二次方增长，这会导致严重的内存瓶颈。
*   **计算复杂度**：注意力机制的计算量同样随序列长度呈二次方增长，影响训练和推理速度。
*   **训练数据**：获取高质量、格式统一的长上下文训练数据本身具有挑战性。

![](img/028f9f4bbddc87ababd7402d0c31c158_16.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_18.png)

长序列建模的应用场景非常广泛，包括：
*   处理长文档（如书籍、法律文件）
*   代码库理解与生成
*   长视频或音频内容分析
*   智能体（Agent）的长期历史跟踪
*   基因组序列分析

![](img/028f9f4bbddc87ababd7402d0c31c158_20.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_22.png)

## 评估基准与诊断任务 📊

![](img/028f9f4bbddc87ababd7402d0c31c158_24.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_26.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_27.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_29.png)

为了衡量模型在长上下文任务上的性能，研究人员设计了一些基准测试和诊断任务。

![](img/028f9f4bbddc87ababd7402d0c31c158_31.png)

以下是几个重要的评估方式：

![](img/028f9f4bbddc87ababd7402d0c31c158_33.png)

*   **Long Range Arena**：包含多种具有长程依赖关系的任务（不限于NLP）。
*   **SCROLLS**：一个NLP特定的基准，包含需要对长文档进行总结、问答等任务。
*   **针在干草堆（Needle in a Haystack）**：一个简单的诊断任务，用于测试模型能否从超长上下文中准确检索出特定信息。早期模型在此任务上表现不佳。
*   **上下文学习（In-Context Learning）**：通过增加上下文中的示例数量，可以提升模型在新任务上的表现，这本身也是长上下文能力的一种体现。

![](img/028f9f4bbddc87ababd7402d0c31c158_35.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_37.png)

## Transformer的瓶颈与高效注意力 ⚡

现在，让我们回顾一下Transformer注意力机制为何会成为处理长序列的瓶颈。

![](img/028f9f4bbddc87ababd7402d0c31c158_39.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_41.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_43.png)

标准的注意力计算公式为：
`Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) V`

![](img/028f9f4bbddc87ababd7402d0c31c158_45.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_47.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_49.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_51.png)

其中，计算 `QK^T` 会得到一个形状为 `[batch_size, num_heads, sequence_length, sequence_length]` 的矩阵。这导致了 `O(n^2)` 的内存和计算复杂度。

![](img/028f9f4bbddc87ababd7402d0c31c158_53.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_54.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_56.png)

在实际的GPU硬件中，快速但容量小的SRAM与慢速但容量大的HBM（高带宽内存）之间的数据迁移会成为主要瓶颈。当序列很长时，注意力矩阵无法放入SRAM，频繁的数据交换会极大降低速度。

![](img/028f9f4bbddc87ababd7402d0c31c158_58.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_60.png)

为了解决这个问题，研究人员提出了**在线Softmax**技巧。其核心思想是将Softmax计算分解为分子和分母的增量更新，从而避免存储整个 `n x n` 的注意力矩阵。

![](img/028f9f4bbddc87ababd7402d0c31c158_62.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_64.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_66.png)

对于一个查询向量 `q`，我们可以按顺序遍历所有键值对 `(k_i, v_i)`：
1.  计算权重 `w_i = exp(q·k_i)`
2.  增量更新分子 `numer += w_i * v_i`
3.  增量更新分母 `denom += w_i`
最终输出为 `numer / denom`。这种方法将内存复杂度从 `O(n^2)` 降低到了 `O(n)`。

基于这一思想，后续工作如 **Flash Attention** 通过编写高效的CUDA内核，更好地管理GPU内存层次结构，显著加速了训练和推理。而 **Ring Attention** 则进一步将这种在线计算分布到多个设备上，实现了“上下文并行”，从而能够处理极长的序列。

![](img/028f9f4bbddc87ababd7402d0c31c158_68.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_70.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_72.png)

## 外推问题与位置编码 🔄

![](img/028f9f4bbddc87ababd7402d0c31c158_74.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_76.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_78.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_80.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_82.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_84.png)

另一个关键问题是**外推（Extrapolation）**：如果一个模型只在固定长度（如4000个令牌）的序列上训练，当输入更长的序列时，它能否正常工作？

![](img/028f9f4bbddc87ababd7402d0c31c158_86.png)

答案通常是：不能。问题主要出在**位置编码**上：

![](img/028f9f4bbddc87ababd7402d0c31c158_88.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_89.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_91.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_93.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_95.png)

*   **绝对位置编码（可学习的）**：模型只学习了前4000个位置的嵌入向量。对于第4001个位置，它使用的是未经过训练的随机向量，导致模型行为不可预测。
*   **绝对位置编码（固定的，如正弦编码）**：虽然具有周期性，但模型在训练中未见过的绝对位置对应的向量模式仍然是新的，可能导致分布外问题。
*   **相对位置编码（如RoPE）**：理论上应该能更好地外推，但模型在训练过程中可能巧妙地学会了依赖绝对位置的特征，因此在实践中，未经调整的RoPE外推能力也有限。

![](img/028f9f4bbddc87ababd7402d0c31c158_97.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_99.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_101.png)

下图展示了使用RoPE的模型在超出训练长度后，性能急剧下降的情况：
![](img/028f9f4bbddc87ababd7402d0c31c158_86.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_103.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_105.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_107.png)

为了解决外推问题，主要有两种互补的策略：

![](img/028f9f4bbddc87ababd7402d0c31c158_109.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_111.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_113.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_115.png)

1.  **在更长序列上继续训练（Post-training）**：收集或合成更长的文档数据，对预训练模型进行继续训练，使其适应更长的上下文。
2.  **调整位置编码**：例如**位置插值（Position Interpolation）**，将原始的位置索引缩放，使其落入模型训练时所见的范围；或者调整RoPE的基频（base frequency），改变其周期，使其衰减更慢，从而更好地泛化到更长距离。

![](img/028f9f4bbddc87ababd7402d0c31c158_117.png)

## 状态空间模型：一种新架构 🌀

![](img/028f9f4bbddc87ababd7402d0c31c158_119.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_121.png)

前面我们讨论了在Transformer框架内改进长序列处理的方法。现在，我们来看看一种不同的架构——**状态空间模型（State Space Models, SSM）**，它融合了RNN和CNN的思想。

![](img/028f9f4bbddc87ababd7402d0c31c158_123.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_125.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_126.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_128.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_130.png)

首先，回顾一下RNN的优势与劣势：
*   **优势**：理论上具有无限上下文，推理时内存效率高（只需维护一个隐藏状态）。
*   **劣势**：训练难以并行化（序列计算依赖），且存在梯度消失/爆炸问题。

![](img/028f9f4bbddc87ababd7402d0c31c158_132.png)

状态空间模型（在离散形式下）的基本方程类似于一个线性RNN：
`h_t = A_bar * h_{t-1} + B_bar * x_t`
`y_t = C * h_t + D * x_t`
其中 `A_bar, B_bar, C, D` 是可学习的参数，`x_t` 是输入，`h_t` 是隐藏状态，`y_t` 是输出。

![](img/028f9f4bbddc87ababd7402d0c31c158_134.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_136.png)

状态空间模型的关键洞见在于**双重视角**：
1.  **循环视角**：如上式所示，可以进行高效、与序列长度无关的推理。
2.  **卷积视角**：通过巧妙的数学变换，整个系统可以等价地视为与一个全局卷积核进行卷积操作。这个卷积核可以通过参数 `A_bar, B_bar, C` 计算得到。由于卷积操作可以并行计算，因此**训练过程也可以高效并行化**。

![](img/028f9f4bbddc87ababd7402d0c31c158_138.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_140.png)

这样，SSM就同时获得了RNN的高效推理能力和CNN的高效训练能力。

![](img/028f9f4bbddc87ababd7402d0c31c158_142.png)

基于这个基础框架，出现了两个重要的变体：

![](img/028f9f4bbddc87ababd7402d0c31c158_144.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_146.png)

*   **S4 (Structured State Space Sequence Model)**：其主要创新是为控制状态更新的矩阵 `A` 设计了一种特殊的**结构化形式**（通过HiPPO理论），这有助于模型更好地记忆和保留历史信息。
*   **Mamba**：它引入了**选择性（Selectivity）** 机制。在S4中，参数 `A, B, C` 是时间不变的。而Mamba让这些参数成为当前输入 `x_t` 的函数，使模型能够动态地决定保留或忽略哪些信息，从而在处理需要选择性关注的任务上表现更佳。Mamba通过**并行扫描（Parallel Scan）** 算法来实现这种条件参数化下的高效训练。

![](img/028f9f4bbddc87ababd7402d0c31c158_148.png)

状态空间模型在需要超长上下文的任务上展现了强大潜力，例如在长达百万令牌的基因组数据或分钟级音频数据上，其性能优于传统Transformer。

![](img/028f9f4bbddc87ababd7402d0c31c158_150.png)

## 总结 🎯

![](img/028f9f4bbddc87ababd7402d0c31c158_152.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_153.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_155.png)

本节课中我们一起学习了长上下文模型的相关知识。

![](img/028f9f4bbddc87ababd7402d0c31c158_157.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_159.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_161.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_163.png)

我们首先了解了长序列建模的**动机、挑战和应用场景**。然后，深入分析了**Transformer模型在处理长序列时的瓶颈**，特别是注意力机制的二次方复杂度问题，并介绍了**高效注意力计算**（如在线Softmax、Flash Attention、Ring Attention）来克服这一瓶颈。

![](img/028f9f4bbddc87ababd7402d0c31c158_165.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_166.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_168.png)

接着，我们探讨了模型的**外推问题**，分析了不同位置编码的局限性，并介绍了通过**继续训练**和**调整位置编码**来提升模型长上下文能力的策略。

![](img/028f9f4bbddc87ababd7402d0c31c158_170.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_172.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_174.png)

最后，我们介绍了一种超越Transformer的新架构——**状态空间模型**。它巧妙地将RNN的**高效推理**和CNN的**高效训练**结合起来，并通过S4、Mamba等改进，在超长序列建模任务上取得了显著成果。

![](img/028f9f4bbddc87ababd7402d0c31c158_176.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_178.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_180.png)

![](img/028f9f4bbddc87ababd7402d0c31c158_182.png)

长上下文建模仍然是一个快速发展的领域，新的方法和技术不断涌现，为处理更复杂、更庞大的序列数据开辟了道路。