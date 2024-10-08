# 【ChatGPT提示词工程师】 DeepLearning.AI - P3：第3集 迭代 - 吴恩达大模型 - BV1Wf421q7cd

![](img/79fc50ec829ef4f32556d1e39e539c36_0.png)

当我用大型语言模型构建应用程序时，我想我从来没有准时过，我第一次尝试就在最后的申请中使用了，这并不重要，只要您有一个好的过程来迭代地使您的提示符更好，然后你就能找到一些对你想要完成的任务很有效的东西。



![](img/79fc50ec829ef4f32556d1e39e539c36_2.png)

你可能听我说过，当我训练一个机器学习模型时，第一次几乎行不通。

![](img/79fc50ec829ef4f32556d1e39e539c36_4.png)

事实上，我对第一个模型感到非常惊讶，我训练工作，我想我们在增加它的可能性，第一次工作可能会更高一点，但就像他说的没关系，如果第一个提示有效，更重要的是获得提示的过程，适合您的应用程序，所以有了这个。

让我们跳到代码中，让我给你们看一些框架。

![](img/79fc50ec829ef4f32556d1e39e539c36_6.png)

思考如何迭代开发提示符，所以如果你以前和我一起上过机器学习班，您可能已经看到我们使用了一个图表，说明随着机器学习的发展，你经常有一个想法，然后实施它，所以写代码，获取数据，训练你的模型。

这给了你一个实验结果，然后你可以看到输出，也许做误差分析，弄清楚它在哪里起作用或不起作用，甚至可能改变你想要解决什么问题的想法，或者如何接近它，然后改变实现，运行另一个实验等等。

并一遍又一遍地迭代以获得有效的机器学习模型，如果你不熟悉机器学习，我以前没见过这个图表，别担心，在接下来的演讲中就不那么重要了，但是当你在写作的时候，提示使用lm开发应用程序，过程可以很相似。

在那里你有一个想法，你想做什么，你想完成的任务，然后，您可以第一次尝试编写一个提示，希望它是清晰和具体的，如果合适的话，可能会给系统时间来思考，然后你可以运行它，看看你得到什么结果，如果效果不好。

不是第一次了，然后计算出，为什么说明书，例如，不够清楚，或者为什么它没有给算法足够的时间来思考，允许你完善想法，完善提示等，绕着这个循环多次，直到您最终得到一个适用于您的应用程序的提示符。

这也是为什么我个人没有那么关注那些说，三十个完美的专业人士，因为我想可能没有一个完美的提示太阳下的一切，更重要的是，您有一个为特定应用程序开发良好提示的过程。



![](img/79fc50ec829ef4f32556d1e39e539c36_8.png)

所以让我们一起看一个代码示例，我这里有你在以前的视频中看到的启动代码，有进口的开口和便便，这里，我们得到Openai API密钥，这是你们上次看到的相同类型的函数，我将在这个视频中作为跑步的例子。



![](img/79fc50ec829ef4f32556d1e39e539c36_10.png)

所以让我把它贴在这里。

![](img/79fc50ec829ef4f32556d1e39e539c36_12.png)

请随时暂停视频，在左边的笔记本上仔细阅读，如果你想，但这里有一张椅子的概况介绍，上面有描述，说它是一个美丽的世纪中期家庭的一部分，受到启发等等。



![](img/79fc50ec829ef4f32556d1e39e539c36_14.png)

嗯，谈建设，有尺寸，椅子材料等选项来自意大利。

![](img/79fc50ec829ef4f32556d1e39e539c36_16.png)

假设你想拿这份概况介绍，帮助一个营销团队为一个在线零售网站写一个描述。

![](img/79fc50ec829ef4f32556d1e39e539c36_18.png)

让我快速运行这三个，然后嗯，我们会想出一个提示，如下，我只是，我只是踱步进去，我的提示是，您的任务是帮助营销团队创建零售网站的描述，基于技术概况介绍的产品，把产品描述等写对。

所以这是我第一次尝试向大型语言模型解释任务，所以让我按下换挡键，这需要几秒钟才能运行。

![](img/79fc50ec829ef4f32556d1e39e539c36_20.png)

我们得到这个结果。

![](img/79fc50ec829ef4f32556d1e39e539c36_22.png)

它看起来写得很好，介绍一款令人惊叹的世纪中期风格办公椅。

![](img/79fc50ec829ef4f32556d1e39e539c36_24.png)

完善版等，但当我看到这个的时候。

![](img/79fc50ec829ef4f32556d1e39e539c36_26.png)

男孩，这真的很长，它做得很好，完全按照我的要求做了，从技术概况介绍开始，写一个产品说明。

![](img/79fc50ec829ef4f32556d1e39e539c36_28.png)

但当我看到这个的时候，这有点长，也许我们想让它短一点。

![](img/79fc50ec829ef4f32556d1e39e539c36_30.png)

所以我有个主意，我写了一个提示，拿到结果了，我对此不是很满意，因为太长了，所以我会澄清我的提示。

![](img/79fc50ec829ef4f32556d1e39e539c36_32.png)

嗯然后说，最多使用50个单词，试图在所需的长度上给出更好的指导。

![](img/79fc50ec829ef4f32556d1e39e539c36_34.png)

让我们在游戏中奔跑，好啦，这实际上看起来像是一个更好的简短描述，呃，办公椅介绍世纪中叶的产品，以此类推五个，我们只是既时尚又实用，不错嘛，嗯，让我再检查一下这个长度，我要接受回应，根据它们的空间。

然后你打印出长度，所以是五个两个字，其实还不错，嗯，大型语言模型还可以，但不太擅长遵循关于非常精确的字数的指示，但这其实还不错，有时它会打印出六十五个字之类的东西，但这是合情合理的，你可以试着说。

最多使用三句话，让我再运行一次，但是这些是不同的方法来告诉大型语言模型，您想要的输出长度是多少，所以这是一二三。



![](img/79fc50ec829ef4f32556d1e39e539c36_36.png)

我数了三句话，看起来我做得很好，嗯，然后我也看到人们有时会做这样的事情。

![](img/79fc50ec829ef4f32556d1e39e539c36_38.png)

我不知道，你说最多二百八十个字，大型语言模型，因为他们用一种叫做标记器的东西来解释文本，我就不说了，但是嗯，他们在数字符方面往往如此，但是让我们看看二百八十一个字符，实际上非常接近，通常。

大型语言模型无法做到这一点，但这些是他们可以玩的不同方式，尝试控制得到的输出的长度，但只要把它调回来，最多使用50个单词，这就是我们刚才的结果，当我们继续从我们的网站上完善这篇文章时。

我们可能会决定那个男孩，这个网站不是直接向消费者销售的，实际上是打算把家具卖给家具零售商，在这种情况下，您可以接受这个提示符，并说我想修改这个提示符，使其在技术细节上更加精准。

所以让我继续修改这个提示符，我要说的是，这个描述是针对家具零售商的，所以应该是技术上的，专注于材料产品和从井中建造。



![](img/79fc50ec829ef4f32556d1e39e539c36_40.png)

让我们运行，让我们看看还不错，说你知道，涂层铝底座气动椅。

![](img/79fc50ec829ef4f32556d1e39e539c36_42.png)

优质材料，所以通过改变提示符，你可以让它更专注于特定的角色，你想要的具体特征当我看到这个的时候，我可能会决定嗯，在描述的末尾，我还想包括产品ID。



![](img/79fc50ec829ef4f32556d1e39e539c36_44.png)

所以这次股票的两次发行。

![](img/79fc50ec829ef4f32556d1e39e539c36_46.png)

所以十秒，一百，所以也许我可以进一步改进这个提示。

![](img/79fc50ec829ef4f32556d1e39e539c36_48.png)

为了让它给我产品编号。

![](img/79fc50ec829ef4f32556d1e39e539c36_50.png)

我可以在描述的末尾添加这个说明，包括每七个字符的产品ID和技术规范。

![](img/79fc50ec829ef4f32556d1e39e539c36_52.png)

让我们运行它，看看会发生什么。

![](img/79fc50ec829ef4f32556d1e39e539c36_54.png)

上面是这么说的，介绍一种文件办公椅，外壳颜色，谈塑料涂层，铝基，嗯实际，关于两个产品ID的一些选项。

![](img/79fc50ec829ef4f32556d1e39e539c36_56.png)

所以这看起来很不错，您刚才看到的是迭代快速开发的一个简短示例。

![](img/79fc50ec829ef4f32556d1e39e539c36_58.png)

很多开发商都会经历，我想我们的指导方针在上一个视频中，你看到的要么是，一些最佳实践所以我通常会记住这些最佳实践，明确具体，如果有必要，给模型时间思考这些想法是值得的，通常第一次尝试写提示符。

看看会发生什么，然后从那里迭代，改进提示符，以越来越接近您需要的结果。

![](img/79fc50ec829ef4f32556d1e39e539c36_60.png)

所以很多成功的提示，你可能会在各种程序中看到使用，在这样一个反复的过程中，只是为了好玩，让我向您展示一个更复杂的提示符的示例。



![](img/79fc50ec829ef4f32556d1e39e539c36_62.png)

这可能会让你对gpt能做什么有所了解。

![](img/79fc50ec829ef4f32556d1e39e539c36_64.png)

就是嗯，我只是在描述之后添加了一些额外的说明，包括一个给出产品尺寸的表，然后你知道，格式，一切都是html，所以让我们运行它，在实践中，你会得到这样的提示，真的只有经过多次迭代。

我想我不知道有人会写这个确切的提示，他们第一次试图让系统处理概况介绍。

![](img/79fc50ec829ef4f32556d1e39e539c36_66.png)

所以这实际上输出了一堆html，让我们显示到html，看看这是否有效。

![](img/79fc50ec829ef4f32556d1e39e539c36_68.png)

看看这是否有效，我不知道这是否行得通，但让我们看看，哦酷。

![](img/79fc50ec829ef4f32556d1e39e539c36_70.png)

好啦，让我们来看看渲染，所以它有一个非常好看的椅子描述。

![](img/79fc50ec829ef4f32556d1e39e539c36_72.png)

嗯，建筑材料，产品尺寸。

![](img/79fc50ec829ef4f32556d1e39e539c36_74.png)

啊，看起来我漏掉了。

![](img/79fc50ec829ef4f32556d1e39e539c36_76.png)

呃，最多使用50个字的说明，所以这个有点长，但如果你想你知道，你甚至可以随意暂停视频。

![](img/79fc50ec829ef4f32556d1e39e539c36_78.png)

告诉它更简洁，重新生成这个，看看你会得到什么结果。

![](img/79fc50ec829ef4f32556d1e39e539c36_80.png)

所以我希望你能从这个视频中了解到，快速开发是一个迭代的过程，尝试一些东西，看看它是如何还没有完全实现你想要的，然后想想如何澄清你的指示，或者在某些情况下考虑如何给它更多的空间。

想让它更接近交付你想要的结果，我认为成为一个有效的快速工程师的关键，不是为了知道完美的提示，它是关于有一个良好的过程来开发对您的应用程序有效的提示，在这个视频中，我演示了开发一个提示符。

仅对更复杂的应用程序使用一个示例，有时你会有多个例子，比如一张十张甚至五十张或一百张概况介绍的清单，并迭代开发一个提示符，并根据大量案例对其进行评估，但对于大多数应用程序的早期开发。

我看到很多人发展它的方式，我只举一个例子，但对于更成熟的应用程序，有时，根据一组更大的示例来评估提示可能是有用的，例如在几十个概况表上测试不同的问题，查看在多个概况介绍中的平均或最坏情况表现如何。

但通常只有当应用程序更加成熟时，您才会这样做，你必须有这些指标，推动这种增量，迅速改进的最后几个步骤，因此，请一定要玩木星密码笔记本的例子，尝试不同的变化，看看你会得到什么结果，当你做完。

让我们进入下一个视频，在这里我们将讨论大型语言模型在软件应用中的一个非常常见的用法，总结一下。

![](img/79fc50ec829ef4f32556d1e39e539c36_82.png)

所以当你准备好了。