# 15：PyTorch中的Softmax回归与梯度下降 🧠

在本节课中，我们将学习如何使用PyTorch框架实现Softmax回归模型，并应用梯度下降算法进行训练。我们将从构建模型的基本模块开始，逐步深入到损失计算、梯度反向传播以及随机梯度下降等核心概念。

---

## 概述：从线性模型到Softmax分类器

上一节我们介绍了线性模型作为神经网络的基础构建块。本节中，我们将看看如何扩展线性模型，构建一个用于多类分类的Softmax回归模型。

Softmax函数将线性层的原始输出（logits）转换为概率分布。其公式为：
**`softmax(z_i) = exp(z_i) / Σ_j exp(z_j)`**
其中，`z_i` 是第i个类别的logit值。该函数确保所有输出概率之和为1，且具有平移不变性（即对logits加上一个常数不会改变输出概率）。

---

## 1. 构建模型：线性层与Softmax

在PyTorch中，线性层（`nn.Linear`）是实现仿射变换 `y = xW^T + b` 的模块。它接受输入维度和输出维度作为参数。

以下是如何定义一个简单的线性层：

```python
import torch.nn as nn
# 定义一个线性层，输入特征为2维，输出为3维
linear_layer = nn.Linear(in_features=2, out_features=3)
```

当我们向该层输入一个形状为 `(n_samples, in_features)` 的张量时，它会独立地对每一行（即每个样本）应用变换，输出形状为 `(n_samples, out_features)` 的张量。偏置项 `b` 会自动添加。

对于分类任务，输出维度通常等于类别数量。在线性层之后，我们应用Softmax函数来获得类别概率。

![](img/989bd8d0948b70d6edcbfe34c2790d7f_1.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_3.png)

---

## 2. 定义完整的Softmax模型

现在，我们将线性层和Softmax组合成一个完整的模型。在PyTorch中，我们通过继承 `nn.Module` 类并定义 `forward` 方法来实现。

以下是Softmax模型的定义：

```python
class SoftmaxModel(nn.Module):
    def __init__(self, input_dim, output_dim):
        super().__init__()
        self.linear = nn.Linear(input_dim, output_dim)

    def forward(self, x):
        # 线性变换得到logits
        logits = self.linear(x)
        # 沿最后一个维度（类别维度）应用Softmax
        probabilities = torch.softmax(logits, dim=-1)
        return probabilities
```

初始化模型时，其权重和偏置是随机设置的。这种随机初始化是必要的，它为优化提供了一个起点。

---

## 3. 生成与理解数据

为了训练模型，我们需要数据。我们将使用一个“真实”的Softmax模型生成合成数据。

1.  **创建真实模型**：实例化一个Softmax模型作为数据生成器，并固定其参数。
2.  **生成特征X**：从标准正态分布中随机采样得到输入特征 `X`。
3.  **生成标签y**：将 `X` 输入真实模型得到概率，然后根据这些概率分布对每个样本采样，得到类别标签 `y`。

这个过程模拟了现实世界中数据存在的噪声：即使模型给出了某个类别的概率最高，实际观察到的标签也可能不同。

---

## 4. 计算损失：负对数似然

我们的目标是让模型预测的概率分布与真实数据分布一致。常用的损失函数是**负对数似然损失**。

对于单个样本 `(x_i, y_i)`，损失是模型赋予真实类别 `y_i` 的概率的负对数：`L_i = -log(p_model(y_i | x_i))`。

对于整个数据集，损失是平均负对数似然：
**`L = - (1/N) * Σ_i log(p_model(y_i | x_i))`**

在代码中，我们可以通过索引操作高效地计算这个损失：
```python
# probs 是模型对所有样本预测的概率矩阵，形状为 (N, C)
# y 是真实标签向量，形状为 (N,)
loss = -torch.mean(torch.log(probs[torch.arange(N), y]))
```

---

## 5. 训练的核心：反向传播与梯度下降

理解了损失函数后，我们来看如何通过优化模型参数来最小化它。这依赖于两个关键步骤：**反向传播**和**梯度下降**。

![](img/989bd8d0948b70d6edcbfe34c2790d7f_5.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_6.png)

*   **反向传播（Backpropagation）**：这是一个利用链式法则，从损失函数开始，向后计算模型中每个参数梯度的高效算法。在PyTorch中，调用 `loss.backward()` 会自动完成此过程，并将梯度填充到每个参数的 `.grad` 属性中。
*   **梯度下降（Gradient Descent）**：在得到梯度后，我们沿着梯度的反方向更新参数，因为梯度方向是损失增长最快的方向。参数更新公式为：
    **`θ_new = θ_old - η * ∇L(θ_old)`**
    其中 `η` 是学习率，控制更新步长。

PyTorch的 `torch.optim` 模块提供了各种优化器（如SGD， Adam）来执行更新。一个基本的训练循环如下：

![](img/989bd8d0948b70d6edcbfe34c2790d7f_8.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_10.png)

```python
optimizer = torch.optim.SGD(model.parameters(), lr=0.1)
for epoch in range(num_epochs):
    # 前向传播，计算预测和损失
    probs = model(X)
    loss = -torch.mean(torch.log(probs[torch.arange(N), y]))

    # 反向传播，计算梯度
    optimizer.zero_grad() # 清除上一轮的梯度
    loss.backward()

    # 根据梯度更新参数
    optimizer.step()
```

![](img/989bd8d0948b70d6edcbfe34c2790d7f_12.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_14.png)

**注意**：在每次 `loss.backward()` 之前，必须调用 `optimizer.zero_grad()` 将参数的梯度清零，否则梯度会不断累积。

![](img/989bd8d0948b70d6edcbfe34c2790d7f_16.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_18.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_20.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_22.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_24.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_26.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_28.png)

---

![](img/989bd8d0948b70d6edcbfe34c2790d7f_30.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_32.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_33.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_35.png)

## 6. 随机梯度下降（SGD）与小批量训练

![](img/989bd8d0948b70d6edcbfe34c2790d7f_37.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_39.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_41.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_43.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_45.png)

当数据集很大时，每次迭代都计算所有样本的损失和梯度（批量梯度下降）会非常慢。**随机梯度下降** 是更实用的方法。

![](img/989bd8d0948b70d6edcbfe34c2790d7f_47.png)

其核心思想是：每次迭代只随机抽取一小部分样本（称为一个**小批量**或**批次**）来计算损失和梯度。虽然基于单个批次的梯度估计噪声更大，但它仍然是真实梯度的一个无偏估计，并且计算效率极高。

![](img/989bd8d0948b70d6edcbfe34c2790d7f_49.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_50.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_52.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_54.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_56.png)

以下是实现小批量SGD的关键代码：

![](img/989bd8d0948b70d6edcbfe34c2790d7f_58.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_60.png)

```python
batch_size = 64
for epoch in range(num_epochs):
    # 随机打乱数据索引
    indices = torch.randperm(N)
    for i in range(0, N, batch_size):
        # 获取一个小批量的索引
        batch_idx = indices[i:i+batch_size]
        X_batch, y_batch = X[batch_idx], y[batch_idx]

        # 在这个小批量上进行前向传播、反向传播和参数更新
        probs = model(X_batch)
        loss = -torch.mean(torch.log(probs[torch.arange(len(batch_idx)), y_batch]))

        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
```

与批量梯度下降相比，SGD的训练损失曲线会更波动，但通常能更快地达到一个不错的解，有时甚至有助于跳出局部最优。

---

## 7. 模型评估与决策边界

训练完成后，我们需要评估模型性能。对于分类任务，一个直观的指标是**准确率**，即模型预测类别（取概率最高的类别）与真实标签一致的样本比例。

![](img/989bd8d0948b70d6edcbfe34c2790d7f_62.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_64.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_66.png)

我们可以通过可视化**决策边界**来理解模型学到了什么。对于二维输入的多类Softmax回归，决策边界是多个线性边界的交汇区域。在噪声较低的情况下，训练后的模型决策边界应能较好地逼近真实模型生成数据时的边界。

![](img/989bd8d0948b70d6edcbfe34c2790d7f_68.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_70.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_72.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_74.png)

然而，评估时必须使用**独立的测试集**。如果只在训练集上评估，当样本量很小时，模型可能会“记住”数据（过拟合），从而得到虚假的高准确率。这强调了将数据分为训练集和测试集的重要性。

![](img/989bd8d0948b70d6edcbfe34c2790d7f_76.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_78.png)

---

## 总结与展望

本节课中我们一起学习了：
1.  使用 `nn.Linear` 和 `nn.Module` 在PyTorch中构建Softmax回归模型。
2.  理解并实现了负对数似然损失函数。
3.  掌握了训练神经网络的**核心循环**：前向传播、损失计算、反向传播（`loss.backward()`）和参数更新（`optimizer.step()`），并理解了梯度清零（`optimizer.zero_grad()`）的必要性。
4.  认识了**随机梯度下降**的原理与优势，并实现了小批量训练。
5.  了解了模型评估的基本方法和过拟合的风险。

![](img/989bd8d0948b70d6edcbfe34c2790d7f_80.png)

![](img/989bd8d0948b70d6edcbfe34c2790d7f_82.png)

Softmax回归是一个线性分类器。当数据本身不是线性可分时（例如，一个类别被另一个类别环形包围），它的性能会受限。下一节，我们将探讨解决此问题的两种主要思路：**特征映射**（将数据投影到更高维空间使其线性可分）和**神经网络**（通过堆叠非线性层来构建复杂的非线性决策边界）。神经网络正是这种思路的自然延伸，也是现代AI模型的基础。