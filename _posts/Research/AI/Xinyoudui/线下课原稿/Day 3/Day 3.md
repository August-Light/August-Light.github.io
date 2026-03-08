# Example: 真假图片

- 加噪音
- 加随机旋转 / 翻转
- 加 epoch
- 调 learning rate

# Example: 宫格图

- 提交
  - 上传一个 `.pth` 文件
  - 在 ipynb 文件中 `torch.load` 加载 `.pth`，生成答案 `.csv`

---

- 无监督
  - 检测缝
- 有监督（手动打标签）

TODO:

## 优化

拼接

随机裁剪

dropout

# CV 进阶

https://d2l.ai/chapter_computer-vision/index.html

## Batch Normalization

TODO:

## CNN 架构

https://d2l.ai/chapter_convolutional-modern/index.html

### AlexNet (2012)

https://d2l.ai/chapter_convolutional-modern/alexnet.html

使用了如下的典型结构：

$$\text{Convolution} \to \text{ReLU} \to \text{Pooling}$$

并且使用了 dropout。

据 ChatGPT 所说，在这之前大家用的普遍是 sigmoid 函数，而 AlexNet 开创性地使用了 ReLU，以保证梯度不消失且训练更快。

### VGG (2014)

https://d2l.ai/chapter_convolutional-modern/vgg.html

反复堆叠地使用 $3 \times 3$ 卷积与池化。

以下图片展示了 AlexNet 与 VGG 的结构：

<img src="https://d2l.ai/_images/vgg.svg" width=400/>

### GoogLeNet

https://d2l.ai/chapter_convolutional-modern/googlenet.html

TODO:

### ResNet

https://d2l.ai/chapter_convolutional-modern/resnet.html

最好用的一个！

TODO:

### DenseNet

TODO:

## Fine Tuning

TODO:

## Object Detection

### Bounding Box

TODO:

### Anchor Box

TODO:

### Multiscale object detection

TODO:

## Semantic segmentation

### Transposed convolution

https://d2l.ai/chapter_computer-vision/transposed-conv.html

是一种**上采样**的方式。

对于一张 $n_h \times n_w$ 的二维张量，在被一个 $k_h \times k_w$ 的卷积核进行转置卷积后，会扩张为一个 $(n_h + k_h - 1) \times (n_w + k_w - 1)$ 的新张量。

<img src="https://d2l.ai/_images/trans_conv.svg" width=500/>

API 为 `nn.ConvTranspose2d`。

### FCN (Fully Convolutional Network)

https://d2l.ai/chapter_computer-vision/fcn.html

与普通 CNN 对整张图像分类不同，FCN 利用 CNN 对图像中的每个像素分类。

TODO:

# Example: Radar

池化是下采样减小数据，转置卷积是上采样增加数据。

注意最后格式对不上，需要 `interpolate` 插值一下，`mode` 可以选 `"bilinear"`。

```py
class MyModel(nn.Module):
    def __init__(self):
        super().__init__()

        NUM_CLASSES = 5

        self.block1 = nn.Sequential(
            nn.Conv2d(6, 32, 3, padding=1),  # (B, 32, 50, 181)
            nn.BatchNorm2d(32),
            nn.ReLU(),
            nn.MaxPool2d(2)  # (B, 32, 25, 90)
        )

        self.block2 = nn.Sequential(
            nn.Conv2d(32, 64, 3, padding=1),  # (B, 64, 25, 90)
            nn.BatchNorm2d(64),
            nn.ReLU(),
            nn.MaxPool2d(2)  # (B, 64, 12, 45)
        )

        self.block3 = nn.Sequential(
            nn.Conv2d(64, 128, 3, padding=1),  # (B, 128, 12, 45)
            nn.BatchNorm2d(128),
            nn.ReLU(),
            nn.MaxPool2d(2)  # (B, 128, 6, 22)
        )

        self.up1 = nn.ConvTranspose2d(128, 64, 2, stride=2)  # (B, 64, 12, 44)
        self.up2 = nn.ConvTranspose2d(64, 32, 2, stride=2)  # (B, 32, 24, 88)
        self.up3 = nn.ConvTranspose2d(32, NUM_CLASSES, 2, stride=2) # (B, NUM_CLASSES, 48, 176)

    def forward(self, x):
        x = self.block1(x)
        x = self.block2(x)
        x = self.block3(x)
        x = self.up1(x)
        x = self.up2(x)
        x = self.up3(x)
        x = F.interpolate(x, size=(50, 181), mode='bilinear',
                          align_corners=False)
        return x
```