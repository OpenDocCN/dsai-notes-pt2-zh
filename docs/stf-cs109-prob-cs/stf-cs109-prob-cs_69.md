# 贝叶斯病毒载量测试

> 原文：[`chrispiech.github.io/probabilityForComputerScientists/en/examples/bayesian_viral_load_test/`](https://chrispiech.github.io/probabilityForComputerScientists/en/examples/bayesian_viral_load_test/)

* * *

*2022 年秋季斯坦福期中考试问题*

我们将构建一个贝叶斯病毒载量测试，该测试更新关于患者病毒载量的信念分布。尽管病毒载量是连续的，但在我们的测试中，我们通过将数量离散化为 0 到 99 之间的整数来表示它，包括 99。病毒载量的单位是每百万样本中的病毒实例数。

如果一个人的病毒载量为 9（换句话说，每 1,000,000 个样本中有 9 个病毒），那么从这个人随机抽取的样本是病毒的概率是多少？

$$\frac{9}{1,000,000}$$

我们对一个患者进行 100,000 个样本的病毒测试。如果这个人的真实病毒载量为 9，那么在我们的 100,000 个样本中恰好有 1 个是病毒的概率是多少？使用计算效率高的近似值来计算你的答案。你的近似值应该尊重得到负病毒样本的概率为 0 的事实。

让我们定义一个随机变量$X$，表示在真实病毒载量为 9 的情况下，病毒样本的数量。问题是询问$P(X = 1)$。我们可以将其视为一个二项过程，其中试验次数$n$是样本数量，概率$p$是样本为病毒的概率。\[ n = 100,000, p = \frac{9}{1,000,000} \] 注意到$n$非常小，$p$非常大，因此我们可以使用泊松近似来近似我们的答案。我们发现$\lambda = np = 100,000 \cdot 9/1,000,000 = 0.9$，所以$X \sim \Poi(\lambda = 0.9)$。最后一步是使用泊松分布的 PMF。 \[ P(X = 1) = \frac{(0.9)¹ e^{-0.9}}{1!} \]

根据我们对患者（他们的症状和个人病史）的了解，我们在列表`prior`中编码了一个先验信念，其中`prior[i]`是病毒载量等于$i$的概率。`prior`的长度为 100，键为 0 到 99。

给出一个方程，表示在观察到 100,000 个测试样本中有 1 个病毒样本的情况下，真实病毒载量是$i$的更新概率。记住$0 \leq i \leq 99$。你可以使用近似值。

我们想要找到 \begin{equation} P(\text{病毒载量} = i | \text{观察到的计数} \frac{1}{100000}) \end{equation} 我们可以应用贝叶斯定理得到 \begin{equation}\label{eq:bayes} = \frac{P(\text{观察到的计数} \frac{1}{100000} | \text{病毒载量} = i)P(\text{病毒载量} = i)}{P(\text{观察到的计数} \frac{1}{100000})} \end{equation} 我们知道我们可以定义一个随机变量 $X \sim \text{观察到的计数 out of 100,000} | \text{病毒载量} = i$，并且我们可以将 $X$ 模型化为一个二项分布的泊松近似，其中 $n = 100000$ 和 $p = \frac{i}{1000000}$，有 \[ \lambda = np = 100000 \cdot \frac{i}{1000000} = \frac{i}{10} \] 所以 $X$ 可以写成 \[ X \sim Poi(\lambda = \frac{i}{10}) \] 现在，我们可以将我们的贝叶斯定理方程重写为 \[ = \frac{P(X = 1)P(\text{病毒载量} = i)}{P(\text{观察到的计数} \frac{1}{100000})} \] 现在，我们可以使用泊松概率质量函数和我们的给定 \texttt{先验} 来得到： \begin{equation} = \frac{\frac{\frac{i}{10}e^{\frac{-i}{10}}}{1!}\cdot \texttt{prior[i]}}{P(\text{观察到的计数} \frac{1}{100000})} \end{equation} 现在，我们需要展开我们的分母。我们可以使用全概率公式来展开 \[ P(\text{观察到的计数} \frac{1}{100000}) = \sum_{j = 0}^{99} P(\text{观察到的计数} \frac{1}{100000} | \text{病毒载量} = i)P(\text{病毒载量} = i) \] 我们可以将其重写为 \[ = \sum_{j = 0}^{99} \frac{\frac{j}{10}e^{\frac{-j}{10}}}{1!}\cdot \texttt{prior[j]} \] \[ = \sum_{j = 0}^{99} \frac{j}{10}e^{\frac{-j}{10}}\cdot \texttt{prior[j]} \] 最后，我们可以将这个结果代入得到 \[ \boxed{% \frac{ \frac{i}{10} e^{\frac{-i}{10}} \cdot \texttt{prior[i]}}{\sum_{j = 0}^{99} \frac{j}{10}e^{\frac{-j}{10}}\cdot \texttt{prior[j]}}% }].
