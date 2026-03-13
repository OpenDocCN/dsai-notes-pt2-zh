# 变量的独立性

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part3/independent_vars/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part3/independent_vars/)

* * *

## 离散型

两个离散随机变量 $X$ 和 $Y$ 被称为相互独立，如果：$$\begin{align*} \P(X=x,Y=y) = \P(X=x)\P(Y=y) \text{ 对于所有 } x,y \end{align*}$$ 直观地说：知道 $X$ 的值对我们了解 $Y$ 的分布没有任何帮助。如果两个变量不是独立的，它们被称为相关。这个概念在概念上与独立事件相似，但我们处理的是多个 *变量*。确保将事件和变量区分开来。

## 连续型

两个连续随机变量 $X$ 和 $Y$ 被称为相互独立，如果：$$\begin{align*} \P(X\leq a, Y \leq b) = \P(X \leq a)\P(Y \leq b) \text{ 对于所有 } a,b \end{align*}$$ 这可以使用累积分布函数（CDF）或概率密度函数（PDF）等价地陈述：$$\begin{align*} F_{X,Y}(a,b) &= F_{X}(a)F_{Y}(b) \text{ 对于所有 } a,b \\ f(X=x,Y=y) &= f(X=x)f(Y=y) \text{ 对于所有 } x,y \end{align*}$$ 更一般地，如果你可以分解联合密度函数，那么你的随机变量是独立的（或者对于离散随机变量的联合概率函数）：$$\begin{align*} &f(X=x,Y=y) = h(x)g(y) \\ &\P(X=x,Y=y) = h(x)g(y) \end{align*}$$

## 示例：展示独立性

设 $N$ 为每天对网络服务器的请求数，且 $N \sim \Poi(\lambda)$。每个请求以概率 $p$ 来自人类，以概率 $(1 – p)$ 来自“机器人”。定义 $X$ 为每天来自人类的请求数，$Y$ 为每天来自机器人的请求数。证明来自人类的请求数 $X$ 与来自机器人的请求数 $Y$ 是独立的。

由于请求是独立到达的，因此知道请求数量后 $X$ 的概率分布是一个二项分布。具体来说：$$\begin{align*} (X|N) &\sim \Bin(N,p)\\ (Y|N) &\sim \Bin(N, 1-p) \end{align*}$$ 要开始，我们首先需要写出 $X$ 和 $Y$ 的联合概率的表达式。为了做到这一点，我们使用链式法则：$$\begin{align*} \P(X=x,Y=y) = \P(X = x, Y=y|N = x+y)\P(N = x+y) \end{align*}$$ 我们可以计算这个表达式中的每一项。第一项是二项分布 $X|N$ 的概率质量函数，其中 $x$ 个“成功”。第二项是泊松分布 $N$ 取值为 $x+y$ 的概率：$$\begin{align*} &\P(X = x, Y=y|N = x+y) = { {x + y} \choose x}p^x(1-p)^y \\ &\P(N = x + y) = e^{-\lambda}\frac{\lambda^{x+y}}{(x+y)!} \end{align*}$$ 现在我们可以将这些放在一起，我们得到了联合概率的表达式：$$\begin{align*} &\P(X = x, Y=y) = { {x + y} \choose x}p^x(1-p)^y e^{-\lambda}\frac{\lambda^{x+y}}{(x+y)!} \end{align*}$$ 在这一点上，我们已经推导出 $X$ 和 $Y$ 的联合分布。为了证明这两个变量是独立的，我们需要能够分解联合概率：$$\begin{align*} \P&(X = x, Y=y) \\ &= { {x + y} \choose x}p^x(1-p)^y e^{-\lambda}\frac{\lambda^{x+y}}{(x+y)!} \\ &= \frac{(x+y)!}{x! \cdot y!} p^x(1-p)^y e^{-\lambda}\frac{\lambda^{x+y}}{(x+y)!} \\ &= \frac{1}{x! \cdot y!} p^x(1-p)^y e^{-\lambda}\lambda^{x+y} && \text{消去 (x+y)!} \\ &= \frac{p^x \cdot \lambda^x}{x!} \cdot \frac{(1-p)^y \cdot \lambda ^{y}}{y!} \cdot e^{-\lambda} && \text{重新排列} \\ \end{align*}$$ 因为联合概率可以分解为只包含 $x$ 的项和只包含 $y$ 的项，所以随机变量是独立的。

## 独立性的对称性

独立性是对称的。这意味着如果随机变量 $X$ 和 $Y$ 是独立的，那么 $X$ 与 $Y$ 独立，$Y$ 与 $X$ 也独立。这个说法可能看似无意义，但它可能非常有用。想象一个事件序列 $X_1,X_2, \dots$。令 $A_i$ 为事件 $X_i$ 是一个“记录值”（例如，它比所有之前的值都要大）。$A_{n+1}$ 是否与 $A_n$ 独立？回答 $A_n$ 与 $A_{n+1}$ 独立更容易。由于独立性的对称性，这两个说法都必须是正确的。

## 乘积的期望

**引理：独立随机变量的期望乘积**：

如果两个随机变量 $X$ 和 $Y$ 是独立的，那么它们的乘积的期望是各自期望的乘积。 $$\begin{align*} &E[X \cdot Y] = E[X] \cdot E[Y] && \text{如果 $X$ 和 $Y$ 是独立的}\\ &E[g(X)h(Y)] = E[g(X)]E[h(Y)] && \text{其中 $g$ 和 $h$ 是函数} \end{align*}$$ 注意，这假设 $X$ 和 $Y$ 是独立的。与这个规则的求和版本（随机变量和的期望是各自期望的和）进行对比，后者**不需要**随机变量是独立的。
