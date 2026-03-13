# Python 参考

> [`chrispiech.github.io/probabilityForComputerScientists/en/intro/python/`](https://chrispiech.github.io/probabilityForComputerScientists/en/intro/python/)

* * *

### 阶乘

将 $n!$ 计算为整数。此示例计算 $20!$：

```py
import math
print(math.factorial(20))
```

### 选择

截至 Python 3.8，你可以从 math 模块中计算 $n \choose m$。此示例计算 $10 \choose 5$：

```py
import math
print(math.comb(10, 5))
```

### 自然指数

计算 $e^x$。例如，这计算 $e³$

```py
import math
print(math.exp(3))
```

* * *

## SciPy 统计库

SciPy 是一个基于 NumPy 的免费和开源的科学计算库。你可能发现使用 SciPy 来检查你在问题集的书面部分中获得的答案很有帮助。NumPy 有从许多常见分布中抽取样本的能力（在 python 解释器中输入 `help(np.random)`），但 SciPy 还具有计算观察事件概率的附加功能，并且可以直接在概率质量/密度函数上执行计算。

### 二项分布

创建一个二项分布随机变量 $X$ 并计算其概率质量函数（PMF）或累积密度函数（CDF）。我们非常喜欢 scipy 统计库，因为它定义了所有你可能会关心的随机变量函数，包括期望、方差，甚至我们在 CS109 中没有讨论过的，如熵。此示例声明 $X \sim \text{Bin}(n = 10, p = 0.2)$。然后计算 $X$ 的一些统计量。然后计算 $P(X = 3)$ 和 $P(X \leq 4)$。最后，它从 $X$ 中生成一些随机样本：

```py
from scipy import stats
X = stats.binom(10, 0.2) # Declare X to be a binomial random variable
print(X.pmf(3))           # P(X = 3)
print(X.cdf(4))           # P(X <= 4)
print(X.mean())           # E[X]
print(X.var())            # Var(X)
print(X.std())            # Std(X)
print(X.rvs())            # Get a random sample from X
print(X.rvs(10))          # Get 10 random samples form X
```

从一个**终端**，你总是可以使用“help”命令来查看一个变量（或包）上定义的所有方法的完整列表：

```py
from scipy import stats
X = stats.binom(10, 0.2) # Declare X to be a binomial random variable
help(X)                  # List all methods defined for X
```

### 泊松分布

创建一个泊松随机变量 $Y$。此示例声明 $Y \sim \text{Poi}(\lambda = 2)$。然后计算 $P(Y = 3)$：

```py
from scipy import stats
Y = stats.poisson(2)  # Declare Y to be a poisson random variable
print(Y.pmf(3))       # P(Y = 3)
print(Y.rvs())        # Get a random sample from Y
```

### 几何分布

创建一个几何随机变量 $X$，表示成功所需的试验次数。此示例声明 $X \sim \text{Geo}(p = 0.75)$：

```py
from scipy import stats
X = stats.geom(0.75)  # Declare X to be a geometric random variable
print(X.pmf(3))       # P(X = 3)
print(X.rvs())        # Get a random sample from Y
```

### 正态分布

创建一个正态分布随机变量 $A$。此示例声明 $A \sim N(\mu = 3, \sigma² = 16)$。然后计算 $f_Y(0)$ 和 $F_Y(0)$。**非常重要！！！** 在课堂上，正态分布的第二个参数是方差（$\sigma²$）。在 scipy 库中，第二个参数是标准差（$\sigma$）：

```py
import math
from scipy import stats
A = stats.norm(3, math.sqrt(16)) # Declare A to be a normal random variable
print(A.pdf(4))       			 # f(3), the probability density at 3
print(A.cdf(2))       			 # F(2), which is also P(Y < 2)
print(A.rvs())        			 # Get a random sample from A
```

### 指数分布

创建一个指数随机变量 $B$。此示例声明 $B \sim \text{Exp}(\lambda = 4)$：

```py
from scipy import stats
# `λ` is a common parameterization for the exponential,
#  but `scipy` uses `scale` which is `1/λ`
B = stats.expon(scale=1/4)
print(B.pdf(1))             # f(1), the probability density at 1
print(B.cdf(2))             # F(2) which is also P(B < 2)
print(B.rvs())              # Get a random sample from B
```

### Beta 分布

创建一个 Beta 随机变量 $X$。此示例声明 $X \sim \text{Beta}(\alpha = 1, \beta = 3)$：

```py
from scipy import stats
X = stats.beta(1, 3)  # Declare X to be a beta random variable
print(X.pdf(0.5))     # f(0.5), the probability density at 1
print(X.cdf(0.7))     # F(0.7) which is also P(X < 0.7)
print(X.rvs())        # Get a random sample from X
```
