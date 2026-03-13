# 14：L8.2 - 深度生成模型 🧠

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_1.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_3.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_5.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_7.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_9.png)

在本节课中，我们将要学习深度生成模型。我们将从生成模型的基本概念开始，介绍它与判别式模型的区别，然后深入探讨两种非常流行的深度生成模型：变分自编码器和生成对抗网络。我们将学习它们的原理、推导过程、训练方法以及在实际多模态数据中的应用。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_11.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_12.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_14.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_16.png)

---

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_18.png)

## 1. 生成模型简介 📖

上一节我们回顾了课程的整体安排，本节中我们来看看什么是生成模型。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_20.png)

生成模型通常只给定数据 `x`（例如图像、视频、文本），而没有对应的标签 `y`。其目标是建模数据的概率分布 `p(x)`。这与判别式学习或监督学习不同，后者同时给定数据 `x` 和标签 `y`，目标是估计条件概率 `p(y|x)`。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_22.png)

当我们谈论学习和评估生成模型时，通常关注以下几个方面：

*   **评估问题**：学习 `p(x)` 后，对于新的数据 `x`，我们应该能够评估其概率 `p(x)`。看起来真实的数据（如图像）应具有较高的 `p(x)` 值，而不真实的数据则具有较低的 `p(x)` 值。这对于异常检测等任务非常有用。
*   **采样问题**：学习 `p(x)` 后，我们希望能够根据 `p(x)` 采样新的数据 `x`。这意味着高概率密度区域（对应真实图像）应被更频繁地采样。
*   **表示学习**：生成模型和一般无监督学习的目标通常是学习有用的特征表示。例如，对于狗的图像，我们希望模型不仅能生成新的狗图像，还能学习到“狗有耳朵、尾巴”等特征。

除了无条件生成 `p(x)`，人们还关心条件生成 `p(x|c)`（例如，根据类别“人脸”生成图像）和风格迁移（在保留内容的同时改变风格）。许多生成模型方法都可以扩展到这些任务。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_24.png)

---

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_26.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_28.png)

## 2. 潜在变量模型 🎯

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_30.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_32.png)

上一节我们介绍了生成模型的目标，本节中我们来看看实现这些目标的常用方法：潜在变量模型。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_34.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_36.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_38.png)

潜在变量是指那些未被观测到、但希望显式建模的变量。例如，在人脸图像中，性别、眼睛颜色、头发颜色、姿势等都是潜在的变异因素。除非图像被标注，否则这些信息并不显式可用。

我们通常用贝叶斯网络来建模生成过程。其中，观测变量 `x`（如图像）是阴影节点，潜在变量 `z` 是非阴影节点。有向边 `z -> x` 建模了条件分布 `p(x|z)`，即从潜在变量生成数据的过程。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_40.png)

理想情况下，如果我们有足够的领域知识，可以手动定义这个生成模型的结构和条件分布。但现实中，我们通常只有大量未标注的数据。因此，目标转变为**学习这些未观测的潜在变量**，包括它们的值、分布和结构。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_42.png)

神经网络因其强大的非线性函数拟合能力，非常适合用来学习这些复杂的条件分布。我们可以为连续潜在变量 `z` 设置一个先验分布（如标准高斯分布），然后使用神经网络参数化生成过程 `p(x|z)` 的均值和方差。这样，训练后 `z` 有望对应有意义的变异因素。同时，我们也希望有一个编码器，能够将新数据 `x` 编码为潜在表示 `z`，用于特征提取。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_44.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_46.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_48.png)

然而，直接使用神经网络建模会带来优化上的挑战，我们将在后续章节看到。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_50.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_52.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_54.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_56.png)

---

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_58.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_60.png)

## 3. 从混合高斯模型到变分自编码器 🔄

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_62.png)

上一节我们介绍了使用神经网络学习潜在变量的想法，本节中我们从一个简单的生成模型——混合高斯模型开始，逐步引出变分自编码器。

混合高斯模型包含两组参数：
1.  潜在变量 `z`，代表所属的聚类，服从一个分类分布。
2.  给定聚类 `z`，数据 `x` 服从一个高斯分布，该分布由均值 `μ_z` 和方差 `σ_z` 参数化。

生成过程是：首先从分类分布中采样 `z`，然后从对应的高斯分布中采样 `x`。混合高斯模型虽然每个分量简单，但混合后能覆盖数据的多个模态，表达能力很强。它可以通过期望最大化算法进行拟合。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_64.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_66.png)

混合高斯模型的一个问题是它**缺乏编码过程**。它只定义了从 `z` 到 `x` 的生成过程，但没有一个从 `x` 到 `z` 的编码器来学习数据的特征表示。

**变分自编码器可以看作是混合高斯模型的一种扩展**。它不再使用简单的高斯分布作为 `p(x|z)`，而是用神经网络来学习这个条件分布的参数，从而极大地增强了模型的表达能力。同时，它引入了编码器网络 `q(z|x)` 来学习数据的潜在表示。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_68.png)

---

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_70.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_72.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_74.png)

## 4. 变分自编码器推导 🧮

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_76.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_78.png)

上一节我们看到了VAE的动机，本节中我们来详细推导其训练过程。这些推导技巧不仅适用于VAE，也适用于许多近似推断方法。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_80.png)

我们的起点是最大化数据的对数似然：`log p(x)`。我们有一个联合分布 `p(x, z)`，但只观测到 `x`。为了引入 `z`，我们对 `z` 进行边际化：`p(x) = ∫ p(x, z) dz`。然而，这个积分在高维空间中是难以处理的。

**关键思路**：引入一个易于处理的提议分布 `q(z)`，并使用詹森不等式推导出证据下界。

具体步骤如下：
1.  将对数似然重写为包含 `q(z)` 的期望形式。
2.  应用詹森不等式（因为 `log` 是凹函数），将 `log` 移到期望内部，得到**证据下界**。
    *   `log p(x) >= E_{z~q(z)} [log (p(x, z) / q(z))]`
    *   这个下界对于任何分布 `q(z)` 都成立。
3.  当 `q(z)` 恰好等于真实后验 `p(z|x)` 时，等号成立。但真实后验通常难以计算。
4.  因此，我们的目标是**选择 `q(z)` 使其尽可能接近 `p(z|x)`**，从而让证据下界尽可能紧，进而通过最大化ELBO来近似最大化数据似然。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_82.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_84.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_86.png)

为了衡量两个分布的接近程度，我们引入**KL散度**：`KL(q(z) || p(z|x)) = E_{z~q(z)} [log (q(z) / p(z|x))]`。
*   选择 `KL(q||p)` 而非 `KL(p||q)` 是因为前者是 `q` 下的期望，而 `q` 是我们选择的简单分布，便于采样计算。
*   KL散度是非负的，当且仅当两分布相同时为零。

通过代数变换，我们可以得到重要关系：
`log p(x) = ELBO + KL(q(z) || p(z|x))`
其中，`ELBO = E_{z~q(z)} [log p(x|z)] - KL(q(z) || p(z))`

这个关系式清晰地表明：
*   数据对数似然 `log p(x)` 是固定的。
*   通过优化变分参数 `φ` 来最小化 `KL(q(z) || p(z|x))`，可以最大化ELBO。
*   ELBO越紧，对数据似然的近似就越好。

---

## 5. VAE的损失函数与重参数化技巧 ⚙️

上一节我们推导了ELBO，本节中我们将其分解为具体的损失函数，并解决梯度计算的关键问题。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_88.png)

根据推导，ELBO可以写为：
`ELBO = E_{z~q_φ(z|x)} [log p_θ(x|z)] - KL(q_φ(z|x) || p(z))`

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_90.png)

这自然分解为两项：
1.  **重构损失**：`E_{z~q_φ(z|x)} [log p_θ(x|z)]`。它鼓励解码器 `p_θ(x|z)` 能够从编码器产生的潜在变量 `z` 中准确地重构出原始数据 `x`。
2.  **先验损失**：`-KL(q_φ(z|x) || p(z))`。它鼓励编码器产生的潜在分布 `q_φ(z|x)` 接近我们预设的先验分布 `p(z)`（通常是标准高斯分布）。这起到了正则化的作用，使得潜在空间具有良好结构（如各维度独立）。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_92.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_94.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_96.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_98.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_100.png)

从自编码器的视角看，`q_φ(z|x)` 是编码器，`p_θ(x|z)` 是解码器。

**训练中的挑战**：我们需要计算ELBO关于参数 `θ`（解码器）和 `φ`（编码器）的梯度。
*   对于 `θ`，梯度计算是直接的，因为期望不依赖于 `θ`，梯度可以移入期望内部。
*   对于 `φ`，问题在于ELBO中包含对 `q_φ(z|x)` 的期望，而 `q_φ` 本身依赖于 `φ`。我们不能简单地将梯度符号移入期望内，因为采样操作 `z ~ q_φ(z|x)` 是不可微的。

**解决方案：重参数化技巧**
假设 `q_φ(z|x)` 是一个高斯分布，即 `z ~ N(μ_φ(x), σ_φ(x)^2)`。
我们可以将采样过程重参数化为：
`z = μ_φ(x) + σ_φ(x) ⊙ ε`，其中 `ε ~ N(0, I)`
这里，`ε` 是从标准高斯采样的随机噪声，`⊙` 表示逐元素相乘。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_102.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_103.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_105.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_107.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_109.png)

这样做的妙处在于：
*   随机性被转移到了噪声变量 `ε` 上。
*   `z` 现在成为 `ε` 和 `φ` 的**确定性函数**。
*   原本对 `q_φ` 的期望 `E_{z~q_φ}[f(z)]`，可以转化为对 `ε` 的期望 `E_{ε~N(0,I)}[f(μ_φ(x) + σ_φ(x)⊙ε)]`。
*   现在，梯度 `∇_φ` 可以移入对 `ε` 的期望内部，因为期望不再直接依赖于 `φ`。我们可以通过采样多个 `ε` 来估计这个梯度。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_111.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_113.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_115.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_117.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_119.png)

**VAE训练流程总结**：
1.  输入数据点 `x_i`。
2.  编码器 `q_φ(z|x_i)` 输出均值 `μ` 和方差 `σ`。
3.  采样噪声 `ε ~ N(0, I)`，通过重参数化计算潜在变量 `ẑ = μ + σ ⊙ ε`。
4.  解码器 `p_θ(x|ẑ)` 重构数据。
5.  计算损失：`L = 重构损失(x_i, p_θ(x|ẑ)) + β * KL(q_φ(z|x_i) || p(z))`（`β` 是可选权重）。
6.  通过梯度下降同时更新编码器参数 `φ` 和解码器参数 `θ`。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_121.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_123.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_125.png)

---

## 6. VAE的应用：解耦表示与多模态学习 🎨

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_127.png)

上一节我们完成了VAE的理论构建，本节中我们来看看它的几个有趣应用。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_129.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_131.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_133.png)

**1. 学习解耦表示**
解耦表示是指潜在空间的每个维度对应数据中一个独立且可解释的变化因素（如物体颜色、大小、背景等）。VAE天然倾向于学习解耦表示，因为其先验损失 `KL(q(z|x) || p(z))` 鼓励潜在变量各维度独立（如果 `p(z)` 是各向同性高斯）。
通过调整KL项的权重 `β`（即β-VAE），可以控制解耦的强度。更大的 `β` 施加更强的独立性约束，通常能获得更好的解耦效果。这在风格迁移等任务中非常有用，我们可以分离内容变量和风格变量，然后单独操纵风格。

**2. 多模态数据中的解耦学习**
在多模态场景（如同时包含语言、视觉、音频的数据）中，我们可以设计VAE来学习**共享的跨模态因子**（如情感、主题）和**模态特定因子**（如语言风格、视觉背景）。
*   **共享因子** `z_y`：负责生成所有模态的数据并预测标签。
*   **模态特定因子** `z_m`：只负责生成对应模态的数据，捕捉该模态内部的变异。
损失函数包括：
    *   各模态的重构损失。
    *   从共享因子 `z_y` 预测标签的分类损失。
    *   对所有潜在因子的KL正则化损失（鼓励服从先验）。
这种模型不仅能提升判别任务（如情感分类）的性能，还能实现可控生成，例如保持内容（数字“5”）不变，单独改变SVHN风格或MNIST风格。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_135.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_137.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_139.png)

**3. 超越重构：结合自监督任务**
在某些任务中，直接重构高维输入（如视频）可能很困难或不必要。我们可以让VAE的**解码器预测一些有意义的、低维的自监督信号**（如光流、是否接触、多模态对齐），而不是重构原始输入。
这样，编码器学习到的表示会更专注于对下游任务有用的信息。这种方法在机器人等领域被证明是有效的，并且通过融合多模态信息，模型对单模态的遮挡或噪声具有更强的鲁棒性。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_141.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_143.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_145.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_147.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_149.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_151.png)

---

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_153.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_155.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_157.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_159.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_161.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_163.png)

## 7. 生成对抗网络简介 ⚔️

上一节我们探讨了VAE及其应用，本节我们转向另一种强大的生成模型：生成对抗网络。VAE依赖于像素级重构损失，这可能导致生成的图像模糊。GAN则采用了完全不同的思路。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_165.png)

GAN的动机源于一个统计学问题：**如何在不直接估计概率密度 `p(x)` 的情况下，判断两组样本是否来自同一分布？**
这可以通过**双样本检验**来实现。GAN的思想是：训练一个生成模型 `G`，使其产生的样本分布 `p_G` 尽可能接近真实数据分布 `p_data`，同时训练一个判别器 `D` 来区分真实样本和生成样本。这形成了一个**极小极大博弈**。

**GAN的目标函数**：
`min_G max_D V(D, G) = E_{x~p_data}[log D(x)] + E_{z~p_z}[log(1 - D(G(z)))]`
*   **判别器 `D`**：试图最大化该目标，即正确分类真实样本为真（`D(x)->1`），生成样本为假（`D(G(z))->0`）。
*   **生成器 `G`**：试图最小化该目标，即欺骗判别器，使其将生成样本误判为真（`D(G(z))->1`）。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_167.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_169.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_171.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_173.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_175.png)

理论上，当训练达到最优时，生成器的分布 `p_G` 会匹配真实数据分布 `p_data`，此时判别器对所有输入都输出0.5（无法区分）。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_177.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_179.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_181.png)

**GAN的训练算法**：
1.  从真实数据中采样一批样本。
2.  从先验噪声分布 `p_z` 中采样一批噪声 `z`。
3.  使用生成器 `G` 将噪声 `z` 转换为生成样本 `G(z)`。
4.  **固定 `G`，更新 `D`**：最大化 `log D(x) + log(1 - D(G(z)))`。
5.  **固定 `D`，更新 `G`**：最小化 `log(1 - D(G(z)))`（或最大化 `log D(G(z))`，实践中后者梯度更稳定）。
6.  重复步骤1-5。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_183.png)

---

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_185.png)

## 8. GAN的改进：从JS散度到Wasserstein距离 📈

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_187.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_189.png)

原始的GAN使用JS散度作为衡量 `p_data` 和 `p_G` 之间差异的度量。然而，JS散度在高维空间中存在严重问题：
*   **支撑集问题**：如果真实数据分布 `p_data` 和生成分布 `p_G` 的支撑集（概率非零的区域）没有重叠或重叠部分测度为零，那么JS散度会是一个常数（`log 2`），其梯度为零。这导致生成器无法获得有效的训练信号，即“梯度消失”问题。
*   这在实践中很常见，因为高维数据通常位于低维流形上，两个随机分布几乎没有重叠。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_191.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_193.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_195.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_197.png)

**Wasserstein GAN 的改进**
WGAN提出使用**Wasserstein距离**（也称推土机距离）来代替JS散度。Wasserstein距离衡量的是将一个分布“搬移”成另一个分布所需的最小“工作量”。
*   **优点**：
    1.  即使两个分布的支撑集不重叠，Wasserstein距离仍然能提供有意义的、平滑的度量。
    2.  其梯度几乎处处非零，为生成器提供了更稳定的训练信号。
*   **实现**：通过其对偶形式，WGAN的判别器（在WGAN中常称为“评论家”）不再输出0/1分类概率，而是输出一个实数分数。其目标函数变为：
    `max_D E_{x~p_data}[D(x)] - E_{z~p_z}[D(G(z))]`
    同时，需要约束判别器 `D` 为1-Lipschitz函数（通常通过权重裁剪或梯度惩罚来实现）。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_199.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_201.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_203.png)

直观上，对于支撑集不重叠的两个分布，原始GAN的判别器梯度很快饱和为零；而WGAN的评论家会给出一个线性变化的分数，引导生成器向真实分布移动。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_205.png)

---

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_207.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_209.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_211.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_213.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_215.png)

## 9. 总结与展望 🚀

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_217.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_219.png)

在本节课中，我们一起学习了深度生成模型的核心内容。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_221.png)

我们首先理解了生成模型与判别模型的根本区别，以及生成模型在评估、采样和表示学习方面的目标。然后，我们深入探讨了两种主流的深度生成模型：

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_223.png)

1.  **变分自编码器**：通过引入变分推断和重参数化技巧，将生成模型训练转化为一个可优化的证据下界最大化问题。VAE具有编码器-解码器结构，能同时学习生成数据和数据的低维表示，在多模态学习和解耦表示方面有很好的应用。
2.  **生成对抗网络**：通过生成器和判别器的对抗博弈来学习数据分布，无需显式定义似然函数。我们从原始GAN的JS散度问题，讲到了其改进版WGAN如何利用Wasserstein距离来提供更稳定的训练。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_225.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_227.png)

这些模型都结合了图模型的结构化建模能力和神经网络的强大表达能力。VAE训练稳定且有编码器，但生成样本可能较模糊；GAN生成样本质量高，但训练过程可能不稳定且缺乏编码器。

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_229.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_231.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_233.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_235.png)

![](img/d5e5f010bbf85f2dbcc1cafefb74f76c_237.png)

在接下来的课程中，我们将探讨如何将这些生成模型应用于离散数据（如文本），并会引入强化学习技术（如策略梯度）来解决离散输出带来的梯度计算挑战。我们还将看到GAN和VAE在更多实际场景中的应用。