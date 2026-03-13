# 符号参考

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/intro/notation/`](https://chrispiech.github.io/probabilityForComputerScientists/en/intro/notation/)

* * *

### 核心概率

| 符号 | 含义 |
| --- | --- |
| $E$ | 大写字母可以表示事件 |
| $A$ | 有时它们表示集合 |
| $ | E | $ | 事件或集合的大小 |
| $E^C$ | 事件或集合的补集 |
| $EF$ | 事件的“与”（也称为交集） |
| $ E \and F$ | 事件的“与”（也称为交集） |
| $ E \cap F$ | 事件的“与”（也称为交集） |
| $ E \lor F$ | 事件的“或”（也称为并集） |
| $ E \cup F$ | 事件的“或”（也称为并集） |
| $\text{count}(E)$ | $E$ 发生的次数 |
| $\p(E)$ | 事件 $E$ 的概率 |
| $\p(E\vert F)$ | 在给定 $F$ 的条件下事件 $E$ 的条件概率 |
| $\p(E,F)$ | 事件 $E$ 和 $F$ 的概率 |
| $\p(E\vert F,G)$ | 在给定 $F$ 和 $G$ 的条件下事件 $E$ 的条件概率 |
| $n!$ | $n$ 的阶乘 |
| ${n \choose k}$ | 二项式系数 |
| ${n \choose {r_1,r_2,r_3} }$ | 多项式系数 |

### 随机变量

| 符号 | 含义 |
| --- | --- |
| $x$ | 小写字母表示常规变量 |
| $X$ | 大写字母用于表示随机变量 |
| $K$ | 大写 $K$ 保留用于常数 |
| $\E[X]$ | $X$ 的期望值 |
| $\Var(X)$ | $X$ 的方差 |
| $\p(X=x)$ | $X$ 在 $x$ 处的概率质量函数 (PMF) |
| $\p(x)$ | $X$ 在 $x$ 处的概率质量函数 (PMF) |
| $f(X=x)$ | $X$ 在 $x$ 处的概率密度函数 (PDF) |
| $f(x)$ | $X$ 在 $x$ 处的概率密度函数 (PDF) |
| $f(X=x,Y=y)$ | 联合概率密度 |
| $f(X=x\vert Y=y)$ | 条件概率密度 |
| $F_X(x)$ 或 $F(x)$ | $X$ 的累积分布函数 (CDF) |
| IID | 独立同分布 (Independent and Identically Distributed) |

### 参数分布

| 符号 | 含义 |
| --- | --- |
| $X \sim \Ber(p)$ | $X$ 是一个 Bernoulli 分布的随机变量 |
| $X \sim \Bin(n,p)$ | $X$ 是一个 Binomial 分布的随机变量 |
| $X \sim \Poi(p)$ | $X$ 是一个 Poisson 分布的随机变量 |
| $X \sim \Geo(p)$ | $X$ 是一个 Geometric 分布的随机变量 |
| $X \sim \NegBin(r, p)$ | $X$ 是一个 Negative Binomial 分布的随机变量 |
| $X \sim \Uni(a,b)$ | $X$ 是一个 Uniform 分布的随机变量 |
| $X \sim \Exp(\lambda)$ | $X$ 是一个 Exponential 分布的随机变量 |
| $X \sim \Beta(a,b)$ | $X$ 是一个 Beta 分布的随机变量 |
