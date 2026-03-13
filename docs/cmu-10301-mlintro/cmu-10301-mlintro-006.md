# 6：感知机与在线学习 👨‍🏫

![](img/223aea760bce52b872e46ca99b14c6fe_0.png)

![](img/223aea760bce52b872e46ca99b14c6fe_2.png)

![](img/223aea760bce52b872e46ca99b14c6fe_3.png)

![](img/223aea760bce52b872e46ca99b14c6fe_4.png)

![](img/223aea760bce52b872e46ca99b14c6fe_5.png)

![](img/223aea760bce52b872e46ca99b14c6fe_6.png)

![](img/223aea760bce52b872e46ca99b14c6fe_7.png)

![](img/223aea760bce52b872e46ca99b14c6fe_9.png)

![](img/223aea760bce52b872e46ca99b14c6fe_10.png)

![](img/223aea760bce52b872e46ca99b14c6fe_12.png)

![](img/223aea760bce52b872e46ca99b14c6fe_14.png)

![](img/223aea760bce52b872e46ca99b14c6fe_16.png)

![](img/223aea760bce52b872e46ca99b14c6fe_17.png)

![](img/223aea760bce52b872e46ca99b14c6fe_18.png)

![](img/223aea760bce52b872e46ca99b14c6fe_19.png)

![](img/223aea760bce52b872e46ca99b14c6fe_21.png)

![](img/223aea760bce52b872e46ca99b14c6fe_22.png)

在本节课中，我们将学习一种新的机器学习模型——感知机，并引入一个全新的学习范式——在线学习。这与我们之前接触的、一次性提供所有数据的“批量学习”模式有很大不同。

![](img/223aea760bce52b872e46ca99b14c6fe_23.png)

![](img/223aea760bce52b872e46ca99b14c6fe_25.png)

![](img/223aea760bce52b872e46ca99b14c6fe_26.png)

![](img/223aea760bce52b872e46ca99b14c6fe_27.png)

![](img/223aea760bce52b872e46ca99b14c6fe_29.png)

![](img/223aea760bce52b872e46ca99b14c6fe_30.png)

## 课程提醒与答疑 📝

![](img/223aea760bce52b872e46ca99b14c6fe_32.png)

在开始新内容之前，先提醒大家：第二次作业今天截止。第三次作业将在今天下午发布，请注意，第三次作业最多只能使用两个迟交日。今天的辅导课将在周三同一时间地点进行。

![](img/223aea760bce52b872e46ca99b14c6fe_33.png)

![](img/223aea760bce52b872e46ca99b14c6fe_34.png)

![](img/223aea760bce52b872e46ca99b14c6fe_35.png)

![](img/223aea760bce52b872e46ca99b14c6fe_37.png)

![](img/223aea760bce52b872e46ca99b14c6fe_38.png)

![](img/223aea760bce52b872e46ca99b14c6fe_40.png)

![](img/223aea760bce52b872e46ca99b14c6fe_42.png)

![](img/223aea760bce52b872e46ca99b14c6fe_43.png)

以下是针对上节课后一些常见问题的解答：

![](img/223aea760bce52b872e46ca99b14c6fe_45.png)

![](img/223aea760bce52b872e46ca99b14c6fe_46.png)

![](img/223aea760bce52b872e46ca99b14c6fe_47.png)

![](img/223aea760bce52b872e46ca99b14c6fe_49.png)

![](img/223aea760bce52b872e46ca99b14c6fe_50.png)

![](img/223aea760bce52b872e46ca99b14c6fe_52.png)

*   **模型选择后的数据使用**：在通过验证集选定最佳模型后，一个合理的做法是将训练集和验证集合并，以使用更多的数据来训练最终模型，同时保持测试集的独立性以评估最终性能。
*   **KNN与分类特征**：K最近邻算法完全可以用于分类特征，关键在于选择合适的、适用于分类特征的距离度量方法。

![](img/223aea760bce52b872e46ca99b14c6fe_54.png)

![](img/223aea760bce52b872e46ca99b14c6fe_55.png)

![](img/223aea760bce52b872e46ca99b14c6fe_57.png)

![](img/223aea760bce52b872e46ca99b14c6fe_59.png)

## 从KNN到线性决策边界 📈

![](img/223aea760bce52b872e46ca99b14c6fe_61.png)

![](img/223aea760bce52b872e46ca99b14c6fe_63.png)

![](img/223aea760bce52b872e46ca99b14c6fe_65.png)

![](img/223aea760bce52b872e46ca99b14c6fe_66.png)

![](img/223aea760bce52b872e46ca99b14c6fe_67.png)

回顾之前使用的鸢尾花数据集，我们曾用KNN学习复杂的决策边界。但观察数据分布，一个更简单的想法是：**直接用一条直线将两类数据分开**。这就是我们今天要学习的内容。

![](img/223aea760bce52b872e46ca99b14c6fe_69.png)

![](img/223aea760bce52b872e46ca99b14c6fe_70.png)

![](img/223aea760bce52b872e46ca99b14c6fe_71.png)

![](img/223aea760bce52b872e46ca99b14c6fe_72.png)

![](img/223aea760bce52b872e46ca99b14c6fe_73.png)

![](img/223aea760bce52b872e46ca99b14c6fe_75.png)

![](img/223aea760bce52b872e46ca99b14c6fe_77.png)

![](img/223aea760bce52b872e46ca99b14c6fe_79.png)

![](img/223aea760bce52b872e46ca99b14c6fe_80.png)

![](img/223aea760bce52b872e46ca99b14c6fe_81.png)

在深入之前，我们先统一一些数学符号和概念，作为热身复习。

![](img/223aea760bce52b872e46ca99b14c6fe_82.png)

![](img/223aea760bce52b872e46ca99b14c6fe_84.png)

![](img/223aea760bce52b872e46ca99b14c6fe_85.png)

![](img/223aea760bce52b872e46ca99b14c6fe_86.png)

![](img/223aea760bce52b872e46ca99b14c6fe_87.png)

![](img/223aea760bce52b872e46ca99b14c6fe_89.png)

![](img/223aea760bce52b872e46ca99b14c6fe_91.png)

![](img/223aea760bce52b872e46ca99b14c6fe_93.png)

### 向量与几何概念复习 📐

![](img/223aea760bce52b872e46ca99b14c6fe_95.png)

![](img/223aea760bce52b872e46ca99b14c6fe_96.png)

![](img/223aea760bce52b872e46ca99b14c6fe_97.png)

![](img/223aea760bce52b872e46ca99b14c6fe_99.png)

![](img/223aea760bce52b872e46ca99b14c6fe_101.png)

在本课程中，我们默认所有向量为**列向量**。向量 **a** 是列向量，其转置 **aᵀ** 是行向量。

![](img/223aea760bce52b872e46ca99b14c6fe_103.png)

![](img/223aea760bce52b872e46ca99b14c6fe_104.png)

![](img/223aea760bce52b872e46ca99b14c6fe_105.png)

![](img/223aea760bce52b872e46ca99b14c6fe_106.png)

![](img/223aea760bce52b872e46ca99b14c6fe_107.png)

![](img/223aea760bce52b872e46ca99b14c6fe_109.png)

![](img/223aea760bce52b872e46ca99b14c6fe_110.png)

![](img/223aea760bce52b872e46ca99b14c6fe_112.png)

![](img/223aea760bce52b872e46ca99b14c6fe_113.png)

*   **点积（内积）**：两个向量 **a** 和 **b** 的点积定义为 **aᵀb**。
*   **L2范数**：向量 **a** 的L2范数，即其长度，定义为 `||a|| = √(aᵀa)`。我们经常使用其平方形式 `||a||²`。
*   **正交性**：在多维空间中，两个向量垂直（正交）的条件是它们的点积为零，即 **aᵀb = 0**。

![](img/223aea760bce52b872e46ca99b14c6fe_114.png)

![](img/223aea760bce52b872e46ca99b14c6fe_115.png)

![](img/223aea760bce52b872e46ca99b14c6fe_116.png)

![](img/223aea760bce52b872e46ca99b14c6fe_117.png)

![](img/223aea760bce52b872e46ca99b14c6fe_119.png)

![](img/223aea760bce52b872e46ca99b14c6fe_121.png)

### 热身练习：理解线性不等式 🧮

![](img/223aea760bce52b872e46ca99b14c6fe_123.png)

![](img/223aea760bce52b872e46ca99b14c6fe_125.png)

![](img/223aea760bce52b872e46ca99b14c6fe_126.png)

![](img/223aea760bce52b872e46ca99b14c6fe_127.png)

请花几分钟时间，在二维平面上画出由不等式 `w₁x₁ + w₂x₂ + b > 0` 定义的区域，其中 `w = [1, 2]ᵀ`, `b = -2`。同时，在同一坐标系中画出向量 **w**。

![](img/223aea760bce52b872e46ca99b14c6fe_129.png)

![](img/223aea760bce52b872e46ca99b14c6fe_130.png)

![](img/223aea760bce52b872e46ca99b14c6fe_132.png)

![](img/223aea760bce52b872e46ca99b14c6fe_133.png)

![](img/223aea760bce52b872e46ca99b14c6fe_134.png)

![](img/223aea760bce52b872e46ca99b14c6fe_136.png)

![](img/223aea760bce52b872e46ca99b14c6fe_137.png)

**答案与核心结论**：
该不等式定义的是一条直线，向量 **w** 总是与该直线**垂直（正交）**，并且 **w** 的方向指向不等式成立（即 `wᵀx + b > 0`）的半空间。这一几何关系是理解后续内容的关键。

![](img/223aea760bce52b872e46ca99b14c6fe_139.png)

![](img/223aea760bce52b872e46ca99b14c6fe_141.png)

![](img/223aea760bce52b872e46ca99b14c6fe_143.png)

![](img/223aea760bce52b872e46ca99b14c6fe_145.png)

## 线性分类器与在线学习范式 🚀

![](img/223aea760bce52b872e46ca99b14c6fe_147.png)

![](img/223aea760bce52b872e46ca99b14c6fe_148.png)

![](img/223aea760bce52b872e46ca99b14c6fe_150.png)

上一节我们复习了直线和超平面的几何表示，本节我们将看看如何将其转化为一个机器学习分类器。

![](img/223aea760bce52b872e46ca99b14c6fe_152.png)

![](img/223aea760bce52b872e46ca99b14c6fe_154.png)

![](img/223aea760bce52b872e46ca99b14c6fe_156.png)

![](img/223aea760bce52b872e46ca99b14c6fe_157.png)

![](img/223aea760bce52b872e46ca99b14c6fe_159.png)

![](img/223aea760bce52b872e46ca99b14c6fe_161.png)

### 线性决策边界作为分类器

![](img/223aea760bce52b872e46ca99b14c6fe_163.png)

![](img/223aea760bce52b872e46ca99b14c6fe_165.png)

![](img/223aea760bce52b872e46ca99b14c6fe_166.png)

![](img/223aea760bce52b872e46ca99b14c6fe_167.png)

![](img/223aea760bce52b872e46ca99b14c6fe_168.png)

我们的目标是学习形式为 `f(x) = sign(wᵀx + b)` 的分类器。其中：
*   `sign(·)` 是符号函数，输出 +1 或 -1。
*   当 `wᵀx + b > 0` 时，预测为正类（+1）。
*   当 `wᵀx + b < 0` 时，预测为负类（-1）。

![](img/223aea760bce52b872e46ca99b14c6fe_170.png)

![](img/223aea760bce52b872e46ca99b14c6fe_171.png)

![](img/223aea760bce52b872e46ca99b14c6fe_172.png)

![](img/223aea760bce52b872e46ca99b14c6fe_173.png)

![](img/223aea760bce52b872e46ca99b14c6fe_175.png)

![](img/223aea760bce52b872e46ca99b14c6fe_177.png)

![](img/223aea760bce52b872e46ca99b14c6fe_178.png)

![](img/223aea760bce52b872e46ca99b14c6fe_179.png)

![](img/223aea760bce52b872e46ca99b14c6fe_180.png)

![](img/223aea760bce52b872e46ca99b14c6fe_182.png)

这里的核心问题是：**如何从数据中学习参数 w 和 b？**

![](img/223aea760bce52b872e46ca99b14c6fe_184.png)

![](img/223aea760bce52b872e46ca99b14c6fe_186.png)

![](img/223aea760bce52b872e46ca99b14c6fe_187.png)

![](img/223aea760bce52b872e46ca99b14c6fe_189.png)

![](img/223aea760bce52b872e46ca99b14c6fe_191.png)

![](img/223aea760bce52b872e46ca99b14c6fe_193.png)

![](img/223aea760bce52b872e46ca99b14c6fe_195.png)

![](img/223aea760bce52b872e46ca99b14c6fe_196.png)

### 引入在线学习

![](img/223aea760bce52b872e46ca99b14c6fe_198.png)

![](img/223aea760bce52b872e46ca99b14c6fe_200.png)

![](img/223aea760bce52b872e46ca99b14c6fe_202.png)

![](img/223aea760bce52b872e46ca99b14c6fe_203.png)

![](img/223aea760bce52b872e46ca99b14c6fe_205.png)

![](img/223aea760bce52b872e46ca99b14c6fe_206.png)

![](img/223aea760bce52b872e46ca99b14c6fe_207.png)

传统的批量学习假设我们一次性获得所有静态数据。然而，在许多现实场景中，数据是持续不断产生的（例如：推荐系统、在线广告、传感器数据流、强化学习）。**在线学习** 就是针对这种场景的范式。

![](img/223aea760bce52b872e46ca99b14c6fe_209.png)

![](img/223aea760bce52b872e46ca99b14c6fe_210.png)

![](img/223aea760bce52b872e46ca99b14c6fe_211.png)

![](img/223aea760bce52b872e46ca99b14c6fe_213.png)

![](img/223aea760bce52b872e46ca99b14c6fe_214.png)

![](img/223aea760bce52b872e46ca99b14c6fe_216.png)

![](img/223aea760bce52b872e46ca99b14c6fe_217.png)

![](img/223aea760bce52b872e46ca99b14c6fe_218.png)

![](img/223aea760bce52b872e46ca99b14c6fe_220.png)

在线学习的流程如下：
1.  在时刻 t，收到一个未标记的数据点 **x_t**。
2.  使用当前模型（参数为 w, b）对其做出预测 ŷ_t。
3.  收到真实标签 y_t。
4.  如果预测错误（ŷ_t ≠ y_t），则根据错误更新模型参数。
5.  目标是随着时间推移，最小化犯错误的总数。

![](img/223aea760bce52b872e46ca99b14c6fe_222.png)

![](img/223aea760bce52b872e46ca99b14c6fe_224.png)

![](img/223aea760bce52b872e46ca99b14c6fe_225.png)

![](img/223aea760bce52b872e46ca99b14c6fe_227.png)

![](img/223aea760bce52b872e46ca99b14c6fe_229.png)

## 感知机学习算法 🤖

![](img/223aea760bce52b872e46ca99b14c6fe_231.png)

![](img/223aea760bce52b872e46ca99b14c6fe_232.png)

![](img/223aea760bce52b872e46ca99b14c6fe_233.png)

![](img/223aea760bce52b872e46ca99b14c6fe_234.png)

![](img/223aea760bce52b872e46ca99b14c6fe_236.png)

![](img/223aea760bce52b872e46ca99b14c6fe_238.png)

![](img/223aea760bce52b872e46ca99b14c6fe_240.png)

现在，我们介绍用于在线学习的**感知机算法**。该算法是学习线性分类器的一种简单而有效的方法。

![](img/223aea760bce52b872e46ca99b14c6fe_242.png)

![](img/223aea760bce52b872e46ca99b14c6fe_243.png)

![](img/223aea760bce52b872e46ca99b14c6fe_245.png)

![](img/223aea760bce52b872e46ca99b14c6fe_247.png)

![](img/223aea760bce52b872e46ca99b14c6fe_249.png)

![](img/223aea760bce52b872e46ca99b14c6fe_251.png)

![](img/223aea760bce52b872e46ca99b14c6fe_252.png)

![](img/223aea760bce52b872e46ca99b14c6fe_253.png)

![](img/223aea760bce52b872e46ca99b14c6fe_254.png)

![](img/223aea760bce52b872e46ca99b14c6fe_256.png)

![](img/223aea760bce52b872e46ca99b14c6fe_258.png)

![](img/223aea760bce52b872e46ca99b14c6fe_260.png)

### 算法步骤

![](img/223aea760bce52b872e46ca99b14c6fe_262.png)

![](img/223aea760bce52b872e46ca99b14c6fe_264.png)

![](img/223aea760bce52b872e46ca99b14c6fe_265.png)

![](img/223aea760bce52b872e46ca99b14c6fe_267.png)

![](img/223aea760bce52b872e46ca99b14c6fe_268.png)

![](img/223aea760bce52b872e46ca99b14c6fe_269.png)

![](img/223aea760bce52b872e46ca99b14c6fe_270.png)

![](img/223aea760bce52b872e46ca99b14c6fe_272.png)

![](img/223aea760bce52b872e46ca99b14c6fe_274.png)

![](img/223aea760bce52b872e46ca99b14c6fe_276.png)

1.  **初始化**：将权重向量 **w** 和截距 b 初始化为 0。
2.  **循环**：对于每个接收到的数据点 (**x_t**, y_t)，其中 y_t ∈ {+1, -1}：
    *   **预测**：计算 ŷ_t = sign(wᵀx_t + b)。（我们规定，当 wᵀx_t + b = 0 时，预测为 +1）。
    *   **观察与更新**：如果 ŷ_t ≠ y_t（即发生错误）：
        *   如果 y_t = +1（误判为负）：`w ← w + x_t`, `b ← b + 1`
        *   如果 y_t = -1（误判为正）：`w ← w - x_t`, `b ← b - 1`
3.  持续接收数据并重复步骤2。

![](img/223aea760bce52b872e46ca99b14c6fe_278.png)

![](img/223aea760bce52b872e46ca99b14c6fe_279.png)

![](img/223aea760bce52b872e46ca99b14c6fe_281.png)

![](img/223aea760bce52b872e46ca99b14c6fe_283.png)

![](img/223aea760bce52b872e46ca99b14c6fe_285.png)

![](img/223aea760bce52b872e46ca99b14c6fe_286.png)

![](img/223aea760bce52b872e46ca99b14c6fe_288.png)

![](img/223aea760bce52b872e46ca99b14c6fe_290.png)

![](img/223aea760bce52b872e46ca99b14c6fe_292.png)

![](img/223aea760bce52b872e46ca99b14c6fe_294.png)

![](img/223aea760bce52b872e46ca99b14c6fe_296.png)

**简化的更新规则**：可以将两种错误情况的更新统一为：如果 ŷ_t ≠ y_t，则执行 `w ← w + y_t * x_t`, `b ← b + y_t`。

![](img/223aea760bce52b872e46ca99b14c6fe_298.png)

![](img/223aea760bce52b872e46ca99b14c6fe_300.png)

![](img/223aea760bce52b872e46ca99b14c6fe_302.png)

![](img/223aea760bce52b872e46ca99b14c6fe_304.png)

![](img/223aea760bce52b872e46ca99b14c6fe_306.png)

### 算法演示与直观理解

![](img/223aea760bce52b872e46ca99b14c6fe_308.png)

![](img/223aea760bce52b872e46ca99b14c6fe_309.png)

![](img/223aea760bce52b872e46ca99b14c6fe_311.png)

![](img/223aea760bce52b872e46ca99b14c6fe_313.png)

![](img/223aea760bce52b872e46ca99b14c6fe_314.png)

![](img/223aea760bce52b872e46ca99b14c6fe_316.png)

通过课堂互动演示，我们可以看到感知机算法的工作方式：
*   它试图修正最近的错误。
*   每次更新都通过将权重向量 **w** 向误分类点方向（根据其真实标签）移动，来调整决策边界。
*   这个过程可能使之前分类正确的点又变得错误，但算法会在后续迭代中继续调整。

![](img/223aea760bce52b872e46ca99b14c6fe_318.png)

![](img/223aea760bce52b872e46ca99b14c6fe_319.png)

![](img/223aea760bce52b872e46ca99b14c6fe_321.png)

![](img/223aea760bce52b872e46ca99b14c6fe_323.png)

![](img/223aea760bce52b872e46ca99b14c6fe_325.png)

![](img/223aea760bce52b872e46ca99b14c6fe_326.png)

![](img/223aea760bce52b872e46ca99b14c6fe_328.png)

![](img/223aea760bce52b872e46ca99b14c6fe_330.png)

![](img/223aea760bce52b872e46ca99b14c6fe_332.png)

![](img/223aea760bce52b872e46ca99b14c6fe_333.png)

![](img/223aea760bce52b872e46ca99b14c6fe_335.png)

![](img/223aea760bce52b872e46ca99b14c6fe_337.png)

### 偏置项 b 的作用

![](img/223aea760bce52b872e46ca99b14c6fe_339.png)

![](img/223aea760bce52b872e46ca99b14c6fe_340.png)

![](img/223aea760bce52b872e46ca99b14c6fe_341.png)

![](img/223aea760bce52b872e46ca99b14c6fe_343.png)

![](img/223aea760bce52b872e46ca99b14c6fe_345.png)

![](img/223aea760bce52b872e46ca99b14c6fe_346.png)

![](img/223aea760bce52b872e46ca99b14c6fe_348.png)

![](img/223aea760bce52b872e46ca99b14c6fe_349.png)

![](img/223aea760bce52b872e46ca99b14c6fe_350.png)

![](img/223aea760bce52b872e46ca99b14c6fe_352.png)

![](img/223aea760bce52b872e46ca99b14c6fe_354.png)

![](img/223aea760bce52b872e46ca99b14c6fe_356.png)

偏置项 b 允许决策边界不必须穿过坐标原点。其更新规则是：
*   增加 b 会使决策边界向负半空间移动（即扩大被分类为正的区域）。
*   减少 b 会使决策边界向正半空间移动。

![](img/223aea760bce52b872e46ca99b14c6fe_358.png)

![](img/223aea760bce52b872e46ca99b14c6fe_359.png)

![](img/223aea760bce52b872e46ca99b14c6fe_361.png)

![](img/223aea760bce52b872e46ca99b14c6fe_363.png)

![](img/223aea760bce52b872e46ca99b14c6fe_365.png)

![](img/223aea760bce52b872e46ca99b14c6fe_367.png)

### 简化表示：增广向量

![](img/223aea760bce52b872e46ca99b14c6fe_369.png)

![](img/223aea760bce52b872e46ca99b14c6fe_371.png)

![](img/223aea760bce52b872e46ca99b14c6fe_373.png)

![](img/223aea760bce52b872e46ca99b14c6fe_374.png)

为了更简洁地处理 w 和 b，我们可以使用**增广向量**：
*   定义新的参数向量 **θ = [b; w]**（将 b 放在 w 前面）。
*   定义新的特征向量 **x̃ = [1; x]**（在 x 前面添加一个常数 1）。
*   这样，决策函数变为 `f(x) = sign(θᵀx̃)`，更新规则简化为：如果误分类，则 `θ ← θ + y_t * x̃_t`。

![](img/223aea760bce52b872e46ca99b14c6fe_376.png)

![](img/223aea760bce52b872e46ca99b14c6fe_378.png)

![](img/223aea760bce52b872e46ca99b14c6fe_380.png)

![](img/223aea760bce52b872e46ca99b14c6fe_381.png)

![](img/223aea760bce52b872e46ca99b14c6fe_382.png)

![](img/223aea760bce52b872e46ca99b14c6fe_384.png)

![](img/223aea760bce52b872e46ca99b14c6fe_385.png)

![](img/223aea760bce52b872e46ca99b14c6fe_386.png)

![](img/223aea760bce52b872e46ca99b14c6fe_387.png)

## 算法的特性与讨论 💭

![](img/223aea760bce52b872e46ca99b14c6fe_388.png)

![](img/223aea760bce52b872e46ca99b14c6fe_390.png)

![](img/223aea760bce52b872e46ca99b14c6fe_392.png)

![](img/223aea760bce52b872e46ca99b14c6fe_394.png)

![](img/223aea760bce52b872e46ca99b14c6fe_395.png)

![](img/223aea760bce52b872e46ca99b14c6fe_396.png)

![](img/223aea760bce52b872e46ca99b14c6fe_397.png)

![](img/223aea760bce52b872e46ca99b14c6fe_399.png)

### 关于过拟合的思考

![](img/223aea760bce52b872e46ca99b14c6fe_401.png)

![](img/223aea760bce52b872e46ca99b14c6fe_402.png)

![](img/223aea760bce52b872e46ca99b14c6fe_403.png)

![](img/223aea760bce52b872e46ca99b14c6fe_404.png)

![](img/223aea760bce52b872e46ca99b14c6fe_405.png)

![](img/223aea760bce52b872e46ca99b14c6fe_406.png)

![](img/223aea760bce52b872e46ca99b14c6fe_407.png)

![](img/223aea760bce52b872e46ca99b14c6fe_408.png)

![](img/223aea760bce52b872e46ca99b14c6fe_409.png)

![](img/223aea760bce52b872e46ca99b14c6fe_411.png)

![](img/223aea760bce52b872e46ca99b14c6fe_412.png)

![](img/223aea760bce52b872e46ca99b14c6fe_413.png)

![](img/223aea760bce52b872e46ca99b14c6fe_415.png)

**问题**：感知机算法超参数很少，这是否意味着它不容易过拟合？
**讨论**：感知机学习的是线性决策边界，其模型复杂度本身较低，这在一定程度上提供了对过拟合的抵抗力。然而，它仍然是在拟合训练数据。在在线学习中，如果数据顺序有偏，或者算法对近期错误反应过度，仍然可能导致学到的边界不是最优的，这可以看作是一种对数据顺序的“过拟合”。

![](img/223aea760bce52b872e46ca99b14c6fe_417.png)

![](img/223aea760bce52b872e46ca99b14c6fe_419.png)

![](img/223aea760bce52b872e46ca99b14c6fe_420.png)

![](img/223aea760bce52b872e46ca99b14c6fe_421.png)

![](img/223aea760bce52b872e46ca99b14c6fe_423.png)

![](img/223aea760bce52b872e46ca99b14c6fe_425.png)

![](img/223aea760bce52b872e46ca99b14c6fe_426.png)

### 感知机的假设

![](img/223aea760bce52b872e46ca99b14c6fe_428.png)

![](img/223aea760bce52b872e46ca99b14c6fe_430.png)

![](img/223aea760bce52b872e46ca99b14c6fe_432.png)

感知机算法隐含了一些假设：
1.  **真实决策边界是线性的**（在所用特征空间中）。
2.  **最近的错误比过去的错误更重要**（更新只针对当前错误）。
3.  **数据顺序会影响最终结果**（不同的数据出现顺序可能导致不同的决策边界）。

![](img/223aea760bce52b872e46ca99b14c6fe_434.png)

![](img/223aea760bce52b872e46ca99b14c6fe_436.png)

![](img/223aea760bce52b872e46ca99b14c6fe_437.png)

![](img/223aea760bce52b872e46ca99b14c6fe_438.png)

### 批量学习设置下的感知机

![](img/223aea760bce52b872e46ca99b14c6fe_440.png)

![](img/223aea760bce52b872e46ca99b14c6fe_442.png)

![](img/223aea760bce52b872e46ca99b14c6fe_443.png)

![](img/223aea760bce52b872e46ca99b14c6fe_445.png)

感知机也可以应用于传统的批量学习：
1.  将全部 N 个数据点随机排列。
2.  重复以下过程直至**收敛**：
    *   按顺序遍历每个数据点 (**x_i**, y_i)。
    *   使用在线更新规则（如果误分类就更新参数）。
3.  **收敛条件**可能包括：一次完整遍历后没有发生任何错误；验证集错误率不再下降；权重向量的变化小于某个阈值等。

![](img/223aea760bce52b872e46ca99b14c6fe_446.png)

![](img/223aea760bce52b872e46ca99b14c6fe_447.png)

![](img/223aea760bce52b872e46ca99b14c6fe_449.png)

![](img/223aea760bce52b872e46ca99b14c6fe_450.png)

![](img/223aea760bce52b872e46ca99b14c6fe_452.png)

![](img/223aea760bce52b872e46ca99b14c6fe_454.png)

![](img/223aea760bce52b872e46ca99b14c6fe_455.png)

### 权重向量的表示定理

![](img/223aea760bce52b872e46ca99b14c6fe_457.png)

![](img/223aea760bce52b872e46ca99b14c6fe_459.png)

![](img/223aea760bce52b872e46ca99b14c6fe_461.png)

![](img/223aea760bce52b872e46ca99b14c6fe_462.png)

一个有趣的性质是，在算法收敛后，最终的权重向量 **w** 可以表示为训练数据点的线性组合：
`w = Σ_{i=1}^{N} c_i * y_i * x_i`
其中，系数 c_i 是非负整数，代表数据点 **x_i** 被误分类的次数。这表明模型的预测只依赖于新数据点与训练数据点之间的**点积**，这一性质是后续“核方法”的基础。

![](img/223aea760bce52b872e46ca99b14c6fe_464.png)

![](img/223aea760bce52b872e46ca99b14c6fe_466.png)

![](img/223aea760bce52b872e46ca99b14c6fe_467.png)

![](img/223aea760bce52b872e46ca99b14c6fe_469.png)

## 理论保证：感知机的错误上界 ⚖️

![](img/223aea760bce52b872e46ca99b14c6fe_471.png)

![](img/223aea760bce52b872e46ca99b14c6fe_473.png)

![](img/223aea760bce52b872e46ca99b14c6fe_475.png)

![](img/223aea760bce52b872e46ca99b14c6fe_477.png)

对于简单的模型，我们常常可以给出理论性能保证。对于感知机，有一个著名的**错误上界定理**。

![](img/223aea760bce52b872e46ca99b14c6fe_479.png)

![](img/223aea760bce52b872e46ca99b14c6fe_480.png)

![](img/223aea760bce52b872e46ca99b14c6fe_482.png)

**定义**：
*   **线性可分**：存在一个超平面能够完美分开所有数据点。
*   **间隔（Margin）γ**：在所有能完美分类数据的超平面中，找到那个距离最近数据点最远的超平面，这个距离就是该数据集的间隔 γ。
*   **数据范围 R**：所有数据点都位于一个半径为 R 的超球体内（即对于所有 **x**，有 `||x|| ≤ R`）。

![](img/223aea760bce52b872e46ca99b14c6fe_484.png)

![](img/223aea760bce52b872e46ca99b14c6fe_485.png)

![](img/223aea760bce52b872e46ca99b14c6fe_486.png)

![](img/223aea760bce52b872e46ca99b14c6fe_487.png)

![](img/223aea760bce52b872e46ca99b14c6fe_489.png)

![](img/223aea760bce52b872e46ca99b14c6fe_491.png)

**定理**：如果在线学习算法接收到的数据是线性可分的，且具有间隔 γ，数据范围受限于 R，那么感知机算法在整个学习过程中犯的错误总数最多为 `(R / γ)²`。

![](img/223aea760bce52b872e46ca99b14c6fe_493.png)

![](img/223aea760bce52b872e46ca99b14c6fe_495.png)

![](img/223aea760bce52b872e46ca99b14c6fe_497.png)

![](img/223aea760bce52b872e46ca99b14c6fe_499.png)

![](img/223aea760bce52b872e46ca99b14c6fe_500.png)

![](img/223aea760bce52b872e46ca99b14c6fe_501.png)

**意义**：
*   在批量学习中，只要训练数据线性可分，感知机保证在有限步内收敛到一个完美分类器。
*   间隔 γ 越大（数据点离边界越远），算法犯的错误越少，收敛越快。
*   这为算法的有效性提供了数学上的保证。

![](img/223aea760bce52b872e46ca99b14c6fe_502.png)

![](img/223aea760bce52b872e46ca99b14c6fe_504.png)

![](img/223aea760bce52b872e46ca99b14c6fe_506.png)

![](img/223aea760bce52b872e46ca99b14c6fe_507.png)

![](img/223aea760bce52b872e46ca99b14c6fe_509.png)

### 附录：点到超平面的距离公式 📏

给定超平面定义为 `wᵀx + b = 0`（其中 **w** 是法向量），点 **x₀** 到该超平面的距离为：
`distance = |wᵀx₀ + b| / ||w||`
数据集的间隔 γ 就是所有数据点到“最优”分离超平面距离中的最小值。

![](img/223aea760bce52b872e46ca99b14c6fe_511.png)

![](img/223aea760bce52b872e46ca99b14c6fe_512.png)

![](img/223aea760bce52b872e46ca99b14c6fe_513.png)

## 总结 🎯

![](img/223aea760bce52b872e46ca99b14c6fe_515.png)

![](img/223aea760bce52b872e46ca99b14c6fe_517.png)

![](img/223aea760bce52b872e46ca99b14c6fe_518.png)

![](img/223aea760bce52b872e46ca99b14c6fe_519.png)

本节课我们一起学习了：
1.  **感知机模型**：一种基于线性决策边界 `sign(wᵀx + b)` 的简单二分类器。
2.  **在线学习范式**：数据以流式方式到达，模型在每次预测错误后立即更新，旨在最小化累计错误。
3.  **感知机学习算法**：通过初始化参数为0，然后在每次误分类时，将参数向误分类点方向（根据其标签）更新的简单规则来学习。
4.  **算法的性质与假设**：包括其对线性可分性的依赖、对近期错误的侧重，以及数据顺序的影响。
5.  **理论错误上界**：对于线性可分且具有间隔 γ 的数据，感知机犯的错误总数有明确的上限 `(R/γ)²`，这保证了其在理想条件下的收敛性。

![](img/223aea760bce52b872e46ca99b14c6fe_521.png)

![](img/223aea760bce52b872e46ca99b14c6fe_523.png)

![](img/223aea760bce52b872e46ca99b14c6fe_524.png)

![](img/223aea760bce52b872e46ca99b14c6fe_525.png)

![](img/223aea760bce52b872e46ca99b14c6fe_526.png)

感知机是神经网络和支持向量机等更复杂模型的基础，理解它对于掌握机器学习核心概念至关重要。