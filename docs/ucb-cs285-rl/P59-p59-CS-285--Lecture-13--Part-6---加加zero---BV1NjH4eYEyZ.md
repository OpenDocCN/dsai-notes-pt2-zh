# P59：p59 CS 285： Lecture 13, Part 6 - 加加zero - BV1NjH4eYEyZ

好的，接下来我们将讨论的深度强化学习探索方法的最后一类是基于信息增益的方法。

![](img/90689b8a306b223de80c819076a7e599_1.png)

所以，当我们思考信息增益时，我们想要干的是，我们想要选择一个行动，这将导致一个观察，在预期中将给我们提供关于我们感兴趣的变量z的最多信息。



![](img/90689b8a306b223de80c819076a7e599_3.png)

当然，当我们实际实现这些算法时，我们需要回答的问题信息增益是关于什么，所以我们可以询问关于奖励函数的信息增益，但那不是很有用，如果我们有一个困难的探索问题，因为奖励可能在几乎任何地方都是零，所以这不好。

我们可以要求关于状态密度的信息增益，P(s)。

![](img/90689b8a306b223de80c819076a7e599_5.png)

这听起来有点奇怪，但实际上有些道理，因为关于状态密度的信息增益意味着你想要做那些会改变状态密度的事情，这意味着你会做新颖的事情。



![](img/90689b8a306b223de80c819076a7e599_7.png)

所以这回到了第一种方法的类别，所以这是一种有点奇怪的选择，但实际上它有点道理，另一种你可以做的事情是关于给定s的情况下，s'动态的信息增益。



![](img/90689b8a306b223de80c819076a7e599_9.png)

而且这是一种非常合理的选择，因为关于动态的信息增益表明你在学习关于mdp的东西。

![](img/90689b8a306b223de80c819076a7e599_11.png)

所以如果你假设mdp的奖励主要是稀疏的，意味着它大部分地方都是零，那么在那里主要的事情是要学习mdp的动态。



![](img/90689b8a306b223de80c819076a7e599_13.png)

因为mdp完全由初始状态决定，动态和奖励以及奖励并不提供信息，并且初始状态很容易确定。

![](img/90689b8a306b223de80c819076a7e599_15.png)

因此，你可以问关于动态的信息增益。

![](img/90689b8a306b223de80c819076a7e599_17.png)

因为那是变化最频繁且提供有用信号的东西，所以，这是一个学习mdp的好代理，尽管它还是一个启发式。

![](img/90689b8a306b223de80c819076a7e599_19.png)

现在，通常无法精确使用信息增益，无论你正在估计哪一个，如果你有一个大的状态空间或动作空间。

![](img/90689b8a306b223de80c819076a7e599_21.png)

所以，如果我们想要使用信息增益进行探索。

![](img/90689b8a306b223de80c819076a7e599_23.png)

我们必须做出某种形式的近似，"而且，使用这些方法时，许多技术复杂性确实在于近似性的本质。"。

![](img/90689b8a306b223de80c819076a7e599_25.png)

"你将要做的"，所以，有一些近似值，一种我们可以做出的近似是叫做预测增益的东西，"预测增益并不等于信息增益"，"但它可以被证明是对信息增益的一种粗糙近似"。



![](img/90689b8a306b223de80c819076a7e599_27.png)

"预测增益是s的log p theta与log之间的差值。"，"对数s的b'theta和对数s的p'theta"，"所以，如果你回想起关于伪计数的讲座"。

"Theta prime表示我们得到的密度模型的新参数"。

![](img/90689b8a306b223de80c819076a7e599_29.png)

在更新到最新的状态theta后，所以如果你仅仅比较那个新状态的对数概率，在更新它前后。

![](img/90689b8a306b223de80c819076a7e599_31.png)

这指的是被称为预测增益的东西，它是信息增益的近似。

![](img/90689b8a306b223de80c819076a7e599_33.png)

特别是关于状态密度的信息，所以这导致了一种算法，它可能稍微类似于那种伪计数方法，但实际上并不涉及明确尝试估计伪计数。



![](img/90689b8a306b223de80c819076a7e599_35.png)

所以直觉是如果密度变化很大，那么状态就非常新颖，另一种我们可以使用的近似方法是变分推断。

![](img/90689b8a306b223de80c819076a7e599_37.png)

接下来我将更详细地讨论这一点。

![](img/90689b8a306b223de80c819076a7e599_39.png)

这是从一篇叫做'精细'的论文中来的，所以一个有趣的观察是，信息增益可以等价地写成，作为p(z|y)和p(z)的KL散度。



![](img/90689b8a306b223de80c819076a7e599_41.png)

这听起来很有道理，因为如果p(z|y)非常类似于p(z)。

![](img/90689b8a306b223de80c819076a7e599_43.png)

那么你从观察y中学习到关于z的信息不多，而如果他们非常非常不同，那么你从观察y中学习到关于z的信息很多。



![](img/90689b8a306b223de80c819076a7e599_45.png)

所以实际上它们正是，它与KL散度完全等价。

![](img/90689b8a306b223de80c819076a7e599_47.png)

现在我们要学习动态学，所以z的数量是描述动态模型参数向量theta，所以我们有一些动态模型，P theta of s t plus one given s t a t。

使用我们在基于模型的RL讲座中讨论的任何技术。

![](img/90689b8a306b223de80c819076a7e599_49.png)

感兴趣的数量z是theta。

![](img/90689b8a306b223de80c819076a7e599_51.png)

观察y是过渡，它是一个元组，状态加一，我们即将问的问题很好，我们应该采取什么行动来获取最信息丰富的过渡。



![](img/90689b8a306b223de80c819076a7e599_53.png)

关于theta最信息丰富的过渡。

![](img/90689b8a306b223de80c819076a7e599_55.png)

所以我们想要的KL散度是下面的，我们想要最大化KL散度给定我们的历史p theta。

![](img/90689b8a306b223de80c819076a7e599_57.png)

给我们所看到的所有数据。

![](img/90689b8a306b223de80c819076a7e599_59.png)

和对于只有历史给定的theta的p的新过渡，所以h这里基本上表示我们的回放缓冲区，没有将这个新过渡添加到它中。



![](img/90689b8a306b223de80c819076a7e599_61.png)

并且θ知道模型参数，所以我们想要观察新过渡后的模式参数。

![](img/90689b8a306b223de80c819076a7e599_63.png)

与仅观察没有那个新过渡的历史时得到的模型参数有很大的不同。

![](img/90689b8a306b223de80c819076a7e599_65.png)

所以直觉是，一个过渡提供了更多的信息，如果它现在导致对θ的信念发生变化，这个问题的。

![](img/90689b8a306b223de80c819076a7e599_67.png)

当然，是估计参数后验，正如我们多次讨论过的，一般来说是不可解的，所以，如果θ代表神经网络的某个参数，那么我们通常无法得到θ的真实后验分布p(θ)。



![](img/90689b8a306b223de80c819076a7e599_69.png)

但我们可以得到它的近似值。

![](img/90689b8a306b223de80c819076a7e599_71.png)

所以，想法将是使用变分推断来估计某个近似后验分布，我们将其称为q(θ)，给定一些变分参数φ，我们将尝试使用这些参数来紧密地近似p(θ)给定h。



![](img/90689b8a306b223de80c819076a7e599_73.png)

然后，给定一个新的转换，将会更新变分参数φ以获取新的变分参数φ'。

![](img/90689b8a306b223de80c819076a7e599_75.png)

然后我们将比较这两个分布，所以我们将得到给定φ的θ近似后验q，大约等于给定h的θ概率p，然后，我们需要做的就是实际训练这个近似后验，我们将它训练以优化变分下界，这是由q。

Theta给定phi和p给定theta的h时的kl散度乘以p给定theta时的p给出的。

![](img/90689b8a306b223de80c819076a7e599_77.png)

所以这是通常的变分下界，如果你不，如果你不熟悉变分下界，不要紧，我们在后续的讲座中将详细讨论这些内容，但简短的版本是，给定φ，你将训练θ的q以接近θ的p。



![](img/90689b8a306b223de80c819076a7e599_79.png)

给定h和h，根据贝叶斯规则，实际上这相当于试图使p(h，θ)接近p(h)，这因子化为p(h|θ)乘以p(θ)，所以这是获取q的目标，现在我们如何很好地表示q，正如我们在基于模型的强化学习讲座中所讨论的。

我们可以通过产品的形式来表示参数分布的一个分布，例如独立的高斯分布。

![](img/90689b8a306b223de80c819076a7e599_81.png)

所以对于我们的参数向量中的每个数字，我们都有一个高斯分布，有一个均值和一个方差，并且phi代表均值。

![](img/90689b8a306b223de80c819076a7e599_83.png)

它也可能代表方差，但现在让我们只说它代表均值。

![](img/90689b8a306b223de80c819076a7e599_85.png)

所以这就是，这是我们在基于模型的强化学习讲座中的贝叶斯神经网络图片。

![](img/90689b8a306b223de80c819076a7e599_87.png)

所以给定d，theta的p就是所有参数值的乘积。

![](img/90689b8a306b223de80c819076a7e599_89.png)

的p of theta i given d，所以i这里索引到参数向量，所以参数v中的第一个数字是第二个。



![](img/90689b8a306b223de80c819076a7e599_91.png)

第三个，等等，并且每个那些嗯，独立的边际分布只是某个均值mu_i和某个方差。

![](img/90689b8a306b223de80c819076a7e599_93.png)

Sigma_i的高斯分布，这就是phi所指的，要么是仅均值，要么是均值和方差，如果我们只有均值，那么它的方差就是常数。



![](img/90689b8a306b223de80c819076a7e599_95.png)

好的，一种我们可能使用的非常简单的方法，我在基于模型的强化学习幻灯片中也提到了这种方法，这种方法在神经网络中被称为权重不确定性。



![](img/90689b8a306b223de80c819076a7e599_97.png)

那篇论文描述了一种算法叫做贝叶斯后传播，这是一种非常简单的贝叶斯神经网络变分推断方法，它使用重参数化技巧，好的，然后当我们被给予一个新的转换，逗号，一个逗号 s 的原子。



![](img/90689b8a306b223de80c819076a7e599_99.png)

我们将更新 phi 来得到 phi 的原子，所以我们将简单地取那个目标，即KL散度，然后我们将再次最小化它，将其与新的过渡附加到它。



![](img/90689b8a306b223de80c819076a7e599_101.png)

所以现在我们有两个 phi 参数，在看到过渡之前旧的一个。

![](img/90689b8a306b223de80c819076a7e599_103.png)

在看到过渡之后新的一个，它们两者都定义参数上的分布。

![](img/90689b8a306b223de80c819076a7e599_105.png)

这意味着我们可以计算它们之间的KL散度。

![](img/90689b8a306b223de80c819076a7e599_107.png)

所以当我们观察到一个新的过渡，我们更新贝叶斯神经网络的均值和方差。

![](img/90689b8a306b223de80c819076a7e599_109.png)

然后我们可以计算给定φ'的qθ与给定φ的qθ之间的KL散度。

![](img/90689b8a306b223de80c819076a7e599_111.png)

并将qθ给定φ作为近似奖励，高斯分布之间的KL散度有一个封闭形式的方程。

![](img/90689b8a306b223de80c819076a7e599_113.png)

所以我们只需要查找方程并插入它，直观上，这个方程将看起来很类似于均值的变化量。

![](img/90689b8a306b223de80c819076a7e599_115.png)

综上所述，我们最终得到的算法基本上只是更新我们的神经网络。

![](img/90689b8a306b223de80c819076a7e599_117.png)

在这种情况下，一个带有不确定性的贝叶斯神经网络。

![](img/90689b8a306b223de80c819076a7e599_119.png)

并使用参数变化的量作为信息增益的估计。

![](img/90689b8a306b223de80c819076a7e599_121.png)

然后我们将简单地将这个分配为那个转换的奖励，所以我们将分配一个奖励给转换，基于我们从中获得的信息量，就像在基于计数的方法中一样。



![](img/90689b8a306b223de80c819076a7e599_123.png)

我们将简单地构建一个新的奖励，R加上这个奖励，它有这个奖励添加到它中。

![](img/90689b8a306b223de80c819076a7e599_125.png)

![](img/90689b8a306b223de80c819076a7e599_126.png)

在论文中，嗯，他们描述了这种方法的工作效果如何，他们展示了一些评估，并表明实际上。

![](img/90689b8a306b223de80c819076a7e599_128.png)

添加这种信息增益奖励确实导致探索性能的一些显著提高，在广泛的强化学习任务中，近似信息增益的一个优点是，它确实提供了一个非常吸引人的数学形式，一个缺点是这些模型有些复杂。

你需要训练整个动力模型才能得到你的探索奖励。

![](img/90689b8a306b223de80c819076a7e599_130.png)

一般来说，使用这些东西的效果有些困难，所以如果你能估计密度，也许使用类似于伪计数的东西更容易，尽管这些方法有一些非常吸引人的理论形式，虽然卡莱散度可以被视为网络平均参数phi的变化。

如果我们忘记信息增益，有许多其他方法可以测量你的网络是如何变化的，所以这里我们有这种多样的贝叶斯方法，它实际上估计参数分布的分布，并测量分布变化的探索奖励，但如果我们忘记分布，只测量参数向量的变化。



![](img/90689b8a306b223de80c819076a7e599_132.png)

我们可以基本上恢复出与我们以前有过的基于错误的方法非常相似的东西。

![](img/90689b8a306b223de80c819076a7e599_134.png)

所以，例如。

![](img/90689b8a306b223de80c819076a7e599_136.png)

我们可以使用自编码器来编码我们的图像观察，在自编码器的潜在状态上构建预测模型。

![](img/90689b8a306b223de80c819076a7e599_138.png)

然后使用模型误差作为我们的探索奖励，此外，还有一些，与这相关的工作在这篇由施密特·胡伯等人撰写的论文中。



![](img/90689b8a306b223de80c819076a7e599_140.png)

你可以使用你的探索奖励来处理模型误差，以及模型梯度。

![](img/90689b8a306b223de80c819076a7e599_142.png)

等等，并且有许多其他变体，因此，一般来说，利用错误和模型作为探索奖励的想法是一种非常，非常深入研究的一种。



![](img/90689b8a306b223de80c819076a7e599_144.png)

往往它不是直接与信息增益绑定的，但有时候它是可以的。

![](img/90689b8a306b223de80c819076a7e599_146.png)

所以总结一下，我们在深度强化学习中讨论了不同类型的探索方法。

![](img/90689b8a306b223de80c819076a7e599_148.png)

我们讨论了乐观探索，比如使用计数和伪计数的探索。

![](img/90689b8a306b223de80c819076a7e599_150.png)

不同估计密度的模型，我们讨论了汤普森采样风格的算法。

![](img/90689b8a306b223de80c819076a7e599_152.png)

其中，你通过抽样来维护模型分布，例如，你可以维护一个关于q函数的分布，然后为每个episode采样一个不同的q函数。



![](img/90689b8a306b223de80c819076a7e599_154.png)

然后我们讨论了信息增益风格的算法，这些算法通常不可解。

![](img/90689b8a306b223de80c819076a7e599_156.png)

但你可以使用像变分近似的信息增益这样的东西，来实际上得到这类算法。

![](img/90689b8a306b223de80c819076a7e599_158.png)

如果你想了解更多关于这个材料的信息。

![](img/90689b8a306b223de80c819076a7e599_160.png)

所以这是施密特·胡伯的一个较旧的论文，称为实现好奇心和厌倦以及构建神经控制器的模型方法，嗯，这是一个有些宏伟的标题。



![](img/90689b8a306b223de80c819076a7e599_162.png)

这篇论文介绍了一些基于模型误差的有趣探索方法，这是另一篇使用模型误差的论文，利用深度预测模型激励探索和强化学习，这是一篇关于通过Bootstrap DQN进行后验采样的深度探索的论文。



![](img/90689b8a306b223de80c819076a7e599_164.png)

这是葡萄藤论文，这是一篇关于基于计数的探索的论文。

![](img/90689b8a306b223de80c819076a7e599_166.png)

基于伪计数的探索抱歉，这是一篇关于哈希的论文，这是我之前覆盖过的一篇旧论文。

![](img/90689b8a306b223de80c819076a7e599_168.png)

如果你想学习强化学习的探索。

![](img/90689b8a306b223de80c819076a7e599_170.png)