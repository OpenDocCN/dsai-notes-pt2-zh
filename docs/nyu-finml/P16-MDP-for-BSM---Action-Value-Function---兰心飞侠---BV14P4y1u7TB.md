# P16：MDP for BSM - 动作值函数 - 兰心飞侠 - BV14P4y1u7TB

现在，让我们讨论如何在这个模型中计算最优策略。我们已经知道，最优策略Pi*是一个使值函数V_t最大化的策略。最优值函数V*满足这里所示的贝尔曼最优性方程。如果我们知道动态系统，则可以使用值迭代等方法解这个方程。

我们在之前的课程中已经回顾过了这些方程。但特别是对于处理第二种情况，且更有趣的情况——当动态系统未知时，事实证明另一版本的值函数对于此类任务更为有用。这个版本被称为动作值函数。

动作值函数Q在时间t是两个变量的函数，而不是值函数V(x_t)那样是一个变量x_t的函数。Q函数的第一个参数是相同的x_t，而第二个参数是时间t的动作at。Q函数被确定为相同表达式的期望值。

这个方程确定了值函数V，但这次它是基于特定的初始动作at = A来求解，而所有后续动作at将遵循策略pi。现在，通过使用相同的技巧，将最后一项拆分成时间t项和未来时间值的总和。

我们可以得到动作值函数的贝尔曼方程。这个方程适用于任何策略pi的Q函数，但我们更感兴趣的是找到最优策略pi star。这与之前的定义相同。最优策略pi star应该最大化动作值函数。

如最后一个方程所示。现在，Q函数的贝尔曼方程将其与值函数V联系起来，而不是与它自身联系起来。但如果我们看一下最优Q函数Q star，我们可以得到一个只涉及该函数的贝尔曼方程。为此，让我们注意到这里实际上有两个方程。

第一个方程是通过在Q函数的贝尔曼方程中将pi替换为pi star而得到的Q star的方程。但这里也有第二个方程，它表明最优值函数V star是通过在其第二个参数AT被最优选择时从Q star获得的。因此，如果我们将第二个方程代入第一个方程。

我们得到一个只包含Q star的方程。这被称为动作值函数的贝尔曼最优性方程，并且在强化学习中起着核心作用。贝尔曼最优性方程是一个反向方程，它应从时间T-1开始逆向求解。

我们还可以通过 T 时刻到期的投资组合价值 πT 的分布，得到 Q 星的终端条件。因此，在 T 时刻的最优动作由一个最大化 Q 函数的 AT 值给出。这有时被称为贪婪策略。它选择一个当前的动作，使 Q 函数最大化，而不关心这个动作如何影响未来的选择或动作。现在，如果我们将词函数 R 的显式形式代入贝尔曼最优性方程。

我们得到这个方程。这个方程显示的是，Q 函数是关于动作 AT 的二次函数。因此，它容易相对于 AT 进行最大化。我们还可以检查如果我们取风险版本 lambda 趋近于零时，这个公式会发生什么变化。在这个极限下，我们得到这里展示的第一个方程。

但现在我们可以用负的投资组合价值来替代最优的 Q 函数。其期望值正是我们之前讨论的平均期权价格 C hat。因此，通过使用这个并翻转整体符号，第一个方程可以写成第二个方程。

但第二个方程是我们已经看到的。它是一个递归关系，用于计算平均期权价格，并且具有右侧的黑-斯科尔斯极限。当时间步长 delta T 非常小时，因此我们看到当风险版本 lambda 和时间步长 delta T 都消失时，我们的公式简化为黑-斯科尔斯模型。

![](img/b846bffa40e119a5a96df19e9ea886f9_1.png)

![](img/b846bffa40e119a5a96df19e9ea886f9_2.png)
