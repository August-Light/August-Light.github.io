[官方文档](https://docs.pytorch.org/vision/main/index.html)

# Dataset

```py
from torch.utils.data import Dataset

# TODO: data 太泛泛而谈
class MyDataset(Dataset):
    def __init__(self, data):
        self.data = data

    def __len__(self):
        return len(self.data)

    def __getitem__(self, idx):
        return self.data[idx]
```

加载已有数据集（以 MNIST 为例）：

```py
train_data = datasets.MNIST(
    root="/personal/data",
    train=True,
    download=True,
    transform=transform
)
```

# Dataloader

```py
train_loader = DataLoader(train_data, batch_size=64, shuffle=True)
test_loader = DataLoader(test_data, batch_size=64, shuffle=False)
```

- batch 是批量加载。
- `num_workers` 为子进程数，多进程加速。

$$\text{len(dataloader)} = \left\lceil \frac {\text{len(dataset)}} {\text{batch size}} \right\rceil$$

# 加载 / 保存图像

使用 `PIL`。

```py
from PIL import Image

image_path = "/share/xinyoudui_logo.jpg"
image = Image.open(image_path).convert("RGB")
```

```py
transformed_image.save("/personal/xinyoudui_logo_transformed.jpg")
```

# 格式转换

都是 `callable` 的对象，像函数一样调用：

- `transforms.ToTensor()` PIL / ndarray -> tensor
- `transforms.ToPILImage()` tensor / ndarray -> PIL

# 图像变换

都是 `callable` 的对象，像函数一样调用：

- `transforms.Resize((h, w))` 缩放。
- `transforms.CenterCrop((h, w))` 中心裁剪。
- `transforms.Normalize(mean, std)` **在 tensor 格式下**，把颜色标准化。
- `transforms.RandomRotation(degrees)` 随机旋转 $[-\text{degrees}, +\text{degrees}]$ 度
- `transforms.RandomHorizontalFlip()`
- `transforms.RandomVerticalFlip()`
- `transforms.Compose` 组合技：

```py
transform = transforms.Compose([
    transforms.Resize((256, 256)),
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.5, 0.5, 0.5], std=[0.5, 0.5, 0.5]),
    transforms.ToPILImage()
])

transformed_image = transform(image)
```

