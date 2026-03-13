# 11：L11- 循环神经网络 🧠

![](img/52a90b78aac5c82b5fa7c88e786484f1_1.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_3.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_5.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_7.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_9.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_11.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_13.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_15.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_17.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_19.png)

在本节课中，我们将学习循环神经网络。我们将从回顾前几节课的内容开始，然后探讨如何将状态机的思想应用于监督学习，特别是处理文本预测这类序列数据。最后，我们将定义循环神经网络，并了解其工作原理。

![](img/52a90b78aac5c82b5fa7c88e786484f1_21.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_23.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_25.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_27.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_29.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_31.png)

## 回顾：强化学习与监督学习

![](img/52a90b78aac5c82b5fa7c88e786484f1_33.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_35.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_37.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_39.png)

上一节我们介绍了强化学习。现在，我们来明确一下强化学习与监督学习的区别。

![](img/52a90b78aac5c82b5fa7c88e786484f1_41.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_43.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_45.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_47.png)

强化学习的核心思想是：通过与环境的交互来学习如何最大化奖励。这与监督学习不同。在监督学习中，我们通常有固定的输入和输出对，目标是学习一个从输入到输出的映射。虽然可以将负损失视为一种奖励，但强化学习的关键在于，我们的行动不仅影响即时奖励，还会通过改变环境状态来影响未来的奖励和可观测信息。

![](img/52a90b78aac5c82b5fa7c88e786484f1_49.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_51.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_53.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_55.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_57.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_59.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_61.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_63.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_65.png)

以下是强化学习的一些应用场景：
*   **游戏玩法**：通过不断试错来学习最佳策略。
*   **数字营销**：通过与潜在客户的多次互动，寻找最优策略以达成目标。
*   **自动化任务**：如工业机器人、自动驾驶汽车等。
*   **医疗应用**：但需注意安全性和数据效率等挑战。

![](img/52a90b78aac5c82b5fa7c88e786484f1_67.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_69.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_71.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_73.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_75.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_77.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_79.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_81.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_83.png)

## 从状态机到序列数据

![](img/52a90b78aac5c82b5fa7c88e786484f1_85.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_87.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_89.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_91.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_93.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_95.png)

上一节我们介绍了状态机和马尔可夫决策过程，本节我们来看看如何将这些思想应用于监督学习。

![](img/52a90b78aac5c82b5fa7c88e786484f1_97.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_99.png)

我们之前看到的状态机模型，其状态变化不仅仅局限于强化学习场景。实际上，我们可以将其应用于监督学习，处理具有递归性质的序列数据。今天的示例将围绕文本预测展开。

![](img/52a90b78aac5c82b5fa7c88e786484f1_101.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_103.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_105.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_107.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_109.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_111.png)

## 动机示例：文本预测 📝

![](img/52a90b78aac5c82b5fa7c88e786484f1_113.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_115.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_117.png)

文本预测在我们的生活中很常见。例如，在Gmail中撰写邮件时，系统会建议接下来可能输入的字符；在搜索引擎中输入时，会出现自动补全的选项。

![](img/52a90b78aac5c82b5fa7c88e786484f1_119.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_121.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_123.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_125.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_127.png)

对于行动不便的人士（如斯蒂芬·霍金或唐·法伊兹·韦伯斯特），高效的文本预测技术是至关重要的辅助工具。

![](img/52a90b78aac5c82b5fa7c88e786484f1_129.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_131.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_133.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_135.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_137.png)

我们将研究一个简化的文本预测问题：根据已输入的文本，预测下一个字符。这是一个典型的监督学习任务。

![](img/52a90b78aac5c82b5fa7c88e786484f1_139.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_141.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_143.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_145.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_147.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_149.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_151.png)

### 获取训练数据

![](img/52a90b78aac5c82b5fa7c88e786484f1_153.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_155.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_157.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_159.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_161.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_163.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_165.png)

我们可以从大量在线文本（如维基百科、诗歌）中获取训练数据。从一段文本中，我们可以提取出许多训练样本。

![](img/52a90b78aac5c82b5fa7c88e786484f1_167.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_169.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_171.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_173.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_175.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_177.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_179.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_181.png)

例如，对于句子 “what happens”，我们可以得到以下训练样本：
*   输入 “w”，预测下一个字符 “h”。
*   输入 “wh”，预测下一个字符 “a”。
*   输入 “wha”，预测下一个字符 “t”。

![](img/52a90b78aac5c82b5fa7c88e786484f1_183.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_185.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_187.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_189.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_191.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_193.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_195.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_197.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_199.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_201.png)

### 特征化挑战

![](img/52a90b78aac5c82b5fa7c88e786484f1_203.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_205.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_207.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_209.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_211.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_213.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_215.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_217.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_219.png)

这看起来像一个分类问题（预测27个字符类别之一）。但挑战在于如何将变长的输入序列转化为固定维度的特征向量。

![](img/52a90b78aac5c82b5fa7c88e786484f1_221.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_223.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_225.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_227.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_229.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_231.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_233.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_235.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_237.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_238.png)

一个想法是使用所有之前的字符作为特征（上下文），但这会导致特征维度不固定。另一个想法是只使用最后一个字符，但这可能丢失重要信息。

![](img/52a90b78aac5c82b5fa7c88e786484f1_240.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_242.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_244.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_246.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_248.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_250.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_252.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_254.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_256.png)

折中的方案是使用最后 `m` 个字符作为特征。`m` 是一个超参数，代表我们考虑的上文长度。

![](img/52a90b78aac5c82b5fa7c88e786484f1_258.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_260.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_262.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_264.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_266.png)

## 构建状态机模型

![](img/52a90b78aac5c82b5fa7c88e786484f1_268.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_270.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_272.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_274.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_276.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_278.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_280.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_282.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_284.png)

将问题建模为状态机有助于我们思考。在这个状态机中：
*   **状态**：最近看到的 `m` 个字符（上下文）。
*   **输入**：新输入的一个字符。
*   **状态转移**：当输入新字符时，我们更新状态：移除最旧的字符，加入最新的字符。
*   **输出**：基于当前状态（最近 `m` 个字符），预测下一个字符的概率分布。这可以通过一个多类逻辑回归分类器（使用Softmax函数）来实现。
*   **初始状态**：可以用 `m` 个特殊的“开始”字符填充。

![](img/52a90b78aac5c82b5fa7c88e786484f1_286.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_288.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_290.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_292.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_294.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_296.png)

通过这种方式，我们将变长的序列预测问题，转化为了一个具有固定维度特征（状态 `s`）的分类问题。

![](img/52a90b78aac5c82b5fa7c88e786484f1_298.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_300.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_302.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_304.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_306.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_308.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_310.png)

## 定义方程与循环神经网络

![](img/52a90b78aac5c82b5fa7c88e786484f1_312.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_314.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_316.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_318.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_320.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_322.png)

上一节我们构建了状态机模型，本节我们来看看如何用数学方程定义它，并进一步演变为循环神经网络。

![](img/52a90b78aac5c82b5fa7c88e786484f1_324.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_326.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_328.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_330.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_332.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_334.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_336.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_338.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_340.png)

首先，我们为状态转移函数 `f` 和输出函数 `g` 写出方程。为了简化，假设字母表只有 {0, 1}，且 `m=3`。

![](img/52a90b78aac5c82b5fa7c88e786484f1_342.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_344.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_346.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_348.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_349.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_351.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_353.png)

状态转移函数 `f` 可以表示为一个线性操作，将新输入 `x_t` 放入状态向量的顶部，并将旧状态 `s_{t-1}` 的元素向下移位。

![](img/52a90b78aac5c82b5fa7c88e786484f1_355.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_357.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_359.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_361.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_363.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_365.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_367.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_369.png)

输出函数 `g` 则是一个标准的线性分类器（后接Softmax），将状态 `s_t` 作为输入特征，输出下一个字符的概率向量 `p_t`。

![](img/52a90b78aac5c82b5fa7c88e786484f1_371.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_373.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_375.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_377.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_379.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_381.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_383.png)

到目前为止，我们只是将状态机与逻辑回归结合。但我们可以更进一步：**学习特征本身**，而不仅仅是分类器的权重。

![](img/52a90b78aac5c82b5fa7c88e786484f1_385.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_387.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_389.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_391.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_393.png)

就像我们在神经网络和卷积神经网络中所做的一样，我们可以将状态转移方程中的固定矩阵（用于移位操作）替换为可学习的权重矩阵 `W_{sx}` 和 `W_{ss}`，并加入偏置项 `W_{ss0}` 和非线性激活函数 `f1`（如ReLU或Sigmoid）。

![](img/52a90b78aac5c82b5fa7c88e786484f1_395.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_397.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_399.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_401.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_403.png)

于是，我们的状态更新和预测方程变为：
*   **状态更新**：`s_t = f1( W_{ss} s_{t-1} + W_{sx} x_t + W_{ss0} )`
*   **预测输出**：`p_t = f2( W_{os} s_t + W_{o0} )`，其中 `f2` 通常是Softmax函数。

![](img/52a90b78aac5c82b5fa7c88e786484f1_405.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_407.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_409.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_411.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_413.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_415.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_417.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_419.png)

这个包含可学习参数和递归结构的模型，就是**循环神经网络**。

![](img/52a90b78aac5c82b5fa7c88e786484f1_421.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_423.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_425.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_426.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_428.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_430.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_432.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_434.png)

## RNN的结构与对比

![](img/52a90b78aac5c82b5fa7c88e786484f1_436.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_438.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_439.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_441.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_443.png)

循环神经网络的结构可以展开成一条时间链，也可以折叠成一个带循环的图。

![](img/52a90b78aac5c82b5fa7c88e786484f1_445.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_447.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_449.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_451.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_453.png)

*   **展开视图**：清晰地展示了数据在时间步上的流动。
*   **折叠视图**：强调了参数的共享和循环的本质。

![](img/52a90b78aac5c82b5fa7c88e786484f1_455.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_457.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_459.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_460.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_462.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_464.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_466.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_468.png)

与之前学过的模型对比：
*   **与前馈神经网络**：RNN在隐藏层之间增加了循环连接，允许信息在时间步之间传递，适合处理序列数据。
*   **与卷积神经网络**：CNN为空间数据（如图像）设计，具有平移不变性；RNN为序列数据（如文本、时间序列）设计，能捕捉时间依赖关系。
*   **与强化学习**：在当前的RNN应用中，我们是在固定的训练数据上进行监督学习，并不涉及通过自身行动改变环境状态来学习策略。

![](img/52a90b78aac5c82b5fa7c88e786484f1_470.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_472.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_474.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_476.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_478.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_479.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_481.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_483.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_485.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_487.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_488.png)

## 训练RNN：损失与优化

![](img/52a90b78aac5c82b5fa7c88e786484f1_490.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_492.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_494.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_496.png)

遵循我们熟悉的监督学习模式，要训练RNN，我们需要：
1.  **定义预测方式**：已由RNN方程给出。
2.  **定义损失函数**：对于序列中的每个时间步 `t`，使用负对数似然损失比较预测分布 `p_t^i` 和真实标签 `y_t^i`。整个序列的损失是各时间步损失之和，整个数据集的损失是所有序列损失之和。
3.  **优化参数**：使用梯度下降或随机梯度下降最小化总损失。参数包括 `W_{ss}`, `W_{sx}`, `W_{ss0}`, `W_{os}`, `W_{o0}`。

![](img/52a90b78aac5c82b5fa7c88e786484f1_498.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_500.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_502.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_504.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_506.png)

由于RNN在时间步之间共享参数，计算梯度时会涉及时间上的反向传播，这比标准反向传播更复杂一些，因为梯度需要通过多个时间步反向流动。现代深度学习框架的自动微分功能可以很好地处理这一点。

![](img/52a90b78aac5c82b5fa7c88e786484f1_508.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_510.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_512.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_514.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_516.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_518.png)

## 总结

![](img/52a90b78aac5c82b5fa7c88e786484f1_520.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_522.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_524.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_526.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_528.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_530.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_532.png)

本节课中我们一起学习了循环神经网络。

![](img/52a90b78aac5c82b5fa7c88e786484f1_534.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_536.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_538.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_540.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_542.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_544.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_546.png)

我们首先回顾了强化学习，并指出状态机的思想同样可以应用于监督学习中的序列数据。接着，我们以文本预测为例，展示了如何将问题建模为状态机，并使用固定上下文的逻辑回归进行预测。

![](img/52a90b78aac5c82b5fa7c88e786484f1_548.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_550.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_552.png)

然后，我们迈出了关键一步：将状态转移中的固定操作替换为可学习的权重和非线性变换，从而得到了循环神经网络。RNN通过其循环结构，能够维护一个内部状态，从而有效地处理和预测序列数据。

![](img/52a90b78aac5c82b5fa7c88e786484f1_554.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_556.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_558.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_560.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_562.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_564.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_566.png)

最后，我们讨论了RNN的训练框架，即定义损失函数并使用基于梯度的优化方法。虽然由于参数在时间上共享使得梯度计算（随时间反向传播）略显复杂，但这仍然是可行的。

![](img/52a90b78aac5c82b5fa7c88e786484f1_568.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_570.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_572.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_574.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_576.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_578.png)

![](img/52a90b78aac5c82b5fa7c88e786484f1_580.png)

至此，我们掌握了另一种强大的神经网络架构，它专门为挖掘序列数据中的时序依赖关系而设计。