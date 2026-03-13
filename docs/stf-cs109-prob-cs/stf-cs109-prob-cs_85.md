# 差分隐私

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/differential_privacy/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/differential_privacy/)

* * *

最近，许多组织已经发布了在大型数据集上训练的机器学习模型（GPT-3、YOLO 等...）。这对科学是一个巨大的贡献，并简化了现代人工智能研究。然而，公布这些模型可能会允许对模型进行潜在的“逆向工程”，以揭示模型的训练数据。具体来说，攻击者可以下载一个模型，查看参数值，然后尝试重建原始训练数据。这对于在敏感数据（如健康信息）上训练的模型来说尤其糟糕。在本节中，我们将使用随机性作为防御算法“逆向工程”的方法。

### 注入随机性

一种对抗算法逆向工程的方法是在已经存在的数据集中添加一些随机元素。设

$$\begin{align*} X_1, \dots, X_i \overset{\text{i.i.d}} \sim \text{Bern}(p) \end{align*}$$

代表一组真实的人类数据。考虑以下代码片段：

```py
def calculateXi(Xi): 
	return Xi
```

简单来说，攻击者可以针对所有 100 个样本调用上述操作，揭示所有 100 个数据点。相反，我们可以注入一些随机性：

```py
def calculateYi(Xi): 
	obfuscate = random() # Bern with parameter p=0.5
	if obfuscate:
		return indicator(random())
	else:
		return Xi
```

攻击者可以期望调用新函数 100 次，并得到其中 50 个的正确值（但他们不知道是哪 50 个）。

### 恢复 $p$

现在考虑如果我们发布 calculateYi 函数，一个对样本均值感兴趣的研究者如何获取有用的数据？他们可以查看：

$$\begin{align*} Z = \sum^{100}_{n=1} Y_i. \end{align*}$$

其期望值为：

$$\begin{align*} E[Z] = E\left[\sum^{100}_{n=1} Y_i\right] = \sum^{100}_{n=1} E[Y_i] = \sum^{100}_{n=1}\left(\frac{p}{2} + \frac{1}{4}\right) = 50p + 25 \end{align*}$$

然后为了揭示一个估计值，科学家可以这样做，

$$\begin{align*} p \approx \frac{Z - 25}{50} \end{align*}$$

然后继续进行更多研究！
