# 3：决策树

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_1.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_2.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_3.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_5.png)

在本节课中，我们将继续学习决策树。我们将了解如何使用决策树进行预测，并深入探讨如何从数据中学习构建决策树的核心算法。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_7.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_9.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_10.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_12.png)

## 课程公告与提醒

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_14.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_15.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_17.png)

在开始之前，有一些课程相关的提醒。

首先，作业一今天截止。对于晚加入课程或需要额外时间的同学，可以联系助教申请延期。

其次，今晚有一次背景知识测试的补考，详细信息可以在课程论坛上找到。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_19.png)

最后，作业二将于今天下午晚些时候发布。请注意，与作业一不同，作业二将严格执行课程大纲中规定的延期和迟交政策。

## 课堂互动与投票

每节课我们都会通过在线表单进行课堂投票。今天的投票链接是 `poll.mlCourse.org`，你也可以在课程网站的日程表页面找到它。请使用你的学校邮箱登录以记录参与分数。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_21.png)

投票中通常会有一个“有毒选项”，选择它会带来负的期望分数，这是为了防止随机猜测。如果你无法参加课程，请不要随意填写投票，而是使用你的“免费投票点数”。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_23.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_25.png)

现在，让我们测试一下投票系统。请访问投票链接并回答第一个问题：**“你今天使用什么设备访问课堂投票？”**

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_27.png)

## 递归概念回顾

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_29.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_31.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_33.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_34.png)

在深入决策树之前，我们先简要回顾一个重要的编程概念：递归。递归是一种通过将问题分解为结构相同的更小子问题来解决问题的方法。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_36.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_37.png)

以**二叉搜索树**为例。二叉搜索树的每个节点包含一个值，以及最多两个子节点（左子节点和右子节点）。其关键特性是：左子树的所有节点值都小于当前节点值，右子树的所有节点值都大于当前节点值。

例如，一个根节点值为7的二叉搜索树，其左子树的所有节点值都小于7，右子树的所有节点值都大于7。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_39.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_40.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_42.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_44.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_46.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_48.png)

二叉搜索树允许我们在 **O(log n)** 时间内搜索特定值，其中 **n** 是树中节点的数量。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_50.png)

搜索功能可以通过迭代或递归的方式实现。以下是迭代搜索的伪代码思路：
```python
def contains_iterative(root, key):
    current_node = root
    while True:
        if key < current_node.value:
            if current_node.left is not None:
                current_node = current_node.left
            else:
                break
        elif key > current_node.value:
            if current_node.right is not None:
                current_node = current_node.right
            else:
                break
        else:
            # key == current_node.value
            return True
    return key == current_node.value
```

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_52.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_54.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_56.png)

递归方法则将搜索问题分解：要判断值是否在树中，只需判断它是否在左子树或右子树中。每个递归函数都需要一个**递归调用**和一个**基准情况**。以下是递归搜索的伪代码思路：
```python
def contains_recursive(node, key):
    if node is None:
        return False
    if key == node.value:
        return True
    elif key < node.value:
        return contains_recursive(node.left, key)
    else: # key > node.value
        return contains_recursive(node.right, key)
```
递归是构建和理解决策树算法的强大工具。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_58.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_59.png)

## 从决策树桩到决策树

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_61.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_62.png)

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_63.png)

上节课我们以决策树桩（仅使用一个特征的决策树）结束。虽然决策树桩可能有非零的训练误差，但它比单纯记忆所有训练数据的“记忆器”更具泛化能力。

然而，我们为什么要止步于只使用一个特征呢？即使是小孩也能构建考虑多个特征的更复杂的分类器。本节我们将探讨如何构建更完整的决策树。

为了直观理解，我们用一个预测一个人是“爱猫人士”还是“爱狗人士”的决策树示例来说明。假设我们使用两个特征：
1.  偏好温暖还是寒冷的温度？
2.  是晨型人还是夜猫子？

通过现场收集数据并让同学根据特征在树上移动，我们演示了决策树如何通过一系列问题（特征判断）将数据点分配到不同的“叶节点”。每个叶节点包含一组具有相同特征组合的数据点，但其标签可能仍然混杂。

这个例子引出了几个关键问题：
1.  如何对到达叶节点的数据做出最终预测？（例如，通过多数投票或概率预测）。
2.  当叶节点为空（没有训练数据到达）时如何预测？（例如，使用父节点或整个数据集的多数标签）。
3.  我们如何决定在哪个节点、使用哪个特征进行分割？

## 使用决策树进行预测

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_65.png)

首先，我们明确如何用已构建好的决策树进行预测。预测过程就是从根节点出发，沿着与数据点特征值对应的分支，走到叶节点，然后返回该叶节点存储的预测值。

以下是预测函数的迭代式伪代码：
```python
def predict(tree_root, x_prime):
    current_node = tree_root
    while current_node.is_internal_node:
        feature_index = current_node.feature_index # 当前节点用于分割的特征
        feature_value = x_prime[feature_index] # 数据点在该特征上的值
        current_node = current_node.children[feature_value] # 沿对应分支向下
    return current_node.label # 到达叶节点，返回预测标签
```
这个过程与我们之前演示的预测流程一致。同样，我们也可以编写递归函数来实现预测。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_67.png)

## 学习决策树：选择分割特征

现在我们来探讨核心问题：如何从数据中学习（构建）决策树？这可以分解为两个子问题：
1.  在每个节点，我们如何选择用哪个特征进行分割？
2.  我们如何决定分割的顺序？

首先解决第一个问题。我们需要一个**分割标准**，它是一个为每个可能的分割特征打分的函数，分数越高表示用该特征分割效果越好。

一个直观的想法是使用**训练误差率**作为标准。即，对于每个特征，构建一个决策树桩，计算其在训练集上的错误率，选择错误率最低的特征。

然而，这种方法存在缺陷。在某些数据集上，两个特征可能导致相同的训练误差，但其中一个特征可能实际上与标签完全无关，没有提供任何信息。这显然不是我们想要的结果。

因此，我们需要一个更好的标准：**互信息**。互信息衡量的是，知道一个特征的值后，能为我们减少多少关于标签的“不确定性”。不确定性由**熵**来度量。

熵衡量一个集合的“混杂程度”或我们对其结果的不确定性。对于一个包含两类标签的集合 **S**，其熵 **H(S)** 的计算公式为：
```
H(S) = - p * log₂(p) - (1-p) * log₂(1-p)
```
其中 **p** 是正类样本的比例。
*   当集合中所有标签相同时（p=0或1），熵为 **0**（最纯）。
*   当正负样本各占一半时（p=0.5），熵为 **1**（最混杂）。

**互信息 I(特征; 标签)** 的计算如下：
```
I(特征; 标签) = H(原始标签集合) - Σ [ (|Sv|/|S|) * H(Sv) ]
```
其中 **Sv** 是根据特征值 **v** 分割后的子集。互信息表示原始标签的熵减去按特征分割后各子集熵的加权平均。它衡量了特征能为标签带来多少信息。
*   如果特征能完美预测标签，互信息最高（在二分类情况下为1）。
*   如果特征与标签完全无关，互信息为0。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_69.png)

使用互信息作为分割标准，可以解决训练误差率标准的问题，它能识别出真正提供信息的特征。

## 学习决策树：递归构建流程

接下来解决第二个问题：决定分割的顺序。这里我们自然要用到**递归**。

构建决策树的递归思路是：
1.  **在当前节点**，从所有可用特征中选择互信息最高的特征进行分割。
2.  根据该特征的每个可能取值，将当前数据集划分成多个子集。
3.  **对每个子集**，递归地调用相同的建树过程，创建对应的子节点。
4.  重复上述步骤，直到满足**停止条件**。

停止条件（即递归的基准情况）包括：
*   当前节点包含的所有数据点都具有相同的标签（纯节点）。
*   没有更多特征可供分割。
*   数据集为空。
*   达到预设的停止条件（如最大深度，下周详述）。

当满足停止条件时，该节点成为**叶节点**，其预测标签通常设定为该节点数据中多数票对应的标签（或存储标签分布用于概率预测）。

以下是递归训练函数的核心伪代码框架：
```python
def train_decision_tree(D): # D是训练数据集
    root = build_tree_recursive(D)
    return root

def build_tree_recursive(D_prime):
    node = new Node()
    # 检查停止条件（纯节点、无特征、数据空等）
    if stopping_criteria_met(D_prime):
        node.label = majority_vote(D_prime)
        return node
    # 选择最佳分割特征
    best_feature = argmax_over_features( mutual_information(feature, D_prime) )
    node.feature_index = best_feature
    # 根据特征值划分数据并递归构建子树
    for each value v of best_feature:
        D_v = subset of D_prime where best_feature == v
        node.children[v] = build_tree_recursive(D_v)
    return node
```

## 总结

本节课我们一起深入学习了决策树。
*   我们首先回顾了递归的概念，这是理解树形结构算法的基础。
*   我们通过一个生动的例子，理解了决策树如何进行预测以及构建过程中面临的挑战。
*   我们明确了使用决策树进行预测的迭代过程。
*   我们深入探讨了学习决策树的核心：如何选择分割特征。我们分析了使用训练误差的不足，并引入了更可靠的**互信息**标准，它基于**熵**来衡量特征所带来的信息增益。
*   最后，我们勾勒出使用**递归**方法构建完整决策树的算法框架，包括如何选择特征、划分数据以及设定递归停止条件。

![](img/a1e5ccf52cd6990c8635cc9a617ab47f_71.png)

下节课，我们将继续讨论决策树，包括如何避免过拟合以及其他高级话题。