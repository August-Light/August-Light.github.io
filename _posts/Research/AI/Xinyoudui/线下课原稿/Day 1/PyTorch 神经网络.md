https://www.runoob.com/pytorch/pytorch-neural-network.html

TODO:

```py
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

```py
optimizer = optim.Adam(model.parameters(), lr=0.001)
```

`lr` 为 learning rate。

```py
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

X_test = torch.randn(5, 4)
Y_test = torch.randn(5, 1)

model.eval()
with torch.no_grad():
    predictions = model(X_test)
    print("Predictions:", predictions)
    loss = criterion(predictions, Y_test)
    print(f'Test Loss: {loss.item():.4f}')

torch.save(model, 'path_model.pth')
loaded_model = torch.load('path_model.pth')
```