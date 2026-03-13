# 6：L6-神经网络 🧠

![](img/e3bbdee916775b6931caeacad960048d_0.png)

![](img/e3bbdee916775b6931caeacad960048d_2.png)

![](img/e3bbdee916775b6931caeacad960048d_4.png)

![](img/e3bbdee916775b6931caeacad960048d_6.png)

![](img/e3bbdee916775b6931caeacad960048d_8.png)

![](img/e3bbdee916775b6931caeacad960048d_10.png)

![](img/e3bbdee916775b6931caeacad960048d_12.png)

![](img/e3bbdee916775b6931caeacad960048d_14.png)

![](img/e3bbdee916775b6931caeacad960048d_16.png)

![](img/e3bbdee916775b6931caeacad960048d_18.png)

![](img/e3bbdee916775b6931caeacad960048d_20.png)

![](img/e3bbdee916775b6931caeacad960048d_22.png)

![](img/e3bbdee916775b6931caeacad960048d_24.png)

在本节课中，我们将学习神经网络这一强大的假设类。我们将从回顾线性分类和特征变换开始，逐步引入使用阶跃函数作为特征的思想，并最终构建出神经网络的基本形式。我们还将探讨如何学习神经网络的参数，并了解其面临的独特挑战。

![](img/e3bbdee916775b6931caeacad960048d_26.png)

![](img/e3bbdee916775b6931caeacad960048d_28.png)

![](img/e3bbdee916775b6931caeacad960048d_30.png)

![](img/e3bbdee916775b6931caeacad960048d_32.png)

![](img/e3bbdee916775b6931caeacad960048d_34.png)

---

![](img/e3bbdee916775b6931caeacad960048d_36.png)

![](img/e3bbdee916775b6931caeacad960048d_38.png)

![](img/e3bbdee916775b6931caeacad960048d_40.png)

![](img/e3bbdee916775b6931caeacad960048d_42.png)

![](img/e3bbdee916775b6931caeacad960048d_44.png)

![](img/e3bbdee916775b6931caeacad960048d_46.png)

## 📚 回顾：线性分类与特征

![](img/e3bbdee916775b6931caeacad960048d_48.png)

![](img/e3bbdee916775b6931caeacad960048d_50.png)

![](img/e3bbdee916775b6931caeacad960048d_52.png)

![](img/e3bbdee916775b6931caeacad960048d_54.png)

![](img/e3bbdee916775b6931caeacad960048d_56.png)

在之前的课程中，我们讨论了线性分类和线性回归。我们通过选择不同的特征（例如多项式特征），可以获得非常有趣的分类边界和回归曲线。

线性分类的核心思想是找到一个超平面来划分数据。对于一个数据点 **x**，我们计算 **z = θᵀx + θ₀**。根据 **z** 的符号（大于0或小于0），我们预测不同的标签（例如+1或-1）。

![](img/e3bbdee916775b6931caeacad960048d_58.png)

![](img/e3bbdee916775b6931caeacad960048d_60.png)

![](img/e3bbdee916775b6931caeacad960048d_62.png)

![](img/e3bbdee916775b6931caeacad960048d_64.png)

当我们引入特征变换 **φ(x)** 时，分类函数变为 **z = θᵀφ(x) + θ₀**。这允许我们获得非线性的决策边界，而模型在参数 **θ** 上仍然是线性的。

![](img/e3bbdee916775b6931caeacad960048d_66.png)

![](img/e3bbdee916775b6931caeacad960048d_68.png)

![](img/e3bbdee916775b6931caeacad960048d_70.png)

![](img/e3bbdee916775b6931caeacad960048d_72.png)

---

![](img/e3bbdee916775b6931caeacad960048d_74.png)

![](img/e3bbdee916775b6931caeacad960048d_76.png)

![](img/e3bbdee916775b6931caeacad960048d_78.png)

![](img/e3bbdee916775b6931caeacad960048d_80.png)

![](img/e3bbdee916775b6931caeacad960048d_82.png)

![](img/e3bbdee916775b6931caeacad960048d_84.png)

![](img/e3bbdee916775b6931caeacad960048d_86.png)

## 🧩 使用阶跃函数作为特征

![](img/e3bbdee916775b6931caeacad960048d_88.png)

![](img/e3bbdee916775b6931caeacad960048d_90.png)

![](img/e3bbdee916775b6931caeacad960048d_92.png)

![](img/e3bbdee916775b6931caeacad960048d_94.png)

![](img/e3bbdee916775b6931caeacad960048d_96.png)

本节中，我们将探索一种新的特征构建方法：使用阶跃函数。与之前将阶跃函数直接用作分类器不同，我们现在将其用作构建更复杂模型的**特征**。

![](img/e3bbdee916775b6931caeacad960048d_98.png)

![](img/e3bbdee916775b6931caeacad960048d_100.png)

一个阶跃函数特征可以定义为：
**φᵢ(x) = step(wᵢᵀx + w₀ᵢ)**
其中，**step(z)** 函数在 **z > 0** 时输出1，否则输出0。参数 **wᵢ** 和 **w₀ᵢ** 决定了这个“阶跃”发生的位置和方向。

我们可以创建多个这样的阶跃函数特征，每个都有自己独立的参数。然后，我们像往常一样，对这些特征进行线性组合以进行分类：
**z = θ₁φ₁(x) + θ₂φ₂(x) + ... + θₙφₙ(x) + θ₀**

通过组合多个阶跃函数特征，我们可以构建出复杂的决策区域。例如，我们可以表达“当条件A和条件B同时满足时预测为正类”这样的逻辑。

![](img/e3bbdee916775b6931caeacad960048d_102.png)

![](img/e3bbdee916775b6931caeacad960048d_104.png)

![](img/e3bbdee916775b6931caeacad960048d_106.png)

---

![](img/e3bbdee916775b6931caeacad960048d_108.png)

![](img/e3bbdee916775b6931caeacad960048d_110.png)

![](img/e3bbdee916775b6931caeacad960048d_112.png)

![](img/e3bbdee916775b6931caeacad960048d_113.png)

![](img/e3bbdee916775b6931caeacad960048d_115.png)

## 🏗️ 构建神经网络：符号与结构

![](img/e3bbdee916775b6931caeacad960048d_117.png)

![](img/e3bbdee916775b6931caeacad960048d_119.png)

上一节我们引入了阶跃函数特征，本节我们将用更通用的符号来形式化这一思想，这就是神经网络。

![](img/e3bbdee916775b6931caeacad960048d_121.png)

![](img/e3bbdee916775b6931caeacad960048d_123.png)

神经网络可以看作是多层函数的组合。我们首先定义一些符号：
*   **层（Layer）**：用上标 **ℓ** 表示。
*   **输入维度**：第 **ℓ** 层的输入向量大小为 **m^ℓ**。
*   **输出维度**：第 **ℓ** 层的输出向量大小为 **n^ℓ**。

![](img/e3bbdee916775b6931caeacad960048d_125.png)

![](img/e3bbdee916775b6931caeacad960048d_127.png)

![](img/e3bbdee916775b6931caeacad960048d_129.png)

![](img/e3bbdee916775b6931caeacad960048d_131.png)

![](img/e3bbdee916775b6931caeacad960048d_133.png)

![](img/e3bbdee916775b6931caeacad960048d_135.png)

对于一个两层神经网络：
1.  **第一层（特征构建层）**：输入是原始数据 **x**（维度 **m¹ = d**）。我们计算：
    **z¹ = W¹x + b¹**
    **a¹ = f¹(z¹)**
    其中，**W¹** 是权重矩阵，**b¹** 是偏置向量，**f¹** 是激活函数（如阶跃函数）。输出 **a¹** 是构建出的特征向量，维度为 **n¹**。
2.  **第二层（输出层）**：输入是第一层的输出 **a¹**（因此 **m² = n¹**）。我们计算：
    **z² = W²a¹ + b²**
    **a² = f²(z²)**
    其中，**f²** 是输出层的激活函数。**a²** 就是网络的最终预测输出，维度为 **n²**（例如，二分类时 **n²=1**）。

![](img/e3bbdee916775b6931caeacad960048d_137.png)

![](img/e3bbdee916775b6931caeacad960048d_139.png)

![](img/e3bbdee916775b6931caeacad960048d_141.png)

![](img/e3bbdee916775b6931caeacad960048d_143.png)

![](img/e3bbdee916775b6931caeacad960048d_145.png)

![](img/e3bbdee916775b6931caeacad960048d_147.png)

整个网络函数 **N(x)** 就是将 **x** 映射为 **a²** 的过程。通过选择不同的参数 **{W¹, b¹, W², b²}**，我们得到了一个庞大的假设类。

![](img/e3bbdee916775b6931caeacad960048d_149.png)

![](img/e3bbdee916775b6931caeacad960048d_151.png)

![](img/e3bbdee916775b6931caeacad960048d_153.png)

![](img/e3bbdee916775b6931caeacad960048d_155.png)

---

![](img/e3bbdee916775b6931caeacad960048d_157.png)

![](img/e3bbdee916775b6931caeacad960048d_159.png)

![](img/e3bbdee916775b6931caeacad960048d_161.png)

![](img/e3bbdee916775b6931caeacad960048d_163.png)

## 🕸️ 函数图表示法

![](img/e3bbdee916775b6931caeacad960048d_165.png)

![](img/e3bbdee916775b6931caeacad960048d_167.png)

![](img/e3bbdee916775b6931caeacad960048d_169.png)

除了数学符号，我们还可以用**函数图**来直观表示神经网络。这种表示法清晰地展示了数据流动和计算过程。

![](img/e3bbdee916775b6931caeacad960048d_171.png)

![](img/e3bbdee916775b6931caeacad960048d_173.png)

![](img/e3bbdee916775b6931caeacad960048d_175.png)

以下是函数图中的关键组件：
*   **节点（Neuron/Unit）**：表示一个计算单元，通常执行 **z = wᵀ输入 + b** 和 **a = f(z)** 操作。
*   **边（Edges）**：表示数据流动方向，并携带权重参数。
*   **层（Layer）**：处于相同计算深度的节点集合。
*   **前向传播（Forward）**：数据从输入层流向输出层的过程。
*   **全连接（Fully Connected）**：当前层的每个节点都与前一层的所有节点相连。

![](img/e3bbdee916775b6931caeacad960048d_177.png)

![](img/e3bbdee916775b6931caeacad960048d_179.png)

![](img/e3bbdee916775b6931caeacad960048d_181.png)

![](img/e3bbdee916775b6931caeacad960048d_182.png)

一个两层神经网络的函数图清晰地分为输入层、隐藏层（特征层）和输出层。这种可视化有助于理解网络的运作方式和复杂性。

![](img/e3bbdee916775b6931caeacad960048d_184.png)

![](img/e3bbdee916775b6931caeacad960048d_186.png)

![](img/e3bbdee916775b6931caeacad960048d_188.png)

---

![](img/e3bbdee916775b6931caeacad960048d_190.png)

![](img/e3bbdee916775b6931caeacad960048d_192.png)

![](img/e3bbdee916775b6931caeacad960048d_194.png)

![](img/e3bbdee916775b6931caeacad960048d_196.png)

![](img/e3bbdee916775b6931caeacad960048d_198.png)

## ⚙️ 激活函数的选择与学习

![](img/e3bbdee916775b6931caeacad960048d_200.png)

![](img/e3bbdee916775b6931caeacad960048d_202.png)

![](img/e3bbdee916775b6931caeacad960048d_204.png)

![](img/e3bbdee916775b6931caeacad960048d_206.png)

![](img/e3bbdee916775b6931caeacad960048d_208.png)

![](img/e3bbdee916775b6931caeacad960048d_210.png)

![](img/e3bbdee916775b6931caeacad960048d_212.png)

我们之前一直使用阶跃函数作为激活函数，但这在实际学习中存在几个问题：
1.  导数几乎处处为零，无法使用基于梯度的优化方法（如梯度下降）。
2.  输出仅为0或1，不适合回归任务。
3.  输出不是概率，难以直接使用负对数似然损失函数。

![](img/e3bbdee916775b6931caeacad960048d_214.png)

![](img/e3bbdee916775b6931caeacad960048d_216.png)

![](img/e3bbdee916775b6931caeacad960048d_218.png)

![](img/e3bbdee916775b6931caeacad960048d_220.png)

![](img/e3bbdee916775b6931caeacad960048d_222.png)

![](img/e3bbdee916775b6931caeacad960048d_224.png)

为了解决这些问题，我们需要使用其他更合适的激活函数：

![](img/e3bbdee916775b6931caeacad960048d_226.png)

以下是常见的激活函数选择：
*   **输出层激活函数 f²**：
    *   **恒等函数（Identity）**：**f(z) = z**。用于回归任务，输出连续值。
    *   **Sigmoid函数**：**f(z) = 1 / (1 + e^{-z})**。用于二分类，输出可以解释为概率。
*   **隐藏层激活函数 f¹**：
    *   **Sigmoid函数**：平滑的阶跃函数，导数良好。
    *   **双曲正切函数（tanh）**：**f(z) = (e^z - e^{-z}) / (e^z + e^{-z})**。输出范围在(-1, 1)。
    *   **线性整流单元（ReLU）**：**f(z) = max(0, z)**。计算简单，在实践中非常有效。

![](img/e3bbdee916775b6931caeacad960048d_228.png)

更换激活函数后（例如用Sigmoid代替阶跃函数），网络的输出会变得更加平滑，便于使用梯度下降等算法进行优化。

![](img/e3bbdee916775b6931caeacad960048d_230.png)

![](img/e3bbdee916775b6931caeacad960048d_232.png)

![](img/e3bbdee916775b6931caeacad960048d_234.png)

![](img/e3bbdee916775b6931caeacad960048d_236.png)

---

![](img/e3bbdee916775b6931caeacad960048d_238.png)

## 🧭 神经网络的训练与挑战

![](img/e3bbdee916775b6931caeacad960048d_240.png)

![](img/e3bbdee916775b6931caeacad960048d_242.png)

![](img/e3bbdee916775b6931caeacad960048d_244.png)

![](img/e3bbdee916775b6931caeacad960048d_246.png)

确定了网络结构和激活函数后，我们就可以定义学习目标。与之前一样，我们最小化训练误差：
**J(W, b) = (1/m) Σᵢ L( N(xⁱ; W, b), yⁱ )**
其中 **L** 是损失函数（如均方误差、交叉熵损失），**N(xⁱ; W, b)** 是神经网络对样本 **xⁱ** 的预测。

![](img/e3bbdee916775b6931caeacad960048d_248.png)

![](img/e3bbdee916775b6931caeacad960048d_250.png)

![](img/e3bbdee916775b6931caeacad960048d_252.png)

理论上，我们可以使用梯度下降或随机梯度下降来最小化 **J**。因为现在所有的激活函数都是可微的（ReLU在0点除外，但可做特殊处理），我们可以计算梯度。

![](img/e3bbdee916775b6931caeacad960048d_254.png)

![](img/e3bbdee916775b6931caeacad960048d_256.png)

![](img/e3bbdee916775b6931caeacad960048d_258.png)

![](img/e3bbdee916775b6931caeacad960048d_260.png)

![](img/e3bbdee916775b6931caeacad960048d_262.png)

![](img/e3bbdee916775b6931caeacad960048d_264.png)

然而，神经网络的优化面临一个核心挑战：
**神经网络的损失函数 **J** 是高度非凸的**。这意味着存在许多局部最优解和鞍点，梯度下降算法不能保证收敛到全局最优解。

![](img/e3bbdee916775b6931caeacad960048d_266.png)

![](img/e3bbdee916775b6931caeacad960048d_268.png)

这与我们之前学习的线性模型形成鲜明对比。因此，训练神经网络需要一整套技巧：
*   **参数初始化策略**
*   **优化算法变种**（如带动量的SGD、Adam等）
*   **正则化技术**（如Dropout、权重衰减）以防止过拟合，因为神经网络模型容量很大。

![](img/e3bbdee916775b6931caeacad960048d_270.png)

![](img/e3bbdee916775b6931caeacad960048d_272.png)

![](img/e3bbdee916775b6931caeacad960048d_274.png)

![](img/e3bbdee916775b6931caeacad960048d_276.png)

![](img/e3bbdee916775b6931caeacad960048d_278.png)

![](img/e3bbdee916775b6931caeacad960048d_280.png)

理解这些挑战是有效使用神经网络的关键。

![](img/e3bbdee916775b6931caeacad960048d_282.png)

![](img/e3bbdee916775b6931caeacad960048d_284.png)

![](img/e3bbdee916775b6931caeacad960048d_286.png)

---

## 🏗️ 扩展：深度神经网络

![](img/e3bbdee916775b6931caeacad960048d_288.png)

![](img/e3bbdee916775b6931caeacad960048d_290.png)

![](img/e3bbdee916775b6931caeacad960048d_292.png)

![](img/e3bbdee916775b6931caeacad960048d_294.png)

我们为什么要停留在两层网络呢？我们可以很容易地添加更多层，构建**深度神经网络**。

在一个深度网络中，我们递归地构建特征：
*   第一隐藏层从原始数据中学习基础特征。
*   第二隐藏层从第一层的特征中学习更高级、更抽象的特征。
*   依此类推，最后的输出层基于这些高级特征进行预测。

![](img/e3bbdee916775b6931caeacad960048d_296.png)

![](img/e3bbdee916775b6931caeacad960048d_298.png)

这种层次化的特征学习能力是深度学习强大表现力的来源。值得注意的是，单层神经网络（即没有隐藏层）就退化为了我们最初学习的线性分类器或回归器。

![](img/e3bbdee916775b6931caeacad960048d_300.png)

![](img/e3bbdee916775b6931caeacad960048d_302.png)

在后续课程中（如卷积神经网络），我们将看到深度网络在图像等复杂数据上的具体应用和强大能力。

![](img/e3bbdee916775b6931caeacad960048d_304.png)

![](img/e3bbdee916775b6931caeacad960048d_306.png)

![](img/e3bbdee916775b6931caeacad960048d_308.png)

![](img/e3bbdee916775b6931caeacad960048d_310.png)

![](img/e3bbdee916775b6931caeacad960048d_312.png)

![](img/e3bbdee916775b6931caeacad960048d_314.png)

![](img/e3bbdee916775b6931caeacad960048d_316.png)

---

![](img/e3bbdee916775b6931caeacad960048d_318.png)

![](img/e3bbdee916775b6931caeacad960048d_320.png)

![](img/e3bbdee916775b6931caeacad960048d_322.png)

## 📝 总结

![](img/e3bbdee916775b6931caeacad960048d_324.png)

![](img/e3bbdee916775b6931caeacad960048d_326.png)

![](img/e3bbdee916775b6931caeacad960048d_328.png)

![](img/e3bbdee916775b6931caeacad960048d_330.png)

![](img/e3bbdee916775b6931caeacad960048d_332.png)

本节课我们一起学习了神经网络的基本概念：
1.  我们从使用阶跃函数作为特征出发，构建了基本的神经网络模型。
2.  我们学习了神经网络的数学表示法和函数图表示法，理解了层、节点、前向传播等概念。
3.  我们探讨了不同激活函数（Sigmoid, tanh, ReLU）的作用和选择，以适应分类、回归任务和梯度优化。
4.  我们明确了神经网络的训练目标，并认识到其损失函数的非凸性所带来的优化挑战。
5.  我们了解了深度神经网络通过多层隐藏层进行层次化特征学习的基本思想。

![](img/e3bbdee916775b6931caeacad960048d_334.png)

![](img/e3bbdee916775b6931caeacad960048d_336.png)

![](img/e3bbdee916775b6931caeacad960048d_338.png)

![](img/e3bbdee916775b6931caeacad960048d_340.png)

![](img/e3bbdee916775b6931caeacad960048d_342.png)

![](img/e3bbdee916775b6931caeacad960048d_344.png)

神经网络提供了一个极其灵活且强大的假设类，是现代机器学习的核心工具。理解其基本原理是后续学习更复杂模型（如CNN、RNN）的基础。