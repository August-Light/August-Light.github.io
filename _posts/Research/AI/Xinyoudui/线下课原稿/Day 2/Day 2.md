# CNN

## 卷积层

输入 $n_h \times n_w$，卷积核 $k_h \times k_w$，输出

$$(n_h - k_h + 1) \times (n_w - k_w + 1)$$

往往设置 padding $p = k - 1$ 以保持图像尺寸不变。

### 完整版尺寸计算

- Padding 为 $p$（上下左右均向外扩张）
- Stride 为 $s$
- 图像大小 $n \times n$
- 卷积核 $k \times k$

输出的边长为：

$$\boxed{
    \left\lfloor \frac {n + 2p - k} s \right\rfloor + 1
}$$

## 多输入输出通道

TODO:


# CNN MNIST

```py
class SimpleCNN(nn.Module):
    def __init__(self):
        super(SimpleCNN, self).__init__()
        self.conv1 = nn.Conv2d(1, 32, kernel_size=3, padding=1)
        self.conv2 = nn.Conv2d(32, 64, kernel_size=3, padding=1)
        self.pool = nn.MaxPool2d(2, 2)
        self.fc1 = nn.Linear(64 * 7 * 7, 128)
        self.fc2 = nn.Linear(128, 10)

    def forward(self, x):
        x = self.pool(F.relu(self.conv1(x)))
        x = self.pool(F.relu(self.conv2(x)))
        x = x.view(-1, 64 * 7 * 7)
        x = F.relu(self.fc1(x))
        x = self.fc2(x)
        return x
```

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