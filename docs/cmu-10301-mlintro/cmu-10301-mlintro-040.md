# 40：决策树与互信息基础教程 🌳

![](img/cfb8fc811311cce0a32c27eb65612cf8_1.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_3.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_5.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_7.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_9.png)

在本节课中，我们将要学习决策树的基本概念、树结构遍历以及互信息的计算。这些知识是构建决策树分类器的核心基础。

![](img/cfb8fc811311cce0a32c27eb65612cf8_11.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_13.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_15.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_17.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_19.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_21.png)

## 树结构基础定义 📚

![](img/cfb8fc811311cce0a32c27eb65612cf8_23.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_25.png)

上一节我们介绍了课程背景，本节中我们来看看决策树中关于树结构的基本定义。

![](img/cfb8fc811311cce0a32c27eb65612cf8_27.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_28.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_29.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_31.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_33.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_35.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_36.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_37.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_39.png)

**树的深度** 是指从根节点到最远叶子节点的最长路径上的**边数**。

**节点的深度** 是指从根节点到该节点的路径上的**边数**。根节点的深度为0。

![](img/cfb8fc811311cce0a32c27eb65612cf8_41.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_43.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_45.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_47.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_48.png)

以下是几个计算示例：
*   对于树A，根节点是x1，到最远叶子节点（例如x7）的路径边数为3，因此树A的深度为3。
*   对于树A中的节点x4，从根节点x1到x4的路径边数为2，因此节点x4的深度为2。
*   树B（决策树桩）的深度为1。
*   对于树C，节点x1（根节点）的深度为0，节点x5的深度为2。

![](img/cfb8fc811311cce0a32c27eb65612cf8_50.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_51.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_53.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_54.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_56.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_58.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_60.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_62.png)

## 树的遍历算法 🔄

![](img/cfb8fc811311cce0a32c27eb65612cf8_64.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_66.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_68.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_69.png)

理解了树的基本结构后，本节中我们来看看如何系统地访问树中的所有节点，即树的遍历。

![](img/cfb8fc811311cce0a32c27eb65612cf8_71.png)

以下是三种常见的二叉树遍历方式及其伪代码描述：

![](img/cfb8fc811311cce0a32c27eb65612cf8_73.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_75.png)

**后序遍历**
```python
def traversal1(root):
    if root is not None:
        traversal1(root.left)
        traversal1(root.right)
        print(root.value)
```
遍历顺序：完全访问左子树 -> 完全访问右子树 -> 访问当前节点。
对于示例树（根1，左子2（左4右5），右子3），输出顺序为：4, 5, 2, 3, 1。

![](img/cfb8fc811311cce0a32c27eb65612cf8_77.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_79.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_81.png)

**先序遍历**
```python
def traversal2(root):
    if root is not None:
        print(root.value)
        traversal2(root.left)
        traversal2(root.right)
```
遍历顺序：访问当前节点 -> 完全访问左子树 -> 完全访问右子树。
对于同一棵示例树，输出顺序为：1, 2, 4, 5, 3。

![](img/cfb8fc811311cce0a32c27eb65612cf8_83.png)

**中序遍历**
```python
def traversal3(root):
    if root is not None:
        traversal3(root.left)
        print(root.value)
        traversal3(root.right)
```
遍历顺序：完全访问左子树 -> 访问当前节点 -> 完全访问右子树。
对于同一棵示例树，输出顺序为：4, 2, 5, 1, 3。对于二叉搜索树，中序遍历会产生有序序列。

![](img/cfb8fc811311cce0a32c27eb65612cf8_85.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_86.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_88.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_90.png)

## 熵与互信息 💡

![](img/cfb8fc811311cce0a32c27eb65612cf8_92.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_94.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_96.png)

在学会了如何遍历树之后，我们需要一个标准来决定如何构建树。本节中我们来看看用于评估信息不确定性的核心概念——熵与互信息。

![](img/cfb8fc811311cce0a32c27eb65612cf8_98.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_99.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_101.png)

**熵** 衡量一个随机变量的平均不确定性（惊奇度）。其公式为：
`H(Y) = - Σ P(y) * log₂(P(y))`，对所有可能的y值求和。

![](img/cfb8fc811311cce0a32c27eb65612cf8_103.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_104.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_105.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_107.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_109.png)

**条件熵** 衡量在已知另一个随机变量X的条件下，Y剩余的不确定性。其公式为：
`H(Y|X) = Σ P(x) * H(Y|X=x)`，对所有可能的x值求和。

![](img/cfb8fc811311cce0a32c27eb65612cf8_111.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_113.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_114.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_116.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_118.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_119.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_121.png)

**互信息** 衡量已知变量X后，Y的不确定性减少了多少。它是我们选择分裂特征的标准。其公式为：
`I(Y; X) = H(Y) - H(Y|X)`

![](img/cfb8fc811311cce0a32c27eb65612cf8_122.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_124.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_126.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_128.png)

以下是熵的计算示例：
1.  抛掷均匀硬币：`H(Y) = -[0.5*log₂(0.5) + 0.5*log₂(0.5)] = 1`
2.  抛掷永远朝上的硬币：`H(Y) = -[0*log₂(0) + 1*log₂(1)] = 0`（确定事件，无不确定性）
3.  投掷均匀骰子：`H(Y) = -6 * (1/6 * log₂(1/6)) = log₂(6)`

![](img/cfb8fc811311cce0a32c27eb65612cf8_130.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_132.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_134.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_135.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_136.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_138.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_140.png)

**互信息何时为零？**
当 `I(Y; X) = 0` 时，意味着 `H(Y) = H(Y|X)`。这在数学和直觉上都意味着随机变量X和Y是**相互独立的**。知道X的信息并不能帮助我们减少关于Y的不确定性。

![](img/cfb8fc811311cce0a32c27eb65612cf8_142.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_143.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_144.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_145.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_146.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_147.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_149.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_151.png)

## 构建决策树：一个完整示例 🛠️

![](img/cfb8fc811311cce0a32c27eb65612cf8_153.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_154.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_155.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_156.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_158.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_160.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_162.png)

掌握了熵与互信息的计算方法后，本节我们将通过一个具体的数据集，一步步演示如何构建一棵决策树。

![](img/cfb8fc811311cce0a32c27eb65612cf8_164.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_166.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_167.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_169.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_170.png)

我们有以下数据集，包含三个特征（Outlook, Temperature, Humidity）和一个标签（Play）：

![](img/cfb8fc811311cce0a32c27eb65612cf8_172.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_173.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_174.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_175.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_176.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_177.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_178.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_179.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_181.png)

| Outlook (X1) | Temperature (X2) | Humidity (X3) | Play (Y) |
| :--- | :--- | :--- | :--- |
| Sunny | Hot | High | No |
| Sunny | Hot | High | No |
| Sunny | Mild | High | No |
| Overcast | Hot | High | Yes |
| Rain | Mild | High | Yes |
| Rain | Cool | Normal | Yes |
| Rain | Cool | Normal | No |
| Overcast | Cool | Normal | Yes |

![](img/cfb8fc811311cce0a32c27eb65612cf8_183.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_185.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_187.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_189.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_191.png)

**第一步：选择根节点（第一次分裂）**
我们需要计算Y与每个特征的互信息，并选择互信息最大的特征进行分裂。

![](img/cfb8fc811311cce0a32c27eb65612cf8_193.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_195.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_197.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_198.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_200.png)

1.  计算 `H(Y)`：P(No)=2/8， P(Yes)=6/8。`H(Y) = -[(2/8)*log₂(2/8) + (6/8)*log₂(6/8)] ≈ 0.811`
2.  计算 `H(Y|X1)`：
    *   X1=Sunny (3例): P(No)=2/3， P(Yes)=1/3。`H(Y|Sunny) ≈ 0.918`
    *   X1=Rain (3例): P(Yes)=3/3。`H(Y|Rain) = 0`
    *   X1=Overcast (2例): P(Yes)=2/2。`H(Y|Overcast) = 0`
    *   `H(Y|X1) = (3/8)*0.918 + (3/8)*0 + (2/8)*0 ≈ 0.344`
3.  计算 `I(Y; X1) = H(Y) - H(Y|X1) ≈ 0.811 - 0.344 = 0.467`

![](img/cfb8fc811311cce0a32c27eb65612cf8_202.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_204.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_206.png)

同理计算（过程略）：
*   `I(Y; X2) ≈ 0.061`
*   `I(Y; X3) ≈ 0.311`

![](img/cfb8fc811311cce0a32c27eb65612cf8_208.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_209.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_211.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_213.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_215.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_217.png)

由于 `I(Y; X1)` 最大，因此选择 **Outlook (X1)** 作为根节点进行分裂。

![](img/cfb8fc811311cce0a32c27eb65612cf8_219.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_220.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_222.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_224.png)

**第二步：递归构建子树**
根据X1的取值，数据集被分成三部分：
*   X1=Rain 和 X1=Overcast 对应的子集，其Y标签都是纯的（全是Yes），因此成为叶子节点，直接预测为Yes。
*   X1=Sunny 对应的子集（3条数据）Y标签不纯，需要继续分裂。我们在这个子集上重新计算Y与剩余特征（X2, X3）的互信息。
    *   在该子集上，`I(Y; X2) ≈ 0.251`， `I(Y; X3) ≈ 0.918`。
    *   选择互信息更大的 **Humidity (X3)** 进行分裂。
        *   X3=High (2例): Y均为No，成为叶子节点，预测为No。
        *   X3=Normal (1例): Y为Yes，成为叶子节点，预测为Yes。

![](img/cfb8fc811311cce0a32c27eb65612cf8_226.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_227.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_228.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_229.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_230.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_231.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_233.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_234.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_235.png)

最终构建的决策树如下图所示（文本描述）：
```
Outlook (X1)
├── Sunny -> Humidity (X3)
│   ├── High -> No
│   └── Normal -> Yes
├── Overcast -> Yes
└── Rain -> Yes
```

![](img/cfb8fc811311cce0a32c27eb65612cf8_237.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_239.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_240.png)

**关键点提醒**：
*   在子树中计算互信息时，**只考虑**到达当前节点路径上条件所对应的数据子集。
*   当节点中所有样本属于同一类别（纯节点），或没有更多特征可供分裂时，停止递归，并将该节点设为叶子节点（通常采用多数表决）。

![](img/cfb8fc811311cce0a32c27eb65612cf8_242.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_244.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_245.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_247.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_249.png)

## 决策树实现要点 💻

![](img/cfb8fc811311cce0a32c27eb65612cf8_251.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_253.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_255.png)

通过上面的例子，我们理解了决策树的手动构建过程。本节中我们来看看如何将这些步骤转化为具体的编程实现逻辑。

![](img/cfb8fc811311cce0a32c27eb65612cf8_257.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_259.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_261.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_263.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_264.png)

**任务概述**：给定训练集、测试集和树的最大深度，需要：
1.  使用训练集学习一个决策树分类器。
2.  用学到的树对训练集和测试集进行预测。
3.  计算训练误差和测试误差。

![](img/cfb8fc811311cce0a32c27eb65612cf8_266.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_268.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_270.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_272.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_274.png)

**训练阶段**：
*   **输入**：训练数据，最大深度。
*   **输出**：训练好的决策树模型。
*   **节点存储信息**：分裂特征、当前数据子集、左右子节点、节点深度等。
*   **训练过程（递归）**：
    1.  检查停止条件：达到最大深度 或 节点数据纯 或 无特征可分。若满足，则创建叶子节点（返回多数类）。
    2.  否则，计算所有特征与标签的互信息。
    3.  选择互信息最大的特征进行分裂。
    4.  根据该特征划分数据子集，并递归创建左右子树。

![](img/cfb8fc811311cce0a32c27eb65612cf8_276.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_278.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_280.png)

**测试阶段**：
*   **重要原则**：**切勿**使用测试数据重新训练模型。
*   **过程**：使用训练好的决策树模型，遍历树的节点，根据测试样本的特征值决定路径，直到到达叶子节点并获得预测标签。

![](img/cfb8fc811311cce0a32c27eb65612cf8_282.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_284.png)

**关于最大深度**：
*   如果最大深度为0，则树仅包含一个根节点，直接对全体数据做多数表决。
*   如果最大深度大于特征数量，当所有特征都用尽时，即使未达到深度限制也应停止分裂。

## 编程与调试技巧 🐛

![](img/cfb8fc811311cce0a32c27eb65612cf8_286.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_288.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_289.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_291.png)

最后，在动手实现之前，本节我们分享一些实用的编程和调试技巧，帮助你更高效地完成代码。

![](img/cfb8fc811311cce0a32c27eb65612cf8_293.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_294.png)

**调试工具**：
*   **打印调试**：在关键位置打印变量值（如数组、中间计算结果），简单有效。
*   **使用PDB**：Python内置调试器。在代码中插入 `import pdb; pdb.set_trace()`，程序运行到此处会进入交互调试模式。

![](img/cfb8fc811311cce0a32c27eb65612cf8_296.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_297.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_298.png)

**常见错误示例**：
1.  **索引错误**：注意Python列表是0索引的。循环时 `for i in range(1, len(rows)+1)` 会导致索引越界，应为 `for i in range(len(rows))`。
2.  **创建二维列表的陷阱**：
    ```python
    # 错误：所有行都是第一行的引用
    arr = [[0]*cols] * rows
    arr[0][0] = 1  # 会导致所有行的第一列都变成1
    ```
    ```python
    # 正确：创建独立的子列表
    arr = [[0 for _ in range(cols)] for _ in range(rows)]
    ```
3.  **逻辑与边界条件**：实现“返回非零值最多的列索引，平局时返回最小索引”的函数时，需注意：
    *   计数条件应为 `if val != 0`，而非 `if val == 0`。
    *   比较更新条件应为 `if count > max_count:`，使用 `>` 确保平局时保留第一个（索引最小）的列；若使用 `>=`，则会保留最后一个。

![](img/cfb8fc811311cce0a32c27eb65612cf8_300.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_302.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_304.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_306.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_308.png)

---

![](img/cfb8fc811311cce0a32c27eb65612cf8_310.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_312.png)

![](img/cfb8fc811311cce0a32c27eb65612cf8_314.png)

本节课中我们一起学习了决策树的基础知识，包括树结构的定义与遍历、熵与互信息的概念及计算、手动构建决策树的完整步骤，以及实现决策树的关键逻辑和编程技巧。这些内容将为完成相关的编程作业打下坚实的基础。