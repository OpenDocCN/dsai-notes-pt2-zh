# LangChain_微调ChatGPT提示词_RAG模型应用_agent_生成式AI - P27：3——记忆 - 吴恩达大模型 - BV1gLeueWE5N

![](img/c86c51310bd0360f0802bd988e1cb8c6_0.png)

![](img/c86c51310bd0360f0802bd988e1cb8c6_1.png)

当你与这些模型交互，它们自然不会记得你之前说过什么或之前的对话，这是一个问题，当你构建像聊天机器人这样的应用程序时，你想与他们进行对话，因此，在这一节中我们将涵盖记忆。

基本上是如何记住对话的前一部分并将其输入语言模型，这样他们就可以在你与他们交互时有这种对话流程，是的，所以lang提供了多种复杂的选项来管理这些记忆，让我们深入了解一下，所以让我先导入我的API密钥。



![](img/c86c51310bd0360f0802bd988e1cb8c6_3.png)

然后让我导入一些我需要使用的工具。

![](img/c86c51310bd0360f0802bd988e1cb8c6_5.png)

让我们以管理聊天或聊天机器人的对话为例。

![](img/c86c51310bd0360f0802bd988e1cb8c6_7.png)

使用lag chain来管理。

![](img/c86c51310bd0360f0802bd988e1cb8c6_9.png)

所以要做这件事，我将将lm设置为openai的聊天接口。

![](img/c86c51310bd0360f0802bd988e1cb8c6_11.png)

温度等于0，并且我将使用记忆作为对话缓冲记忆。

![](img/c86c51310bd0360f0802bd988e1cb8c6_13.png)

稍后你会看到这是什么意思，嗯，然后我将再次构建对话链。

![](img/c86c51310bd0360f0802bd988e1cb8c6_15.png)

在这门短课程中，Harrison将更深入地探讨链和lag chain到底是什么，所以现在不要过于担心语法的细节，但这构建了一个llm，如果我开始对话，对话点预测，给定输入嗨。



![](img/c86c51310bd0360f0802bd988e1cb8c6_17.png)

我的名字是安德鲁，让我们看看它说什么 你好，很高兴见到你 是的 等等，然后假设我问它，1加1等于几，嗯 1加1等于2，然后再次问它，你知道我的名字吗，你的名字是安德鲁，正如你之前提到的。



![](img/c86c51310bd0360f0802bd988e1cb8c6_19.png)

有一点讽刺的味道，不确定，所以如果你想，你可以将verbals变量设置为真，看看当运行预测高时lang chain实际上在做什么。



![](img/c86c51310bd0360f0802bd988e1cb8c6_21.png)

我的名字是安德鲁，这是lang chain生成的提示，它说以下是人类和AI之间的对话。

![](img/c86c51310bd0360f0802bd988e1cb8c6_23.png)

作为健谈和等等。

![](img/c86c51310bd0360f0802bd988e1cb8c6_25.png)

所以这是lang chain生成的提示，让系统，有一个希望和友好的对话，并且它必须保存对话，保存对话，这里是回应，当你执行这个时。



![](img/c86c51310bd0360f0802bd988e1cb8c6_27.png)

嗯，因果的第二三部分，它保持提示如下，注意当我念出我的名字时，这是第三个术语。

![](img/c86c51310bd0360f0802bd988e1cb8c6_29.png)

这是我的第三个输入，它已将当前对话存储如下。

![](img/c86c51310bd0360f0802bd988e1cb8c6_31.png)

你好，我叫安德鲁，1加1等，因此，对话的历史越来越长。

![](img/c86c51310bd0360f0802bd988e1cb8c6_33.png)

实际上在顶部，我用内存变量存储了记忆。

![](img/c86c51310bd0360f0802bd988e1cb8c6_35.png)

所以如果我打印内存缓冲，它已存储到目前为止的对话。

![](img/c86c51310bd0360f0802bd988e1cb8c6_37.png)

你也可以打印这个。

![](img/c86c51310bd0360f0802bd988e1cb8c6_39.png)

内存加载内存变量，嗯，这里的花括号实际上是一个空字典。

![](img/c86c51310bd0360f0802bd988e1cb8c6_41.png)

有一些更高级的功能你可以使用。

![](img/c86c51310bd0360f0802bd988e1cb8c6_43.png)

但在这门短课程中我们不会讨论它们，所以不用担心。

![](img/c86c51310bd0360f0802bd988e1cb8c6_45.png)

为什么这里有一个空的花括号，但这是lang chain记住的。

![](img/c86c51310bd0360f0802bd988e1cb8c6_47.png)

到目前为止对话的记忆，它只是AI或人类所说的一切，我鼓励你暂停视频并运行代码。

![](img/c86c51310bd0360f0802bd988e1cb8c6_49.png)

lang chain存储对话的方式是使用这个对话缓冲内存。

![](img/c86c51310bd0360f0802bd988e1cb8c6_51.png)

如果我使用组合。

![](img/c86c51310bd0360f0802bd988e1cb8c6_53.png)

缓冲内存指定几个输入和输出，这就是你如何向记忆中添加新东西。

![](img/c86c51310bd0360f0802bd988e1cb8c6_55.png)

如果你想明确地这样做，记忆，保存上下文说你好。

![](img/c86c51310bd0360f0802bd988e1cb8c6_57.png)

怎么了，我知道这不是最令人兴奋的对话。

![](img/c86c51310bd0360f0802bd988e1cb8c6_59.png)

但我想让它有一个简短的例子，有了这个，这就是记忆的状态。

![](img/c86c51310bd0360f0802bd988e1cb8c6_61.png)

再次让我实际上显示，嗯，内存变量现在，如果你想添加额外的。

![](img/c86c51310bd0360f0802bd988e1cb8c6_63.png)

嗯数据到内存，你可以继续保存更多上下文，因果继续不多。

![](img/c86c51310bd0360f0802bd988e1cb8c6_65.png)

只是冷静地挂着，如果你打印出内存。

![](img/c86c51310bd0360f0802bd988e1cb8c6_67.png)

你知道现在有更多的内容，所以当你使用大型语言模型进行聊天对话时。

![](img/c86c51310bd0360f0802bd988e1cb8c6_69.png)

嗯大型语言模型本身实际上是无状态的。

![](img/c86c51310bd0360f0802bd988e1cb8c6_71.png)

语言模型本身不记对话，每笔交易，每次API调用独立。

![](img/c86c51310bd0360f0802bd988e1cb8c6_73.png)

聊天机器人，仅因为通常有代码提供，迄今为止的完整对话作为上下文。

![](img/c86c51310bd0360f0802bd988e1cb8c6_75.png)

因此内存可以明确存储。

![](img/c86c51310bd0360f0802bd988e1cb8c6_77.png)

嗨，我叫安德鲁，很高兴见到你等，这种内存存储用作输入或附加上下文。

![](img/c86c51310bd0360f0802bd988e1cb8c6_79.png)

以便它们可以生成输出，就像只有下一个对话回合。

![](img/c86c51310bd0360f0802bd988e1cb8c6_81.png)

知道之前说了什么。

![](img/c86c51310bd0360f0802bd988e1cb8c6_83.png)

随着对话变长，所需内存量变得非常长，发送大量令牌到LM的成本也会增加。

![](img/c86c51310bd0360f0802bd988e1cb8c6_85.png)

通常按需要处理的令牌数收费。

![](img/c86c51310bd0360f0802bd988e1cb8c6_87.png)

因此链提供了几种方便的内存类型。

![](img/c86c51310bd0360f0802bd988e1cb8c6_89.png)

以存储和累积对话。

![](img/c86c51310bd0360f0802bd988e1cb8c6_91.png)

我们一直在看对话缓冲内存，让我们看看另一种类型的内存。

![](img/c86c51310bd0360f0802bd988e1cb8c6_93.png)

我将导入对话缓冲窗口AR。

![](img/c86c51310bd0360f0802bd988e1cb8c6_95.png)

它只保留一段内存，我设置内存为缓冲窗口内存，k等于一。

![](img/c86c51310bd0360f0802bd988e1cb8c6_97.png)

变量k等于一，指定我只想记住一次对话交换。

![](img/c86c51310bd0360f0802bd988e1cb8c6_99.png)

即一次我的回合，和一次聊天机器人的发言。

![](img/c86c51310bd0360f0802bd988e1cb8c6_101.png)

所以现在如果我让它保存上下文嗨，怎么了，不只是挂着。

![](img/c86c51310bd0360f0802bd988e1cb8c6_103.png)

如果我查看内存加载变量。

![](img/c86c51310bd0360f0802bd988e1cb8c6_105.png)

它只记得最近的发言，注意'嗨'被丢弃。

![](img/c86c51310bd0360f0802bd988e1cb8c6_107.png)

怎么了，它只说人类说不多，只是挂着，AI说酷。

![](img/c86c51310bd0360f0802bd988e1cb8c6_109.png)

因为k等于一，这是一个很好的功能。

![](img/c86c51310bd0360f0802bd988e1cb8c6_111.png)

因为它让你跟踪最近的几次对话。

![](img/c86c51310bd0360f0802bd988e1cb8c6_113.png)

实践中你可能不会用k等于一，你会用k设置为较大的数字。

![](img/c86c51310bd0360f0802bd988e1cb8c6_115.png)

嗯，但这防止了内存无限制增长。

![](img/c86c51310bd0360f0802bd988e1cb8c6_117.png)

![](img/c86c51310bd0360f0802bd988e1cb8c6_118.png)

随着对话变长，如果我们重新运行刚才的对话，我们说嗨，我叫安德鲁。

![](img/c86c51310bd0360f0802bd988e1cb8c6_120.png)

1加1等于几，我叫什么名字。

![](img/c86c51310bd0360f0802bd988e1cb8c6_122.png)

因为k等于一，它只记得最后交流。

![](img/c86c51310bd0360f0802bd988e1cb8c6_124.png)

哪个是一加一，答案是1，加等于2，然后它忘记了，这个早期交流。

![](img/c86c51310bd0360f0802bd988e1cb8c6_126.png)

现在说抱歉，我没有访问这些信息。

![](img/c86c51310bd0360f0802bd988e1cb8c6_128.png)

我希望你会暂停视频，在左边的代码中改为true，并重新运行此对话，verbose等于true。

![](img/c86c51310bd0360f0802bd988e1cb8c6_130.png)

然后你会看到实际使用的提示。

![](img/c86c51310bd0360f0802bd988e1cb8c6_132.png)

当你调用lm时，希望你能看到记忆。

![](img/c86c51310bd0360f0802bd988e1cb8c6_134.png)

我叫什么名字，记忆已经丢失这个交流，我学到，我叫什么名字，这就是为什么现在说不知道，我叫什么名字。

![](img/c86c51310bd0360f0802bd988e1cb8c6_136.png)

使用对话令牌缓冲记忆，记忆将限制保存的令牌数。

![](img/c86c51310bd0360f0802bd988e1cb8c6_138.png)

因为许多lm定价基于令牌，这更直接地映射到lm调用的成本。

![](img/c86c51310bd0360f0802bd988e1cb8c6_140.png)

如果我设定最大令牌限制等于五十，实际上让我插入一些注释。

![](img/c86c51310bd0360f0802bd988e1cb8c6_142.png)

比如对话是人工智能是什么惊人的反向传播，美丽的教堂是什么迷人的，我用abc作为所有这些国家术语的第一个字母，我们可以跟踪何时说了什么。



![](img/c86c51310bd0360f0802bd988e1cb8c6_144.png)

如果我以高令牌限制运行，它几乎有整个对话，如果我增加令牌限制到一百，现在它有整个对话，人工智能的标志是什么，如果我减少它，那么你知道它切掉了对话的早期部分，以保留对应最近交流的令牌数。

但受限于不超过令牌限制，如果你想知道为什么我们需要指定，因为不同的lm使用不同的计数令牌方式，所以这告诉它使用聊天openai lm使用的计数令牌方式。



![](img/c86c51310bd0360f0802bd988e1cb8c6_146.png)

我鼓励你暂停视频并运行代码，并尝试修改提示以查看是否可以得到不同的输出，最后，这里有一种我想说明的最后一种记忆，即对话摘要缓冲记忆。



![](img/c86c51310bd0360f0802bd988e1cb8c6_148.png)

想法不是限制记忆到固定数量的令牌。

![](img/c86c51310bd0360f0802bd988e1cb8c6_150.png)

基于最近的陈述，而是基于最相关的陈述，或固定对话次数。

![](img/c86c51310bd0360f0802bd988e1cb8c6_152.png)

用语言模型写对话摘要。

![](img/c86c51310bd0360f0802bd988e1cb8c6_154.png)

让那成为记忆，示例如下。

![](img/c86c51310bd0360f0802bd988e1cb8c6_156.png)

我将创建某人日程的字符串，你知道与产品团队的会议，你需要PPT演示等，这是长字符串说。

![](img/c86c51310bd0360f0802bd988e1cb8c6_158.png)

你的日程是什么，你知道，中午在意大利餐厅结束，与客户，带上笔记本电脑，展示最新电影演示，因此让我使用对话摘要。



![](img/c86c51310bd0360f0802bd988e1cb8c6_160.png)

缓冲，内存，嗯，最大标记限制为400。

![](img/c86c51310bd0360f0802bd988e1cb8c6_162.png)

在这种情况下，很高的标记限制，我将要。

![](img/c86c51310bd0360f0802bd988e1cb8c6_164.png)

我们以'你好'开始的一些对话术语，怎么了，没，就挂着，嗯，酷。

![](img/c86c51310bd0360f0802bd988e1cb8c6_166.png)

今天日程上有什么，回答是。

![](img/c86c51310bd0360f0802bd988e1cb8c6_168.png)

你知道那长长的日程，现在这段记忆包含了很多文本。

![](img/c86c51310bd0360f0802bd988e1cb8c6_170.png)

实际上让我们看看记忆变量，包含全部文本，400个标记足够存储，但若减少最大标记数，比如100个标记，记住存储全部对话历史，若减少标记数至100，实际上使用了OpenAI的lm端点，因为我们说过。

让lm生成对话摘要，所以摘要是人类和AI闲聊，通知人类早会，blah blah blah，嗯，与对AI感兴趣的客户午餐会议，因此，如果我们进行对话，使用此LM，让我创建对话链，与之前相同，嗯。

假设我们要问。

![](img/c86c51310bd0360f0802bd988e1cb8c6_172.png)

你知道输入，展示什么好呢？我说详细为真，所以这是提示，Dlm认为对话已讨论这些，因为那是对话总结，仅一点注意，如果你熟悉openai聊天API端点，有一个特定系统消息，在这个例子中。

这不是使用官方OpenAI系统消息，只是将其作为提示的一部分，但它仍然工作得很好，考虑到这个提示，你知道，输出基本上很有趣，发展正在展示我们最新的NLP能力，好的，那很酷，好吧，你知道，给酷演示提建议。

让你思考，如果见客户，我会说，伙计，若开源框架可用，助我建酷NLP应用，好东西，比如，有趣的是，看内存发生了什么，注意，这里整合了最新AI系统输出，我询问的演示不会好，已集成到系统消息中，嗯。

你知道到目前为止的对话概要，缓冲内存，它试图做的是保持消息的显式存储，直到我们指定的标记数为止，所以你知道这部分显式存储，或尝试限制在一百个标记，因为这是我们要求的。

然后任何超出部分它将使用lm生成摘要，这就是上面所见的，尽管我已用聊天示例，说明了这些不同记忆，这些记忆对其他应用也有用，在那里你可能不断收到文本片段，或不断收到新信息，例如。

如果你的系统反复在线搜索事实，但你想保持总记忆量，不要让列表任意增长，我建议你暂停，视频并运行代码，你看到几种内存。



![](img/c86c51310bd0360f0802bd988e1cb8c6_174.png)

嗯，包括基于交换次数或标记数的缓冲内存，或可总结超过一定限制标记的内存。

![](img/c86c51310bd0360f0802bd988e1cb8c6_176.png)

实际上，该链还支持其他类型的内存，最强大的是向量数据内存。

![](img/c86c51310bd0360f0802bd988e1cb8c6_178.png)

如果你熟悉词嵌入和文本嵌入。

![](img/c86c51310bd0360f0802bd988e1cb8c6_180.png)

向量数据库实际上存储这样的嵌入（如不知道，别担心）。

![](img/c86c51310bd0360f0802bd988e1cb8c6_182.png)

别担心，哈里森稍后会解释，然后检索最相关文本块，使用这种向量数据库存储记忆。

![](img/c86c51310bd0360f0802bd988e1cb8c6_184.png)

Lankan也支持实体记忆，适用于你想记住特定人或特定实体的细节时。

![](img/c86c51310bd0360f0802bd988e1cb8c6_186.png)

比如谈论特定朋友，可以让Lang Chain记住关于那个朋友的事实，这应该以明确方式作为实体。

![](img/c86c51310bd0360f0802bd988e1cb8c6_188.png)

在使用Lang Chain实现应用时，也可以使用多种类型的记忆。

![](img/c86c51310bd0360f0802bd988e1cb8c6_190.png)

如使用视频中看到的对话记忆类型之一，另外，还有实体记忆以回忆个人。

![](img/c86c51310bd0360f0802bd988e1cb8c6_192.png)

这样你可以记住对话的概要，以及关于对话中重要人物的重要事实的明确存储方式。

![](img/c86c51310bd0360f0802bd988e1cb8c6_194.png)

当然，除了使用这些记忆类型，开发人员将整个对话存储在传统数据库中也不罕见，某种键值存储或SQL数据库。



![](img/c86c51310bd0360f0802bd988e1cb8c6_196.png)

因此可以回顾整个对话，用于审计或系统改进。

![](img/c86c51310bd0360f0802bd988e1cb8c6_198.png)

这就是内存类型，希望您觉得有用。

![](img/c86c51310bd0360f0802bd988e1cb8c6_200.png)

构建自己的应用，现在让我们继续下一视频，学习语言链的关键构建块。

![](img/c86c51310bd0360f0802bd988e1cb8c6_202.png)