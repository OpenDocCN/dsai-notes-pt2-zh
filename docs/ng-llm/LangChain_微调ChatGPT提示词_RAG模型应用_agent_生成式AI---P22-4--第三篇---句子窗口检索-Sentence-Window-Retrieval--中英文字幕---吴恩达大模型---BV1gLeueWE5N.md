# LangChain_微调ChatGPT提示词_RAG模型应用_agent_生成式AI - P22：4. 第三篇 - 句子窗口检索(Sentence Window Retrieval) 中英文字幕 - 吴恩达大模型 - BV1gLeueWE5N

在这节课中，我们将深入研究一种高级的拉格技术，我们的句子窗口检索方法。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_1.png)

在这种方法中，我们基于较小的句子进行检索，以更好地匹配相关上下文，然后，根据扩展的上下文窗口合成句子，让我们看看如何为某些上下文设置它，标准的拉格管道使用相同的文本干来同时进行嵌入和合成。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_3.png)

问题是，嵌入基础检索通常与较小的片段工作得很好，而llm需要更多的上下文和大的片段来合成一个好的答案，句子窗口检索做的就是稍微分离这两个。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_5.png)

我们首先对较小的片段或句子进行嵌入，并将其存储在向量数据库中，我们还为每个片段添加了前后出现的句子的上下文，在检索时，我们检索与问题最相关的句子，使用相似性搜索，然后，将句子替换为完整的周围上下文。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_7.png)

这允许我们扩大实际上被馈入概要的上下文，为了回答问题，这个笔记本将介绍构建一个使用单个索引的句子窗口检索器所需的各种组件，各种组件将在最后详细覆盖。

Anion将展示如何实验参数和评估与真实错误相关的性能，这是同样的设置，你在之前的课程中已经使用过，所以确保安装了相关的包，例如。

llama index和true lines email用于这个快速启动，你需要一个类似于之前许可证的开放ai密钥，这个开放ai密钥用于嵌入，嗯，Lens，以及评估部分。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_9.png)

现在我们设置并检查我们的文档，以便用于迭代和实验，类似第一课，我们鼓励你上传你自己的pdf文件，以及之前，我们将加载如何在人工智能中构建职业生涯的电子书。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_11.png)

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_12.png)

它是之前的同一份文档，所以我们看到它是一份文档列表，共有四十一页，对象模式是文档对象，这里是从第一页的一些样本文本。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_14.png)

接下来的部分将将这些合并为一个文档，因为它有助于使用更先进的检索器时提高整体文本分割的准确性。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_16.png)

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_17.png)

现在让我们设置句子窗口检索方法，我们将详细解释如何设置这个，我们将从窗口大小为三，top k值为六开始，首先，我们将导入我们称为句子窗口节点解析器的对象。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_19.png)

句子窗口节点解析器是一个对象，它将文档分成单独的句子，然后，为每个句子片段添加周围上下文的增强，这里我们演示如何节点解析器与一个小例子工作，我们看到我们的文本，它有三个句子，被分成了三个节点。

每个节点包含一个句子，包含一个包含更大句子周围上下文的元数据，我们将在这里展示第二个节点的元数据看什么样子，你看到这个元数据包含原始句子，但也包含在它前后出现的句子，我们鼓励你尝试自己的文本，例如。

让我们试试这样。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_21.png)

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_22.png)

对于这个样本文本，让我们看看周围的元数据，对于第一个节点，由于窗口大小为三，我们有两个额外的相邻节点出现在前面，当然，嗯，在它后面没有，因为它是第一个节点，所以我们看到有原始句子或你好。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_24.png)

但也是fubar和ta，下一步实际上是构建索引，并且我们首先会做是设置一个lone，在这个情况下我们将使用open，嗯，具体来说。

Gpt t three five five turbo with the temperature zero dot one。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_26.png)

下一步是设置一个service contacts对象，哪个，作为提醒，是一个包含所有必要联系以用于索引的包装对象，包括l one嵌入模型和节点解析器。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_28.png)

请注意，我们指定的嵌入模型是bg small模型，我们实际上从hugging face下载并本地运行它，这是一个紧凑，快速且准确于其大小的嵌入模型，我们也可以使用其他嵌入模型，例如。

一个相关模型是bg large，我们在下面的注释代码中有这个模型，下一步是设置向量存储索引与源文档，因为我们已经定义了节点解析器作为服务上下文的一部分，这将做是它会取源文档。

将其转换为一系列附加了周围上下文的句子，并嵌入它，并加载到向量排序中，我们可以将索引保存到磁盘上，以便您可以后来加载它而不必重建它。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_30.png)

如果您已经构建了索引，保存了它，并且您不想重建它，这里有一个有用的代码块，允许您从现有的文件加载索引，如果存在，否则它将构建它，索引现在构建好了，下一步是设置并运行Android查询。

我们将定义我们称为元数据替换后处理器的东西，这取存储在元数据中的值，并替换节点的文本为该值。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_32.png)

因此，这是在获取笔记并发送笔记到大纲之前完成的，我们将首先解释这是如何工作的。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_34.png)

使用我们使用句子窗口节点解析器创建的节点，我们可以测试这个后处理器。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_36.png)

请注意，我们备份了原始节点，让我们再看一下第二个节点，太好了，让我们在这些节点上应用后处理器，如果我们现在查看第二个节点的文本，我们可以看到它已经被替换为一个完整的上下文。

包括在当前节点之前和之后的句子，下一步是添加句子变换重新排序模型，这取查询并检索节点，并按相关性重新排序节点，使用专门为任务设计的模型，一般来说，您将使初始相似度top k更大。

然后重新排序器将恢复节点并返回一个小的top end，所以过滤出一个较小的集，一个重新排序器的例子是bg reanker base，这是基于bg嵌入的重排序器。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_38.png)

这串字符串代表从hugging face命名的模型，您可以在hugging face上找到更多关于模型的详细信息，让我们看看这是如何重新排序的，我们将输入一些玩具数据。

然后看看重新排序器如何实际重新排序，原始节点到一个新的节点集，让我们假设原始查询是我想要一只狗，并且原始节点的得分是这是只猫，但得分是0。6，然后这是只狗，得分是0。4，直觉上。

您将期望第二个节点实际上有一个更高的得分，所以它与查询匹配得更好，这就是重新排序器可以发挥作用的地方，在这里我们看到重新排序器正确地浮出水面并已知关于狗的信息，并给它了一个高的相关性得分。

现在让我们将此应用于我们之前提到的实际查询。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_40.png)

我们要求的相似度top k大于top end值，我们选择了为重新排序器，以便给重新排序器一个公平的机会来浮出水面正确的信息，我们设置了top k为6和top end等于2。

这意味着我们首先获取最相似的6个片段，使用句子检索，然后我们过滤出使用句子重新排序器最相关的两个冠军。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_42.png)

现在，我们已经设置好了完整的查询引擎，让我们运行一个基本的示例，让我们对这个数据集提一个问题。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_44.png)

我们获取到关于在ai领域建立职业生涯的关键是什么，然后我们得到响应，我们看到最终的响应是，在ai领域建立职业生涯的关键是。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_46.png)

学习基础的技术技能，参与项目并找到实习机会。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_48.png)

现在，我们已经将句子窗口查询引擎设置好了，让我们把所有的东西都放在一起，我们将大量的代码放入这个笔记本细胞中，但是请注意，这与util y文件中的函数本质上是一样的。

我们有用于构建我们之前在这本笔记本中展示的句子窗口索引的功能，它包括由节点解析器使用句子的能力，从文档中提取句子并增强其周围上下文，它包含设置句子上下文或使用服务上下文对象的功能。

它还包括使用源文档和服务联系人设置向量排序索引的功能，包含行和击球模型，并且没有解析器，这个部分的实际内容是获取句子窗口查询引擎，我们展示了它包括获取句子窗口检索器。

使用元数据替换后处理器实际上替换节点为周围上下文，然后最后使用重排模块过滤出顶级结果。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_50.png)

我们使用as查询和模块将所有这些结合起来。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_52.png)

首先，让我们调用构建句子窗口索引函数，使用源文档，鹰，以及保存目录，然后，让我们调用第二个函数来获取查询和伟大的含义，你现在准备好尝试句子窗口检索了，在下一节关于棕榈的章节中。

我们将向您展示如何实际运行评估，使用句子窗口检索器，以便您可以评估结果，并实际上玩出参数，看看这对您引擎性能有何影响，在这些例子之后，我们鼓励你添加自己的问题，甚至找到属于自己的评估基准。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_54.png)

只是为了玩一玩，看看一切都如何工作，谢谢杰瑞，现在，你已经设置了句子窗口检索器，让我们看看如何用三段式评估它，并比较其性能与基本三段式，带有实验跟踪，现在，让我们看看如何评估和迭代于句子窗口大小参数。

为了在评估指标之间做出正确的权衡，应用程序的质量和运行应用和评价的成本，我们将逐渐增加句子窗口的大小，从第一个版本开始，使用船员镜头和破布三叉戟评估这些连续的应用版本，跟踪实验以选择最佳的句子窗口大小。

随着我们进行这个练习，我们将想要了解标记使用或成本的权衡，随着窗口大小的增加，标记使用和成本会增加，在许多情况下，上下文的相关性会同时增加，在开始增加窗口大小时，我们预期会提高上下文的相关性，因此。

也会间接提高锚定性，那个的原因之一是当检索步骤没有产生足够的相关上下文时，在完成步骤中的llm倾向于通过利用预训练阶段的，现有知识来填补这些空白，而不是明确依赖于检索到的上下文片段。

这种选择可能会导致更低的接地分数，因为回忆，接地性意味着最终响应的组件应该可以追溯到检索到的上下文片段，因此，我们期待的是，随着您不断增大句子窗口大小，上下文的相关性会增加到某个点，接地性也会增加。

然后，从那一点之外，我们将看到上下文的相关性是增减不一的，扎根性也很可能遵循类似的模式，此外，上下文相关性和扎根性之间还存在一个非常有趣的关系，你可以在实践中看到，当上下文相关性低时，扎根性也往往较低。

这是因为，因为llm通常会尝试填充检索到的上下文片段中的缺口，通过利用预训练阶段的知识，这导致了扎根性的减少，即使答案实际上在语境相关性增加时变得相当相关，基础性也倾向于在某个点上增加。

但如果上下文大小变得太大，即使上下文相关性很高，可能出现基础性的降低，因为llm可能会被过大的上下文所淹没，并回归到训练阶段的预存知识库。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_56.png)

现在让我们尝试句子窗口的大小，我会带你通过一个笔记本来加载一些问题进行评估，然后逐渐增加句子窗口大小，并观察这对该rag的影响，首先，评估三叉戟指标。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_58.png)

我们加载一套预先生成的评估问题，在这里，你可以看到一些这些问题，从这份列表中，接下来，我们运行评估，对于预加载的评估问题集合中的每个问题，然后，使用真正的记录器对象，我们记录提示，响应，应用的中间结果。

以及真数据库中的评估结果，现在让我们调整句子窗口大小参数，看看那个的影响，对不同的三角形评估指标，我们将首先重置真数据库，使用这段代码片段，我们将句子窗口大小设置为一，你会发现在这条指令中。

所有其他的一切都与以前相同，然后，我们使用获取句子窗口查询引擎设置句子窗口引擎，与这个索引相关联，接下来，我们已准备好以句子窗口大小设置为一的方式设置真正的记录器。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_60.png)

这设置了拉格三重奏的所有反馈函数定义，包括答案相关性，上下文相关性和锚定性，现在，我们已经一切就绪，可以运行评估，对于设置，以句子窗口大小设置为一，和所有相关的提示，响应，中间结果。

并且这些反馈函数的评估结果，我们将登录到真实数据库，哦，K，现在运行得非常好，让我们在仪表板上查看它，你将看到，这个指令启动了一个本地托管的流let应用，并且你可以点击。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_62.png)

链接来到达修剪它，所以，应用排行榜展示了我们通过二十一个记录运行的所有聚合指标，并使用真实长矛进行了评估，这里的平均延迟是4。5秒，7秒，总成本大约是两分钱，处理总token的数量大约是9，000个。

你可以看到评估指标，应用在无关性和扎根性方面表现良好，但在上下文相关性方面，它表现较差，现在，让我们深入探讨由应用程序处理的个别记录。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_64.png)

评估，如果我滚动到右侧，我可以看到一些例子，在这些指标上，应用程序表现不佳，所以让我选择这行。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_66.png)

然后，我们可以。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_68.png)

更深入地检查它对他的影响。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_70.png)

所以，这里的问题是在项目选择和执行的背景下。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_72.png)

解释准备就绪和准备、发射、瞄准的方法之间的差异。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_74.png)

提供每个方法可能更有益的例子，"你可以在这里详细看到从布条中收集到的整体反应"。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_76.png)

"然后如果我们往下滚动"，"我们可以看到接地性的总分"。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_78.png)

"上下文相关性和答案相关性"。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_80.png)

"在这个例子中，检索到了两段上下文"，"并且对于检索的上下文的一部分"，"上下文相关性相当低"，"让我们深入探讨那个例子，仔细看看"，"在这里，通过这个例子，你将看到上下文的部分非常小。"，记住。

我们正在使用一个句子窗口的大小为一，这意味着我们在开始和结束时各添加了一句额外的句子，在检索的上下文周围，这将产生一个相对较小的缺失重要信息的上下文片段，这将使其与被问的问题相似相关，如果你看接地性。

你会看到这两个检索到的上下文片段都在最终总结中，接地的，得分相当低，让我们选择得分更高的接地性得分，它有更多的理由，如果我们看看这个例子。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_82.png)

在这里，我们看到在开始有一些句子，对于这些句子，检索到的上下文中有很好的支持证据，因此这里的得分很高，它是在0到10的尺度上的10分，但对于这些句子在这里，没有支持证据，因此接地性得分是0。

让我们拿一个具体的例子，也许这个，我认为它经常在执行成本相对较低的情况下使用，并且快速迭代和适应的能力比前期规划更重要，这感觉像是一个可能的文本，这可能作为对问题的响应的一部分有用。

然而它不在检索到的上下文中，所以它不是由检索到的上下文支持的任何证据，这可能是模型在训练阶段学到的一部分，要么是从同一文档，安德鲁在这里的职业建议文档，或者是关于AI职业建议的其他来源，讨论同样的主题。

模型可能学到了类似的信息，但它不是基于那个的，句子不是由检索到的上下文支持的，在这个特定情况下，所以这是一个普遍问题，并且句子窗口太小，上下文相关性往往较低，因此，接地性也变得缓慢。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_84.png)

因为LLM开始使用其训练阶段的预存知识，来开始回答问题，而不是仅仅依赖提供的上下文，现在我已经展示了一个失败模式，当句子窗口设置为1时。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_86.png)

我想走通几个步骤，看看指标如何改善，随着我们改变句子窗口大小，以快速浏览笔记本，我将重新加载评估问题，但在这种情况下，只设置一个问题，模型有问题的问题，这个问题，我们刚刚用句子窗口大小设置为1时走过。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_88.png)

这个问题，我们刚刚讨论过，然后，我想将这个与句子窗口大小为的句子一起运行，他说两个、三个Discord片段将要。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_90.png)

设置句子窗口大小为的rag，设置三个，并且也设置真记录器，我们现在已经设置了反馈函数的定义，除了句子窗口大小设置为三的rag之外。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_92.png)

接下来，我们将使用那个井来运行评估，对于我们详细审查的特定评估问题，使用句子窗口大小为一，在那里，我们观察到成功运行的失败模式。



![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_94.png)

现在，让我们看看这个句子窗口引擎的结果，设置为三，在真镜头仪表板中，你可以在这里看到结果，我在一个记录上运行它，那是有问题的记录，当我们看句子窗口大小为一时，你可以看到上下文的相关性大大增加。

它从零点五七增加到零点九现在，如果我选择应用程序并查看这个例子。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_96.png)

在更详细的情况下，现在，我们来看看与句子窗口大小为一时我们查看的同一个问题。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_98.png)

现在，我们处于三。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_100.png)

这里是完整的最终响应现在，如果你看检索到的上下文片段。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_102.png)

你会注意到，这个特定的检索上下文与早期我们写的上下文相似。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_104.png)

但现在它有了扩展，因为更大的句子窗口大小，如果你看这个部分的得分。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_106.png)

我们将看到，这个上下文获得了一个上下文相关性得分为零点九，这比早期获得分数为零点八的较小上下文更高，这个例子表明，随着句子窗口大小的扩大，即使是相对良好的检索上下文也可以变得更好。

一旦完成这些显著改进的上下文部分，接地得分会上升很多，我们看到，通过在这些高度相关的上下文中找到支持证据，接地得分实际上上升到一，因此，将句子窗口大小从一增加到三，导致了rag三叉戟评估指标的显著改进。

接地性和上下文相关性都显著提高。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_108.png)

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_109.png)

以及答案相关性。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_111.png)

现在，我们可以看句子窗口设置为五。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_113.png)

如果你看这里的指标，有几件事需要注意，一个是总标记数增加了，这可能会对成本产生影响，如果我们增加记录的数量，这就是我之前提到的一种权衡，随着句子窗口大小的增加，它变得更加昂贵，因为更多的标记被处理，嗯。

在评估期间，由LMS处理，另一个值得注意的事情是，尽管上下文相关性和答案无关性保持不变，扎根性实际上随着句子窗口大小的增加而下降，这可能发生在某个点之后，因为随着上下文大小的增加。

LLM在完成步骤中可能会被过多的信息所淹没，在摘要过程中，它可能会开始引入自己已有的知识，而不是仅在检索到的上下文片段中的信息，所以，让我们在这里总结一下，结果，当我们从一句增加到三句，再到五句时。

三句，对于我们特定的评估来说，三句的大小是最佳选择，我们看到上下文相关性和答案相关性，以及扎根性的增加，当我们从一句增加到三句时，然后，在增加到五句时，扎根性步骤可能会有所减少或退化。

当你在笔记本中尝试时，增加到五句的大小，我们鼓励你使用更多的记录重新运行它，在这两步中，检查个别记录，哪些对特定指标如上下文相关性或扎根性造成问题，并获取一些直觉，建立一些直觉，了解失败模式的原因。

并知道如何解决它们，在下一节中，我们将看另一个高级拖放技术，自动合并，以解决一些失败模式。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_115.png)

不相关的上下文可能会渗入最终响应，导致，嗯，不。

![](img/4a1fc26221d3b2f04bf8ca6e27e0a318_117.png)