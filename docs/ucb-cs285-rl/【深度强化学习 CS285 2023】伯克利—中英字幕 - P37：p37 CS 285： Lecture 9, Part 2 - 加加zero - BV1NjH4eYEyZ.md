# 【深度强化学习 CS285 2023】伯克利—中英字幕 - P37：p37 CS 285： Lecture 9, Part 2 - 加加zero - BV1NjH4eYEyZ

好的，那么让我们谈谈我们可以在什么情况下使用p theta。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_1.png)

将p theta替换为st，st的导数，并且仍然有一个合理的目标，准确地近似新政策的回报。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_3.png)

所以，我们要总结我们要做的事情是，我们要忽略分布不匹配。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_5.png)

我们要使用st处的p theta，而不是st处的p theta prime。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_7.png)

使得在这个整个方程中，theta prime的唯一依赖只在权重上。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_9.png)

因为我们从我们的前一个政策梯度讲座中知道。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_11.png)

如果我们对右边的东西进行微分。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_13.png)

我们精确地得到了政策梯度，所以我们想要这是真的。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_15.png)

以便j theta prime减去j theta能被一个横杠很好地近似。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_17.png)

Theta prime是这个右侧的东西，以便我们可以仅仅最大化一个横杠并得到更好的新策略。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_19.png)

我们试图要证明的是，是p theta of st接近p theta prime of st。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_21.png)

当pi theta接近pi theta prime时，当这种情况发生时，则右侧近似左侧。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_23.png)

意味着它们之间的差异可以被一些量所限制。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_25.png)

这是小的，如果πθ和πθ'之间的差异小。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_27.png)

好的，所以我们感兴趣的就是这个，我们想要证明πθt接近πθ's st，抱歉p p θ s t接近p θ' of st，当πθ接近πθ'时。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_29.png)

所以让我们从简单的情况开始，首先假设πθ是一个确定性的策略，这意味着我们可以将其表示为t等于pi theta的s t。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_31.png)

我们将 later 将这个一般化到随机策略。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_33.png)

但我认为确定性的推导提供了一些直觉，这然后使随机情况更容易理解。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_35.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_36.png)

所以在这种情况下，我们试图要证明的是。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_38.png)

对于theta和theta prime的状态边缘，如果pi theta prime接近pi theta，那么theta prime和theta的状态边缘也将接近。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_40.png)

现在pi theta prime并不一定是确定性的。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_42.png)

我们定义'接近'的方式是，是pi theta prime分配给任何不是pi theta所分配的动作的概率，"派西塔将采取的行动小于或等于 epsilon"，本质上，πθ'做不同事情的概率是有限的。

所以如果这种情况属实，"然后，我们可以将时间步t处的θ'边缘状态写为两个术语的和"。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_44.png)

"第一个术语描述了从t时间步开始，直到所有步骤的情况"。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_46.png)

"新的π'政策与πθ政策做了同样的事情。"，"并且，由于做与一减epsilon完全相同的事情的概率"。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_48.png)

"这个术语有一个一减去 epsilon 的幂次方的乘数"。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_50.png)

在它前面，"并且状态边缘等于p theta st"。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_52.png)

"因为如果你做了和派西塔相同的事情"，"你的状态分布相同"，另一个术语就是所有其他的一切，"它是1减去1减去ε的t次方"，"并且它复制了一些其他状态分布"，"我们假设我们对此一无所知"。

所以我们把它叫做"p错误"，"这是你在各州得到的分布"，"如果你犯了至少一个错误"，"我们假设我们对此一无所知"。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_54.png)

所以，它可以像模仿学习讲座中的那个钢丝走者一样。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_56.png)

在课程开始的地方，where，如果你从钢丝上掉下来，你永远无法恢复，并且你在一个完全不同的地方。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_58.png)

所以，当然，我希望大多数你们能认出这个方程式，它是与我们之前在分析行为克隆时遇到的方程式完全相同的。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_60.png)

当我们分析行为克隆时。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_62.png)

And，实际上，我们的假设与以前有过的假设非常相似，嗯。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_64.png)

那就是新的政策偏离旧政策的概率是有限的。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_66.png)

所以这是我们没有犯错误的概率。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_68.png)

这是另一个我们完全不做假设的分布。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_70.png)

所以希望对所有人来说都看起来很熟悉。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_72.png)

就像以前那样，这个方程暗示我们可以将p theta'与p theta的总变异距离写为基本上只是不同的部分。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_74.png)

右。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_76.png)

因此，那个减去ε的t乘以pθ的数，st部分的总变分散度对pθ的st部分为零。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_78.png)

所以只有那个第二部分，并且那个第二部分有一个乘数为一减去一，减去ε的t在它前面。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_80.png)

并且这个乘数乘以p错误和pθ之间的总变分散度。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_82.png)

现在我们不能对这个总变分散度进行界限，因为p错误减去pθ。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_84.png)

因为我们对p错误没有假设，所以唯一的界限就是我们有的无意义的界限。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_86.png)

那就是任何总变异距离都必须小于或等于二。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_88.png)

这意味着状态边缘的总变异距离被两个倍数所限制。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_90.png)

一减一减epsilon到t。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_92.png)

这正好等于我们第二堂课中讨论的，就像我们在第二堂课中的模仿学习和分析中提到的。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_94.png)

我们使用相同的有用身份。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_96.png)

那就是一减epsilon到t大于，或等于一减epsilon乘以t，对于任何介于零和一的epsilon。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_98.png)

这允许我们将这个限制表达为一个量。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_100.png)

那就是线性在epsilon上，线性在t上，所以状态边缘的差异小于等于。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_102.png)

或者等于两个倍数的epsilon乘以t。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_104.png)

好的，所以这不是一个很好的界限，但它是一个界限，因为它表明随着epsilon的减小。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_106.png)

状态边缘将越来越相似于彼此，当然，这是关于确定性政策的所有内容，πθ一般情况。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_108.png)

πθ不会是确定性的，所以我们接下来要做的是。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_110.png)

我们将分析一般情况，其中πθ是一个任意的分布。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_112.png)

这个证明遵循信任区域政策优化论文的证明。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_114.png)

这是参考在幻灯片底部的，好的，所以这里，我们将说πθ'接近πθ。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_116.png)

如果他们的总变分距离对于所有状态s和t都被epsilon所限制。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_118.png)

实际上，我们发现我们并不需要这个界限是点wise的。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_120.png)

实际上，我们可以使用一个界限，这是一个期望，但我们现在暂时使用点wise的界限。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_122.png)

因为它更容易解释，但请记住。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_124.png)

这也将适用于，如果界限是无限的，嗯，点wise的意思是预期的总变分距离小于等于epsilon，好的。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_126.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_127.png)

所以对于这个分析，我们将使用的一个有用引理，是这个。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_129.png)

这个引理需要一些解包，我不会证明它。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_131.png)

这是之前的工作，但它在信任区域政策优化论文中被引用，位于底部，这个引理说，如果你有两个分布。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_133.png)

我将它们称为px和py。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_135.png)

并且这两个分布的总变分距离，意味着对于所有x值的和。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_137.png)

绝对值px(x)和py(x)的差等于epsilon，所以这两个分布的总变分距离等于epsilon，然后存在联合分布px， y。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_139.png)

所以，其边缘px是px(x)，边缘py是py(y)，x等于y的概率是1-epsilon，来解包一下这个引理一点。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_141.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_142.png)

这个说什么是，如果你有两个对同一变量的分布，我将它们称为px和py，并且这两个分布的总变分距离等于epsilon。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_144.png)

那么存在联合分布px， y，所以，其边缘px是px(x)，边缘py是py(y)，x等于y的概率是1-epsilon。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_146.png)

P(x)和p(y)关于x的分布差异为epsilon。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_148.png)

然后，你可以构造一个关于两个变量的联合分布。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_150.png)

这样，该联合分布的边际分布。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_152.png)

以其第一和第二个参数为依据，就是你开始时的两个分布。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_154.png)

并且其两个参数的概率相等为1-epsilon。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_156.png)

直觉上，这个引理对我们有用的原因，是因为我们实际上想要前一个幻灯片的假设的一般化。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_158.png)

所以在前一个幻灯片，我们的假设是存在一个1-epsilon。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_160.png)

πθ'与πθ采取相同行动的概率。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_162.png)

所以如果我们能表达出πθ'和πθ采取相同行动的概率。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_164.png)

当两者都是随机的时，那么我们就可以使用那个来从之前的幻灯片中一般化结果。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_166.png)

到政策是随机的情况，所以本质上这是说px(x)与py(y)的协议一致性的概率为ε。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_168.png)

并且，这意味着πθ'与πθ采取不同行动的概率最多为ε。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_170.png)

回过头来看，这实际上有点显而易见。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_172.png)

因为如果他们的总体变化差异如epsilon，并且总体变化差异是概率差异。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_174.png)

那么，它们在概率质量上的差异部分。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_176.png)

应该有epsilon的体积，所以如果你，如果你以一种更几何的方式来思考它。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_178.png)

就想象两个分布作为条形图重叠在它们上面。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_180.png)

并看条形图的差异，那些差异的体积将等于epsilon，这意味着你以epsilon做不同事情的概率。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_182.png)

所以这就是一种几何直觉，但如果你更喜欢用象征的方式来思考。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_184.png)

那么希望这个引理，嗯，能让你安心一些。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_186.png)

实际上，如果总变分距离是epsilon，并且错误的概率最多是epsilon。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_188.png)

所以这个引理允许我们做什么。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_190.png)

是它允许我们陈述与前一张幻灯片相同的结果。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_192.png)

总变分距离州边缘分布之间的差异等于一减去，一减去epsilon到t乘以p的错误减去p的theta现在。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_194.png)

我们可以说这一点，即使pi theta是随机的，只要pi theta prime和pi theta的总变分距离被epsilon所限制。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_196.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_197.png)

所以从这里一切都完全相同，我们可以写同样的界限。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_199.png)

我们可以说状态边缘分布最多相差两次epsilon，T，好的，所以本质上，我们在幻灯片上使用的技巧是使用这个性质。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_201.png)

以总方差来描述两个政策可能采取不同行动的概率。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_203.png)

差异。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_205.png)

好的，所以这是我们在状态边缘分布上的结果，所以这告诉我们关于实际目标值的什么，对，我们想要实际上是想要将两个以优势值表达的目标联系起来。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_207.png)

所以对于这一点，我将推导出另一个小计算，它描述了在分布下函数期望值的描述。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_209.png)

当那些分布的总变异差异被限制时。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_211.png)

所以我们将有一个关于st的函数f。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_213.png)

在我们的情况下，它是这个涉及到我们行动期望和优势值的复杂东西。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_215.png)

但它实际上并不重要，无论它被称为f(st)的东西是什么，我们可以将其期望值限制在两个分布之间。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_217.png)

所以我们可以写p' theta下s的期望值，T(f(st))作为p' theta对所有可能状态的和，乘以f。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_219.png)

并且我们知道这个量是大于。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_221.png)

或等于p theta对所有状态的和的f。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_223.png)

减去p theta和p theta prime的总变分距离乘以。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_225.png)

f可能取到的最大值，所以我到达这个计算的方式，是我将p theta prime写为等于p theta prime加上p theta减去b theta。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_227.png)

我分组术语得到p theta乘以f减去a，p theta减去p theta prime乘以f，虽然我不知道概率差异的绝对值。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_229.png)

我只限制总变分距离，如果我将它们乘以f的最大值，我正在尽可能地悲观，所以这就是让我能够写这个不等式的原因。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_231.png)

如果你不理解这个，那么我建议你现在暂停讲座，拿出一张纸，实际推导这个不等式你自己。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_233.png)

这是一个好做的练习，确保你理解如何操纵总变分距离。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_235.png)

所以如果这个不等式不理解，请拿出一张纸。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_237.png)

现在试着解决它，所以暂停讲座，做那个。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_239.png)

如果那里有困难，请在评论中提问。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_241.png)

然后在课堂上我们将更详细地讨论这个问题，好的，所以然后我们只需要，我们取第一个术语。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_243.png)

并注意到它只是p theta下期望值的定义，我们取第二个术语并用它来替换我们对总变异性分布的界限。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_245.png)

这意味着在p theta prime下f的期望值只是。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_247.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_248.png)

它被其下p theta的期望值所下界，减去一个误差项，它是两个 epsilon 乘以的，T 乘以 f 可以在其上取到的最大值。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_250.png)

现在，这个误差项可能看起来很大，因为你知道 f 的最大值可能非常大。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_252.png)

但记住，一切都被 epsilon 乘以，所以当两个政策越来越接近，epsilon 越来越小时。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_254.png)

那个第二个项总是可以被使得很小，只要 f 基本上被限制。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_256.png)

只要 f 不为任何状态趋向无穷大，所以这是我们最初关心的方程，我们关心的是 p theta  prime 下 s st 的期望值，对于重要采样估计器的行动值期望。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_258.png)

对于优势。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_260.png)

所以将括号内的所有内容视为f。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_262.png)

然后我们可以将这个量下界地由p theta下的条件期望的st的同一量来绑定。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_264.png)

并且，这个现在看起来正好像我们通过不同分部来获取策略梯度的东西。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_266.png)

减去一个误差项，并且误差项是2乘以epsilon乘以，T乘以一个常数c，并且常数c是括号内的最大值。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_268.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_269.png)

状态期望内的东西可以取到的，花一点时间来思考那个，嗯，那个括号内的最大可能值可能是。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_271.png)

基本上我们应该用什么来代替c，括号内的东西是一个非常复杂的方程，但请注意，那个方程中的大部分术语都是概率，我们知道，概率必须相加等于一。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_273.png)

所以实际上，我们可以注意到，括号内的数量基本上就是它的。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_275.png)

它是某个优势的预期值，以及什么是优势。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_277.png)

很好，优势是时间上的奖励总和。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_279.png)

所以这意味着c的最大值可以是可能的最大奖励乘以。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_281.png)

时间步数，因为所有那些重要性权重和所有那些期望他们必须加起来等于一。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_283.png)

所以这意味着基本上。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_285.png)

任何函数的预期值，不可能比函数取值最大的值更大。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_287.png)

并且优势的最大值是时间步数乘以。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_289.png)

最大的奖励，因为最终，优势是时间上的奖励总和，所以这意味着c的数量级与时间步数相同，乘以r的最大值，如果你有时间步数无限，但是你使用了折扣，那么你知道折扣值形成的几何序列。

所以他们必须相加等于一除以一减去gamma，所以在有限期限的情况下，c在无限期限的情况下是资本t乘以r的最大值。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_291.png)

顺便说一句，r的最大值等于一减去gamma。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_293.png)

在这里，作为一个插曲，如果你正在学习强化学习理论，并且你曾经看到一种看起来像是一除以一减去伽马这样的术语。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_295.png)

就在心理上替换那个时间范围，因为 一除以一减去伽马 本质上相当于一个时间范围。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_297.png)

在无限时间范围的情况下。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_299.png)

它基本上等于时间步数，是你在奖励上求和的有效时间步数。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_301.png)

好的，所以，本质上所有这些都在说，最大化这个方程底部的最大化这个边界。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_303.png)

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_304.png)

我们真正想要的一件事情，在p theta prime下的期望是什么。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_306.png)

我们已经证明这是同时最大化rl目标的事情。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_308.png)

我们需要注意的事情是，我们会得到一个误差项，它将我们缩放到epsilon t。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_310.png)

嗯，乘以一个常数，误差项中的所有东西都是常数。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_312.png)

除了epsilon和epsilon之外，是你新策略与旧策略的总变分距离。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_314.png)

所以，在这个点上花一点时间来思考我们应该使用哪种强化学习算法。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_316.png)

嗯，基于这个推导，基本上。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_318.png)

这个推导建议在某种情况下，一个特定的，非常可处理的目标函数是一个对真实强化学习目标的良好近似。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_320.png)

这暗示了我们应该使用哪种类型的强化学习算法。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_322.png)

如果我们想要得到好的性能。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_324.png)

好的，所以我们到目前为止是，最大化这个嗯。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_326.png)

这一目标，基本上，p theta下预期值在pi theta下预期值重要性的预期值的期望值，加权优势是最大化rl目标的好方法，只要pi theta prime在总变分距离上接近pi theta，基本上。

如果你限制theta prime不要走得太远从theta，使得这个约束被满足，那么最大化这个可处理的目标就是最大化真正的rl目标，我们如何很好地最大化这个目标。



![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_328.png)

我们认为它是关于theta prime的导数，并且θ'仅在重要性权重中出现。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_330.png)

所以当我们对它求导时，我们得到精确的政策梯度，我们的推导，到目前为止，它已经表明这样做是好的。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_332.png)

如果θ'接近θ，所以对于足够小的ε。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_334.png)

这被保证会提高Jθ' - Jθ，这意味着它被保证会提高RL的目标。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_336.png)

好的，所以，讲座的下一部分。

![](img/a6bbf1c27fc0a5a67b201d9a15c018ee_338.png)