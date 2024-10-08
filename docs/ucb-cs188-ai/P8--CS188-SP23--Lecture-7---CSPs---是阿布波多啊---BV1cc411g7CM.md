# P8：[CS188 SP23] Lecture 7 - CSPs - 是阿布波多啊 - BV1cc411g7CM

![](img/2c690b61e462e71a8f2f836a836f07a3_0.png)

录得很好，非常好，好的，所以我要给你一个快速的，就像20分钟的CSPS介绍，然后我们在星期四完成剩下的工作，然后希望我们回到正轨，所以再忍耐一下，所以让我们回到过去，考虑一下搜索，请记住，在搜索过程中。

我们做了几个假设，我们说只有一个特工在做计划，所以只有一个代理人决定采取什么行动是正确的，所有的行动都是决定性的，如果你采取了行动，那个动作会发生，其他一些行动不会发生对吧。

我们说世界是完全可以观察到的，所以你知道所有东西都在哪里与我们在搜索过程中所做的逻辑单元如此不同，我们假设一切都是可以观察到的，然后我们假设状态空间是离散的，这些都是我们在构建搜索问题时所做的假设。

在接下来的几周里，我们会试着思考搜索问题是如何改变的，如果我们改变其中的一些假设，就像如果你改变关于确定性动作的假设，如果行动不是决定性的呢，这如何改变搜索问题和我们使用的算法，我们会考虑的好吗。

但今天我们要谈谈，比如搜索问题的更具体版本，所以让我们回头想想搜索问题的目的是什么，记住目标，或者像你想从搜索问题中实现的那样，就是得到一系列的行动，把你的状态转化为目标，所以你可以想到。

就像这里的这张照片，这就像我们的防盗机器人，或者像我们的小偷机器人，它在思考动作的顺序是什么，我得拿去拿这颗钻石，我必须喜欢，往这个方向，那我就得这么做，那我就得这么做，所以它在制定计划，思考如何。

它要去偷钻石了，这就是我们第一周谈论的，今天我们将研究搜索问题的一个更具体的版本，所以现在我们对达到目标的行动顺序并不感兴趣，我们只是对目标本身感兴趣，所以现在想想这个侦探机器人。

这个侦探机器人好像还行，嗯，钻石不见了，我想为发生的事情建立一个解释，这并不重要，侦探采取了什么行动来弄清楚，解释是什么，我们所关心的是在一天结束时，这个侦探想出了一个很好的解释，就像发生了什么对吧。

所以这是我们的目标，为了今天，我们将稍微重新制定搜索问题，看看这会有什么影响，不同的算法，好的，所以我们再来看一下，我们有一个数学定义，就像我们搜索一样，在搜索中记住，我们有一个数学定义。

我们说你的任何问题都可能是，煎饼可以成为罗马尼亚的地图，可以是吃豆人，只要你能用状态空间来表示它，你的起始状态，您的后续功能和目标测试，那么我们建立的任何搜索算法都可以解决你的问题，只要你给它。

只要你喜欢，弄清楚你如何看待你的问题，并将其转化为非常具体的数学定义，像这样注意到一件事非常有用，那就是抽象，对呀，所以如果你在想那些通用的搜索算法，比如深度优先搜索广度优先搜索。

那些算法并不关心状态是什么，你可以给这些算法任何类型的状态，他们可以解决你的问题，可能涉及成堆的煎饼或城市或吃豆人的位置，这些算法总能解决你的问题，对，你可以这样想，这是另一张照片，这就像目标测试。

这个目标测试是评委，所以法官看你的状态，然后说这是目标，或者法官看着你的状态说这不是目标继续努力，算法的其余部分不必知道任何关于状态的信息，它只需要把国家，把它呈给法官，或者目标测试和目标测试要么说是。

这是你完成或没有的目标，这不是目标，继续努力，所以它有点像黑匣子搜索算法，深度优先搜索，从来不用看状态是什么，它只需要把这个州，把它呈现给法官，目标测试和目标测试要么说是，要么说不是，好今天。

我们要深入一点，我们将打破抽象的障碍，创建更具体的问题类，这些被称为约束满足问题，我要叫他们csps，对呀，所以这又是，这是一类特殊的搜索问题，我们又有了另一个数学定义，它与搜索问题的数学定义相同。

但我们要把它说得更具体一点，所以它就像一个子类，所以现在你的状态不是任何类型的对象，你想要城市、地图或PAC，人的位置或食物点，你的状态现在是非常具体的，它将是一组变量。

每个变量都可以从某个域中获得一个值，如果这听起来真的很困惑，我们会有例子，现在你的目标测试也将不同，现在不是法官来找你说，是呀，否，是呀，否，现在你的目标测试总是遵循这个特定的结构。

你会得到一个规则列表，所以这个法官不会告诉你什么是对的，什么是错的，你得到一套规则告诉你，这就是这些变量应该如何分配，或者你有一个满足这些规则的作业，或者不符合这些规则，所以这是一个更具体的问题。

对而不是状态是你想要的，状态现在是非常具体的东西，一堆变量，每个变量都可以从一组域中获得一些值，和你的目标测试，而不是这个黑匣子，你给法官一些东西，并要求一个，是或否，现在是一套规则。

你可以自己检查规则，呃，我目前的解决方案是否遵守规则，是或否，现在因为我们有比一般搜索更具体的问题，现在我们可以考虑，我们是否可以使用特殊的技术来更有效地解决这个问题，因为那样很好，好的。

这就是数学定义，就像以前一样，我们可以处理不同的问题，只要我们能以这种非常具体的方式来表达它，那么我们的CSP算法可以解决它们看起来不错，到目前为止很好，让我们看一些例子，这里是CSPS最经典的例子。

这叫地图着色，原来你是个地图设计师，你想给澳大利亚的各州着色，在这种情况下，作为地图设计师，你想要的是，你不想给相邻的两个状态着色，同样的颜色，因为那有点恶心，现在你真的不知道美国在哪里开始和结束。

对呀，所以作为一个地图设计师你真的想给相邻的任何州着色，不同的颜色，就像，在这里结账，我们有西澳大利亚的红色，好的，你不会希望北方领土也是红色的，因为他们互相触摸。

把它们都涂成红色在地图上看起来真的很奇怪，所以你的目标是试着弄清楚颜色的分配，我想在这张地图上，使没有接触状态具有相同的颜色，这不是唯一的CSP，但这是我们会经常看到的，那么我们如何将其定义为CSP。

记得我们有一个特定的数学定义，所以让我们试着把这个问题放在那个定义中，所以现在你的状态空间不仅仅是任何旧的状态，这是非常具体的事情，变量集，每个变量接受域中的一个值，所以这里是你的变量。

我每个状态有一个变量，就像，西澳大利亚是变量W，北部领土是变量，塔斯马尼亚是变量t看起来不错，然后每个变量接受来自其中一个域的值，对呀，在本例中，所有变量都具有相同的域，它是红色的，绿色或蓝色。

这是你必须选择的三种颜色，所以现在我们已经定义了我们的状态，这是一个比通用搜索问题更具体的问题，现在我们必须定义我们的目标测试，通常目标测试可以是你喜欢的任何检查，但是在CSP中，目标测试将是一组规则。

告诉你，你的作业是否好，还是不好，那么我们这里的规则是什么，我们用英语设置，我们要强加的规则，你必须在邻近的州有不同的颜色吗，你可以用几种不同的方式来写这个，所以写它的一种方法是使用隐式约束。

我们以后再谈这个，我也是，但你可以把它写成，就像你执行的一段代码来检查，是否已满足约束，所以这就是我们在这里所做的，我们含蓄地写道，你想让西澳大利亚和北领地有不同的颜色，就像一小段代码。

你可以执行和检查，是否已满足约束，所以你有点塞瓦的颜色，你把n的颜色插入表达式，看看是不是真的，或者你可以露骨地说，你实际上可以写出西澳大利亚和北领地，你必须选择。

这种颜色组合可以是红色和绿色红色和蓝色蓝色和绿色，您也可以列出所有有效的作业，这是表达约束的另一种方式，所以这有点取决于你，你想在这里如何表达它们，我们用英语来表达，我们还向您展示了隐式约束。

你喜欢的地方，编写一小段代码，用于检查，也可以显式写，只是说，这是所有有效的方法的列表，最后，我们的目标是什么，所以请记住，我们的目标是将所有变量分配给一个值，希望你得到一个分配所有变量的赋值。

并给它们都一个颜色，在本例中，为一个值，您希望满足所有的约束，所以所有的规则都应该检查出来，所以这里有一个解决方案的图片版本，满足所有约束，如果你非常仔细地盯着它，你会注意到邻近的州都没有相同的颜色。

所以我们有一张漂亮的地图，这就是我们的解决方案，剩下的时间也是如此，比如今天和周四，我们将思考你到底如何编写算法来改变你的问题，以下是变量，以下是域，以下是有效解决方案的约束。

其中每个变量从其域中获得一个值，一切都满足了，圆，看起来不错，准备给地图上色一周，我将给你们看几个其他的例子，只是为了向你证明这不是唯一的CSP，即使是我们会经常看到的那个，这是另一个你几周前见过的。

这是结束皇后，我们最喜欢的游戏，所以记住结束后的规则是，如果你是棋盘上的女王，你可以移动，你知道在同一排，在同一列对角线中，你想在黑板上放皇后，这样它们就不会互相攻击了，如果这没有意义。

我们几周前讨论过这个，所以你可以去看看右边，我们想把它表述为CSP，所以我们想把刚才用英语描述的这个问题，并将其转化为非常具体的定义，我们周四的算法将能够为我们解决，那会是什么样子。

所以我们可以尝试几种不同的方法，这里有一种方法你可以把它写出来，我可以对每个方块都有一个变量，所以我可以有一个左上角正方形的变量，然后是右上角正方形的变量，和每个正方形的变量，十六变量。

每个变量必须在域中具有一个值，所以在这种情况下，我将选择我的域为零，一个零表示广场上没有女王，一个意思是广场上有个女王，好的，所以我写下了我的状态，我的变量每平方一，每个人要么有王后，要么没有王后。

这些都是世界可以呈现的所有可能的配置，好的，现在我们可以考虑约束，那么有什么规则可以让这个问题，或者让CSP可解，那么对于一个解决方案，我们需要什么是真的，这个游戏的规则是什么。

所以游戏规则是蚁后不能再互相攻击，你可以用几种不同的方法把它写出来，所以这里有一种方法可以明确地写出它，我们在那里列出了所有可能的配置，我们说你知道在同一排有两个正方形，所以i指数在相同的。

那么两个方块中的任何一个都没有女王，没关系，或者其中一个方块有女王没关系，或者另一个广场有女王没关系，但是我们不能有两个皇后在同一排，他们会互相攻击，所以这只是我们写规则的数学方式。

你可以写一堆其他规则，说同一列没有女王，同一条对角线上没有皇后，你可以把这些都写出来，然后将这些插入通用求解器，这会给你一个漂亮干净的解决方案，但这不是我能提出这个问题的唯一方法。

我也可以把这个英语语言和皇后的问题转换成，你知道的，另一种类型的CSP，实际上我错过了一个限制，这张幻灯片让我想起了，所以还有一个限制，为什么我需要这个约束，如果我没有这个约束。

这里有什么有效的解决办法，那真的很容易，我可以给所有的变量分配什么来解决这个问题，并确保所有的规则都得到满足，我不能把任何东西放在黑板上，这将满足所有的规则，所以有时候你得小心一点，谢天谢地。

幻灯片抓住了我，我们再增加一条规则，上面说你必须在黑板上有N个皇后，否则你可能会有一个愚蠢的解决方案，就像整个董事会都是空的，所有的规则都得到了满足，没有蚁后互相攻击，也没有皇后，那就太傻了。

所以这里有一个公式，还有其他配方，这里有一个我们有点喜欢，承担了问题的一部分，然后把它烤到配方里，所以这里有一个我们认识到的地方，嗯，这个版本在解题上有很多变数，会有点难，但我们也许马上就能意识到。

我已经知道每排只有一个女王，就像，为什么我要把时间浪费在所有这些不同的变量上，我也可以说实际上，我知道每排必须有一个皇后，所以如果我需要在黑板上放四个皇后，有四排，那么每一行都必须有一个皇后，不再。

一点也不少，所以现在我可以说我的变量是每一行，我唯一的问题是女王在哪个专栏，所以现在就像第一排，女王在第0栏吗，第1栏第2栏第3栏，就在第二排，第二个皇后在零栏里吗，一个，两个，三个，以此类推。

这是一个等价的提法，它解决了同样的问题，但它用一组不同的变量和域来做到这一点，再次，你必须写出你需要确保满足的规则，在这种情况下，我们有点懒，刚刚写了女王可以互相攻击，但您也可以显式地编写它。

你可以说像第一排的女王和第二排的女王，不能都在第0列，但它们可以是0和1或0和2 0和3，你想怎么写就怎么写，哦哦，我几乎是在，好的，有明确的版本，好的，我再给你看几个，哪儿也别去，然后我们就结束了。

你也可以把这些画成图表，所以记得几周前我们说过的，当你看到一个图表时，你得停下来问问自己，我为什么要画这个图，有什么意义，这是另一个图表，节点是变量，这些是我们试图在地图着色问题中分配的变量。

我每个状态有一个变量，所以这里每个状态有一个节点，这些线告诉我是否有两个变量，它们之间有一个约束，所以在这种情况下，如果西澳大利亚和北领地不能有色，同样的颜色，我在他们之间画了一条边。

这告诉我有一个规则将这两个变量联系起来，这张幻灯片上就说了这么多，所以你可以把这些画出来，如果你想，但如果你真的要小心，记住当你看到一个图表，记住它代表什么，否则你可能会迷路。

所以这是用图片表示CSP的一种方式，对呀，还有其他例子，我很快就会喜欢的，所以这里有一个可能你以前玩过这些小谜题，他们就像，每一个呃，上面的字母对应着从零到九的数字，你能把数字。

这样这个数学表达式就为真了，你可以写出所有这些变量和域，所以f必须是一个数字，o必须是一个数字，u必须是一个数字，r必须是一个数字，对呀，你需要三位数，因为你会喜欢，有时带有一些数字，域为零到九。

因为每个字母都有一个数字，然后你有约束，就像你知道的，应该等于r加上一些进位，所以你必须小心你如何制定它，但是您可以使用CSP来解决这个问题，好的，有点可爱的问题，也可以再次将其绘制为约束图。

当你看到一个图形，真的要小心，你在想什么，我对每个变量都有圆节点，在这种情况下，是字母，这一次我有一些约束，涉及两个或更多的变量，所以如果我有，我就画一个正方形，然后将正方形连接到约束中涉及的所有变量。

所以在这种情况下，我有一个涉及O和R和X 1的，这是一个小进位数字，所以我画了一个正方形，连接你，我画了一个连接O、R和X 1的正方形，这告诉我他们之间有一个约束，所以如果你想把CSP画成一张图。

你可以在一个看起来不错的图表中这样做，差不多了，再给我两分钟，好的，数独经典CSP右，每个盒子都是你的变量之一，你得用数字0到9来填，在专栏中记住数独的规则，必须有不同的数字，可以在行内有两个相同的。

不要在一个小方块里有两个相同的，不要有两个相同的，这是你能做的一件事，可以用CSP玩数独，你就像，为什么这些东西甚至像现实一样，在现实世界中人们会这么做吗，这里有一个比较老的csp，他们试图找出。

就像三个D形，用CSP，不打算说太多细节，但这有点酷，哦绵羊，好的，让我们快点把这件事做完，所以在这门课上，我们不会有很多时间，所以我们将向你们展示有限域的CSP，这意味着定义域是有限的，它是离散的。

这是哪里，好的，所以这意味着变量可以承担，就像一组有限的值，就像我可以列出变量可以接受的所有可能的值，但你也可以有无限的域，像整数，所以这个变量可以接受任何整数，有无限多的，所以这可能是一个选择。

我们没有时间讨论这个，你也可以有连续变量，就像这个变量可以取一个实数，现在又有无限多的实数，你可以把它们都列出来，所以这些也是CSP的变种，我们不会有时间谈论他们，我们只是要谈谈更简单的版本。

其中变量在有限离散列表中具有一个值，非常离散域，所以这就是我们所有的时间，这张幻灯片说，但要知道还有其他类型的，好的，真的很快，我们有我们已经讨论过的约束，有二进制，有一元约束，它涉及一个变量。

所以在这种情况下，如果你说南澳大利亚不能是绿色的，这是一个涉及一个变量的规则，所以它是一元的，您可以有二进制约束，像南澳大利亚和西澳大利亚不可能是相同的颜色，这涉及两个变量，所以它是二进制约束。

你可以有更多像数独的，你说过，这九个变量可以有两次相同的数字，这就像一个更高阶的约束，也有软约束，就像，也许你真的更喜欢红色而不是绿色，但又一次，只是让你知道那些存在，当我有时间谈论他们的时候，好吧。

这些东西总是出现，所以在现实生活中，你经常自己解决CSP，大家什么时候有空见面你得喜欢，根据每个人的喜好，计算出你分配了哪些变量，就像，你几点有空？你可以知道秋天谁教哪个班，或者呃，你知道就像。

我怎么把这些硬件放在船上，任何权利，有很多不同的调度或分配问题，CSP可以解决，希望下次我们能向你展示一些解决它们的方法，好的，对不起，我迟到了三分钟。



![](img/2c690b61e462e71a8f2f836a836f07a3_2.png)

![](img/2c690b61e462e71a8f2f836a836f07a3_3.png)