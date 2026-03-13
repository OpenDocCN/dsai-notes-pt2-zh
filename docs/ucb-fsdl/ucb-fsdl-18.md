# 18：【Lab7】段落识别 📝

在本节课中，我们将学习如何从识别单行手写文字扩展到识别整个段落。我们将引入新的数据集、改进的模型架构，并学习如何保存最佳模型以及在生产环境中进行推理。

---

## 🏗️ 引入 ResNet-Transformer 模型

上一节我们介绍了基于 CNN 的 Transformer 模型。本节中，我们将使用 PyTorch Vision 提供的 **ResNet** 作为编码器，替代我们之前自建的 CNN 结构。

以下是 `ResNetTransformer` 模型的核心代码片段：

```python
class ResNetTransformer(nn.Module):
    def __init__(self, data_config, args):
        super().__init__()
        # 使用 torchvision 的 ResNet18，不加载预训练权重
        self.resnet = torchvision.models.resnet18(pretrained=False)
        # 移除最后的平均池化层和全连接层
        self.resnet = nn.Sequential(*list(self.resnet.children())[:-2])
        # 添加一个线性层，将 ResNet 输出投影到 Transformer 的嵌入维度
        self.projection = nn.Linear(512, args.d_model)
```

由于 ResNet 期望输入是三通道（RGB）图像，而我们的手写数据是单通道（灰度）图像，因此我们需要在输入时复制通道：

```python
# 将单通道图像复制为三通道
if x.shape[1] == 1:
    x = x.repeat(1, 3, 1, 1)
```

一个重要的改进是引入了 **二维位置编码**。传统的 Transformer 位置编码是为一维序列设计的，而图像是二维结构。因此，我们为特征图的每个位置添加了基于 X 轴和 Y 轴的编码，使模型能理解字符在图像中的空间位置。

---

## 📊 使用真实手写数据：IAM Lines

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_1.png)

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_3.png)

在之前的实验中，我们使用了合成数据。现在，我们引入真实的、基于行的手写数据集 **IAM Lines**。

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_4.png)

以下是查看 IAM Lines 数据集的示例代码：

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_6.png)

```python
# 在 notebook 中查看数据
from text_recognizer.data.iam_lines import IAMLines
dataset = IAMLines()
sample = dataset[0]
print(sample["image"].shape, sample["label"])
```

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_8.png)

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_10.png)

我们可以使用 `LineCNNTransformer` 或新的 `ResNetTransformer` 在这个数据集上进行训练。使用 ResNetTransformer 进行训练后，验证集字符错误率（CER）可以降至约 9.4%，最终测试集 CER 约为 11.7%。通过调整超参数，这个结果可以进一步优化。

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_12.png)

---

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_14.png)

## 📄 扩展到段落识别：IAM Paragraphs

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_16.png)

现在，我们从识别单行文本升级到识别整个段落。为此，我们引入了 **IAM Paragraphs** 数据集。

以下是 IAM Paragraphs 数据集的关键信息：
*   **图像尺寸**：576 x 640 像素
*   **最大序列长度**：682 个字符（包含换行符）
*   **数据划分**：训练集 1000 张，验证集 260 张，测试集 230 张

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_18.png)

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_20.png)

在训练时，我们对图像进行了数据增强，包括随机偏移、倾斜和对比度变化，以提升模型的鲁棒性。在测试时，图像会被完美居中且不做增强处理。

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_22.png)

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_24.png)

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_26.png)

---

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_28.png)

## 🔧 合成数据增强：IAM Synthetic Paragraphs

由于真实段落数据量有限，我们创建了 **IAM Synthetic Paragraphs** 数据集来扩充训练数据。

这个数据集的生成逻辑如下：
1.  随机生成多行文本。
2.  将这些文本行拼接成一个段落。
3.  将生成的段落图像随机放置在画布中。

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_30.png)

通过结合真实数据和合成数据，我们可以为模型提供更丰富、多样的训练样本。

---

## 🧩 组合数据集进行训练

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_32.png)

为了充分利用所有可用数据，我们创建了一个组合数据集 `IAMOriginalAndSyntheticParagraphs`。

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_34.png)

以下是其实现方式：

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_36.png)

```python
class IAMOriginalAndSyntheticParagraphs(pl.LightningDataModule):
    def setup(self, stage=None):
        # 分别实例化真实和合成数据集
        self.iam_paragraphs = IAMParagraphs(...)
        self.synth_paragraphs = IAMSyntheticParagraphs(...)
        # 使用 PyTorch 的 ConcatDataset 合并两者
        self.dataset = ConcatDataset([self.iam_paragraphs.dataset, self.synth_paragraphs.dataset])
```

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_38.png)

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_40.png)

使用 `ResNetTransformer` 在这个组合数据集上训练约 1000 个周期后，模型在测试集上可以达到约 17% 的字符错误率，并且仍有提升空间。

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_42.png)

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_44.png)

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_46.png)

---

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_48.png)

## 💾 自动保存最佳模型

在运行了大量实验后，我们需要一个方法来保存和复用性能最佳的模型。我们编写了 `training/save_best_model.py` 脚本。

该脚本的功能是：
1.  连接到 Weights & Biases 项目。
2.  根据指定的指标（默认为验证损失）找到最佳训练记录。
3.  将该最佳模型的配置、权重和训练命令保存到 `text_recognizer/artifacts/paragraph_text_recognizer/` 目录下。

保存的 `config.json` 文件包含了重现模型所需的所有超参数和训练设置。

---

## 🚀 生产环境推理：ParagraphTextRecognizer

保存最佳模型后，我们创建了 `ParagraphTextRecognizer` 类，用于加载模型并在生产环境中进行推理。

以下是该类的核心 `predict` 方法：

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_50.png)

```python
def predict(self, image_filename):
    """加载图像并进行预测"""
    # 1. 打开图像
    image = Image.open(image_filename)
    # 2. 应用与训练时相同的转换
    image_tensor = self.transform(image).unsqueeze(0)  # 增加批次维度
    # 3. 模型推理
    with torch.no_grad():
        pred_indices = self.model(image_tensor)
    # 4. 将索引序列解码为字符串
    pred_str = self.data_config["mapping"]["indices_to_char"](pred_indices)
    return pred_str
```

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_52.png)

我们可以在 notebook 中加载这个识别器，并对新的段落图像进行预测，观察其实际表现。

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_54.png)

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_56.png)

---

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_58.png)

## ⚠️ 模型局限性分析与改进方向

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_60.png)

在评估模型时，我们发现了一个常见的失败模式：**行重复**。模型有时会重复预测同一行或相邻行的内容。

这可能是由于 Transformer 的注意力机制在较长的二维序列中产生了混淆。模型在“看”完一行后，可能错误地再次将注意力集中到同一区域。

潜在的改进方案包括：
1.  调整或增强**二维位置编码**，使行与行之间的位置信息区分度更大。
2.  调整模型超参数，如增加注意力头的数量（`nhead`）或 Transformer 的层数（`num_layers`）。
3.  使用更复杂的解码策略，如集束搜索（Beam Search）。

---

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_62.png)

## 📚 课程总结

![](img/fbe43c373add6ec80e9d3cdcb887fd9c_64.png)

本节课中我们一起学习了段落识别系统的构建。我们从单行识别过渡到段落识别，引入了 `ResNetTransformer` 模型和二维位置编码。我们使用了 `IAM Paragraphs` 真实数据集和 `IAM Synthetic Paragraphs` 合成数据集来训练模型，并学会了如何自动保存最佳模型以及如何使用 `ParagraphTextRecognizer` 类进行推理。最后，我们分析了模型当前存在的局限性并探讨了未来的改进方向。