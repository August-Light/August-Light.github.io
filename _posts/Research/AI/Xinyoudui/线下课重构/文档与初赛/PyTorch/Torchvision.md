# Dataset

```py
from torch.utils.data import Dataset

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
from torch.utils.data import DataLoader

train_loader = DataLoader(train_data, batch_size=64, shuffle=True)
test_loader = DataLoader(test_data, batch_size=64, shuffle=False)
```

- 从 `DataLoader` 中每次取出的一个 batch 的数据为一个 $\text{batch size} \times \text{data size}$ 的 tensor。
- `num_workers` 为子进程数，多进程加速。若设为 $0$ 则代表主进程。
- `shuffle` 代表是否打乱。训练集一般打乱，测试集由于可能需要看一下具体情况一般不打乱。

$$\text{len(dataloader)} = \left\lceil \frac {\text{len(dataset)}} {\text{batch size}} \right\rceil$$

# 加载 / 保存图像

使用 `PIL`。

```py
from PIL import Image

# 加载
image = Image.open(image_path).convert("RGB")

# 保存
image.save(image_path)
```

这种加载方式不太安全，可能导致泄露。使用 `with` 来规避这一点：

```py
with Image.open(image_path) as img:
    img_rgb = img.convert("RGB")
    # ...
```

# 格式转换 & 图像变换

都是 `callable` 的对象，像函数一样调用：

- 格式转换
  - `transforms.ToTensor()` PIL / ndarray -> tensor
  - `transforms.ToPILImage()` tensor / ndarray -> PIL
- 图像变换
  - `transforms.Resize((h, w))` 缩放。
  - `transforms.CenterCrop((h, w))` 中心裁剪。
  - `transforms.Normalize(mean, std)` **在 tensor 格式下**，把颜色标准化。
  - `transforms.RandomRotation(degrees)` 随机旋转 $[-\text{degrees}, +\text{degrees}]$ 度
  - `transforms.RandomHorizontalFlip(p=0.5)`
  - `transforms.RandomVerticalFlip(p=0.5)`
  - `transforms.Compose` 组合技：

```py
from torchvision import transforms

transform = transforms.Compose([
    transforms.Resize((256, 256)),
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.5, 0.5, 0.5], std=[0.5, 0.5, 0.5]),
    transforms.ToPILImage()
])

transformed_image = transform(image)
```