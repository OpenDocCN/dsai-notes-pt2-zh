# 012：Transformer与大语言模型

![](img/283b2a14cc3ae4ea301d0fbb0afece88_1.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_2.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_4.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_6.png)

在本节课中，我们将要学习Transformer架构以及现代大语言模型的基础知识。我们将从自然语言处理任务的历史讲起，逐步拆解Transformer的各个核心组件，并探讨其多种变体设计。最后，我们将了解一些主流大语言模型的特点及其带来的挑战。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_7.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_8.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_10.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_12.png)

## Transformer基础

上一节我们介绍了课程概述，本节中我们来看看Transformer的基础架构。Transformer彻底改变了自然语言处理领域，它解决了循环神经网络和卷积神经网络在处理序列数据时的一些根本性限制。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_14.png)

### NLP任务回顾

在Transformer时代之前，人们主要使用循环神经网络和卷积神经网络来处理自然语言任务。这些任务大致可以分为两类：

*   **判别式任务**：给定一个句子，目标是得到一个分类结果。例如情感分析、文本分类、文本蕴含等。
*   **生成式任务**：给定一个句子，目标是生成新的词元。例如语言建模、机器翻译、文本摘要等。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_16.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_17.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_19.png)

循环神经网络通过一个固定大小的隐藏状态作为“工作记忆”，但难以维持长距离的依赖关系。虽然它在内存上很高效，但其序列依赖的特性限制了训练时的并行性。卷积神经网络则通过一维卷积操作，但其感受野有限，通常只能关注相邻的几个词元，需要通过堆叠多层来扩大感受野。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_20.png)

### 注意力机制

![](img/283b2a14cc3ae4ea301d0fbb0afece88_22.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_23.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_25.png)

Transformer的核心创新在于**自注意力机制**。它允许模型在处理某个词元时，直接关注到序列中所有其他词元的信息，而不仅仅是相邻的词元。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_26.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_28.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_29.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_30.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_32.png)

以下是自注意力机制的计算流程：

![](img/283b2a14cc3ae4ea301d0fbb0afece88_34.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_35.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_37.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_38.png)

1.  **线性变换**：对于输入序列（n个词元，每个词元是d维向量），我们通过三个不同的权重矩阵 **W_q**、**W_k**、**W_v** 将其分别投影为查询（Query）、键（Key）和值（Value）向量。
    ```
    Q = X * W_q
    K = X * W_k
    V = X * W_v
    ```
2.  **计算注意力分数**：通过计算查询向量和所有键向量的点积，得到一个n x n的矩阵，表示每个词元与其他所有词元的相关性。为了稳定梯度，通常会将点积结果除以键向量维度的平方根。
    ```
    Attention Scores = (Q * K^T) / sqrt(d_k)
    ```
3.  **应用Softmax**：对注意力分数矩阵的每一行应用Softmax函数，使得每一行的权重之和为1，得到注意力权重矩阵。
    ```
    Attention Weights = softmax(Attention Scores)
    ```
4.  **加权求和**：将注意力权重矩阵与值向量相乘，得到每个词元新的表示，它融合了序列中所有相关信息。
    ```
    Output = Attention Weights * V
    ```

这种机制的直观理解类似于检索系统：查询（Query）是搜索请求，键（Key）是内容的标题/描述，值（Value）是内容本身。模型根据查询与键的匹配程度（注意力权重），对值进行加权求和，从而得到输出。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_40.png)

### 多头注意力

![](img/283b2a14cc3ae4ea301d0fbb0afece88_42.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_44.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_46.png)

单一的注意力头可能只捕获一种类型的词元关系。为了增强模型的容量，Transformer引入了**多头注意力**。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_48.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_50.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_52.png)

以下是多头注意力的实现方式：

![](img/283b2a14cc3ae4ea301d0fbb0afece88_54.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_56.png)

*   将查询、键、值向量再次投影到多个（例如h个）更低维的子空间。
*   在每个子空间中独立执行自注意力计算。
*   将h个头计算出的结果拼接起来，最后通过一个线性投影层进行融合。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_58.png)

不同的注意力头可以学习关注句子中不同方面的关系，例如语法结构、指代关系或语义关联。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_60.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_62.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_63.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_64.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_66.png)

### 注意力掩码

![](img/283b2a14cc3ae4ea301d0fbb0afece88_68.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_70.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_72.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_74.png)

注意力掩码用于控制词元之间的可见性，主要有两种类型：

![](img/283b2a14cc3ae4ea301d0fbb0afece88_76.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_77.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_79.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_80.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_82.png)

*   **全局注意力（双向）**：每个词元都可以看到序列中的所有其他词元（包括其后的词元）。这通常用于编码器或类似BERT的模型。
*   **因果注意力（单向）**：每个词元只能看到它自身以及它之前的词元，不能看到未来的词元。这用于自回归生成任务，如GPT系列模型。

### 前馈网络

![](img/283b2a14cc3ae4ea301d0fbb0afece88_84.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_86.png)

自注意力机制专注于建模词元之间的关系。为了对每个词元的特征进行独立、复杂的变换，Transformer在每个注意力层之后添加了一个**前馈网络**。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_88.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_90.png)

一个典型的前馈网络由两个线性变换和一个激活函数组成，形成一个“瓶颈”结构：
```
FFN(x) = ReLU(x * W1 + b1) * W2 + b2
```
其中，第一个线性层将维度从d投影到更大的维度（如4d），第二个线性层再投影回d维。这种设计为模型提供了强大的非线性变换能力。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_92.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_94.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_96.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_98.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_100.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_102.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_103.png)

### 层归一化与残差连接

![](img/283b2a14cc3ae4ea301d0fbb0afece88_105.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_107.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_108.png)

为了稳定深度网络的训练，Transformer广泛使用了**层归一化**和**残差连接**。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_110.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_111.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_112.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_113.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_114.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_115.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_117.png)

*   **层归一化**：对每个样本的所有特征维度进行归一化，减去均值，除以方差，然后应用可学习的缩放因子γ和偏移量β。
    ```
    LayerNorm(x) = γ * (x - mean(x)) / sqrt(var(x) + ε) + β
    ```
*   **残差连接**：将子层（如注意力层或前馈层）的输入直接加到其输出上。这有助于缓解梯度消失问题，使模型能够训练得更深。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_119.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_121.png)

层归一化的放置位置有两种主流方式：**前置归一化**（先归一化再进入子层）和**后置归一化**（先经过子层再归一化）。前置归一化因其更好的训练稳定性而越来越流行。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_123.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_125.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_126.png)

### 位置编码

自注意力机制本身是置换不变的，它不考虑词元的顺序。为了将序列的顺序信息注入模型，我们需要**位置编码**。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_128.png)

*   **绝对位置编码**：为每个位置分配一个独特的向量，然后将其加到词嵌入向量中。原始Transformer使用正弦和余弦函数来生成这些编码。
*   **相对位置编码**：不关注词元的绝对位置，而是关注词元之间的相对距离。通常通过修改注意力分数计算来实现（例如，添加一个与相对距离相关的偏置项）。这种方法对于处理长文本更具优势。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_130.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_132.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_134.png)

### 完整架构

![](img/283b2a14cc3ae4ea301d0fbb0afece88_136.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_138.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_139.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_141.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_143.png)

现在，我们可以将所有这些组件组合起来，形成一个完整的Transformer块（以解码器为例）：

![](img/283b2a14cc3ae4ea301d0fbb0afece88_145.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_147.png)

1.  输入词元序列。
2.  词嵌入层将词元转换为向量。
3.  加上位置编码。
4.  进入多个堆叠的Transformer层，每层包含：
    *   多头自注意力子层（带残差连接和层归一化）。
    *   前馈网络子层（带残差连接和层归一化）。
5.  最后一个Transformer层的输出经过一个线性层和Softmax，预测下一个词元的概率分布。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_149.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_150.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_151.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_153.png)

## Transformer变体

![](img/283b2a14cc3ae4ea301d0fbb0afece88_155.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_156.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_157.png)

上一节我们介绍了标准的Transformer架构，本节中我们来看看一些重要的变体设计，它们旨在提升模型效率、处理长文本或改善性能。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_159.png)

### 编码器-解码器架构

![](img/283b2a14cc3ae4ea301d0fbb0afece88_161.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_163.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_165.png)

原始的Transformer是一个编码器-解码器架构，适用于机器翻译等序列到序列任务。编码器处理输入序列，解码器基于编码器的输出和已生成的部分结果，自回归地生成目标序列。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_167.png)

### 仅编码器架构

![](img/283b2a14cc3ae4ea301d0fbb0afece88_169.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_170.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_172.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_173.png)

以BERT为代表，仅使用编码器堆叠。它通过“掩码语言建模”等预训练任务学习双向上下文表示，然后可以针对各种下游任务（如分类、问答）进行微调。其注意力是全局的。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_175.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_177.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_179.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_181.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_182.png)

### 仅解码器架构

![](img/283b2a14cc3ae4ea301d0fbb0afece88_184.png)

以GPT为代表，是目前大语言模型的主流架构。它通过“下一个词元预测”进行预训练，擅长文本生成。其注意力是因果的（只能看到过去的信息）。这种架构在零样本和少样本学习上展现出强大能力。

### 相对位置编码：RoPE

旋转位置编码是一种广泛使用的相对位置编码方法。它的核心思想是将词嵌入向量视为复数，根据词元的位置对其进行旋转。

具体来说，对于嵌入向量的每一对元素 `(x_m, x_{m+1})`，将其视为一个二维向量，然后根据该词元的位置 `pos` 进行旋转：
```
[ x'_m, x'_{m+1} ] = [ x_m, x_{m+1} ] * [ cos(pos * θ_m), -sin(pos * θ_m);
                                          sin(pos * θ_m),  cos(pos * θ_m) ]
```
其中 `θ_m` 是一个与维度相关的频率。这样，两个词元之间的点积就只依赖于它们的相对位置 `(pos_i - pos_j)`。RoPE对于外推（处理比训练时更长的序列）非常有效。

### KV缓存与高效注意力

![](img/283b2a14cc3ae4ea301d0fbb0afece88_186.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_187.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_188.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_189.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_190.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_192.png)

在自回归生成过程中，为了计算当前新词元的输出，需要之前所有词元的键和值向量。如果每次都重新计算，效率极低。因此，推理时会使用**KV缓存**来存储之前所有时间步的键和值。

然而，随着生成序列变长，KV缓存的大小会线性增长，成为内存消耗的主要瓶颈。对于一个批次大小为B、序列长度为L、层数为N、注意力头数为h、每个头维度为d_k的模型，KV缓存的总大小约为：
```
KV Cache Size = B * L * N * h * d_k * 2 * bytes_per_element
```
这很容易超过模型参数本身所占用的内存。

为了减少KV缓存的开销，出现了几种高效的注意力变体：

*   **多头注意力**：每个注意力头都有自己独立的K和V投影。容量最大，但KV缓存也最大。
*   **多查询注意力**：所有注意力头共享同一套K和V投影。极大地减少了KV缓存，但可能损失模型容量。
*   **分组查询注意力**：折中方案。将注意力头分成若干组，组内共享K和V投影。在显著减少KV缓存的同时，能较好地保持模型性能。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_194.png)

### 前馈网络变体：GLU

![](img/283b2a14cc3ae4ea301d0fbb0afece88_196.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_197.png)

门控线性单元是前馈网络的一种高效变体，被用于LLaMA等现代模型。与标准FFN相比，GLU通常使用三个线性变换和一个门控机制（如Swish激活函数）：
```
GLU(x) = (Swish(x * W1) ⊙ (x * W2)) * W3
```
其中 `⊙` 表示逐元素相乘。这种设计被证明能带来更好的性能。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_199.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_201.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_203.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_205.png)

## 大语言模型简介

![](img/283b2a14cc3ae4ea301d0fbb0afece88_207.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_209.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_211.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_213.png)

上一节我们探讨了Transformer的各种优化变体，本节中我们来看看这些技术如何催生出强大的现代大语言模型，并了解它们的一些关键特性。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_215.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_216.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_217.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_219.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_221.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_223.png)

### 涌现能力与缩放定律

![](img/283b2a14cc3ae4ea301d0fbb0afece88_225.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_226.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_228.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_229.png)

当语言模型的规模（参数数量、训练数据量、计算量）超过某个阈值时，会表现出一些在较小模型中没有的、意想不到的能力，这被称为**涌现能力**。例如，执行复杂推理、理解指令、进行少样本学习等。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_231.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_233.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_235.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_237.png)

**缩放定律**描述了模型性能与规模之间的经验关系。例如，Chinchilla定律指出，在给定计算预算下，最优的模型性能需要参数数量和训练数据量之间取得平衡，而不是一味增大模型。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_239.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_241.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_243.png)

### 指令微调与对齐

![](img/283b2a14cc3ae4ea301d0fbb0afece88_245.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_246.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_248.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_249.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_251.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_253.png)

仅通过下一个词元预测预训练的模型，可能不会按照人类期望的方式回答问题。为了使模型有用、无害、诚实，需要进行**指令微调**和**对齐**。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_255.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_257.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_259.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_261.png)

*   **监督微调**：使用人类编写的指令-回答对来微调模型，教会它遵循指令。
*   **基于人类反馈的强化学习**：让模型生成多个答案，人类对这些答案进行偏好排序。然后训练一个奖励模型来预测人类偏好，最后使用强化学习算法（如PPO）来优化语言模型，使其输出更符合人类偏好的内容。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_263.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_264.png)

### 主流开源模型

以下是几个具有代表性的开源大语言模型系列：

![](img/283b2a14cc3ae4ea301d0fbb0afece88_266.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_268.png)

*   **LLaMA系列**：Meta发布的开源模型。采用了前置层归一化、SwiGLU激活函数、RoPE位置编码等技术。LLaMA 2引入了分组查询注意力以减少KV缓存，并进行了指令微调。LLaMA 3进一步扩大了训练数据和模型规模。
*   **Mistral系列**：以其小巧的7B参数模型和出色的性能而闻名。它采用了滑动窗口注意力，即每个词元只关注其前面一定窗口大小内的词元，这能线性降低长序列的计算复杂度，再结合分层注意力，可以有效处理长上下文。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_270.png)

### 长上下文处理

![](img/283b2a14cc3ae4ea301d0fbb0afece88_272.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_273.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_275.png)

处理长文档、书籍或多轮对话需要模型具备长上下文能力。除了使用RoPE等支持外推的位置编码外，还需要在注意力机制上进行优化，如：
*   **KV缓存压缩**：通过量化、剪枝或选择性存储来减少KV缓存的内存占用。
*   **流式注意力**：如Mistral的滑动窗口注意力，限制每个位置可见的上下文范围。
*   **层次化注意力**：在多个层次上聚合信息，在高层关注更广的上下文。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_277.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_278.png)

## 总结

![](img/283b2a14cc3ae4ea301d0fbb0afece88_280.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_282.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_283.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_285.png)

本节课中我们一起学习了Transformer架构与大语言模型的核心知识。

我们首先回顾了Transformer出现之前的NLP方法及其局限，然后深入剖析了Transformer的各个组件：自注意力机制、多头注意力、前馈网络、层归一化、残差连接和位置编码。接着，我们探讨了多种Transformer变体，包括不同的架构（编码器、解码器）、更高效的位置编码（如RoPE）、以及为了降低KV缓存开销而设计的注意力机制（如分组查询注意力）。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_287.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_288.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_290.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_291.png)

最后，我们介绍了现代大语言模型的特性，如涌现能力、缩放定律，以及指令微调和对齐的重要性，并简要概述了LLaMA和Mistral等主流开源模型的特点。

![](img/283b2a14cc3ae4ea301d0fbb0afece88_293.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_295.png)

![](img/283b2a14cc3ae4ea301d0fbb0afece88_297.png)

理解这些基础知识，是后续我们探讨如何高效地部署、压缩和加速这些大模型的前提。在下一讲中，我们将重点关注大语言模型推理的优化技术。