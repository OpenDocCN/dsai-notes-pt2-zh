# 随机数生成器和蒙特卡洛方法

> 原文：[`cs357.cs.illinois.edu/textbook/notes/random-monte-carlo.html`](https://cs357.cs.illinois.edu/textbook/notes/random-monte-carlo.html)

## 学习目标

+   理解随机数生成器的特性以及随机数生成器中期望的特性。

+   给出使用蒙特卡洛方法的例子。

+   描述蒙特卡洛方法的误差。

## 随机数生成器

***随机数生成器 (RNG)*** 是一种算法或方法，可以用来生成一组无法合理预测的数字序列。通常有两种主要的随机数生成方法：***真随机方法***和***伪随机方法***。真随机方法根据某些随机物理现象生成数字。例如，掷一个公平的骰子将生成 1 到 6 之间的真随机数。其他示例来源包括大气噪声和热噪声。伪随机方法使用计算算法生成看似随机的结果序列，实际上是可以预测和可重复的。

当使用伪随机方法时，由于计算机只能表示有限数量的数字，任何生成的序列最终都会重复。伪随机数生成器的**周期**定义为序列无重复前缀的最大长度。

### 随机数生成器的特性

随机数生成器具有以下特性：

+   *随机模式*：通过随机性的统计测试。

+   *效率*：执行速度快，存储需求小。

+   *长周期*：在重复之前尽可能长。

+   *可重复性*：如果以相同的初始条件启动，则会产生相同的序列。

+   *可移植性*：在不同的计算机上运行，并且能够在每个计算机上产生相同的序列。

### 线性同余生成器

一个***线性同余生成器*** (LCG) 是一种伪随机数生成器，其形式为：

$$ x_0 = \text{种子} $$$$ x_{n+1} = (a x_{n} + c) (\text{mod} \phantom{x} M) $$

其中$a$（乘数）和$c$（增量）是给定的整数，$x_0$被称为***种子***。LCG 的周期不能超过$M$（模数）。周期可能小于$M$，这取决于$a$和$c$的值。质量取决于$a$和$c$。

### LCG 的示例

下面是 Python 代码示例，展示了一个 LCG，它根据初始种子$1$生成数字$1,3,7,5,1,3,7,5,\dots$。为了遵循模式，我们将前一个数字翻倍，加$1$，然后对$10$取模，因此$a=2$，$c=1$，$M=10$。

```py
def lcg_gen_next(modulus: int, a: int, c: int, xk: int) -> int:
  """ Uses an LCG to generate a pseudo-random number.

  Args:
    modulus (int): the period of the LCG
    a (int): the multiplier
    c (int): the increment
    xk (int): the previously generated random number(or the seed)

  Returns:
    int: the next pseudo-random number, xk_p1 
  """ 
  xk_p1 = (a * xk + c) % modulus
  return xk_p1

x = 1 # initial seed M = 10 
a = 2
c = 1
for i in range(100):
  print(x)
  x = lcg_gen_next(M, a, c, x) 
```

## 随机变量

一个***随机变量*** $X$ 可以被视为一个函数，它将不可预测（随机）过程的输出映射到数值。如果你有先前的统计学经验，你可能会熟悉这个概念。

随机变量的例子包括：

+   明天我们会下多少雨？

+   我的黄油面包会正反面朝下吗？

我们没有确切的数字来表示这些随机过程，但我们可以通过[大数定律](https://en.wikipedia.org/wiki/Law_of_large_numbers)来近似随机变量的长期结果。

### 离散随机变量

每个***离散随机变量*** $X$ 可以取一个离散值 $x_i$，其概率为 $p_i$，对于 $i = 1,…m$，且 $\Sigma_{i=1}^m p_i = 1$（即可能值是可数的）。这与连续随机变量形成对比，连续随机变量的可能值是不可数的无限多。

#### 离散随机变量的期望值

离散随机变量的**期望值** $E(x)$ 定义为 $\Sigma_{i=1}^m p_i x_i$。这个概念可以被视为“平均结果”。

### 离散随机变量的例子：硬币投掷

考虑一个随机变量 $X$，它是硬币投掷的结果，可以是正面或反面。

$$ X=1\text{: 投掷为正面} $$$$ X=0\text{: 投掷为反面} $$

对于每一次投掷，$x_i$ 是 $0$ 或 $1$，并且每个 $x_i$ 的概率 $p_i=0.5$。

这个硬币投掷的期望值是多少？



**答案**

对于硬币投掷，期望值是 $ E(X) = 1 \cdot 0.5 + 0 \cdot 0.5 = 0.5$。

现在，假设我们投掷一枚“公平”的硬币 1000 次，并记录得到正面的次数。如果我们运行这个 $1000$ 次硬币投掷实验 $N$ 次（比如说 $N=100$），分布会是什么样子？



**答案**

每次进行 1000 次硬币投掷实验所记录的数字可能会接近期望值 $0.5$。进行实验 $N$ 次的结果将看起来像正态分布，大多数结果接近 $0.5$。这也被称为大数定律（当 $N$ 很大时）。

## Monte Carlo

***Monte Carlo 方法*** 是依赖于重复随机采样来近似所需量的算法。Monte Carlo 方法通常用于模拟以下类型的问题：

+   非确定性过程，

+   复杂的确定性系统和高维度的确定性问题（例如，非平凡函数的积分）。

Monte Carlo 最常见的一个应用是近似给定形状的面积/体积。例如，为了近似圆的面积，我们可以在圆周围的正方形区域内均匀地采样大量点。然后，我们检查哪些点在圆内，以得到圆内点的百分比 $p$。最后，我们将 $p$ 乘以正方形的面积来近似圆的面积。Monte Carlo 在这种情况下之所以有效，是因为：

1.  **均匀随机采样**意味着我们确保点在整个区域内分散并覆盖良好

1.  根据**大数定律**，随着样本数量的增加，平均面积值将收敛到真实面积值。因此，使用大量的样本可以提高我们的估计。

### Monte Carlo 积分

考虑使用蒙特卡洛方法估计积分 $I = \int_a^b f(x) dx$。设 $X$ 是在 $[a, b]$ 上均匀分布的随机变量。那么，$I = (b-a) \mathbb{E}[f(X)]$。使用蒙特卡洛方法并取 $n$ 个样本，我们估计的期望值是：

$$S_n = \frac{1}{n} \sum_i^n f(X_i)$$

因此，积分的近似值是：

$$ I_n = (b-a) \frac{1}{n} \sum_i^n f(X_i) $$

根据大数定律，当 $n \to \infty$ 时，样本平均值 $S_n$ 将收敛到期望值 $\mathbb{E}[f(X)]$。因此，当 $n \to \infty$ 时，$I_n \to \int_a^b f(x) dx$。

根据中心极限定理，当 $n \to \infty$ 时，

$$ \sqrt{n} (S_n - \mu) \to N(0, \sigma²) $$

其中 $N(0, \sigma²)$ 是正态分布；$\mu = \mathbb{E}[f(X)]$ 和 $\sigma² = Var[X]$。

### 错误/收敛性

设 $Z$ 是具有正态分布 $N(0, \sigma²)$ 的随机变量。那么蒙特卡洛估计的误差 $err = S_n - \mu$ 可以表示为

$$ err \to \frac{1}{\sqrt{n}} Z $$

当 $n \to \infty$ 时。

因此，蒙特卡洛方法的渐近行为是 $\mathcal{O}(\frac{1}{\sqrt{n}})$，其中 $n$ 是样本数量。

### 示例：应用蒙特卡洛

我们可以使用蒙特卡洛方法有效地近似复杂函数的定积分，这在高维空间中尤其有用，因为其他数值积分技术可能非常昂贵。以下是用 Python 代码近似函数 $f(x,y) = x+y$ 在域 $[x_{min}, x_{max}] \times [y_{min}, y_{max}]$ 上的积分的代码：

```py
import random

def f(x: float, y: float) -> float:
  """ Returns the value for function *f* at point (x, y).

  Args:
    x: float: the point x.
    y: float: the point y.

  Returns:
    float: f(x, y)
  """ 
  return x + y

# set x_min, x_max, y_min and y_max for integral interval total = 0.0

# n is the number of points used in Monte Carlo integration for i in range(n):
  x = random.uniform(x_min, x_max)
  y = random.uniform(y_min, y_max)
  total += f(x, y)

# estimated integral value est = (1.0/n * total)*((x_max-x_min)*(y_max-y_min)) 
```

## 复习问题

1.  什么是伪随机数生成器？

1.  好的随机数生成器的特性有哪些？

1.  与使用真正的随机数相比，伪随机数生成器的优缺点是什么？

1.  什么是线性同余发生器（LCG）？

1.  随机数生成器的种子是什么？

1.  随机数生成器会重复吗？它们是可复制的吗？

1.  蒙特卡洛方法是什么？它们是如何使用的？

1.  对于蒙特卡洛，误差与采样点数的关系如何？

1.  给定蒙特卡洛计算值和采样误差，对于不同数量的样本，你期望的采样误差是多少？

1.  对于一个小型示例问题，使用蒙特卡洛方法估计特定区域的面积。

1.  对于一个小型示例问题，使用蒙特卡洛方法估计函数的积分。

## 更新日志

+   2024 年 2 月 17 日：Bhargav Chandaka (bhargav9) — 对内容进行重大重组，以与幻灯片/视频中的内容相匹配

+   2018 年 1 月 25 日：Yu Meng (yumeng5) — 第一份完整草案

+   2018 年 1 月 25 日：Erin Carrier (ecarrie2) — 全文小修，增加复习问题

+   

查看剩余条目



    +   2018 年 1 月 17 日：Erin Carrier (ecarrie2) — 概述

## 作者

+   CS 357 课程工作人员
