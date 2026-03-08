# 卷积

https://d2l.ai/chapter_convolutional-neural-networks/index.html

https://d2l.ai/chapter_convolutional-neural-networks/why-conv.html

对于一个图像相关的任务，如果我们对整张图使用全连接层，我们需要的参数数量过大。也就是说，我们需要把普通的 NN 往图像相关问题特化。

我们来看一个具体例子来寻找灵感。

> 国外一个很火的游戏：给定一张有很多很多人的图片，在里面找到 Waldo 这个人。
>
> <img src="https://compote.slate.com/images/da10c202-1283-4e22-9edf-a2a26f5880dc.jpg" width=400/>

我们发现一个关键性质：**Waldo 的样子与 Waldo 所在的位置无关**，即 Waldo 的样子具有**平移不变性**。

因此我们使用一个全局的大 NN 是愚蠢的，应该关注**局部**的信息。

TODO:

对于图片 $X$，它往隐藏层 $H$ 的转移被定义为一个卷积（严谨地说是 Cross-Correlation）：

$$H_{i,j} = U_{i,j} + \sum_{a \in [-\Delta, \Delta], b \in [-\Delta, \Delta]} V_{a,b} X_{i+a, j+b}$$

权值矩阵 $V$ 被称为卷积核。

对于一个 $n_h \times n_w$ 的图片，在经过一个 $k_h \times k_w$ 的卷积核卷积后，其大小为：

$$(n_h - k_h + 1) \times (n_w - k_w + 1)$$

## Padding & Stride

https://d2l.ai/chapter_convolutional-neural-networks/padding-and-strides.html

不难发现，我们过卷积层时图像会变小，而且边缘的像素利用不足。

我们可以在外圈补上一层厚度为 $p$ 的 $0$，然后再卷积。此处的 $p$ 被称为 padding。

与此同时，卷积核一格一格走，对于某些情况来说计算量太大。我们可以让卷积核每次走 $s$ 格，此处的 $s$ 被称为 stride。这同时可以起到 downsampling 的作用。

输出尺寸计算公式：

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

TODO:

池化在不够的时候也会直接丢弃。

# 实践：MNIST

https://www.kaggle.com/competitions/digit-recognizer

$1 \times 28 \times 28$ 灰度图输入

TODO:

