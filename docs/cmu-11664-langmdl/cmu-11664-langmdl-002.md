# 2：概率基础回顾与代码示例 📊

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_1.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_3.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_5.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_6.png)

在本节课中，我们将学习语言建模中至关重要的概率基础概念，并通过代码示例来演示这些概念的实际应用。我们将从条件概率开始，逐步介绍采样、边缘化、隐变量等核心思想，并使用一个简单的二元语法模型和一个小型Transformer模型进行实践。

## 概率基础回顾 🔍

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_8.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_9.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_11.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_12.png)

上一节我们介绍了课程的整体安排。本节中，我们来看看语言建模的核心——概率论基础。理解这些概念对于后续学习各种推断算法至关重要。

### 条件概率与自回归语言模型

我们主要处理的是自回归语言模型。自回归语言模型基于条件概率来预测下一个词元。其核心公式是：

**P(y | x)**

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_14.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_16.png)

其中，`x` 代表所有先前的词元，`y` 代表下一个要预测的词元。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_18.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_20.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_22.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_24.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_26.png)

为了演示，我们使用一个简单的二元语法模型。该模型仅根据前一个词来预测下一个词，这体现了马尔可夫假设——即只关注有限数量的先前词。

以下是该模型的词汇表和条件概率表示例：

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_28.png)

```python
# 示例：一个简单的二元语法模型条件概率表
vocab = ['<s>', 'the', 'cat', 'dog', 'park', 'mat', 'sat', 'ran', 'walked', 'played', 'on', 'in', 'too', 'quickly', 'slowly', '</s>']
# 条件概率 P(next_token | current_token) 存储在一个矩阵中
```

### 从语言模型中采样

从语言模型中采样是最简单的推断算法。其基本流程是：从起始词元开始，根据条件概率分布采样下一个词，更新当前上下文，然后重复此过程，直到遇到结束词元或达到最大长度。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_30.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_32.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_34.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_36.png)

温度采样是一种常用的采样技术，它可以调整概率分布的“尖锐”程度。其公式如下：

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_38.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_39.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_41.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_42.png)

**P_i' = exp(log(P_i) / T) / Σ_j exp(log(P_j) / T)**

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_44.png)

其中，`T` 是温度参数。
*   当 `T = 1` 时，分布不变。
*   当 `T → ∞` 时，分布趋近于均匀分布。
*   当 `T → 0` 时，分布趋近于一个独热向量，即总是选择概率最高的词元（贪婪解码）。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_46.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_48.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_50.png)

以下是采样的核心代码逻辑：

```python
def sample_from_model(initial_token, max_len, temperature=1.0):
    sequence = [initial_token]
    current_token = initial_token
    for _ in range(max_len):
        # 获取当前词元下的下一个词元条件概率
        probs = get_conditional_probs(current_token)
        # 应用温度调整
        adjusted_logits = torch.log(probs) / temperature
        adjusted_probs = torch.softmax(adjusted_logits, dim=-1)
        # 根据调整后的概率采样下一个词元
        next_token = torch.multinomial(adjusted_probs, 1).item()
        sequence.append(next_token)
        if next_token == end_of_sequence_token:
            break
        current_token = next_token
    return sequence
```

### 通过采样进行估计

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_52.png)

对于复杂的模型（如Transformer），我们通常无法解析地计算某些量（如联合概率 `P(x, y)`）。此时，我们可以通过采样来估计这些量。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_54.png)

基本思想是：从模型中生成大量样本，然后基于这些样本计算我们感兴趣的统计量（例如，两个词共同出现的频率）。随着采样数量的增加，估计值会越来越接近真实值。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_56.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_57.png)

以下是通过采样估计联合概率的示例：

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_59.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_61.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_62.png)

```python
def estimate_joint_prob_from_samples(num_samples):
    bigram_counts = defaultdict(int)
    total_bigrams = 0
    for _ in range(num_samples):
        seq = sample_from_model(start_token, max_len=20, temperature=1.0)
        for i in range(len(seq)-1):
            bigram = (seq[i], seq[i+1])
            bigram_counts[bigram] += 1
            total_bigrams += 1
    # 估计联合概率 P(a, b) ≈ count(a, b) / total_bigrams
    joint_probs = {k: v/total_bigrams for k, v in bigram_counts.items()}
    return joint_probs
```

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_64.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_65.png)

**重要提示**：只有使用温度 `T=1` 进行采样，才能获得模型真实的概率分布的无偏估计。使用其他温度值会导致有偏估计。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_67.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_69.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_71.png)

### 边缘化与隐变量

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_73.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_74.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_76.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_77.png)

边缘化是指对联合概率中的某些变量求和，以得到其他变量的边际概率。例如，从联合概率 `P(x, y)` 通过对 `y` 求和得到 `P(x)`。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_78.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_80.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_82.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_84.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_86.png)

在语言模型中，一个重要的概念是**隐变量**。隐变量是影响最终输出但不直接可见的隐藏结构。当前语言模型中的一个典型例子是**思维链**。在思维链模型中：
*   `x` 是输入提示。
*   `z` 是推理过程（隐变量）。
*   `y` 是最终答案。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_88.png)

我们关心的是 `P(y | x)`，但模型生成的是 `P(z, y | x)`。通过对所有可能的推理路径 `z` 进行求和（边缘化），我们可以得到更好的 `P(y | x)` 估计：

**P(y | x) ≈ Σ_z P(z, y | x)**

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_90.png)

这种方法催生了如“自洽性”等推断算法。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_92.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_94.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_96.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_97.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_98.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_100.png)

## 代码实践：Transformer模型与生成 🚀

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_102.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_104.png)

上一节我们回顾了核心的概率概念。本节中，我们将把这些概念应用于一个真实的Transformer模型（GPT-2 small），并观察不同采样策略的效果。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_106.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_107.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_108.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_110.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_111.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_112.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_114.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_115.png)

### 模型初始化与不同温度下的生成

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_117.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_119.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_120.png)

我们使用Hugging Face的 `transformers` 库加载一个小型GPT-2模型，并比较在温度 `T=0`（贪婪）、`T=0.5`、`T=1.0` 和 `T=1.5` 下生成的文本。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_122.png)

提示词为：“The future of artificial intelligence is”。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_124.png)

```python
from transformers import GPT2LMHeadModel, GPT2Tokenizer
model = GPT2LMHeadModel.from_pretrained('gpt2')
tokenizer = GPT2Tokenizer.from_pretrained('gpt2')

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_126.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_127.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_129.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_130.png)

prompt = "The future of artificial intelligence is"
input_ids = tokenizer.encode(prompt, return_tensors='pt')

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_132.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_133.png)

# 贪婪解码 (T=0)
greedy_output = model.generate(input_ids, max_length=50, do_sample=False)
# 温度采样 (T=0.5)
temp_output = model.generate(input_ids, max_length=50, do_sample=True, temperature=0.5)
```

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_135.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_136.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_138.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_140.png)

### 评估生成结果

定性评估生成文本后，我们需要更系统的方法。这里介绍两种：

1.  **确定性指标**：例如计算生成文本的**多样性**。
    *   **内部多样性**：单次生成中唯一词的比例。
    *   **交叉多样性**：多次生成之间词或n-gram的重叠度。

2.  **语言模型即评委**：使用一个更强大的语言模型（如Claude）来评估生成文本的质量，例如要求它对文本的“流畅性与连贯性”进行1-10分的打分。

以下是使用语言模型作为评委的示例提示：

```
“Rate the fluency and coherence of this text on a scale of 0 to 10. 10 equals perfect. Only respond with a number.
Text: {generated_text}”
```

**注意**：语言模型评委并非完美，它们可能不擅长评估自己不擅长的领域，并且可能对自己的生成结果存在偏好。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_142.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_143.png)

### 元生成算法：重排序

元生成算法是指利用生成过程本身或外部信息来改进最终输出的算法。最简单的一种是**重排序**。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_145.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_146.png)

其思想是：用一个较小的、高效的模型（如GPT-2 small）生成多个候选输出，然后用一个更大、更强的模型（如GPT-2 medium）计算每个候选输出的概率（或困惑度），最后选择大模型认为最好的那个输出。

以下是重排序的核心步骤：

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_148.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_149.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_151.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_153.png)

```python
# 1. 用小模型生成N个候选序列
candidates = []
for _ in range(num_candidates):
    output_ids = small_model.generate(input_ids, max_length=50, do_sample=True, temperature=0.8)
    candidates.append(output_ids)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_155.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_157.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_159.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_161.png)

# 2. 用大模型计算每个候选序列的（平均）对数概率
scores = []
for cand in candidates:
    with torch.no_grad():
        outputs = large_model(cand, labels=cand)
        log_likelihood = outputs.loss * -1 * cand.size(1) # 转换为总对数似然
        avg_log_prob = log_likelihood / cand.size(1) # 计算每个词元的平均对数概率，用于公平比较不同长度的序列
        scores.append(avg_log_prob.item())

# 3. 选择分数最高的候选
best_idx = scores.index(max(scores))
best_candidate = candidates[best_idx]
best_text = tokenizer.decode(best_candidate[0], skip_special_tokens=True)
```

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_163.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_165.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_167.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_169.png)

这种方法可以视为一种简单的“推测解码”或“蒸馏”形式，它允许我们在不直接使用大模型进行昂贵生成的情况下，利用其更强的判断力。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_171.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_173.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_175.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_176.png)

## 总结 📝

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_178.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_180.png)

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_182.png)

本节课中我们一起学习了语言建模推断算法的概率基础与初步实践。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_184.png)

我们首先回顾了**条件概率**，这是自回归语言模型的基石。接着，我们探讨了**采样**这一基本推断方法，并引入了**温度**参数来控制生成的多样性与质量。我们了解到，通过采样可以**估计**难以解析计算的量（如联合概率），但只有温度 `T=1` 能提供无偏估计。

然后，我们介绍了**边缘化**和**隐变量**的概念，并以思维链为例，说明了如何通过边缘化隐变量来提升最终输出的概率估计。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_186.png)

在实践部分，我们使用GPT-2模型演示了不同温度下的文本生成，并介绍了两种评估方法：基于统计的**确定性指标**和基于大模型的**语言模型即评委**。最后，我们探讨了最简单的元生成算法——**重排序**，即用小模型生成、大模型挑选，从而结合了效率与质量。

![](img/9d0c55d03e0484cd6b7591cbd3a8f955_188.png)

这些基础概念和简单算法为我们后续深入学习更复杂、更高效的推断算法（如集束搜索、Top-k/p采样、推测解码等）奠定了坚实的基础。