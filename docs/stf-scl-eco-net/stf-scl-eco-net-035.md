#  035：第三周总结 📚

![](img/43bdc5ceee49db5af562cfcab4d2fad2_0.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_2.png)

在本节课中，我们将回顾第三周学习的核心内容，主要聚焦于增长随机网络模型、混合连接机制以及指数随机图模型。我们将探讨这些模型如何解释现实网络中观察到的度分布特性，特别是“厚尾”现象。



## 回顾增长随机网络模型

上一节我们介绍了随机网络的基本概念，本节中我们来看看增长随机网络模型。该模型不仅考虑了节点在不同时间“出生”的现实性，更重要的是引入了基于“年龄”的异质性。

![](img/43bdc5ceee49db5af562cfcab4d2fad2_4.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_5.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_6.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_7.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_8.png)

*   **核心机制**：较早出生的节点有更多机会积累连接，因此拥有更高的度；较晚出生的节点则相反。这导致了节点间度差异的增大。
*   **模型效果**：这种机制开始产生“厚尾”的度分布。当模型进一步极端化，引入**偏好连接**机制时——即新节点倾向于连接到已有连接数更多的节点——我们将得到极端的厚尾分布，即**幂律分布**。
*   **公式表示**：在偏好连接模型中，一个新节点连接到现有节点 `i` 的概率与该节点 `i` 的度 `k_i` 成正比，即 `P(连接到节点i) ∝ k_i`。

![](img/43bdc5ceee49db5af562cfcab4d2fad2_9.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_10.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_11.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_12.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_13.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_14.png)

这为我们理解现实网络中为何普遍存在非常厚的度分布尾部提供了思路。



![](img/43bdc5ceee49db5af562cfcab4d2fad2_15.png)

## 混合连接机制模型

然而，许多现实网络介于完全随机连接和完全偏好连接这两个极端之间。因此，我们研究了一些混合模型，允许节点在形成连接时采用多种策略。

以下是节点形成连接的两种基本方式：

![](img/43bdc5ceee49db5af562cfcab4d2fad2_17.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_18.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_19.png)

*   **随机连接**：以均匀概率随机选择网络中的节点进行连接。
*   **网络搜索连接**：通过已连接节点的邻居（即“朋友的朋友”）来发现并连接新节点。

![](img/43bdc5ceee49db5af562cfcab4d2fad2_20.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_21.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_22.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_23.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_24.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_25.png)

通过结合这两种过程，我们可以得到一系列介于两者之间的度分布。具体分布形态取决于随机连接和网络搜索连接在模型中的相对比重。这种混合模型使我们能够进行参数估计，以推断特定网络的形成机制。例如，有些网络更多地通过搜索形成，而另一些则不然。

![](img/43bdc5ceee49db5af562cfcab4d2fad2_26.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_27.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_28.png)

一个自然的例子是文献引用网络：当你进行文献检索时，你可能会随机发现一些文章，但当你找到一篇相关文章后，你很可能会搜索其参考文献列表来寻找其他相关文章。这种通过已找到文章去发现新文章的过程，正是引用网络中出现厚尾分布的一个重要原因，同时也导致了聚类等网络特征。



![](img/43bdc5ceee49db5af562cfcab4d2fad2_30.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_31.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_32.png)

## 指数随机图模型

![](img/43bdc5ceee49db5af562cfcab4d2fad2_34.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_35.png)

最后，我们讨论了另一类用于统计估计的模型：**指数随机图模型**。这类模型非常灵活，能够捕捉网络的多种特征。

![](img/43bdc5ceee49db5af562cfcab4d2fad2_36.png)

然而，ERGM在估计上面临挑战，主要困难在于计算网络出现的相对概率，因为可能的网络数量极其庞大。不过，已有新的技术被开发出来，例如直接在统计量空间进行操作的模型变体，这些方法可以更快地进行估计。未来可能会有新的软件出现，我们也有可能在练习中接触它们。



## 本周总结

![](img/43bdc5ceee49db5af562cfcab4d2fad2_38.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_39.png)

本节课中我们一起学习了不同的随机网络模型。我们了解了增长模型和偏好连接如何解释度分布的异质性与厚尾现象，探讨了结合随机与搜索的混合模型如何更贴合现实，并初步认识了用于统计推断的指数随机图模型及其挑战。

![](img/43bdc5ceee49db5af562cfcab4d2fad2_40.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_41.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_42.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_43.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_44.png)

![](img/43bdc5ceee49db5af562cfcab4d2fad2_45.png)

至此，我们对现有的各类随机网络模型及其解释力有了基本认识。接下来，我们将转向**策略模型**的研究，并最终探讨网络中的**行为模型**。