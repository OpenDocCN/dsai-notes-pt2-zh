# 99：Python中的递归神经网络 (RNN) 🧠

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_1.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_3.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_5.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_7.png)

在本节课中，我们将学习如何从零开始构建一个简单的递归神经网络 (RNN)。我们将使用字符级语言建模作为示例任务，通过“时间机器”数据集来训练一个能够生成文本的RNN模型。我们将涵盖数据预处理、模型定义、前向传播、训练循环以及文本生成等核心步骤。

---

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_9.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_11.png)

## 数据加载与预处理 📊

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_13.png)

首先，我们需要加载数据集并进行预处理。我们使用“时间机器”数据集，并按字符级别进行划分。

以下是加载数据集和导入必要库的代码：

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_15.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_17.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_18.png)

```python
import torch
import torch.nn.functional as F
from torch import nn, optim
# 假设 load_data_time_machine 是一个加载数据集的函数
from utils import load_data_time_machine
```

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_20.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_21.png)

接下来，我们使用独热编码 (One-Hot Encoding) 来处理字符。对于字符数量有限且独特的语言（如中文），这种编码方式非常有效。在本例中，词汇表大小约为43。

```python
def one_hot(x, vocab_size):
    # 将整数索引转换为独热编码向量
    return F.one_hot(x, vocab_size).float()
```

假设我们有一个包含三个字符的数组 `[2, 2, 30]`，经过独热编码后，每个字符会变成一个长度为43的向量，其中对应索引位置为1，其余为0。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_23.png)

为了处理整个小批量数据，我们定义一个映射函数，将小批量中的所有输入转换为独热编码格式。

```python
def to_one_hot_batch(batch, vocab_size):
    # batch 形状: (batch_size, seq_length)
    # 返回形状: (batch_size, seq_length, vocab_size)
    return one_hot(batch, vocab_size)
```

例如，如果小批量形状为 `(2, 5)`，那么编码后的数据形状将是 `(2, 5, 43)`。

---

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_25.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_27.png)

## 模型参数初始化 ⚙️

上一节我们介绍了数据预处理，本节中我们来看看如何初始化RNN模型的参数。

首先，我们设置一些基本参数：
*   **输入数量**：等于词汇表大小，因为我们使用独热编码。
*   **隐藏单元数量**：例如512。
*   **输出数量**：同样等于词汇表大小，因为我们要预测下一个字符。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_29.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_31.png)

我们还需要检查是否有可用的GPU。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_33.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_35.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_37.png)

```python
vocab_size = 43
num_hiddens = 512
num_outputs = vocab_size
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
```

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_39.png)

接下来，我们定义模型参数。一个简单的RNN单元包含以下参数：
*   `W_xh`: 输入到隐藏层的权重。
*   `W_hh`: 隐藏层到隐藏层的权重。
*   `b_h`: 隐藏层的偏置。
*   `W_hq`: 隐藏层到输出层的权重。
*   `b_q`: 输出层的偏置。

我们使用正态分布初始化权重，偏置初始化为零，并为所有参数附加梯度。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_41.png)

```python
def get_params(vocab_size, num_hiddens, device):
    num_inputs = vocab_size
    # 初始化权重
    def normal(shape):
        return torch.randn(size=shape, device=device) * 0.01
    # 隐藏层参数
    W_xh = normal((num_inputs, num_hiddens))
    W_hh = normal((num_hiddens, num_hiddens))
    b_h = torch.zeros(num_hiddens, device=device)
    # 输出层参数
    W_hq = normal((num_hiddens, num_outputs))
    b_q = torch.zeros(num_outputs, device=device)
    # 附加梯度
    params = [W_xh, W_hh, b_h, W_hq, b_q]
    for param in params:
        param.requires_grad_(True)
    return params
```

---

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_43.png)

## 定义RNN模型 🧱

现在我们已经初始化了参数，接下来定义RNN模型本身。这包括初始化隐藏状态和定义RNN单元的前向传播逻辑。

首先，我们定义一个函数来初始化隐藏状态。这里我们简单地将初始隐藏状态设置为全零。返回一个列表是为了保持接口的一致性，以便将来处理具有多个隐藏状态的模型（如LSTM）。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_45.png)

```python
def init_rnn_state(batch_size, num_hiddens, device):
    # 返回一个包含初始隐藏状态的列表
    return (torch.zeros((batch_size, num_hiddens), device=device), )
```

接下来是核心部分：定义RNN单元。该函数接受当前输入、隐藏状态和参数，计算新的隐藏状态和输出。

以下是RNN单元的前向传播公式：
*   新隐藏状态: **`H_t = tanh(X_t @ W_xh + H_{t-1} @ W_hh + b_h)`**
*   输出: **`O_t = H_t @ W_hq + b_q`**

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_47.png)

```python
def rnn(inputs, state, params):
    # inputs 形状: (seq_len, batch_size, vocab_size)
    # state 是一个包含隐藏状态的元组
    W_xh, W_hh, b_h, W_hq, b_q = params
    H, = state
    outputs = []
    for X in inputs:
        # 计算新的隐藏状态
        H = torch.tanh(torch.mm(X, W_xh) + torch.mm(H, W_hh) + b_h)
        # 计算输出
        Y = torch.mm(H, W_hq) + b_q
        outputs.append(Y)
    # 返回新的隐藏状态和所有时间步的输出
    return (H, ), torch.stack(outputs)
```

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_49.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_51.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_53.png)

这个函数遍历输入序列的每个时间步，依次更新隐藏状态并生成输出。最后返回最终的隐藏状态和整个输出序列。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_55.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_57.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_59.png)

---

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_61.png)

## 文本生成预测 🔮

定义好RNN的前向传播后，我们需要一个函数来使用训练好的模型生成文本。这个预测函数接受一个字符串前缀，并生成指定数量的后续字符。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_63.png)

以下是预测函数的步骤概述：
1.  初始化隐藏状态。
2.  将前缀中的字符依次输入RNN，更新状态（但不输出生成的字符，只是为了让模型获得上下文）。
3.  开始生成新字符：将当前预测的字符作为下一步的输入，重复此过程。

```python
def predict_rnn(prefix, num_chars, rnn, params, init_rnn_state,
                num_hiddens, vocab_size, device, idx_to_char, char_to_idx):
    state = init_rnn_state(1, num_hiddens, device) # 批量大小为1用于生成
    output = [char_to_idx[prefix[0]]]
    # 用前缀更新隐藏状态
    for t in range(len(prefix) + num_chars - 1):
        X = to_one_hot_batch(torch.tensor([[output[-1]]], device=device), vocab_size)
        X = X.permute(1, 0, 2) # 调整形状以适应rnn函数
        (state, ), Y = rnn(X, state, params)
        if t < len(prefix) - 1:
            # 仍在前缀中，读取下一个字符
            output.append(char_to_idx[prefix[t + 1]])
        else:
            # 开始生成，选择概率最高的字符
            output.append(int(Y.argmax(dim=2).reshape(1)))
    return ''.join([idx_to_char[i] for i in output])
```

在模型参数未经训练时，这个函数会生成看似随机的字符序列。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_65.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_67.png)

---

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_68.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_70.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_72.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_73.png)

## 梯度裁剪与训练循环 🏋️

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_75.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_77.png)

为了稳定训练过程，我们需要实现梯度裁剪。当梯度向量的范数过大时，梯度裁剪可以防止优化步骤过大，导致模型发散。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_79.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_80.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_82.png)

梯度裁剪的公式如下：如果梯度 `g` 的L2范数超过阈值 `θ`，则将其缩放为 **`g * θ / ||g||`**。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_83.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_85.png)

```python
def grad_clipping(params, theta):
    norm = torch.sqrt(sum(torch.sum((p.grad ** 2)) for p in params if p.grad is not None))
    if norm > theta:
        for param in params:
            if param.grad is not None:
                param.grad[:] *= theta / norm
```

现在，我们可以构建完整的训练循环。训练RNN与训练其他神经网络类似，但我们需要按顺序处理序列数据，并妥善管理隐藏状态在不同批次间的传递（对于顺序采样）。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_87.png)

以下是训练循环的关键步骤：
1.  **迭代周期**：遍历数据集多次。
2.  **状态初始化**：如果是随机采样，每个小批量开始时重置隐藏状态；如果是顺序采样，则在整个周期内保持状态的连续性（但需在反向传播时断开梯度连接）。
3.  **前向与反向传播**：
    *   对小批量数据进行独热编码。
    *   运行RNN，得到输出和最终状态。
    *   计算损失（通常使用交叉熵损失，用于预测下一个字符）。
    *   执行反向传播。
    *   应用梯度裁剪。
    *   使用优化器（如SGD）更新参数。
4.  **评估**：定期计算困惑度（Perplexity），它是衡量语言模型好坏的标准指标，是交叉熵损失的指数。

```python
def train_epoch_ch8(rnn, train_iter, loss, updater, device, use_random_iter):
    state, timer = None, d2l.Timer()
    metric = d2l.Accumulator(2)  # 训练损失之和, 词元数量
    for X, Y in train_iter:
        if state is None or use_random_iter:
            # 第一次迭代或使用随机采样时，初始化state
            state = init_rnn_state(X.shape[0], num_hiddens, device)
        else:
            # 顺序采样时，从计算图分离状态，避免梯度跨批次传播
            if isinstance(state, tuple):
                state = (s.detach() for s in state)
            else:
                state.detach_()
        # 前向传播、损失计算、反向传播、梯度裁剪、参数更新...
        # ... (具体代码较长，此处省略细节)
    return math.exp(metric[0] / metric[1]), metric[1] / timer.stop() # 返回困惑度和速度
```

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_89.png)

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_91.png)

在训练过程中，我们可以观察到困惑度逐渐下降，生成的文本从毫无意义变得逐渐连贯。顺序采样通常比随机采样表现更好，因为它能让模型在更长的序列上下文中进行学习。

---

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_93.png)

## 总结 📝

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_95.png)

本节课中我们一起学习了如何从零开始实现一个简单的递归神经网络 (RNN)。

我们首先学习了如何为字符级语言建模任务准备数据，特别是使用独热编码。接着，我们详细讲解了RNN模型参数的初始化方法。然后，我们定义了RNN的核心前向传播逻辑，包括隐藏状态的更新和输出的计算。在此基础上，我们构建了一个文本生成函数，用于模型预测。

为了确保训练稳定性，我们引入了梯度裁剪技术。最后，我们构建了一个完整的训练循环，它能够处理序列数据、管理隐藏状态、计算损失并优化模型参数。

![](img/467b7ed10f3bdd3b04e7ec5f22cca723_97.png)

通过本课程，你应该对RNN的基本工作原理和实现细节有了扎实的理解，这是学习更复杂序列模型（如LSTM和GRU）的重要基础。