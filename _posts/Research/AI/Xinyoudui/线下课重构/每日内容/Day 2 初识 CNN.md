# 卷积

- [Convolutional Neural Networks](https://d2l.ai/chapter_convolutional-neural-networks/index.html)
- [From Fully Connected Layers to Convolutions](https://d2l.ai/chapter_convolutional-neural-networks/why-conv.html)

对于一个图像相关的任务，如果我们对整张图使用全连接层，我们需要的参数数量过大。也就是说，我们需要把普通的 NN 往图像相关问题特化。

看一个具体例子来寻找灵感：

> 国外一个很火的游戏：给定一张有很多很多人的图片，在里面找到 Waldo 这个人。
>
> <img src="https://compote.slate.com/images/da10c202-1283-4e22-9edf-a2a26f5880dc.jpg" width=400/>

我们发现一个关键性质：**Waldo 的样子与 Waldo 所在的位置无关**，即 Waldo 的样子具有**平移不变性**。因此我们使用一个全局的大 NN 是愚蠢的，应该关注**局部**的信息。

对于每一个像素，我们每次在往隐藏层转移时，都提取它附近一块的信息。对于图片 $X$，它往隐藏层 $H$ 的转移被定义为一个**卷积**（严谨地说是 Cross-Correlation）：

$$H_{i,j} = U_{i,j} + \sum_{a \in [-\Delta, \Delta], b \in [-\Delta, \Delta]} V_{a,b} X_{i+a, j+b}$$

权值矩阵 $V$ 被称为卷积核。

对于一个 $n_h \times n_w$ 的图片，在经过一个 $k_h \times k_w$ 的卷积核卷积后，其大小为：

$$(n_h - k_h + 1) \times (n_w - k_w + 1)$$

## Padding & Stride

不难发现，我们过卷积层时图像会变小，而且边缘的像素利用不足。

我们可以在外圈补上一层厚度为 $p$ 的 $0$，然后再卷积。此处的 $p$ 被称为 padding。

与此同时，卷积核一格一格走，对于某些情况来说计算量太大。我们可以让卷积核每次走 $s$ 格，此处的 $s$ 被称为 stride。

> 对于一条长度为 $n$ 的边，使用一个长度为 $k$ 的卷积核，使用 $p$ 的 padding 和 $s$ 的 stride，最后输出的尺寸是？

$$\boxed{
    \left\lfloor \frac {n + 2p - k} s \right\rfloor + 1
}$$

注意，如果走到最后一步发现像素不够卷了，那么会直接丢弃。

很多时候，为了让输入输出尺寸一致，我们会选取 $s = 1$ 且 $p = \frac {k-1} 2$，所以一般 $k$ 会选一个奇数。

## 多通道

日常生活中的图片都是有 RGB 共 $3$ 个**通道 (channel)** 的，对于 PNG 文件甚至有 RGBA 共 $4$ 个通道。

对于一张 $h \times w$ 的图片 $X$，若它有 $c$ 个通道，则我们记它的大小为 $c \times h \times w$。

进一步思路打开，输出其实也不需要只有 $1$ 个通道。对于输出的第 $d$ 个通道，我们使用第 $d$ 个卷积核，对三维张量 $X$ 进行卷积：

$$H_{i,j,d} = U_{i,j,d} + \sum_{a \in [-\Delta, \Delta], b \in [-\Delta, \Delta]} \sum_c V_{a,b,c,d} X_{i+a, j+b, c}$$

# 池化

但是只识别过于局部的特征也不对。比如我们要识别 Waldo，但是每个神经元要么只能看到 Waldo 的脸要么只能看到 Waldo 的衣服，没有办法看到更大的结构。

我们可以具体定义一下“神经元看到的区域”。我们称神经元的**感受野 (receptive field)** 为神经元依赖原图的区域大小。e.g. 原图经过一个卷积核大小为 $3 \times 3$ 的卷积层后，每个神经元的感受野即为 $3 \times 3$。

不断地叠卷积层来增加感受野有点蠢。我们可以考虑“模糊原图”：把图片上每 $k \times k$ 分一大格，每一格内取最大值作为代表元素：

<img src="https://media.geeksforgeeks.org/wp-content/uploads/Screenshot-from-2017-08-15-17-04-02.png" width=500>

这样的操作可以直接让感受野翻 $k$ 倍，超级赚。

这个过程称作**池化 (Pooling)**。和卷积层一样，池化层在格子不够的时候也会直接丢弃。

由于池化丢弃了信息，因此它属于**下采样 (Downsampling)** 的一种。

# Python 实现

在 PyTorch 中，这些层被称为：
- 卷积层 `Conv2d(in_channels, out_channels, kernel_size, stride=1, padding=0)`
- 池化层 `MaxPool2d(kernel_size)`

## 实践：MNIST

> [Digit Recognizer](https://www.kaggle.com/competitions/digit-recognizer)
>
> 给定一张 $1 \times 28 \times 28$ 的灰度图，图中写了一个 $0$ 到 $9$ 之间的数字。识别这个数字。

我们可以设计一个这样的卷积神经网络（CNN）：

| 操作 | $C \times H \times W$ |
| - | - |
| Input | $1 \times 28 \times 28$ |
| `Conv1` | $32 \times 28 \times 28$ |
| `Pool1` | $32 \times 14 \times 14$ |
| `Conv2` | $64 \times 14 \times 14$ |
| `Pool2` | $64 \times 7 \times 7$ |
| `View` | $3136$ |
| `FC1` | $128$ |
| `FC2` | $10$ |


```py
class MNISTCNN(nn.Module):
    def __init__(self):
        super().__init__()

        self.conv = nn.Sequential(
            nn.Conv2d(1, 32, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2, 2),

            nn.Conv2d(32, 64, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2, 2),

            nn.Flatten()
        )

        self.classifier = nn.Sequential(
            nn.Linear(64 * 7 * 7, 128),
            nn.ReLU(),
            nn.Linear(128, 10)
        )

    def forward(self, x):
        x = self.conv(x)
        x = self.classifier(x)
        return x
```