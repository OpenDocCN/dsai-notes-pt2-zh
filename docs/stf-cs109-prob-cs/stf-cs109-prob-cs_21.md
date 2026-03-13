# 偶然

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/serendipity/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/serendipity/)

***

![图片](img/980c7c4993ba0a002f5fce8a52a31edd.png)“偶然”这个词来源于波斯童话故事《[三个幸运王子](https://en.wikipedia.org/wiki/The_Three_Princes_of_Serendip)》

### 问题

与朋友偶然相遇的概率是多少？想象你生活在一个拥有大量普通人口（例如，有 17,000 名学生的斯坦福大学）。人口中有一小部分是你的朋友。如果你从这个人口中看到一些人，你遇到至少一个朋友的机会有多大？假设从人口中看到每个人都是等可能的。

***

### 答案

你看到至少一个朋友的概率是：

### 术语

首先，让我们定义一些有用的术语：

$p$ = 总人口 = $s$ = 看到的人数 = $f$ = 朋友数量 =

***

### 方法

由于看到 $s$ 个人的每一种方式都是等可能的，我们可以使用“等可能事件”概率计算方法：

$P(E) = \frac{|E|}{|S|}$

其中 $S$ 是样本集（所有看到 $s$ 个人的方式）和 $E$ 是事件集（所有看到 $s$ 个人的方式，其中至少有一个人是朋友）。

解决这个问题的方法之一是直接计算你看到 1 个或更多朋友的所有方式。这很困难。你需要计算你看到正好一个朋友的方式，然后是正好两个朋友，以此类推。计算你没有看到朋友的方式要容易得多。如果我们能计算出看到零个朋友的概率，我们的答案就是那个数字减去 1。

***

### 没有看到朋友的概率

让样本空间 ($S$) 是你可以看到 $s$ 个人的方式集合。样本空间的大小是：总人口中选择看到的人数。

事件空间 ($E$) 是你可以看到没有朋友的方式集合。事件空间的大小是：非朋友的数量（即人口 - 朋友）中选择看到的人数。

因此，没有看到朋友的概率是：

$\text{prob(not seen)} = \frac{ \left( {\begin{array}{*{20}c} p - f \\ s \\ \end{array}} \right) } { \left( {\begin{array}{*{20}c} p \\ s \\ \end{array}} \right) } $

***

### 看到朋友的概率

现在，你看到至少一个朋友的概率是 1 减去你没有看到朋友的概率。

$\text{prob(seen)} = 1 - \frac{ \left( {\begin{array}{*{20}c} p - f \\ s \\ \end{array}} \right) } { \left( {\begin{array}{*{20}c} p \\ s \\ \end{array}} \right) } $

那等于

***

### 这不是令人惊讶的吗？
