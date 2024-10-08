# LangChain_微调ChatGPT提示词_RAG模型应用_agent_生成式AI - P62：5.SC-Laurence_L4_v04.zh - 吴恩达大模型 - BV1gLeueWE5N

![](img/915f4e03e9426f118b05e783568bb8c3_0.png)

技术债无万能解。

![](img/915f4e03e9426f118b05e783568bb8c3_2.png)

但LLMs可极大助力。

![](img/915f4e03e9426f118b05e783568bb8c3_4.png)

技术债随时间由开发者传递。

![](img/915f4e03e9426f118b05e783568bb8c3_6.png)

需维护，但常难理解。

![](img/915f4e03e9426f118b05e783568bb8c3_8.png)

因编写已久，或过于复杂，或有太多依赖难改。

![](img/915f4e03e9426f118b05e783568bb8c3_10.png)

担心系统崩溃，LLMs能帮此问题？

![](img/915f4e03e9426f118b05e783568bb8c3_12.png)

或许让我们探索一种情况，让我们先设置API，所有来自utils的好东西，我将导入，获取API密钥，我还需要导入谷歌生成AI库，我将称它们为palm，然后palm点，配置API密钥。

因此我正在为palm库设置API密钥，一旦完成，我将查看我的模型，并查看可用的模型，所以如果你记得在手掌，有多种不同型号，每种都有不同能力，但我们想使用生成文本的型号，所以如果我运行并输出。

我们将看到将使用名为，models Text Bison 001的模型，记得录音时，你可能有不同的模型可用，实际上你可以选择更适合你使用的，但目前只有一个，我将使用模型0，就是那一个，最后我想做的事。

只是准备一个名为生成文本的帮助函数，我将在这里做，我将导入谷歌API核心重试，然后重试，我将传递生成文本并生成文本将仅传递，我的提示，我的模型和温度到手掌以生成文本，在这种情况下。

我将覆盖默认温度为零点零，您将看到默认温度实际上在模型本身为零点七，我将覆盖它为零点零，只是为了我可以有一些确定性输出并减少任何随机性，因此，我们现在准备开始探索我们的代码，我想用代码做什么。

查看技术债务概念，此处的技术债务情况，嗯，我有段非常复杂的代码，实际上是iOS上的Swift代码，摘自我写的一本关于创建机器学习模型的书，用于移动设备，一大段代码，我将粘贴它。



![](img/915f4e03e9426f118b05e783568bb8c3_14.png)

它所做的，都在注释中，目前都是文本，这段代码的作用是。

![](img/915f4e03e9426f118b05e783568bb8c3_16.png)

允许你从iOS设备获取图像，将该图像传递给TensorFlow Lite模型，然后使用TensorFlow Lite模型进行分类。



![](img/915f4e03e9426f118b05e783568bb8c3_18.png)

真正复杂的地方在于，为了能够进行图像转换，实际上需要读取图像的底层内存。

![](img/915f4e03e9426f118b05e783568bb8c3_20.png)

通过这样做，你在访问移动设备的内存。

![](img/915f4e03e9426f118b05e783568bb8c3_22.png)

如果你是移动开发者，你会意识到每次开始访问内存，操作系统可能认为你在做坏事。

![](img/915f4e03e9426f118b05e783568bb8c3_24.png)

应用商店可能会关闭你，所以他们有一些非常，复杂且安全的API，允许你访问设备内存。

![](img/915f4e03e9426f118b05e783568bb8c3_26.png)

因此，我不得不编写的这段代码，首先将图像的RGB数据转换为张量。

![](img/915f4e03e9426f118b05e783568bb8c3_28.png)

然后还要安全地访问设备内存，在这种情况下，iPhone。

![](img/915f4e03e9426f118b05e783568bb8c3_30.png)

如你所见，很多代码，我在这里滚动，这里有很多代码，对我来说，这是一个很好的技术债务例子。

![](img/915f4e03e9426f118b05e783568bb8c3_32.png)

如果有人构建了一个包含此代码的应用。

![](img/915f4e03e9426f118b05e783568bb8c3_34.png)

现在你继承了此应用，你真的需要了解这个应用在做什么。

![](img/915f4e03e9426f118b05e783568bb8c3_36.png)

它将如何工作，你将如何使用它等所有这些问题。

![](img/915f4e03e9426f118b05e783568bb8c3_38.png)

现在有一个很好的例子，我们可以实际使用大型语言模型来帮助理解这段代码，所以我要从一个提示开始，我将使用我通常的提示模板，我只想说，你能解释这段代码如何工作吗，将问题传递给它，然后我将使用装饰器。

使用大量细节并使其尽可能清晰，我有提示模板，可运行代码补全，生成文本，仅传递代码块，请其解释代码如何工作。



![](img/915f4e03e9426f118b05e783568bb8c3_40.png)

结果已输出。

![](img/915f4e03e9426f118b05e783568bb8c3_42.png)

结果将非常详细，对，告诉我模型数据处理器是TensorFlow模型处理器，具有以下属性。

![](img/915f4e03e9426f118b05e783568bb8c3_44.png)

具有以下初始化器，具有以下方法，甚至解释这些方法。

![](img/915f4e03e9426f118b05e783568bb8c3_46.png)

也许最有趣的是它甚至告诉我关于我的扩展方法，这是一个Swift特有的东西，允许你扩展你的类。

![](img/915f4e03e9426f118b05e783568bb8c3_48.png)

你会看到有一个扩展数据和扩展数组。

![](img/915f4e03e9426f118b05e783568bb8c3_50.png)

扩展数组和扩展数据，这是高级部分，正在复制内存缓冲区，使用我们对直接内存的不安全指针的理解。

![](img/915f4e03e9426f118b05e783568bb8c3_52.png)

但由于我们以Swift期望的方式这样做。

![](img/915f4e03e9426f118b05e783568bb8c3_54.png)

这种类型的应用有望通过应用商店。

![](img/915f4e03e9426f118b05e783568bb8c3_56.png)

它不会意识到，或，不会怀疑，我们在编写某种病毒或访问低级内存，当我们做这种事情时，现在我有了所有解释的代码，除了解释代码，猜猜它实际上还可以记录代码，所以让我们从新的提示模板开始。

我将要求你为这段代码编写技术文档，并使其易于非Swift开发者理解，并且我将要求它在装饰器中输出结果，以Markdown格式，因为当今许多技术讨论都将使用Markdown，这是一种极好的格式。

现在让我添加一个新的单元格，在其中我将仅获取完成，因此我将运行此提示模板，然后我将生成我的完成，让我们看看运行完成时会发生什么，现在我有了技术文档。



![](img/915f4e03e9426f118b05e783568bb8c3_58.png)

它们实际上是以Markdown格式完成的，如果你熟悉Markdown，所以这里它给了我模型数据处理器，类处理，所有数据预处理调用运行推断给定帧，记录公共属性。



![](img/915f4e03e9426f118b05e783568bb8c3_60.png)

它正在使用Markdown中的项目符号，这里在标题部分，在Markdown中。

![](img/915f4e03e9426f118b05e783568bb8c3_62.png)

在Markdown中使用这些哈希。

![](img/915f4e03e9426f118b05e783568bb8c3_64.png)

现在我有一个可以使用的Markdown文档，作为这门课的技术文档的开头，因此，我们可以看到，使用大型语言模型，像这样，在避免技术债务方面非常有用，这只是一个我给的例子，我曾不得不解释一些复杂的代码。

我曾不得不记录代码，但正如你所见，使用相同的技术，有很多方法可以减少你自己的技术债务，我很想看看你会用它建造什么，在我编写《AI和机器学习用于设备开发》一书时，我不得不稍微走出我的舒适区。

并为iOS设备编写Swift代码，这工作非常有趣，Swift可以是一种非常强大的语言，但也有一些情况下，作为相对新手Swift开发者，我遇到了困难，我通常不得不花费数小时寻找可能帮助我的代码示例。

一个这样的例子是将图像传递给移动神经网络，在这种情况下，我需要将底层数据从CV，像素缓冲格式转换为原始RGB数据，即意味着我需要读取内存，由于安全问题，特别是在移动设备上，这可以相当困难，最终。

在大量帮助下，我最终得到了从缓冲区获取RGB数据的函数，在您将在笔记本中看到的代码中，那是几年前的事了，我留下了几乎不记得的代码的技术债务，以及一些场景，一个是为了向其他人解释，如果他们继承了它。

另一个是做明显的工作，记录代码，甚至可能将其输出为Markdown，试试你自己，看看你能想出什么，试试你自己，看看你能想出什么。



![](img/915f4e03e9426f118b05e783568bb8c3_66.png)