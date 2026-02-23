[官方文档](https://docs.pytorch.org/docs/2.10/pytorch-api.html)

# GPU

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
```

# 张量

## 平凡地创建张量

```python
a = torch.zeros((3, 4))
b = torch.ones((5, 6))
c = torch.randn((2, 3))
d = torch.arange(1, 6, 2) # tensor([1, 3, 5])
```

- `a`：$3 \times 4$ 的全 $0$ 张量
- `b`：$5 \times 6$ 的全 $1$ 张量。
- `c`：$2 \times 3$ 的每个元素服从标准正态分布的随机张量。
- `d`：使用 arange 函数，经典的 `start` `end` `step` 格式。

## numpy 转 torch

```python
arr = np.array([[1, 2], [3, 4]])
tensor = torch.from_numpy(arr)
```

## torch 转 numpy / list

```python
tensor = torch.tensor([1, 2, 3])
print(tensor.numpy())
print(tensor.tolist())
```

## 大小与维度

```python
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

```python
a = torch.tensor([1, 2, 3])
b = torch.tensor([4, 5, 6])
print(a + b) # tensor([5, 7, 9])
print(a * b) # tensor([ 4, 10, 18])
```

```python
a = torch.tensor([1, 2, 4])
print(torch.sum(a))          # tensor(7)
print(torch.max(a))          # tensor(4)
print(torch.mean(a.float())) # tensor(2.3333)
```

注意整型的张量不可以取 `mean` 会报错。

## 形状

```python
a = torch.tensor([
    [1, 2, 3],
    [4, 5, 6],
])
print(a.flatten()) # tensor([1, 2, 3, 4, 5, 6])
```

```python
a = torch.tensor([1, 2, 3, 4, 5, 6])
print(a.reshape(2, 3))
"""
tensor([[1, 2, 3],
        [4, 5, 6]])
"""
```

`reshape` 可以调整 tensor 的形状。

```python
a = torch.tensor([1, 2, 3])
b = a.unsqueeze(0)
c = a.unsqueeze(1)

print(a.shape) # torch.Size([3])
print(b.shape) # torch.Size([1, 3])
print(c.shape) # torch.Size([3, 1])
```

`unsqueeze(dim)` 在第 `dim` 维处插入一个大小为 $1$ 的维度。

```python
a = torch.randn(1, 3, 1)

b = a.squeeze()
c = a.squeeze(2)
fail = a.squeeze(1)

print(b.shape)    # torch.Size([3])
print(c.shape)    # torch.Size([1, 3])
print(fail.shape) # torch.Size([1, 3, 1])
```

`squeeze` 可以压缩大小为 $1$ 的维度。

不传参数的话会压掉所有大小为 $1$ 的；`squeeze(dim)` 会尝试压掉第 `dim` 维，但是大小不为 $1$ 的话什么都不会发生。

```python
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

## 向量与矩阵

向量点积：

```python
a = torch.tensor([1, 2, 3])
b = torch.tensor([4, 5, 6])
print(torch.dot(a, b)) # tensor(32)
```

矩阵乘法的三种写法：

```python
a = torch.randn(2, 3)
b = torch.randn(3, 4)
print(torch.matmul(a, b))
print(torch.mm(a, b))
print(a @ b)
```

矩阵转置：

```python
a = torch.tensor([
    [1, 2, 3],
    [4, 5, 6],
])
print(a.T)
```

## 条件判断

```python
tensor = torch.tensor([1, 2, 3, 4, 5])
print(tensor > 2) # tensor([False, False,  True,  True,  True])
print(tensor[tensor > 2]) # tensor([3, 4, 5])
print(torch.where(tensor > 2, tensor, torch.tensor(-1))) # tensor([-1, -1,  3,  4,  5])
```