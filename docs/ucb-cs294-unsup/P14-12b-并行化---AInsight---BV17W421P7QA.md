# P14：12b 并行化 - AInsight - BV17W421P7QA

好的，这是讲座的最后一部分，我想它可能只有大约半小时左右，关于并行化和转换器，这可能与以前我们学习的内容不同，关于如何实际训练这些转换器，例如，gpt三有1750亿个参数。

你不能将这个数量装入单个GPU，你需要在多个GPU上训练，甚至数百或数千个，以及如何确切地做到这一点，这是计算的主要类型概述，TPU与GPU，嗯，我不会深入探讨这些硬件的不同方面。

但是有一些关于这些硬件类型的知识，你可以以类似的方式理解，嗯，你可以根据FLOPs来理解它们，基本上有多少操作，每秒可以进行多少浮点数操作，HBM大小，这是内存大小，对于100。

它可能是80GB或40GB的TPU，这可能是16到32，另一个重要因素，我们将在剩余的讨论中提到，这种演示的主要带宽，主要是设备之间的互联带宽，这非常重要，因为你在16个GPU上训练。

你需要在这些设备之间进行某种形式的通信，这将非常重要，因为它将决定，你可以训练多大的模型，你想要处理多少数据，我将稍后详细讨论，这些模型的基础构建块，至少大多数模型都是，基本上转换器，然后你可以编写。

它只是90%的哺乳动物，或99%的哺乳动物，嗯，这些GPU和TPU可以做的就是大规模矩阵乘法，嗯，稍微不同的方式，GPU有许多小的计算单元，嗯，例如，8x4x8，但比TPU多，TPU，嗯。

有许多小的计算单元，但比GPU少，但比GPU少，在一个脉动数组中，处理程序的方式与在单个设备上不同，但在更大的规模上，基本上，更大的块，但在最后，这些设计的最终目标是它们可以像极快地处理矩阵乘法一样。

这也是我们为什么，我想这可能就像一个循环，就像变压器工作并很好地扩展在我们的快速设备上，因为它们主要是矩阵乘法，并且它们很容易优化，这使得人们开发硬件，使得这种乘法越来越快。

然后人们喜欢使用粘附式变压器，或基于映射模式的计算，因为这个原因，否则，如果你不这样做，对于基于状态的模型，矩阵乘法的数量较少，所以它们有时只是更慢，纯粹从硬件上看，因为这个原因。

尽管从理论上它们应该更快，是的，等等等等，抱歉，我不知道这个，是的，好的，现在，我们知道矩阵乘法基本上由许多块组成，对，你有你的qkv投影计算，你有像你的mlp这样的投影进投影出层。

你有像你的输入密集层，你的输出逻辑层，它们都是矩阵乘法，所以，模型分片在多个设备上的基本构建块，假设我们有一千个GPU，如果我们在训练一个模型，我们如何分片我们的模型，或如何分割我们的训练。

以便实际上可以在所有这些GPU上运行，并且高效，这个构建块的基础就是更多的分片，如果你想要乘以两个矩阵，所以y等于x*a，他们都是矩阵，他们可以有任何形状，让我们假设他们都是正方形，嗯。

你可以做不同类型的分片，所以，假设你在a上进行行分片，在b上进行列分片，由不同的颜色定义，那么，这就是矩阵乘法的工作方式，如果你把它展开，那么乘以这个，这就是顶部左上角的一部分，看，所以是的。

所以实际上我们只是然后如果乘以这个部分，所以这两个列的第一两列，这个两列的第一行，乘以这个两行的第一列，那么你将得到顶部左上角组件的部分和，因为全和更容易，如果我去就像这个满和是这个乘以这个。

但现在我们做的只是，让我们说一半，所以这次这个，所以那意味着什么就是嗯，让我们说那个部分和是y一，然后y二就像这个东西乘以这个，所以这就像矩阵乘法的一种分片方式。

因为在这种情况下你是分片像那个点积部分的加法，然后你可以做的就是如果你乘以，假设首先处理包含所有半列的那一行，然后你可以计算出那一整行的部分和，你可以对整个矩阵这样做，所以基本上如果你乘以这两个半部分。

那么你将得到基本上整个矩阵的部分和，所以最终的结果是这两个的和，所以你实际上是将这个计算分解成两个独立的矩阵乘法计算，你正在将这一个矩阵乘法的计算分解成两个单独的矩阵乘法计算，其中绿色部分在一个设备上。

假设，然后，蓝色的部分也被存储在设备上，问题是我怎么能计算出整个矩阵乘积的结果，你可以在每个设备上分别计算部分，然后，在那之后，你需要在不同的设备上进行像减少这样的操作，嗯，将它们发送到实际上产生。

像原始的y结果，或完整的输出结果，你想要，对这个有任何问题吗，好的，这是另一种分片方式，所以假设你有你的全部x存储在一个设备上，然后你有，让我们说，一个表的列或一半的列存储在像，让我们说，前两列。

在第一个设备上进行排序，然后如果你进行矩阵乘法，那么你得到的不是部分和是，你只是现在有了输出的一部分对吗，然后让我们假设在设备二是没有人的，哦，是的，在设备二中，你将有一个，你有像x的复制品。

所以x是整个张量x将在设备一上存储，整个张量x将在设备二上存储，然后设备一将携带一部分，将携带一个一，设备二将携带一个二，他们各自计算像自己的一部分的矩阵乘法，然后每台设备将有自己的像一半的东西。

最后如果你想要传达，完整的结果，你可以只做像一个聚集者，或者你可以将每半的结果传达给每台设备以便拥有完整的结果，所以这种类型的保持心中那就是像沟通的部分就来了，在像带宽的方面，像，沟通越快，开销就越少。

因为这种情况下，通信确实需要成本，因为你必须等待结果返回，如果非常快，你不需要等待太久，如果非常慢，它可能像网络中的主要瓶颈，所以这是如何处理大量信息，嗯，但这是如何地图更多分片。

在不同种类的线性层中工作，那么让我看看这里有没有1，好的，嗯，我们就谈谈这个，好的，那么你有，你有x x在这里，所以这是你的输入，然后我们现在可以忽略这个，所以所以发生的事情是你你可以将x分成两部分。

然后，你可以像你们描述的那样做部分和，然后，这就是基本情况，嗯，在第一组幻灯片中，我们讲了什么，在哪里，x和a都被分片，然后，如果你想要计算整个y，你可以做全聚，所以gg这里是全聚，或者在这种情况下。

我们叫什么全减，基本上，全减就是，这将需要您所有设备的计算资源，就像您的网络，然后它将在所有设备上汇总相同的张量，所以在这种情况下您有两个设备，所以全减将计算每个设备的y1加上y2，最后。

y为什么将被存储在每个设备上，如果您有三个设备，它将等于y1加上y2，y3或y1加上y2加上y3，嗯，然后我在这里做的部分是f在这里，就像这样，我猜f在这里是一个分裂，所以x被分裂为x1和x2。

类似于我们显示的图表，然后您做反向传播的方式，这基本上是这个这里用于的，是这里g只是身份反向传播，然后这里f就像在反向传播中的all gather，因为从一种角度来看，当您反向传播时。

现在您有像dl dx1和dl dx2这样的偏导数，但现在您需要dl dx嗯，这基本上是我们前向过程的反向，所以不是分裂，我们设备间同步收集，然后列并行类似于我们描述的第二个，我们在这种情况下。

所以f在这里是身份，x被复制，然后现在a是对列的分裂，然后您可以计算y1和y2，然后您可以做all gatherer来获取您的完整y，反向传播的方式类似，因为前向传播是all gather，现在。

在这里反向传播是我们分裂梯度，然后我们反向传播，然后嗯，然后在最后一部分，我们基本上有来自a每个部分的梯度，所以您需要在所有设备上做，减少过，嗯，过您的设备，相反，是的，答案是a就像这两种的结合。

我想我们谈论，我们将看到，是的，我会在接下来一滑上，我想我已经刚刚谈论过，所以我们可以跳过这个，所以这就是我提到的所有，Okay。

So this is how it's done in practice，Which is a little bit more efficient。

Basically the idea is you want to reduce your communication as much as possible。

Like communication is is a is an overhead，You want it you want to like reduce。

And so the less communication operations you do，The better it usually is。

So this is an example of like the mlp，So basically you have your input x and then you project out into like a higher hidden dimension。

And then you project back down，And the way this works is that you can basically do replicate。

And then column sharding here，So this case x is not is not sharded。

And then only your weight matrices here are sharded，A one and a two。

And then and then so you compute that map mole，You compute your activation as usual in the mlp。

And then you have y one y two and then usually here in the standard thing。

If you wanted why you would have to do an all gather。

But because of the way this is constructed is that you can take advantage of that。

This thing is already sharded，And then it's like the the row sharded version now。

Because it is in the row sharded version，We had to take your take。

Let's say x and we had to split it into x one x two，But here it's already split into y one y two。

So then we can just feed it into like a row parallel version，And then have the sharded。

B one b two do the computation，And then g there would be an all reduce，Um。

And then the backwards pass would be kind of similar to what i described where uh。

Where g would be identity，And then f there would be like an all reduce in the backwards pass。

But this is like the fundamental building block of，How like the mlp works and also very similar。

Which i'll show is how the attention works as well，Yes，What they say。

B is the uh weight matrix that will map from um，So let's say for for the standard。

Mlp a would be like like，It would map from dimension d to four d。

And then b would be a matrix that maps from four d to d，Yeah。

Any questions about this is this is probably you're gonna take away one thing。

Should it should be this，Yeah，Yeah，嗯，在这种情况下，它们已经，它们已经预先分割，就像那样，就像你，嗯，它们永久存储在不同的设备上，它们永远不会集体通信。

因为你不需要这样做，所以当你初始化时，它们已经分割，是的，只是，是的，正是如此，如果你有另一个副本，它将只是相同的，嗯，这是这份精确的副本，这样减少了中间不必要的通信，基本上，酷，还有其他的吗，是的。

我会说是的，就像就像是的，这是gpu1，这是gpu2是的，是的，这取决于如果你在做pi torch，它是明确编码的，是的，如果你在做jax，它们有时可以为你做，是的嗯酷，所以注意力基本上是同样的方式。

它具有基本相同的结构，所以你有x在这里，它是复制的，在这种情况下，嗯，你的q kv投影矩阵是分割的，这个分割方式的好处是它是按头分割的，也就是说，如果如果我的注意力层有四个头，并且我有两个设备。

那么每个设备都会在nc two heads或像存储两个分离的头，然后头之间的注意力计算是完全独立的，正确，你可以单独做那个，你可以这样做，没有像跨头交互，至少一开始没有，所以你可以做标准的事情，嗯。

计算你的q和k的点积，Softmax，你可以做dropout，然后乘以你的值，你的值，然后你得到y1和y2，所以这些都是来自两个不同头部部分的结果，然后现在类似于已经分割的情况，y1 y2。

所以然后输出它也有，也有类似一个输出投影，本质上是跨头部混合，所以然后你可以做一个类似的事情，把你的输出全连接层分割成两部分，做你的乘法，然后有一个另外的all reduce。

它几乎是与mlp风格相同的，是的，分片和并行，哦，分片就是并行化，它们是一码事，它们是相同的，是的，是的，它是并行化，我需要计算一个大型哺乳动物，我可以将其分为两部分，在两台不同机器上。

在两个不同设备上，所以最优情况下它将是两倍的速度，是的，有时间加速，然后也有，我猜主要的，主要的主要目的是，嗯，有时间加速，但另一个好处是，你分片了你的参数，如果你有一个非常巨大的模型。

那么你将你的参数分布在不同设备上，因此它节省了内存，为什么我们不从q开始，Kv或，嗯，在这个情况下它们已经，它们已经分片了，因为qkv的投影矩阵已经分片了，我不确定我是否完全理解你的问题，嗯。

它们将接收不同的更新，我猜没有分享它们的目的，那就是一种你可以做分片和变压器的通用方法，现在，我将讨论这种分片是如何具体使用的，在并行性的不同形式方面，我将覆盖其中的一些，有很多不同种类。

但覆盖像几个主要子集，你们中的一些可能很熟悉第一个，那就是数据并行性，或者是任何其他东西，那就是数据并行性，嗯，我们到这里了，你可以基本上把它看作是，让我们说理解这个图的方法是，嗯，它就是一些张量。

而且这里的y是批量维度，其中每一行都是一个单独的批量元素，然后x或水平是，你是，你是你隐藏的维度，或者就像你的你的你的代表，一些e维的代表，所以这形状就像batch by e e ok，然后权重是。

让我们说一个e by e矩阵，输出也像batch by e，因为我们正在乘以一个ee矩阵和数据并行性是简单的，所以这可以处理每个颜色，让我们说绿色作为设备一，蓝色作为设备二，然后这种情况下，e就像是。

它在它们两者之间是复制的，这就是为什么它是黄色的原因，我猜绿色、蓝色和黄色，也许嗯，但是是的，但是但那是复制的，所以这就是你们大多数人可能已经做过的事情，如果你在多块GPU上训练过任何东西，嗯。

在这种情况下，它就像被分割到多个设备上，这样你就可以看到哪一个被复制，然后，你的批次被分割，假设你有一个全局批次大小为四，你有两个设备，你可以在每个设备上做批处理大小为二，这样可以节省你的记忆。

它也可以节省你的时间，取决于你的主要限制是什么，好的，这就是数据并行性，还有一种非常流行的并行方法叫做完全分片数据并行，这相当简单，它非常有用，相对容易理解，所以它仍然是完全数据并行。

在每种设备都会看到自己的批次，所以每种设备都会看到两个不同的元素，让我们说，在数据并行中，你会在所有设备上复制你的权重，但是现在在这种情况下，让我们假设如果我们将它们分散在所有设备上会发生什么。

所以设备一有这个矩阵的一半，设备二有其他的一半，然后我们要计算输出，我没有确切地解释输出是如何的，我想是的，实际上这就是这里分片的方式，这就是你计算输出的方式像，所以对于设备一。

您在绿色块上进行前向传播，然后现在，要做乘法，你需要，你需要完整的矩阵，所以你把所有的都放在一起，所以你们所有人都在你的设备上聚集，所以基本上当他们都聚集在一起后，每个设备都会看到整个e矩阵。

几乎就像被复制了一样，你以这种方式给它，我会解释这实际上有多有用稍后，但是一旦你有完整的矩阵，然后你可以做你的标准前向传播矩阵乘法来计算批量，但是，这里有一个美好的事情，是，你需要一次只做一层。

因为在完全的标准数据并行性中，你将整个模型复制到所有设备上，所以，所有设备在任何时候都存储整个模型参数权重，这可能真的很大，我的意思是，一七十五亿，就像，嗯，七百七十个G，或者可以是三百五十个G。

取决于精度，嗯，但是SDP的一个好处，我想这就是它被称为的，嗯作为一个缩写，嗯是您只需要一次一层，所以让我们说当我在计算时，所以，那么假设有一个层，我在这里减去一，我是，我是，我已经收集了我的e。

所以我有完整的e by e矩阵，然后我在做那个计算，在做计算的同时，我可以异步地与后面的层通信，所以这是关于，"So there's no" 翻译成中文是 "所以没有"。

这句话通常用于表示某件事情不存在或没有发生。例如：这句话的中文翻译是："这里没冲突。"，"I the device can do communication" 翻译成中文是："我设备可以进行通信。"。

"并且它可以同时进行计算"，那就是有点像关键的事情，所以基本上只要你的计算时间足够长，"以至于在计算完成时"，它到达下一层。

"Hopefully it's already been all gathered" 翻译成中文是："希望一切都已经收集好了。"，"你可以进行计算"，然后你就可以继续前进，然后你完成了计算之后。

你可以将e重新分解，然后保留特定设备的碎片，这就是为什么它节省内存，它保留了整个权重矩阵，但仅适用于时间层的单一层，这要便宜得多，尤其是对于非常深的网络，好的，所以，这个的数学方面，某种程度上。

就像我所提到的，就像网络一样。只要计算时间足够长，就像只要，我的计算时间足够长，长到超过所有成员聚集到下一层的时间。这样，就不会有额外的开销。那么，问题来了，什么是标准，什么，什么标准。

我的模型大小或我的培训大小，我的培训批次大小需要，如此这般，这是足够的，如此这般，我在单GPU上做了足够的计算，如此这般，当它完成时，下一层已经全部收集完毕并准备好，而这样做的方式是通过，所以。

我计算的像算术和算术强度，以及像网络带宽这样的，它的工作方式是第一个项目点，我们有我们的矩阵乘法，这是批处理乘以e乘以e矩阵，所以，浮点运算是两批乘以e的平方，嗯，所有聚集要求，然后它就像这样。

我有那么多浮点运算次数用于矩阵乘法，然后如果你想要所有聚集，我需要通信的字节数是多少，这大约是两倍的e的平方字节，如果你假设半精度，嗯，因为你需要在每个地方通信整个权重矩阵，然后算术强度。

所以这是一个被广泛使用的度量，所以这基本上是浮点运算次数和做它之间的比率，我为我的计算需要的浮点运算次数和通信量，以及为此，它就是第一个项目除以第二个项目，所以这最终等于只是，嗯，批处理/芯片。

浮点运算次数/字节，就像bessentially和最后一个部分的第二部分，所以你知道算术强度的，像有多少，它每进行一次计算需要多少浮点运算次数，或者有多少，是的，它每进行一次计算需要多少字节。

和最后一部分要找出的，哦，我的实际批处理大小需要多大，取决于只是，设备的带宽，比如你的设备，在这里我认为是实习连接，所以它是多个TPU或GPU之间的连接，它将像多个GPU之间的带宽一样，在这种情况下。

设备之间的数据传输时间，嗯，强度大约是1180次浮点运算/字节，所以为了使它，所以让我们的计算，至少我们的通信，我们需要至少批处理/芯片由，所以这将基本上是意味着我们想要批处理/芯片像。

在那个点在大约大于1180时，嗯，应该有没有重叠，应该有重叠，是的，只要你的设备批处理大小足够大，所以在这种情况下，如果你想在更多设备上训练，你将在更大的批处理大小上训练，是的，在某一点之后，这有点像。

所以像这些操作，像，我猜我可能会有，嗯，在这种情况下没有，它们是，它们有点可以互换，是的，嗯，你的意思是，像如何像all reduce一样完成，或者这些collectives是如何完成的，我猜那是，嗯。

是的，如何，嗯，这与，像同步两台机器上的计算一样，并且看到像并行会使用，在这种情况下，它是像，它是像使用相同的时钟在，在意义上这些代码将工作，假设每个设备运行完全相同的代码序列。

像完全相同的函数调用序列，所以他们都会在完全相同的时间调用all reduce，或者像它们都会，它们会在完全相同的作为第n命令它们运行时调用all reduce，一些设备可能会落后。

但是其他设备会直到所有其他设备调用它才会被阻塞，是的，是的，我们做像归一化，所以基本上像减去平均值，除以标准差像匹配一个later或ready，这些在这种情况下更昂贵吗，因为你需要整个像，是的。

或者有没有一种方式像预计算，一些这些事情是，嗯，预计算很难对吗，这取决于归一化，所以大多数这些变换器使用层归一化，所以大多数情况下你不会在激活维度上分片，你只分片在批次上。

并且对于层归一化不需要额外的通信，如果你想要使用批次归一化，你需要像pytorch一样进行通信，有一个同步批归一化，它会传递均值和标准差，这会增加一些额外的开销，好的，这是，嗯，我们讨论了SDP。

这是张量并行，这是另一种分片方式，这是，这是之前我描述的，确切地，像，方式，分片的方式，MLP和注意力工作，嗯，嗯，在一定程度上，是的，嗯，但在这种情况下，我猜你可以这样做，所以。

我猜张量并行有两种方式，有，你可以像这里一样分片，你不分实际的批，但你只分qkv的实际权重，然后输出投影，这是张量并行的一种方式，嗯，像，这是比较标准的，另一种方式你可以这样做，除了分片权重之外。

你可以分片你的激活，这在实际应用中稍微少一些明确编码，嗯，但仍然可以使用，这与我开始讨论的分片马耳他东西非常相似，所以现在你有在这种情况下你可以，你可以做你的部分，你的局部乘法，然后你有部分求和。

然后你可以在这种情况下做减少散列，你可以想象，就像所有减少来计算整个输出，然后你可以然后重新分片，这有点像散列操作，所以每个设备仍然只有自己的部分，嗯，然后你可以组合这些，你只能得到更多颜色。

你可以做SDP，因为它们，它们不冲突，任何方式，以任何方式，你需要改变你的方式，所以最容易想到这一点的是，假设你有六十四十六台设备，然后你想要找出你想要进行张量并行的设备，你想要进行sdp的设备。

那么这就会变成一个二维网格，如果我有一个sdp像四，一个tp像四，那就是十六台设备，所以基本上，如果我有一个批大小像四，那么每个sdp或每个数据并行排名将得到一个批大小为一，然后这将被喂入一个序列的。

嗯，像四个设备，张量并行横跨它，嗯，最后你可以做一些相当复杂的计算，它只是变得更，我想，代码编写更麻烦，我真的很想在这里同时列出来，不考虑，是的，它基本上是内置的，所以我可以说，这是我的移动大小。

这是我可用的gpus或tpus，有了那个，但在之间，是的，不，不，嗯，嗯，所以从选择分片来看，这肯定不是，这现在是手动做的，但在未来可能会做，我认为优化它并不难，但即使编写这种并行性。

像pytorch这样的库是非常复杂的，像scp这样的库也非常复杂，嗯，特别是如果你想让事情重叠，当它在计算中通信时，jax要容易得多，我想，因为它都隐式地做了，如果你使用jax，嗯，因为你实际上。

因为jax做的事情是，它会像，它会对待，假设你有一千台设备，它会对待所有的一千台设备作为一个单一的设备，然后jax的工作就是像你，你可以划分，你可以定义一个特定的分片约束，关于矩阵如何分片。

但它会自己编译图，它将确定集体做什么，我需要做什么来做这个计算，嗯，相对于for pi torch，至少对于现在，你必须明确编码每一通通信，嗯，是的，这不理想，但这也更不容易出现。

杰克可以做一些愚蠢的事情，比如它会做集体，在你不想要它的地方，这可能会大大减慢速度，而且很难调试，但当它起作用时，它非常棒，嗯，相对于pi torch做一切，瑞士是烦人的，但它可能更少出错，但是的确。

回答你的问题，这仍然，这仍然是一个非 trivial 的工作量，嗯，所以思考方式的容易方式是，假设在sdp和tp之间，这两者之间的主要区别是他们都是分片你模型的方式，在某种意义上，嗯。

主要区别是sdp仍然需要一个设备上的批大小为1，如果我有一千个设备，我需要至少一千个批大小相对于tp，我可以有一个设备上的批大小为1，例如，四个设备或八个设备，这也让你可以像。

如果你增加你的设备的tp分配，你可以在更低的批大小上训练，哪，嗯，这可能是你想要的，如果你单个批不能在单个设备上适应，如果你在，例如，一个像一百万个长度的序列上训练，那么这个可能无法适应单个批。

那么你可以使用tp来并行化它以适应内存，但一般来说，尽可能多的sdp，这是一般的规则，我遵循，是的，你可能需要使用，我不确定实际上，这不，是的，好吧，从我的头脑中立即想到，我不知道那个问题的答案，好的。

嗯，我认为，我认为我们讨论过这个，好的，是的，酷，是的，那是，嗯，基本上就是这样，还有其他问题或什么吗，是的，嗯，但是这是下一个p，哦，是的，但是那不是，那不是太难，我认为那不太难，是的。

所以至少与当前的方式，一些tp实现是，它是，嗯，它是像阻塞，或者有一些关于内存的事情，但是不管怎样，所以像它的一个方面，它是阻塞，所以所以g，有一个all reduce you。

你不能真正地与任何东西重叠那，因为它必须计算整个输出，然后它可以向前馈，相对于，让我们说sdp，它可以完全重叠，嗯，最终结果在无额外开销，所以然后有一些tp的方面，稍微不那么内存效率，因为就像这里。

它做像复制，这不理想，嗯，所以它是稍微不那么内存效率，并且它可能，嗯，它可能偶尔稍微慢一点，通常我只发现像它，如果你的批量大小足够大并且执行了sdp，而且这更好，我会。

如果它是hugging face模型，然后嗯，你只是希望和祈祷，有人 somewhere 为你做了它，是的，那就是很难，我也不太经常与他们工作，如果只是实现一个transformer分片。

然后我只是使用，我推荐使用jax或其他，在jax中，这要容易得多，在jax中，或者如果这个模型足够流行，例如llama或其他，那么是的，有分片实现的实现，没有官方的实现，嗯，但是就像有，我。

我 我 我 用 嗯，它是叫什么，我忘记打电话，它是一些推理库，来自稻田的那个，或者不是，嗯，我不知道为什么，我忘记了，但是不管怎样，那些支持像，让我们说像张量并行性，我认为这是最主要的，它支持的是。

除了那些之外，实际上没有其他任何东西，除了你自己实现之外，这有点烦人，这些是相互排斥的，你可以同时做这两件事，因为注意力，我解释的内容超出了理解范围，而环形注意力超出了序列长度，因此。

你可以技术上同时做这两件事，酷，好的，我想这就是所有的问题，那是问题，好的，酷。