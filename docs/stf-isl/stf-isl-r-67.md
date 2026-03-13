# R 版 67：非线性支持向量机 📊

在本节课中，我们将学习如何应用非线性支持向量机。上一节我们介绍了线性支持向量机，本节中我们来看看当决策边界为非线性时，如何使用核函数来拟合模型。

## 概述

本节课我们将通过一个二维非线性决策边界的经典示例，演示如何使用核支持向量机。我们将加载模拟数据，拟合模型，并可视化其非线性决策边界。

## 加载数据

首先，我们从《统计学习基础》一书的网站加载示例数据。这些数据是模拟生成的混合数据。

```r
# 从URL加载数据
load(url("http://www-stat.stanford.edu/~tibs/ElemStatLearn/datasets/ESL.mixture.rda"))
```

数据加载后，我们可以查看其结构。这是一个列表，包含多个组件。目前，我们主要关注训练数据 `x` 和 `y`。

```r
# 查看数据结构
names(ESL.mixture)
```

为了避免与之前示例中的变量名冲突，我们先清除旧变量，然后附加这个数据列表。

```r
# 清除旧变量并附加新数据
rm(x, y)
attach(ESL.mixture)
```

## 数据可视化

让我们先绘制数据以观察其分布。数据是二维的，看起来有相当程度的重叠，但其结构具有特殊性。

```r
# 绘制数据点
plot(x, col = ifelse(y == 1, "red", "blue"), pch = 19,
     xlab = "X1", ylab = "X2", main = "混合数据散点图")
```

## 拟合非线性支持向量机

接下来，我们创建一个数据框，将响应变量 `y` 转换为因子，然后使用径向基核函数拟合支持向量机。这里我们将成本参数设为5，并且不缩放数据。

```r
# 创建数据框并拟合SVM
library(e1071)
dat <- data.frame(x, y = as.factor(y))
svmfit <- svm(y ~ ., data = dat, kernel = "radial", cost = 5, scale = FALSE)
```

## 创建预测网格并进行预测

这些数据本身提供了用于绘图的网格点变量 `px1` 和 `px2`。我们直接使用它们来创建网格，并在网格上进行预测。

```r
# 使用数据自带的网格点
grid <- expand.grid(X1 = px1, X2 = px2)
# 在网格上进行分类预测
pred.grid <- predict(svmfit, newdata = grid)
```

## 绘制决策区域

现在，我们绘制决策区域，并根据预测结果对区域进行着色，同时将原始数据点叠加在图上。

```r
# 绘制决策区域
plot(grid, col = ifelse(pred.grid == 1, "indianred", "lightblue"), pch = 20, cex = 0.2,
     xlab = "X1", ylab = "X2", main = "非线性SVM决策边界")
# 叠加原始数据点
points(x, col = ifelse(y == 1, "red", "blue"), pch = 19)
```

可以看到，决策边界是非线性的，红色区域主要在上方，黑色区域在下方。数据点分布与决策边界基本吻合。

## 绘制决策边界曲线

为了更清晰地展示决策边界，我们将使用等高线函数 `contour` 来绘制边界线。首先，我们需要获取模型在网格点上的决策函数值（而不仅仅是分类标签）。

```r
# 预测决策函数值（f(x)）
pred.func <- predict(svmfit, newdata = grid, decision.values = TRUE)
# 提取决策值
func.values <- attributes(pred.func)$decision.values
# 将决策值重塑为矩阵，以便绘制等高线
func.matrix <- matrix(func.values, length(px1), length(px2))
```

现在，我们在同一张图上绘制数据点、SVM学习到的决策边界（决策函数值为0的等高线）以及真实的贝叶斯决策边界（概率为0.5的等高线）。

```r
# 重新绘制基础图（决策区域）
plot(grid, col = ifelse(pred.grid == 1, "indianred", "lightblue"), pch = 20, cex = 0.2,
     xlab = "X1", ylab = "X2", main = "带决策边界的非线性SVM")
points(x, col = ifelse(y == 1, "red", "blue"), pch = 19)

# 添加SVM学习到的决策边界（f(x)=0）
contour(px1, px2, func.matrix, levels = 0, lwd = 2, col = "purple", add = TRUE, drawlabels = FALSE)

# 添加真实的贝叶斯决策边界（Prob=0.5）
contour(px1, px2, prob, levels = 0.5, lwd = 2, lty = 2, col = "black", add = TRUE, drawlabels = FALSE)

# 添加图例
legend("topright", legend = c("SVM边界", "贝叶斯边界"),
       col = c("purple", "black"), lty = c(1, 2), lwd = 2)
```

我们的非线性支持向量机学习到的边界（紫色实线）已经非常接近真实的贝叶斯最优决策边界（黑色虚线），尤其是在数据密集的区域。

## 生成可复现的报告

与之前一样，我们使用R Markdown将文本和代码混合编写。完成所有分析后，可以使用 `knit` 函数运行所有代码，生成一个包含所有图表和结果的精美网页文档，便于分享和展示。

```r
# 在R Markdown环境中，使用以下代码块生成最终报告
# ```{r}
# knitr::knit("your_file.Rmd")
# ```
```

## 总结

本节课中我们一起学习了非线性支持向量机的应用。我们通过一个二维示例，演示了如何：
1.  使用径向基核函数拟合非线性SVM模型。
2.  利用 `contour` 函数可视化复杂的非线性决策边界。
3.  将模型学习到的边界与真实的贝叶斯最优边界进行比较。
4.  使用R Markdown创建可复现、可分享的分析报告。

通过核技巧，支持向量机能够有效地学习并表示高度非线性的决策边界，从而处理更复杂的分类问题。