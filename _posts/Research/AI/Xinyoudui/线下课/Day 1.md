考试环境：https://www.bohrium.com/

# Sklearn

不在本文。

# PyTorch 张量

不在本文。

# PyTorch 神经网络

```python
class Path(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc1 = nn.Linear(3, 4)
        self.fc2 = nn.Linear(4, 2)

    def forward(self, x):
        return self.fc2(F.relu(self.fc1(x)))

model = Path()
print(model)
```

求解：`SGD` 或 `Adam`

```python
optimizer = optim.Adam(model.parameters(), lr=0.001)
```

`lr` 为 learning rate。

```python
import torch
from torch import nn
import torch.nn.functional as F
from torch import optim

class Path(nn.Module):
    # ...

model = Path()
print(model)

criterion = nn.MSELoss()
optimizer = optim.Adam(model.parameters(), lr=0.01)

X = torch.randn(10, 4)
y = torch.randn(10, 1)

EPOCHS = 100
for epoch in range(EPOCHS):
    optimizer.zero_grad()
    output = model(X)
    loss = criterion(output, y)
    loss.backward()
    optimizer.step()
    if (epoch+1) % 10 == 0:
        print(f'Epoch [{epoch+1}/{EPOCHS}], Loss: {loss.item():.4f}')
```