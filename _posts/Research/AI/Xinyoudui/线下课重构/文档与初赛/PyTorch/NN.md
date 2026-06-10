# 常用

这里所有的层都在 `from torch import nn` 中。

- 线性层
  - `Linear(in_features, out_features)`
- 激活函数层
  - `Sigmoid()`
  - `ReLU()`
  - `LeakyReLU(negative_slope=0.01)`
  - `Tanh()`
  - `GELU()`
- 卷积层
  - `Conv2d(in_channels, out_channels, kernel_size, stride=1, padding=0)`
- 池化层
  - `MaxPool2d(kernel_size)`
- Flatten
  - `Flatten()`
- Softmax
  - `Softmax(dim)`
- 归一化层
  - `BatchNorm2d(num_features)`
  - `LayerNorm(normalized_shape)`
- Dropout
  - `Dropout(p=0.5)`

`Sequential()` 可以打包若干个操作。

## 激活函数

除了 `nn` 中的激活函数，`import torch.nn.functional as F` 中也有激活函数：
- `F.sigmoid(input)`
- `F.relu(input)`
- `F.leaky_relu(input, negative_slope=0.01)`
- `F.tanh(input)`
- `F.gelu(input)`

即开即用，写在前向传播中，不作为特别的一层。

## 特别

TODO: 学会了再写这段！

- RNN
- Transformer
  - `Embedding(num_embeddings, embedding_dim)`
  - `MultiheadAttention()`
  - `TransformerEncoderLayer()`
  - `Transformer()`

# 定义自己的神经网络！

继承 `nn.Module`，然后将以上东西组合在一起就好啦！

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

# 训练

- 损失函数 `criterion` 设为交叉熵；
- 优化器 `optimizer` 设为 Adam；
- 对于每个 epoch：
  - 将模型设为 `train` 模式，跑训练集。
    - `loss = criterion(model(images), labels)` 求损失函数。
    - `optimizer.zero_grad()` 清空梯度。
    - `loss.backward()` 反向传播。
    - `optimizer.step()` 更新参数。
  - 将模型设为 `eval` 模式，跑验证集。（此代码没搞验证集，省略这一步）
- 保存参数。

小技巧：使用 `tqdm` 显示进度条。

```py
def train(param_path, num_epochs=5, lr=0.001):
    model = MNISTCNN()
    criterion = nn.CrossEntropyLoss()
    optimizer = optim.Adam(model.parameters(), lr=lr)
    for epoch in range(num_epochs):
        model.train()
        pbar = tqdm(train_loader, desc=f'Epoch {epoch+1}/{num_epochs}')
        for images, labels in pbar:
            outputs = model(images)
            loss = criterion(outputs, labels)

            optimizer.zero_grad()
            loss.backward()
            optimizer.step()

            pbar.set_postfix({'loss': f"{loss.item():.4f}"})
    torch.save(model.state_dict(), param_path)
```

# 预测

- 定义一个一模一样的模型，把保存好的参数装回去。
- 将模型设为 `eval` 模式。

```py
def predict(param_path):
    model = MNISTCNN()
    model.load_state_dict(torch.load(param_path))
    model.eval()

    preds = []
    with torch.no_grad():
        for images in test_loader:
            outputs = model(images)
            predicted = outputs.argmax(1)
            preds.extend(predicted.cpu().numpy())

    return preds
```

# 完整代码

- 定义并加载 dataset；
- 用 dataloader 包装 dataset；
- 定义神经网络；
- 训练并保存参数；
- 使用训练好的模型进行预测。

该代码**未使用 GPU**。

```py
# https://www.kaggle.com/competitions/digit-recognizer/

import pandas as pd
import torch
from torch import nn, optim
from torch.utils.data import Dataset, DataLoader
from torchvision import transforms
from tqdm import tqdm

print("Initialization complete")


class DigitDataset(Dataset):
    def __init__(self, csv_file, transform=None):
        self.data = pd.read_csv(csv_file)
        self.transform = transform

        if "label" in self.data.columns:
            self.labels = self.data["label"].values
            self.images = self.data.drop("label", axis=1).values
        else:
            self.labels = None
            self.images = self.data.values

    def __len__(self):
        return len(self.images)

    def __getitem__(self, idx):
        img = self.images[idx].reshape(28, 28).astype("float32")

        if self.transform:
            img = self.transform(img)

        if self.labels is not None:
            label = torch.tensor(self.labels[idx], dtype=torch.long)
            return img, label
        else:
            return img


transform = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize((0.5,), (0.5,))
])


train_dataset = DigitDataset("digit-recognizer/train.csv", transform=transform)
test_dataset = DigitDataset("digit-recognizer/test.csv", transform=transform)


BATCH_SIZE = 64
train_loader = DataLoader(dataset=train_dataset, batch_size=BATCH_SIZE, shuffle=True)
test_loader = DataLoader(dataset=test_dataset, batch_size=BATCH_SIZE, shuffle=False)


class MNISTCNN(nn.Module):
    # ...


def train(param_path, num_epochs=5, lr=0.001):
    # ...


def predict(param_path):
    # ...

def submit(preds, submission_path):
    submission = pd.DataFrame({
        "ImageId": range(1, len(preds)+1),
        "Label": preds
    })

    submission.to_csv(submission_path, index=False)

if __name__ == "__main__":
    param_path = "mnist_cnn.pth"
    train(param_path, num_epochs=5)
    preds = predict(param_path)
    submit(preds, "submission.csv")
```