# CNN

对于一个图像相关的任务，如果我们对整张图使用全连接层，我们需要的参数数量过大。比如对于一张 $1000 \times 1000$ 的图片，假如隐藏层宽度 $1000$，则我们需要的参数量是 $10^9$ 级别的，这也太可怕了。

因此，我们需要把最普通的 MLP 往图像问题进行特化。

## Convolution

TODO: 平移不变性

TODO: 关注局部

### Padding & Stride

TODO:

$$n + 2p - k + 1$$

TODO:

$$\boxed{
    \left\lfloor \frac {n + 2p - k} s \right\rfloor + 1
}$$

### Multiple Channels

TODO:

$$C \times H \times W$$

## Pooling

TODO: 感受野

# Semantic Segmentation

U-Net

https://arxiv.org/abs/1505.04597



# ImageNet & ILSVRC

- IEEE 上的原论文：[ImageNet: A large-scale hierarchical image database](https://ieeexplore.ieee.org/abstract/document/5206848)
  - 免费阅读：[ImageNet: A Large-Scale Hierarchical Image Database](https://www.image-net.org/static_files/papers/imagenet_cvpr09.pdf)
- [Wiki](https://en.wikipedia.org/wiki/ImageNet)

以李飞飞为首的科学家创建了 ImageNet 数据库，并举办了 [ILSVRC](https://www.image-net.org/challenges/LSVRC/) 挑战赛。概括来说，算法需要做以下任务：
- 图像分类：根据图片中的主要物体给图像分类。
- 目标检测：找出物体，打上标签并框出其在图片中的位置。

ILSVRC 的高光时刻从 2012 年开始，到 2017 年最后一届结束后停止。

https://zhuanlan.zhihu.com/p/561991816

https://d2l.ai/chapter_convolutional-modern/index.html

## 2012 AlexNet

https://en.wikipedia.org/wiki/AlexNet

- GPU 训练
- ReLU
- Dropout

## 2014 1st GoogLeNet

## 2014 2nd VGG

## 2015 ResNet

## 2016 ResNext

