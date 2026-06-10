# Dropout

[5.6. Dropout](https://d2l.ai/chapter_multilayer-perceptrons/dropout.html)

## 原理

- 在训练时，每一个神经元以 $p$ 的概率关闭（当然结果需要缩放）。
- 预测时不关闭。

就这么简单。

## 效果

- 增加噪声，泛化能力提升。
- 这相当于训练了很多子网络，某种程度上像一个 Bagging。

## 代码

[Dropout — PyTorch 2.10 documentation](https://docs.pytorch.org/docs/stable/generated/torch.nn.Dropout.html)

```py
nn.Dropout(p=0.5)
```

# Batch Normalization

[8.5. Batch Normalization](https://d2l.ai/chapter_convolutional-modern/batch-norm.html)

BatchNorm 提出于 2015 年的论文 [Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift](https://arxiv.org/abs/1502.03167)。

## 原理

BatchNorm 层在 train 和 eval 时有不同的运行效果。

### train

BatchNorm 会在每个 batch 之内求出输入 $x$ 的均值和（有偏）方差：

$$\begin{cases}
    \mathbb E[x] = \frac 1 {\lvert B \rvert} \sum_{x \in B} x \\
    \text{Var}(x) = \frac 1 {\lvert B \rvert} \sum_{x \in B} (x - \mathbb E[x])^2
\end{cases}$$

然后将 $x$ 标准化后做一个 $x \mapsto \gamma \odot x + \beta$ 的仿射变换，此处 $\gamma, \beta$ 是可学习参数：

$$\text{BN}(x) = \gamma \odot \frac {x - \mathbb E[x]} {\sqrt{\text{Var}(x) + \epsilon}} + \beta$$

### eval

在预测时是没有一整个 batch 的数据的！每次只有一个数据。

因此其实 train 的时候会记录之前的均值和方差，把有偏方差变换成无偏方差之后，直接使用这组均值和方差对要被预测的数据作变换。

## 使用方式

### 全连接层

对于普通的全连接层：

$$h = \phi(Wx+ b)$$

我们在仿射变换和激活函数之间夹一层 BatchNorm：

$$h = \phi(\text{BN}(Wx + b))$$

### 卷积层

对每个通道单独做 BatchNorm。依旧夹在卷积和激活函数之间。

## 效果

- 让训练更稳定：可以用更大学习率、更快收敛；梯度更稳定。
- 某种程度上起到 regularization 效果。
- 不限制模型的表达能力。

## 代码

- [BatchNorm1d — PyTorch 2.10 documentation](https://docs.pytorch.org/docs/stable/generated/torch.nn.BatchNorm1d.html)
- [BatchNorm2d — PyTorch 2.10 documentation](https://docs.pytorch.org/docs/stable/generated/torch.nn.modules.batchnorm.BatchNorm2d.html)

BatchNorm 常见的 API 有 1d 和 2d 两种：

| API | 格式 |
| - | - |
| `nn.BatchNorm1d` | $N \times F$ |
| `nn.BatchNorm1d` | $N \times C \times L$ |
| `nn.BatchNorm2d` | $N \times C \times H \times W$ |

需要传入的参数是 $F$ 或 $C$。

## 例：还是 MNIST

我们把上次的 MNIST 代码加上 BatchNorm：

```py
class MNISTCNN(nn.Module):
    def __init__(self):
        super().__init__()

        self.conv = nn.Sequential(
            nn.Conv2d(1, 32, kernel_size=3, padding=1),
            nn.BatchNorm2d(32),
            nn.ReLU(),
            nn.MaxPool2d(2, 2),

            nn.Conv2d(32, 64, kernel_size=3, padding=1),
            nn.BatchNorm2d(64),
            nn.ReLU(),
            nn.MaxPool2d(2, 2),

            nn.Flatten()
        )

        self.classifier = nn.Sequential(
            nn.Linear(64 * 7 * 7, 128),
            nn.BatchNorm1d(128),
            nn.ReLU(),

            nn.Linear(128, 10)
        )

    def forward(self, x):
        x = self.conv(x)
        x = self.classifier(x)
        return x
```

# Dropout or BN?

根据[一些野生的资料](https://zhuanlan.zhihu.com/p/561124500)，BN 和 Droput 在统计学上的行为是冲突的。一般如何选择这两者呢？

- MLP 一般使用 Dropout。
- CNN 一般使用 BN。

## CNN 架构

https://d2l.ai/chapter_convolutional-modern/index.html

### [AlexNet](https://d2l.ai/chapter_convolutional-modern/alexnet.html) (2012)

使用了如下的典型结构：

$$\text{Convolution} \to \text{ReLU} \to \text{Pooling}$$

并且使用了 dropout。

据 ChatGPT 所说，在这之前大家用的普遍是 sigmoid 函数，而 AlexNet 开创性地使用了 ReLU，以保证梯度不消失且训练更快。

### [VGG](https://d2l.ai/chapter_convolutional-modern/vgg.html) (2014)

反复堆叠地使用 $3 \times 3$ 卷积与池化。

以下图片展示了 AlexNet 与 VGG 的结构：

<img src="https://d2l.ai/_images/vgg.svg" width=400/>

### [GoogLeNet](https://d2l.ai/chapter_convolutional-modern/googlenet.html)

$1 \times 1$ 卷积

TODO:

### ⭐ [ResNet](https://d2l.ai/chapter_convolutional-modern/resnet.html)

最好用的一个！



TODO:

### DenseNet

TODO: