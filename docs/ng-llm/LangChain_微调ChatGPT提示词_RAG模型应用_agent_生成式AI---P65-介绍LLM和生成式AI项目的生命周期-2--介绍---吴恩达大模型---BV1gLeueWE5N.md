# LangChain_微调ChatGPT提示词_RAG模型应用_agent_生成式AI - P65：介绍LLM和生成式AI项目的生命周期 2——介绍 - 吴恩达大模型 - BV1gLeueWE5N

欢迎回来，这周有很多令人兴奋的材料要讨论，其中，迈克首先将与您分享的主题之一，稍后会是一个关于Transformer网络如何实际工作的深入研究，是的，所以看，这是一个复杂的主题，在2017年。

论文发表了，张力就是你需要的，它详细地展示了所有这些复杂的数据处理过程，这些过程大致发生在Transformer架构内部，所以我们从较高的视角来看待这个问题，但我们也会深入探讨一些细节。

我们将讨论像自注意力和多头自注意力机制这样的东西，这样我们就可以看到为什么这些模型实际上能够工作，它们是如何真正理解语言的，这真是太神奇了，Transformer架构已经存在了多长时间。

并且对于许多模型来说，它仍然是最先进的，我记得在看到变压器论文后，你知道它最初发布的时候，我想是的，我理解了这个方程，我承认这是一个数学方程，嗯，但它实际上在做什么，它总是给人一种有点神秘的感觉。

我花了很长时间玩它，才终于理解了，好的，这就是它为什么起作用的原因，因此，我认为在第一周里，你将学习到这些术语背后的直觉，你可能之前听说过一些这些术语，比如多头注意力，那是什么，以及它为什么有意义。

以及为什么Transformer架构真正取得了成功，我认为注意力已经存在很长时间了，但我认为真正使它起飞的是它允许注意力以大规模并行的方式工作，是吗？允许注意力以大规模并行的方式工作。

所以使它在现代GPU上运行成功，并能够扩展它，我认为关于Transformer的这些细微之处，你知道并不被许多人理解，所以期待，当你深入研究那个时，绝对我意思是规模是其中的一部分。

并且它如何能够处理所有数据，我还想要说，尽管我们不会深入到这个程度，我们将让人们的头爆炸，如果他们想要那样做，那么他们可以继续阅读那篇论文，我们要做的，我们将查看那个变换器架构的重要部分。

这给你需要的直觉，这样你就可以实际地利用这些，嗯，这些模型和是的，我一直在思考，我被变换器如何，尽管这门课程专注于文本，看到基本变换器架构如何为视觉变换器创建基础也真的很有趣。

所以尽管在这门课程中你主要学习大型语言模型，关于文本的模型，我认为理解变换器也是，你知道，帮助人们理解这个非常兴奋的视觉变换器和其他模态，以及成为许多机器学习绝对关键的构建块，然后超越变换器。

未来第一周我们将覆盖的第二个主要主题是，生成式AI项目生命周期，我知道很多人在思考，所有这些lm东西，我该如何使用它，以及AI项目生命周期的性别，我会稍后谈论，它帮助你规划如何思考构建你自己的AI项目。

以及生成式AI项目生命周期将带你走过个体阶段和决策，当你开发生成式AI应用时，你需要首先决定，是否从货架上取一个基础模型，还是实际上预训练你自己的模型，然后作为后续，你是否想要找到并定制那个模型。

也许为你的特定数据，是的，实际上有很多大型语言模型选项，你知道一些开源的，一些不开源的，我看到许多开发者在思考，我该如何选择这些模型，因此有一个方法来评估它，然后也选择正确的模型大小。

我知道在你的其他工作中你谈论过，何时需要一个大型模型，你知道一个万亿或甚至更大的，与一个一亿到三十亿参数模型，甚至小于一亿参数模型对于特定应用多么出色，可能有一些用例你真的需要模型。

以便非常全面并能够概括到许多不同的任务，那就是你可能遇到的一些用例，你可能只是在优化一个特定的用例，对，你可以与较小的模型合作，并且可能获得类似的甚至非常好的结果，是的。

我认为这可能是一些人需要学习的一个真正令人惊讶的事情，那就是你可以实际上使用相当小的模型，仍然能从中获得相当多的能力，是的，你知道，当你想要你的大规模语言模型对世界有广泛的知识时。

当你想要了解历史、哲学和科学等知识，以及如何编写Python代码等等，有一个巨大的模型，含有数百亿个参数是有帮助的，但对于一个任务，比如摘要对话，或作为客服代理，对一个公司，对于这样的应用程序，你知道。

你可以使用一百亿，数百亿个参数模型，但这并不总是必要的，所以，这周有很多令人兴奋的材料可以进入，让我们继续看下一个视频，当Mike开始时。

