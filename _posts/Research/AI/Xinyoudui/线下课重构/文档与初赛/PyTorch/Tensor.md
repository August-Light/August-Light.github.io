# GPU

```py
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
```

# Tensor

## 平凡地创建 tensor

```py
a = torch.zeros((height, width)) # 全 0 tensor
b = torch.ones((height, width))  # 全 1 tensor
c = torch.randn((height, width)) # 每个元素符合标准正态分布的 tensor

d = torch.arange(1, 6, 2) # 用法同内置 range
```

## 类型转换

```py
arr = np.array([[1, 2], [3, 4]])
tensor = torch.from_numpy(arr)
```

```py
tensor = torch.tensor([1, 2, 3])
print(tensor.numpy())
print(tensor.tolist())
```

## 大小与维度

```py
a = torch.tensor([
    [1, 2, 3],
    [4, 5, 6],
])
print(a.shape) # torch.Size([2, 3])
print(a.dim()) # 2
```

# 张量运算

## 计算

四则运算是按位的。

```py
a = torch.tensor([1, 2, 3])
b = torch.tensor([4, 5, 6])
print(a + b) # tensor([5, 7, 9])
print(a * b) # tensor([ 4, 10, 18])
```

```py
a = torch.tensor([1, 2, 4])
print(torch.sum(a))          # tensor(7)
print(torch.max(a))          # tensor(4)
print(torch.mean(a.float())) # tensor(2.3333)
```

注意整型的张量不可以取 `mean` 会报错。

## 拼接

```py
a = torch.tensor([
    [1, 2, 3],
    [4, 5, 6]
])
b = torch.tensor([
    [7, 8, 9],
    [10, 11, 12]
])

print(torch.cat([a, b], dim=0))

"""
tensor([[ 1,  2,  3],
        [ 4,  5,  6],
        [ 7,  8,  9],
        [10, 11, 12]])
"""
```

`cat` 将多个张量在第 `dim` 维上拼接起来。除了第 `dim` 维，其他维度必须大小完全相同。

`cat` 也叫 `concat` 或 `concatenate`。

## 形状调整

`reshape` / `view` 可以改变 tensor 的形状（区别在于 `view` 要求内存连续）：

```py
import torch

a = torch.tensor([1, 2, 3, 4, 5, 6])
print(a.reshape(2, 3))
print(a.view(2, 3))

"""
tensor([[1, 2, 3],
        [4, 5, 6]])
"""
```

若传入的大小中有一维为 `-1`，则意味着这一维的大小会被自动推断（如果遇到不能整除的情况会报错）：

```py
print(a.reshape(-1, 3)) # 输出同上
```

`reshape(-1)` 也可以写为 `flatten`，语义更清晰：

```py
a = torch.tensor([[1, 2, 3], [4, 5, 6]])
print(a.reshape(-1)) # tensor([1, 2, 3, 4, 5, 6])
print(a.flatten())   # tensor([1, 2, 3, 4, 5, 6])
```

## 维度调整

`unsqueeze(dim)` 在第 `dim` 维处插入一个大小为 $1$ 的维度。

```py
a = torch.randn([3, 5, 3])
b = a.unsqueeze(0)
c = a.unsqueeze(1)

print(a.shape) # torch.Size([3, 5, 3])
print(b.shape) # torch.Size([1, 3, 5, 3])
print(c.shape) # torch.Size([3, 1, 5, 3])
```

`unsqueeze(dim)` 压掉大小为 $1$ 的第 `dim` 维。
- 若该维度大小不为 $1$，则什么都不发生。
- 若不传入 `dim` 则会压掉所有大小为 $1$ 的维度。

```py
a = torch.randn([1, 3, 1, 5, 3])
b = a.squeeze(2)
c = a.squeeze()
d = a.squeeze(1)

print(b.shape) # torch.Size([1, 3, 5, 3])
print(c.shape) # torch.Size([3, 5, 3])
print(d.shape) # torch.Size([1, 3, 1, 5, 3])
```

## 向量与矩阵

向量点积：

```py
a = torch.tensor([1, 2, 3])
b = torch.tensor([4, 5, 6])
print(torch.dot(a, b)) # tensor(32)
```

矩阵乘法的三种写法：

```py
a = torch.randn(2, 3)
b = torch.randn(3, 4)
print(torch.matmul(a, b))
print(torch.mm(a, b))
print(a @ b)
```

矩阵转置：

```py
a = torch.tensor([
    [1, 2, 3],
    [4, 5, 6],
])
print(a.T)
```

## 条件判断

```py
a = torch.tensor([1, 2, 3, 4, 5])
print(a > 2) # tensor([False, False,  True,  True,  True])
print(a[a > 2]) # tensor([3, 4, 5])
print(torch.where(a > 2, a, torch.tensor(0))) # tensor([0, 0, 3, 4, 5])
print(torch.where(a > 2, torch.tensor(1), torch.tensor(0))) # tensor([0, 0, 1, 1, 1])
```

此处触发了 `where` 的广播机制：`torch.tensor(1)` 被广播成了 `[1, 1, 1, 1, 1]` 的结构。