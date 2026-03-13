# 16：从零实现线性回归 📈

![](img/983f2321ce8f8066e54210877ee3984e_1.png)

在本节课中，我们将学习如何从零开始实现线性回归模型。我们将涵盖数据生成、模型定义、损失计算、参数初始化以及使用随机梯度下降（SGD）进行训练的全过程。最后，我们还会介绍如何使用深度学习框架（如Gluon）来简化实现。

![](img/983f2321ce8f8066e54210877ee3984e_3.png)

---

## 概述

线性回归是机器学习中最基础的模型之一。本节课的目标是手动实现一个线性回归模型，以深入理解其核心原理。我们将生成一个合成数据集，定义模型和损失函数，并使用SGD算法优化模型参数。

![](img/983f2321ce8f8066e54210877ee3984e_5.png)

---

![](img/983f2321ce8f8066e54210877ee3984e_7.png)

## 数据生成

![](img/983f2321ce8f8066e54210877ee3984e_9.png)

首先，我们需要创建一个用于训练的数据集。我们生成一个包含1000个样本的二维特征矩阵 `X`，并为其指定真实的权重 `w` 和偏置 `b`，最后加入一些高斯噪声来模拟现实数据中的不确定性。

![](img/983f2321ce8f8066e54210877ee3984e_11.png)

以下是生成数据集的代码：

![](img/983f2321ce8f8066e54210877ee3984e_13.png)

```python
import numpy as np

![](img/983f2321ce8f8066e54210877ee3984e_14.png)

# 生成特征矩阵 X (1000个样本，2个特征)
num_samples = 1000
num_features = 2
X = np.random.normal(0, 1, (num_samples, num_features))

# 定义真实的权重 w 和偏置 b
true_w = np.array([2, -3.4])
true_b = 4.2

# 生成标签 y = X * w + b + 噪声
noise = np.random.normal(0, 0.01, num_samples)
y = np.dot(X, true_w) + true_b + noise
```

![](img/983f2321ce8f8066e54210877ee3984e_16.png)

生成数据后，我们可以可视化其中一个特征与标签之间的关系，以观察其线性趋势及噪声的影响。

---

## 数据读取与批处理

![](img/983f2321ce8f8066e54210877ee3984e_18.png)

![](img/983f2321ce8f8066e54210877ee3984e_20.png)

为了使用小批量随机梯度下降，我们需要一个能够按批次读取数据的迭代器。这可以提高训练效率并利用计算资源的并行性。

![](img/983f2321ce8f8066e54210877ee3984e_22.png)

以下是如何实现一个简单的数据迭代器：

```python
def data_iter(batch_size, features, labels):
    num_samples = len(features)
    indices = list(range(num_samples))
    np.random.shuffle(indices)  # 随机打乱索引
    for i in range(0, num_samples, batch_size):
        batch_indices = np.array(indices[i: min(i + batch_size, num_samples)])
        yield features[batch_indices], labels[batch_indices]  # 返回一个批次的特征和标签
```

使用这个迭代器，我们可以方便地在训练循环中获取数据批次。

![](img/983f2321ce8f8066e54210877ee3984e_24.png)

---

![](img/983f2321ce8f8066e54210877ee3984e_26.png)

## 模型参数初始化

在开始训练之前，我们需要初始化模型参数（权重 `w` 和偏置 `b`）。合适的初始化对训练收敛至关重要。

我们使用均值为0、标准差为0.01的正态分布来随机初始化权重，并将偏置初始化为0。

```python
# 初始化权重 w
w = np.random.normal(0, 0.01, (num_features, 1))
# 初始化偏置 b
b = np.zeros(1)

# 为参数附加梯度，以便后续自动求导
w.requires_grad = True
b.requires_grad = True
```

---

![](img/983f2321ce8f8066e54210877ee3984e_28.png)

## 定义模型

![](img/983f2321ce8f8066e54210877ee3984e_30.png)

线性回归模型的核心是线性变换：`y_hat = X * w + b`。我们将这个计算过程封装成一个函数。

```python
def linreg(X, w, b):
    """线性回归模型"""
    return np.dot(X, w) + b
```

---

![](img/983f2321ce8f8066e54210877ee3984e_32.png)

## 定义损失函数

![](img/983f2321ce8f8066e54210877ee3984e_34.png)

我们使用平方损失函数（L2损失）来衡量模型预测值与真实值之间的差异。损失函数定义为：

![](img/983f2321ce8f8066e54210877ee3984e_35.png)

**公式：** `loss = (1/2) * (y_hat - y)^2`

在代码中，我们需要注意数组形状的匹配，避免因广播机制产生错误。

```python
def squared_loss(y_hat, y):
    """平方损失函数"""
    # 确保 y_hat 和 y 形状一致
    y_hat = y_hat.reshape(y.shape)
    return 0.5 * ((y_hat - y) ** 2)
```

---

## 定义优化算法

我们将使用随机梯度下降（SGD）来更新模型参数。SGD的更新规则如下：

![](img/983f2321ce8f8066e54210877ee3984e_37.png)

**公式：** `param = param - learning_rate * gradient`

以下是SGD优化器的实现：

![](img/983f2321ce8f8066e54210877ee3984e_39.png)

![](img/983f2321ce8f8066e54210877ee3984e_41.png)

```python
def sgd(params, lr, batch_size):
    """小批量随机梯度下降"""
    for param in params:
        param[:] = param - lr * param.grad / batch_size
```

![](img/983f2321ce8f8066e54210877ee3984e_43.png)

---

![](img/983f2321ce8f8066e54210877ee3984e_45.png)

## 训练循环

现在，我们将所有部分组合起来，构建完整的训练循环。训练过程包括前向传播、损失计算、反向传播和参数更新。

![](img/983f2321ce8f8066e54210877ee3984e_47.png)

以下是训练循环的关键步骤：

![](img/983f2321ce8f8066e54210877ee3984e_49.png)

1.  设置超参数（学习率、训练轮数、批次大小）。
2.  在每个训练轮次（epoch）中，遍历整个数据集。
3.  对每个数据批次，计算预测值和损失。
4.  执行反向传播计算梯度。
5.  使用SGD更新参数。

![](img/983f2321ce8f8066e54210877ee3984e_50.png)

![](img/983f2321ce8f8066e54210877ee3984e_52.png)

```python
# 超参数设置
lr = 0.03  # 学习率
num_epochs = 3  # 训练轮数
batch_size = 10  # 批次大小

![](img/983f2321ce8f8066e54210877ee3984e_53.png)

# 训练循环
for epoch in range(num_epochs):
    for X_batch, y_batch in data_iter(batch_size, X, y):
        # 前向传播：计算预测值
        y_hat = linreg(X_batch, w, b)
        # 计算损失
        loss = squared_loss(y_hat, y_batch).sum()
        # 反向传播：计算梯度
        loss.backward()
        # 使用SGD更新参数
        sgd([w, b], lr, batch_size)
        # 清空梯度，为下一次计算做准备
        w.grad.zero_()
        b.grad.zero_()
    # 每轮结束后，计算并打印整个训练集的平均损失
    total_loss = squared_loss(linreg(X, w, b), y)
    print(f'Epoch {epoch + 1}, loss: {float(total_loss.mean()):.6f}')
```

![](img/983f2321ce8f8066e54210877ee3984e_54.png)

训练结束后，我们可以比较学习到的参数与真实参数的接近程度，以评估模型性能。

![](img/983f2321ce8f8066e54210877ee3984e_56.png)

![](img/983f2321ce8f8066e54210877ee3984e_57.png)

---

## 使用Gluon框架实现

![](img/983f2321ce8f8066e54210877ee3984e_59.png)

上一节我们手动实现了线性回归的各个组件。本节中，我们来看看如何使用深度学习框架Gluon来简化这一过程。Gluon提供了高级API，能让我们更高效地构建和训练模型。

Gluon的实现主要涉及三个核心部分：数据加载、模型定义以及训练过程。

![](img/983f2321ce8f8066e54210877ee3984e_61.png)

### 数据加载

![](img/983f2321ce8f8066e54210877ee3984e_63.png)

Gluon提供了便捷的数据加载工具，可以轻松创建数据迭代器。

![](img/983f2321ce8f8066e54210877ee3984e_65.png)

```python
from mxnet import gluon

![](img/983f2321ce8f8066e54210877ee3984e_67.png)

# 将数据转换为Gluon数据集
dataset = gluon.data.ArrayDataset(X, y)
# 创建数据加载器，自动进行批处理和打乱
data_iter = gluon.data.DataLoader(dataset, batch_size=batch_size, shuffle=True)
```

### 定义模型

在Gluon中，我们可以使用预定义的层来快速构建网络。线性回归对应一个全连接层（Dense Layer）。

```python
from mxnet.gluon import nn

![](img/983f2321ce8f8066e54210877ee3984e_69.png)

# 定义网络结构：一个输出单元为1的全连接层
net = nn.Sequential()
net.add(nn.Dense(1))
```

![](img/983f2321ce8f8066e54210877ee3984e_71.png)

### 初始化模型参数

Gluon提供了多种参数初始化方法。

```python
from mxnet import init

# 使用正态分布初始化网络参数
net.initialize(init.Normal(sigma=0.01))
```

![](img/983f2321ce8f8066e54210877ee3984e_73.png)

![](img/983f2321ce8f8066e54210877ee3984e_74.png)

### 定义损失函数和优化器

同样，损失函数和优化器也有预定义的模块。

![](img/983f2321ce8f8066e54210877ee3984e_76.png)

```python
from mxnet.gluon import loss as gloss
from mxnet import autograd

![](img/983f2321ce8f8066e54210877ee3984e_78.png)

# 定义平方损失函数
loss = gloss.L2Loss()
# 定义优化器为SGD，并指定学习率
trainer = gluon.Trainer(net.collect_params(), 'sgd', {'learning_rate': lr})
```

### 训练循环

使用Gluon后，训练循环的代码更加简洁清晰。

![](img/983f2321ce8f8066e54210877ee3984e_80.png)

```python
for epoch in range(num_epochs):
    for X_batch, y_batch in data_iter:
        with autograd.record():
            l = loss(net(X_batch), y_batch)  # 前向传播并计算损失
        l.backward()  # 反向传播
        trainer.step(batch_size)  # 更新参数（优化器已处理梯度平均）
    # 计算并打印损失
    total_loss = loss(net(X), y)
    print(f'Epoch {epoch + 1}, loss: {float(total_loss.mean().asscalar()):.6f}')
```

可以看到，使用框架后，我们无需手动实现梯度计算和参数更新，代码的可靠性和可读性都得到了提升。

---

![](img/983f2321ce8f8066e54210877ee3984e_82.png)

![](img/983f2321ce8f8066e54210877ee3984e_83.png)

## 总结

本节课中，我们一起学习了线性回归的完整实现流程。

1.  我们首先手动实现了数据生成、模型、损失函数和SGD优化器，并完成了训练循环。这个过程帮助我们深入理解了线性回归和梯度下降的核心机制。
2.  接着，我们介绍了如何使用Gluon框架来高效地实现相同的功能。通过使用预定义的层、损失函数和优化器，我们能够用更少的代码、更稳定地构建和训练模型。

![](img/983f2321ce8f8066e54210877ee3984e_85.png)

掌握从零实现和使用框架两种方法，能让我们既理解底层原理，又能熟练运用工具进行高效开发。