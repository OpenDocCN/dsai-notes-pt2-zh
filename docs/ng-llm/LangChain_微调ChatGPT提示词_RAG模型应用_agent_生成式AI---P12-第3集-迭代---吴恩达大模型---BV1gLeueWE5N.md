# LangChain_微调ChatGPT提示词_RAG模型应用_agent_生成式AI - P12：第3集 迭代 - 吴恩达大模型 - BV1gLeueWE5N

![](img/7e327f4f816b1746e0253f4e08ce0855_0.png)

当我在建立使用大型语言模型的应用程序时，我认为我从未遇到过这样的提示，这是我在第一次尝试中在最终应用程序中使用的提示，这并不是重要的，只要你有一个好的过程来迭代改进你的提示。

那么你就能来 something 适合你想要实现的任务的东西。

![](img/7e327f4f816b1746e0253f4e08ce0855_2.png)

你可能听说过当我训练机器学习模型时，它几乎从不在第一次就工作。

![](img/7e327f4f816b1746e0253f4e08ce0855_4.png)

实际上我对第一个模型感到惊讶，我训练的模型工作，我认为我们在提高它第一次工作的可能性，第一次工作的可能性可能稍微高一些，但他说这不重要，如果第一个提示工作，更重要的是获取到有效提示的过程。

这对于你的应用程序来说更重要，所以，让我们跳入代码，并让我看一些框架。

![](img/7e327f4f816b1746e0253f4e08ce0855_6.png)

来思考如何迭代开发提示，如果你以前在我这里上过机器学习课程，你可能见过我们使用图表说，机器学习开发中，你通常有一个想法，然后实现它，所以写代码，获取数据，训练你的模式，这将给你一个实验结果。

然后你可以看那个输出，也许做错误分析，找出它工作或不工作的地方，然后甚至可能改变你确切想要解决的问题的想法，或如何接近它，然后改变实现并运行另一个实验，等等，并迭代过来过去。

直到得到一个有效的机器学习模型，如果你不熟悉机器学习，我之前没见过这个图表，不要害怕，这不重要对于这个演示的其余部分，但当你在写，为使用lm的应用程序开发提示时，过程可能相当相似。

你有一个想做的任务的想法，然后你可以尝试写一个第一个提示，希望它清晰、具体，如果适当，可以给系统一些时间来思考，然后你可以运行它，看看结果如何，如果效果不好，不是第一次，然后迭代过程来确定，为什么指令。

例如，不够清晰，或者为什么算法没有足够的时间来思考，允许你细化想法，细化提示并如此等等，并且多次环绕这个循环，直到你最终得到一个适合你应用的提示，这也是为什么我个人没有像那些文章说的那样花太多精力。

三十个完美的专业，因为我认为可能没有适合太阳底下的一切的完美提示，更重要的是你有一个过程来为你的特定应用开发一个好的提示。



![](img/7e327f4f816b1746e0253f4e08ce0855_8.png)

所以让我们一起在代码中看看吧，我在这里有您在之前的视频中看到的起始代码，有import openai和poos，在这里，我们获取openai api密钥，这是同样类型的函数，你看到过的最后一次。

我将在这个视频中使用作为运行示例，总结一张椅子的事实表。

![](img/7e327f4f816b1746e0253f4e08ce0855_10.png)

所以让我简单地粘贴在这里。

![](img/7e327f4f816b1746e0253f4e08ce0855_12.png)

您愿意的话，可以暂停视频，并在左侧的笔记本中仔细阅读这个，如果您愿意，但这是一张关于椅子的事实表，带有描述，说它是一个美丽的中期灵感家族成员等。



![](img/7e327f4f816b1746e0253f4e08ce0855_14.png)

嗯，谈论构造，有尺寸，选项为椅子材料来自意大利等来自它。

![](img/7e327f4f816b1746e0253f4e08ce0855_16.png)

假设你想要这个事实表，并帮助营销团队为在线零售网站写描述。

![](img/7e327f4f816b1746e0253f4e08ce0855_18.png)

让我快速运行这三个，然后嗯，我们将生成一个提示，如下，我只是，我只是踱步，所以我的提示在这里说，你的任务是帮助营销团队创建零售网站的描述，基于技术事实表的产品，写产品描述等。

这是我第一次尝试解释任务给大型语言模型，所以让我按Shift Enter，这需要几秒钟来运行。

![](img/7e327f4f816b1746e0253f4e08ce0855_20.png)

我们得到结果。

![](img/7e327f4f816b1746e0253f4e08ce0855_22.png)

看起来它做得很好，写了描述，介绍一款令人惊叹的中期灵感办公室椅。

![](img/7e327f4f816b1746e0253f4e08ce0855_24.png)

完美版等，当我看到这时，我去。

![](img/7e327f4f816b1746e0253f4e08ce0855_26.png)

哇，这真的很长，它做得很好，准确地完成了我的要求，从技术规格表开始编写产品描述。

![](img/7e327f4f816b1746e0253f4e08ce0855_28.png)

但当我看到这个时，我的反应是，这个有点长，也许我们想要它稍微短一些。

![](img/7e327f4f816b1746e0253f4e08ce0855_30.png)

所以我有了一个想法，我写了一个提示，得到了结果，我对它不太满意，因为它太长了，所以我会澄清我的提示。

![](img/7e327f4f816b1746e0253f4e08ce0855_32.png)

嗯，我说，最多使用五十个字来尝试提供关于所需描述长度更好的指导。

![](img/7e327f4f816b1746e0253f4e08ce0855_34.png)

让我们开始游戏，好的，这实际上看起来是一个比较长的短描述，嗯，介绍中世纪风格的办公椅的产品，等等五，我们既时尚又实用，不错，嗯，让我再检查一下这个的长度，我将取回应用程序的响应，根据空格将其分割。

然后您打印出长度，所以它是五二个词，实际上还不错，嗯，大型语言模型是可以的，但不是那么伟大在遵循关于非常精确字数计数的指示上，但这实际上还不错，有时它会打印出包含六十或六十五个单词的内容等。

但这是在一定程度上合理的，你可以尝试做的事情之一是说，最多使用三个句子，让我运行那个 again，但这些是告诉大型语言模型不同的方式，你想要的输出长度是多少，所以这是一个一、二、三。



![](img/7e327f4f816b1746e0253f4e08ce0855_36.png)

我计算了三个句子，看起来我做得不错，嗯，我还见过人们有时做这样的事。

![](img/7e327f4f816b1746e0253f4e08ce0855_38.png)

我不知道，你说最多二百八十个字符，大型语言模型，因为它们使用称为分词器的方法来解释文本，我不会谈论这个，但嗯，它们通常对字符计数非常不准确，但让我们看看二百八十一字符，实际上相当接近。

通常一个大型语言模型并没有那么接近，但这些是他们可以玩的不同方式，以尝试控制您得到的输出长度，然后只需切换回使用最多五十个单词。



![](img/7e327f4f816b1746e0253f4e08ce0855_40.png)

这就是我们刚刚得到的结果。

![](img/7e327f4f816b1746e0253f4e08ce0855_42.png)

随着我们从网站上继续精炼这个文本，我们可能会决定那个男孩，这个网站并不是直接向消费者销售的，实际上是打算向家具零售商销售家具的，那些对椅子的技术细节和椅子的材料更感兴趣的人，在这种情况下。

你可以取这个提示并说我想修改这个提示，以使它更精确地描述技术细节，让我再继续修改这个提示，我说这个描述是打算向家具零售商销售的，所以应该技术性和专注于材料产品，是由高质量的材料制成的。



![](img/7e327f4f816b1746e0253f4e08ce0855_44.png)

让我们运行那个，看，不错，你说你知道，涂层铝基座和气动椅子。

![](img/7e327f4f816b1746e0253f4e08ce0855_46.png)

高质量材料，通过改变提示，你可以使它更专注于特定的角色，专注于你想要的特定特性，当我看到这时，我可能会决定嗯，在描述的末尾，我也想包括产品ID。



![](img/7e327f4f816b1746e0253f4e08ce0855_48.png)

所以这两个产品的提供。

![](img/7e327f4f816b1746e0253f4e08ce0855_50.png)

所以c one ten ssc，一百，也许我可以进一步改进这个提示。

![](img/7e327f4f816b1746e0253f4e08ce0855_52.png)

以使它能给我产品ID。

![](img/7e327f4f816b1746e0253f4e08ce0855_54.png)

我可以在描述的末尾添加这个指令，包括每个七字符的产品ID和技术规格。

![](img/7e327f4f816b1746e0253f4e08ce0855_56.png)

让我们运行它并看看会发生什么。

![](img/7e327f4f816b1746e0253f4e08ce0855_58.png)

所以它说介绍一个办公室椅子，外壳颜色，谈论塑料涂层，铝基座，实用，一些选项。

![](img/7e327f4f816b1746e0253f4e08ce0855_60.png)

谈论两个产品ID，这看起来不错，你所看到的就是短例迭代提示开发的一个例子。

![](img/7e327f4f816b1746e0253f4e08ce0855_62.png)

许多开发者都会经历这个过程，我认为我们的指南在最后一个视频中，你看到要么是分享，要么是一系列最佳实践，我通常的做法是记住像那样最佳实践，清晰和具体，如果必要，给模型时间思考这些是值得的。

常常尝试首次编写一个提示，看看会发生什么，然后从那里开始迭代，精炼提示以越来越接近您需要的结果。

![](img/7e327f4f816b1746e0253f4e08ce0855_64.png)

因此，你可能在许多程序中看到的成功提示，是通过这样的迭代过程到达的，只是为了娱乐，让我为您展示一个甚至更复杂的提示。



![](img/7e327f4f816b1746e0253f4e08ce0855_66.png)

这可能会给您一个关于gpt能做什么的感觉。

![](img/7e327f4f816b1746e0253f4e08ce0855_68.png)

嗯，我在描述之后添加了一些额外的指令，包括一个给出产品尺寸的表格，然后您知道，格式，一切都是html，让我们运行那个，在实际操作中，您最终将得到一个这样的提示，只有在多次迭代之后。

我想我不知道有任何人会写这个确切的提示，当他们第一次试图让系统处理事实表。

![](img/7e327f4f816b1746e0253f4e08ce0855_70.png)

因此，这实际上输出了一些html，让我们将html显示以查看是否有效。

![](img/7e327f4f816b1746e0253f4e08ce0855_72.png)

html并查看是否工作，实际上我不知道它会工作，但让我们看看，哦，酷。

![](img/7e327f4f816b1746e0253f4e08ce0855_74.png)

好的，让我们看渲染，所以它有一个非常漂亮的椅子描述。

![](img/7e327f4f816b1746e0253f4e08ce0855_76.png)

嗯，建设材料，产品尺寸。

![](img/7e327f4f816b1746e0253f4e08ce0855_78.png)

哦，看起来我遗漏了。

![](img/7e327f4f816b1746e0253f4e08ce0855_80.png)

嗯，最多使用五十个字的指示，所以这有点长，但如果你想要知道，你甚至可以自由暂停视频。

![](img/7e327f4f816b1746e0253f4e08ce0855_82.png)

告诉它更简洁一些并再生成这个，看看结果如何。

![](img/7e327f4f816b1746e0253f4e08ce0855_84.png)

我希望你从这个视频中学到，提示开发是一个迭代过程，尝试一下，看看它尚未完全满足您想要的，然后思考如何澄清您的指示，或者在某些情况下，思考如何给它更多的空间，以便更接近您想要的结果。

我认为成为有效提示工程师的关键不在于知道完美的提示，而在于有一个好的过程来开发有效的提示，以适应您的应用程序，在这个视频中，我展示了如何开发一个提示，对于更复杂的应用，仅使用一个例子可能不够。

有时你可能有多个例子，例如，一个包含十个甚至五十个甚至一百个事实单页的列表，然后迭代开发提示并使其与大量的案例进行比较，但对于大多数应用的早期开发，我看到许多人以一种方式开发它，我只使用一个例子。

但是对于更成熟的应用，有时评估提示对更大集例子的效果可能是有用的，例如，测试在数十个事实单页上的不同问题，以查看多个事实单页的平均或最坏性能如何，但通常你只会在那个应用更成熟的时候做那个。

并且你必须有那些指标，来推动那个增量，提示改进的最后几步，所以，请尝试使用Jupyter代码笔记本中的例子，并尝试不同的变化，看看结果如何，当你完成时，让我们继续下一个视频，在那里。

我们将讨论大型语言模型在软件应用中的一个非常常见用途，那就是总结。

![](img/7e327f4f816b1746e0253f4e08ce0855_86.png)

所以，当你准备好时。