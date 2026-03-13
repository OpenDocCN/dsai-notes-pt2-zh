# 最大似然估计

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/part5/mle/`](https://chrispiech.github.io/probabilityForComputerScientists/en/part5/mle/)

* * *

我们用于估计参数的第一个算法被称为最大似然估计（MLE）。MLE 背后的核心思想是选择那些使观察到的数据最可能的参数（$\theta$）。

我们将要用来估计参数的数据将是 $n$ 个独立同分布（IID）的样本：$X_1, X_2, \dots X_n$。

## 似然

我们假设我们的数据是同分布的。这意味着它们必须有相同的概率质量函数（如果数据是离散的）或相同的概率密度函数（如果数据是连续的）。为了简化我们关于参数估计的讨论，我们将使用符号 $f(X=x|\Theta = \theta)$ 来指代这个共享的 PMF 或 PDF。我们的新符号有两个有趣之处。首先，我们现在已经包含了关于 $\theta$ 的条件，这是我们表示不同值 $X$ 的似然依赖于我们的参数值的方式。其次，我们将使用相同的符号 $f$ 来表示离散和连续分布。

似然是什么意思，它与“概率”有何不同？在离散分布的情况下，似然是数据概率质量或联合概率质量的同义词。在连续分布的情况下，似然指的是数据的概率密度。

由于我们假设每个数据点是独立的，因此我们所有数据的似然是每个数据点似然的乘积。从数学上讲，我们的数据给出参数 $\theta$ 的似然是：$$\begin{align*} L(\theta) = \prod_{i=1}^n f(X_i = x_i|\Theta = \theta) \end{align*}$$

对于不同的参数值，我们数据的似然将不同。如果我们有正确的参数，我们的数据将比我们有错误的参数时更有可能。因此，我们将似然写成参数（$\theta$）的函数。

## 最大化

在最大似然估计（MLE）中，我们的目标是选择参数（$\theta$）的值，以最大化上一节中的似然函数。我们将使用符号 $\hat{\theta}$ 来表示参数的最佳选择值。形式上，MLE 假设：$$\begin{align*} \hat{\theta} = \underset{\theta}{\operatorname{argmax }} \text{ }L(\theta) \end{align*}$$

Argmax 是“最大值之论证”的缩写。函数的 argmax 是函数在该域上最大化的值。这适用于任何维度的域。

argmax 的一个酷特性是，由于对数是一个单调函数，函数的 argmax 与其对数的 argmax 是相同的！这很好，因为对数使数学更简单。如果我们找到似然的对数的 argmax，它将等于似然的 argmax。因此，对于 MLE，我们首先写出对数似然函数（$LL$） $$\begin{align*} LL(\theta) &= \log L(\theta) \\ &= \log \prod_{i=1}^n f(X_i=x_i|\Theta = \theta) \\ &= \sum_{i=1}^n \log f(X_i = x_i|\Theta = \theta) \end{align*}$$

要使用最大似然估计器，首先写出给定参数的数据的对数似然。然后选择使对数似然函数最大化的参数值。argmax 可以通过多种方式计算。我们在这个课程中涵盖的所有方法都需要计算函数的第一导数。

## 二项式 MLE 估计

在我们的第一个例子中，我们将使用 MLE 来估计伯努利分布的 $p$ 参数。我们将基于 $n$ 个数据点进行估计，我们将这些数据点称为独立同分布（IID）随机变量 $X_1, X_2, \dots X_n$。这些随机变量中的每一个都被假定为来自相同的伯努利分布，具有相同的 $p$，$X_i \sim \text{Ber}(p)$。我们想找出那个 $p$ 是多少。

MLE 的第一步是将伯努利分布的似然写成我们可以最大化的函数。由于伯努利是一个离散分布，似然是概率质量函数。

伯努利 $X$ 的概率质量函数可以写成 $f(x) = p^{x}(1-p)^{1-x}$。哇！这是怎么回事？这是一个方程，它允许我们说 $X = 1$ 的概率是 $p$，而 $X = 0$ 的概率是 $1- p$。请你自己证明当 $X_i=0$ 和 $X_i=1$ 时，PMF 返回正确的概率。我们这样写 PMF 是因为它可导。

现在我们来进行一些 MLE 估计： $$\begin{align*} L(\theta) &= \prod_{i=1}^n p^{x_i}(1-p)^{1-x_i} && \text{首先写出似然函数} \\ LL(\theta) &= \sum_{i=1}^n \log p^{x_i}(1-p)^{1-x_i} && \text{然后写出对数似然函数}\\ &= \sum_{i=1}^n x_i (\log p) + (1 - x_i) log(1-p) \\ &= Y \log p + (n - Y) \log(1-p) && \text{其中 } Y = \sum_{i=1}^n x_i \end{align*}$$

天哪！我们得到了对数似然方程。现在我们只需要选择使我们的对数似然最大化的 $p$ 值。正如你的微积分老师可能教你的那样，找到使一个函数最大化的值的一种方法就是找到该函数的第一导数并将其设为 0。 $$\begin{align*} \frac{\delta LL(p)}{\delta p} &= Y \frac{1}{p} + (n - Y) \frac{-1}{1-p} = 0 \\ \hat{p} &= \frac{Y}{n} = \frac{\sum_{i=1}^n x_i}{n} \end{align*}$$

所有这些工作，结果发现最大似然估计（MLE）仅仅是样本均值...

## 正态 MLE 估计

实践是关键。接下来，我们将尝试估计正态分布的最佳参数值。我们所能访问的只有来自正态分布的 $n$ 个样本，我们将其称为独立同分布的随机变量 $X_1, X_2, \dots X_n$。我们假设对于所有 $i$，$X_i \sim N(\mu = \theta_0, \sigma² = \theta_1)$。这个例子似乎更复杂，因为正态分布有两个参数需要估计。在这种情况下，$\theta$ 是一个包含两个值的向量，第一个是均值（$\mu$）参数。第二个是方差（$\sigma²$）参数。 $$\begin{align*} L(\theta) &= \prod_{i=1}^n f(X_i|\theta) \\ &=\prod_{i=1}^n \frac{1}{\sqrt{2\pi\theta_1}} e^{-\frac{(x_i - \theta_0)²}{2\theta_1}} && \text{连续变量的似然是概率密度函数}\\ LL(\theta) &= \sum_{i=1}^n \log \frac{1}{\sqrt{2\pi\theta_1}} e^{-\frac{(x_i - \theta_0)²}{2\theta_1}} && \text{我们想要计算对数似然} \\ &= \sum_{i=1}^n\left[ - \log(\sqrt{2\pi\theta_1}) - \frac{1}{2\theta_1}(x_i - \theta_0)² \right] \end{align*}$$

再次，MLE 的最后一步是选择最大化对数似然函数的 $\theta$ 的值。在这种情况下，我们可以计算 $LL$ 函数相对于 $\theta_0$ 和 $\theta_1$ 的偏导数，将两个方程都设为等于 0，然后求解 $\theta$ 的值。这样做会导致最大化似然的 $\hat{\mu} = \hat{\theta_0}$ 和 $\hat{\sigma²} = \hat{\theta_1}$ 的值。结果是：$\hat{\mu} = \frac{1}{n}\sum_{i=1}^n x_i$ 和 $\hat{\sigma²} = \frac{1}{n}\sum_{i=1}^n (x_i - \hat{\mu})²$。

## 线性变换加噪声

最大似然估计（MLE）是一种可以用于任何具有可导似然函数的概率模型的算法。以一个例子来说，让我们估计一个模型中的参数 $\theta$，其中存在一个随机变量 $Y$，使得 $Y = \theta X + Z$，$Z \sim N(0, \sigma²)$，而 $X$ 是一个未知的分布。

在你被告知 $X$ 的值的情况下，$\theta X$ 是一个数字，而 $\theta X + Z$ 是高斯分布和一个数字的和。这意味着 $Y|X \sim N(\theta X, \sigma²)$。我们的目标是选择一个 $\theta$ 的值，以最大化独立同分布的概率：$(X_1, Y_1), (X_2, Y_2), \dots (X_n, Y_n)$。

我们通过首先找到给定 $\theta$ 的数据的对数似然函数来解决这个问题。然后我们找到最大化对数似然函数的 $\theta$ 的值。首先，使用正态分布的概率密度函数来表达 $Y|X,\theta$ 的概率：$$\begin{align*} f(Y_i | X_i , \theta) = \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{(Y_i - \theta X_i)²}{2\sigma²}} \end{align*}$$

现在我们已经准备好编写似然函数，然后取其对数得到对数似然函数：$$\begin{align*} L(\theta) &= \prod_{i=1}^n f(Y_i, X_i | \theta) && \text{让我们分解这个联合函数}\\ &= \prod_{i=1}^n f(Y_i | X_i, \theta)f(X_i ) && f(X_i) \text{ 与 } \theta \text{ 独立}\\ &= \prod_{i=1}^n\frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{(Y_i - \theta X_i)²}{2\sigma²}}f(X_i) &&\text{代入 }f(Y_i | X_i) \text{ 的定义} \end{align*}$$ $$\begin{align*} LL(\theta) &= \log L(\theta) \\ &= \log \prod_{i=1}^n \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{(Y_i - \theta X_i)²}{2\sigma²}} f(X_i) &&\text{代入 }L(\theta)\\ &= \sum_{i=1}^n \log \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{(Y_i - \theta X_i)²}{2\sigma²}} + \sum_{i=1}^n \log f(X_i) &&\text{乘积的对数是各对数之和}\\ &=n \log \frac{1}{\sqrt{2\pi}\sigma} - \frac{1}{2\sigma²} \sum_{i=1}^n (Y_i - \theta X_i)² + \sum_{i=1}^n \log f(X_i ) \end{align*}$$

移除常数乘数和不含 $\theta$ 的项。我们剩下的是尝试找到一个 $\theta$ 的值，使得最大化：$$\begin{align*} \hat{\theta} &= \underset{\theta}{\operatorname{argmax}} - \sum_{i=1}^m (Y_i - \theta X_i)²\\ &= \underset{\theta}{\operatorname{argmin}} \sum_{i=1}^m (Y_i - \theta X_i)² \end{align*}$$

这个结果说明，使数据最可能的 $\theta$ 值是使 $Y$ 的预测平方误差最小化的值。我们将在几天后看到，这是线性回归的基础。
