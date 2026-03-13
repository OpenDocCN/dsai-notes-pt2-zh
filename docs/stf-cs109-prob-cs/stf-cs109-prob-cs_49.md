# 算法艺术

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/algorithmic_art/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/algorithmic_art/)

* * *

我们希望高效地生成概率艺术作品。我们将使用随机变量来制作一个充满非重叠圆的图片：

<canvas id="canvas" width="782" height="782"></canvas>

<btn id="regenerateButton" onclick="draw()" class="btn btn-primary btn-lg">重新生成</btn>

在我们的艺术作品中，圆的大小各不相同。具体来说，每个圆的**半径**是从帕累托分布（以下将进行描述）中抽取的。放置算法是贪婪的：我们抽取 1000 个圆的大小。按大小排序，从大到小。然后逐个遍历圆的大小，并依次放置圆。

要在画布上放置一个圆，我们抽取圆心的位置。x 和 y 坐标在画布的尺寸内均匀分布。一旦我们选择了一个潜在的位置，我们就检查是否与已经放置的圆发生碰撞。如果有碰撞，我们会继续尝试新的位置，直到找到一个没有碰撞的位置。

### 帕累托分布

**帕累托随机变量**

| 符号： | $X \sim \text{Pareto}(a)$ |
| --- | --- |
| 描述： | 长尾分布。大值很少见，小值很常见。 |
| 参数： | $a \ge 1$，形状参数 注意还有其他可选参数。请参阅 [维基百科](https://en.wikipedia.org/wiki/Pareto_distribution) |
| 支持： | $x \in [0, 1]$ |
| PDF 公式： | $$f(x) = \frac{1}{x^{a+1}}$$ |
| CDF 公式： | $$F(x) = 1- \frac{1}{x^a}$$ |

### 从帕累托分布中抽样

我们如何从帕累托分布中抽取样本？在 Python 中很简单：`stats.pareto.rvs(a)`，然而在 JavaScript 或其他语言中，可能不会那么透明。我们可以使用“逆变换抽样”。简单来说，就是选择一个在(0, 1)范围内的均匀随机变量，然后选择值$x$的赋值，使得$F(x)$等于随机选择的值。

\begin{aligned} y &= 1 - (\frac{1}{x})^\alpha \\ (\frac{1}{x})^\alpha &= 1 - y \\ \frac{1}{x} &= (1-y)^{\frac{1}{\alpha}} \\ x &= \frac{1}{(1-y)^{\frac{1}{\alpha}}} \end{aligned}
