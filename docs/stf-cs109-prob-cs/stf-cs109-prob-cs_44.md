# 近似计数

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/approximate_counting/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/approximate_counting/)

* * *

如果你想有一个可以计数到宇宙中原子数量的计数器，但只想用 8 位存储计数器，你将可以使用下面描述的神奇概率算法！在这个例子中，我们将展示 `stochastic_counter(4)` 的期望返回值，其中 `count` 被调用四次，实际上等于四。

```py
def stochastic_counter(true_count):
   n = -1
   for i in range(true_count):
       n += count(n) 
   return 2 ** n  # 2^n, aka 2 to the power of n

def count(n):
   # To return 1 you need n heads. Always returns 1 if n is <= 0
   for i in range(n):
       if not coin_flip():
           return 0
   return 1

def coin_flip():
   # returns true 50% of the time
   return random.random() < 0.5
```

设 $X$ 为在 \texttt{stochastic\_counter(4)} 结束时 $n$ 的值。注意，$X$ 不是一个二项分布，因为每个结果的概率都会变化。

设 $R$ 为函数的返回值。$R = 2^X$，这是 $X$ 的函数。使用无意识统计师定律 $$E[R] = \sum_{x} 2^x \cdot P(X=x)$$ 我们可以单独计算每个概率 $P(X=x)$。注意，前两次调用 count 总是返回 1。设 $H_i$ 为第 $i$ 次调用返回 1 的事件。设 $T_i$ 为第 $i$ 次调用返回 0 的事件。$X$ 不能小于 1，因为前两次调用 count 总是返回 1。$P(X=1) = P(T_3,T_4)$ \\ $P(X=2) = P(H_3,T_4) + P(T_3,H_4)$ \\ $P(X=3) = P(H_3, H_4)$

在第三次调用计数时，$n = 1$。如果 $H_3$，则第四次调用时 $n=2$，循环运行两次。 $$\begin{align*} P(H_3,T_4) &= P(H_3) \cdot P(T_4|H_3) \\ &= \frac{1}{2} \cdot ( \frac{1}{2} + \frac{1}{4}) \end{align*}$$ $$\begin{align*} P(H_3,H_4) &= P(H_3) \cdot P(H_4|H_3) \\ &= \frac{1}{2} \cdot \frac{1}{2} \end{align*}$$

如果 $T_3$，则第四次调用时 $n=1$。 $$\begin{align*} P(T_3,H_4) &= P(T_3) \cdot P(H_4|T_3) \\ &= \frac{1}{2} \cdot \frac{1}{2} \end{align*}$$ $$\begin{align*} P(T_3,T_4) &= P(T_3) \cdot P(T_4|T_3) \\ &= \frac{1}{2} \cdot \frac{1}{2} \end{align*}$$ 将所有内容代入： $$\begin{align*} E[R] &= \sum_{x=1}³ 2^x \cdot P(X=x) \\ &= 2 \cdot \frac{1}{4} + 4\cdot \frac{5}{8} + 8\cdot \frac{1}{8}\\ &= 4 \end{align*}$$
