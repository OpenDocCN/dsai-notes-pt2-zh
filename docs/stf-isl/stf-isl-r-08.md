# R 版 8：R语言入门教程 📊

![](img/e6d07f1378421995839b0f4ccb8eaca7_0.png)

在本节课中，我们将学习R语言的基础知识。R是一种功能强大的免费编程语言，特别适用于数据分析和统计建模。我们将从基本操作开始，逐步介绍向量、矩阵、数据框等核心概念，并学习如何生成数据、绘制图形以及读取外部数据。

---

![](img/e6d07f1378421995839b0f4ccb8eaca7_2.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_4.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_6.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_7.png)

## 向量操作

![](img/e6d07f1378421995839b0f4ccb8eaca7_9.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_11.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_12.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_14.png)

上一节我们介绍了R语言的基本环境，本节中我们来看看如何创建和操作向量。向量是R中最基本的数据结构，可以存储一系列数值。

![](img/e6d07f1378421995839b0f4ccb8eaca7_16.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_17.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_18.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_19.png)

以下是创建向量的几种方法：

![](img/e6d07f1378421995839b0f4ccb8eaca7_21.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_22.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_23.png)

*   `x <- c(1, 3, 2, 5, 4)`：使用`c()`函数将多个数值组合成一个向量。
*   `y <- seq(4, 10, by=3)`：使用`seq()`函数生成一个从4开始，步长为3，长度为3的序列。

我们可以对向量进行元素间的运算：

![](img/e6d07f1378421995839b0f4ccb8eaca7_25.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_27.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_28.png)

*   `x + y`：向量对应元素相加。
*   `x / y`：向量对应元素相除。
*   `x ^ y`：向量对应元素进行幂运算。

![](img/e6d07f1378421995839b0f4ccb8eaca7_30.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_31.png)

访问向量元素使用方括号`[]`：

![](img/e6d07f1378421995839b0f4ccb8eaca7_33.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_34.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_35.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_36.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_37.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_38.png)

*   `x[2]`：获取向量`x`的第二个元素。
*   `x[2:3]`：获取向量`x`的第二到第三个元素。
*   `x[-2]`：获取向量`x`中除第二个元素外的所有元素。
*   `x[c(-1, -2)]`：获取向量`x`中除第一和第二个元素外的所有元素。

![](img/e6d07f1378421995839b0f4ccb8eaca7_40.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_41.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_43.png)

在R中，标量被视为长度为1的向量。

![](img/e6d07f1378421995839b0f4ccb8eaca7_45.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_46.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_47.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_48.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_49.png)

---

![](img/e6d07f1378421995839b0f4ccb8eaca7_50.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_51.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_53.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_54.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_55.png)

## 矩阵操作

![](img/e6d07f1378421995839b0f4ccb8eaca7_57.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_58.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_60.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_62.png)

上一节我们学习了向量，本节中我们来看看矩阵。矩阵是二维数组，在R中通过`matrix()`函数创建。

![](img/e6d07f1378421995839b0f4ccb8eaca7_64.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_65.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_66.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_67.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_68.png)

以下是创建和操作矩阵的方法：

![](img/e6d07f1378421995839b0f4ccb8eaca7_70.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_72.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_73.png)

*   `z <- matrix(1:12, 4, 3)`：创建一个4行3列的矩阵，数据按列填充。
*   `z[3:4, 2:3]`：获取矩阵`z`的第3到4行、第2到3列的子矩阵。
*   `z[, 2:3]`：获取矩阵`z`的第2到3列的所有行。
*   `z[, 1, drop=FALSE]`：获取矩阵`z`的第一列，并保持其矩阵结构（不降维为向量）。
*   `dim(z)`：查询矩阵`z`的维度。

![](img/e6d07f1378421995839b0f4ccb8eaca7_74.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_76.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_77.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_78.png)

使用`ls()`命令可以查看当前工作环境中的所有变量。使用`rm()`命令可以删除指定变量，例如`rm(y)`。

![](img/e6d07f1378421995839b0f4ccb8eaca7_80.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_81.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_82.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_83.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_85.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_86.png)

---

![](img/e6d07f1378421995839b0f4ccb8eaca7_88.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_89.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_91.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_92.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_94.png)

## 数据生成与图形绘制

![](img/e6d07f1378421995839b0f4ccb8eaca7_96.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_97.png)

在统计分析中，经常需要生成模拟数据。R提供了丰富的随机数生成函数。

![](img/e6d07f1378421995839b0f4ccb8eaca7_99.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_100.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_101.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_103.png)

以下是生成随机数据和绘制图形的方法：

![](img/e6d07f1378421995839b0f4ccb8eaca7_105.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_106.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_107.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_109.png)

*   `x <- runif(50)`：生成50个在[0,1]区间内均匀分布的随机数。
*   `y <- rnorm(50)`：生成50个标准正态分布的随机数。
*   `plot(x, y)`：绘制`x`和`y`的散点图。

![](img/e6d07f1378421995839b0f4ccb8eaca7_110.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_112.png)

R的图形系统设计精良，可以轻松定制图形外观：

![](img/e6d07f1378421995839b0f4ccb8eaca7_114.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_115.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_116.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_118.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_119.png)

*   `plot(x, y, xlab="X轴标签", ylab="Y轴标签", main="图形标题", pch=20)`：绘制带标签和标题的散点图，并更改点的形状。
*   `par(mfrow=c(2,1))`：设置图形布局为2行1列。
*   `hist(y)`：绘制`y`的直方图。
*   `par(mfrow=c(1,1))`：将图形布局重置为1行1列。

![](img/e6d07f1378421995839b0f4ccb8eaca7_121.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_122.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_123.png)

---

![](img/e6d07f1378421995839b0f4ccb8eaca7_125.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_126.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_127.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_128.png)

## 读取与操作数据框

![](img/e6d07f1378421995839b0f4ccb8eaca7_129.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_130.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_131.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_132.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_134.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_136.png)

实际工作中，数据常存储在外部文件（如Excel）中。R可以方便地读取这些数据。

![](img/e6d07f1378421995839b0f4ccb8eaca7_138.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_140.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_142.png)

以下是读取和操作数据框的方法：

![](img/e6d07f1378421995839b0f4ccb8eaca7_144.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_145.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_146.png)

*   `auto <- read.csv("Auto.csv")`：读取名为“Auto.csv”的逗号分隔值文件。
*   `names(auto)`：查看数据框的列名（变量名）。
*   `dim(auto)`：查看数据框的维度（行数和列数）。
*   `class(auto)`：查看对象的类别，数据框的类别是`data.frame`。
*   `summary(auto)`：生成数据框中每个变量的摘要统计信息。

数据框类似于矩阵，但各列可以是不同类型的数据（如数值、因子）。可以通过`$`符号访问数据框的列：

![](img/e6d07f1378421995839b0f4ccb8eaca7_148.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_150.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_152.png)

*   `plot(auto$cylinders, auto$mpg)`：绘制`cylinders`列与`mpg`列的散点图。

![](img/e6d07f1378421995839b0f4ccb8eaca7_154.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_155.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_156.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_157.png)

为了更方便地访问数据框的列，可以使用`attach()`函数：

![](img/e6d07f1378421995839b0f4ccb8eaca7_159.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_160.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_162.png)

*   `attach(auto)`：将数据框`auto`添加到搜索路径，使其列名可直接作为变量使用。
*   `search()`：查看当前的搜索路径。
*   `plot(cylinders, mpg)`：直接使用变量名绘制图形，R会根据变量类型（此处`cylinders`为因子）自动选择图形类型（如箱线图）。

![](img/e6d07f1378421995839b0f4ccb8eaca7_164.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_165.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_166.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_167.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_169.png)

---

![](img/e6d07f1378421995839b0f4ccb8eaca7_171.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_173.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_175.png)

![](img/e6d07f1378421995839b0f4ccb8eaca7_177.png)

本节课中我们一起学习了R语言的基础操作。我们掌握了如何创建和操作向量与矩阵，学习了生成随机数据并绘制精美的图形，最后还实践了如何读取外部数据文件并使用数据框进行统计分析。这些技能是进行后续数据分析和统计建模的基石。