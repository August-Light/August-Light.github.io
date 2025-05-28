---
title: 'Use Mathematica in Python'
date: 2024-06-12
permalink: /posts/2024/06/Use-Mathematica-in-Python/
excerpt: "在 Python 中使用 Wolfram Mathematica 的计算能力。"
tags:
  - Coding
  - Mathematica
---

## 准备工作

- 需要有 Wolfram Mathematica。
- 需要安装 `wolframclient` 这个第三方库。

## 起手式

导入 `wolframclient`：

```python
from wolframclient.evaluation import WolframLanguageSession
from wolframclient.language import wl, wlexpr
```

启动：

**注意：这一步有概率出现无法启动的报错。建议用 try-except 判一下。**

```python
# KERNEL_PATH 要改成自己的
KERNEL_PATH = r"D:\Program Files\Wolfram Research\Mathematica\13.2\WolframKernel.exe"
session = WolframLanguageSession(KERNEL_PATH)
```

运行 `1+1` 判断是否启动成功：

```python
def test():
    try:
        session.evaluate(wlexpr("1+1"))
        print("Started Successfully")
    except Exception as e:
        print("BOOMED!")
        print(e)
        exit(0)
```

## 运行代码

### 直接运行 Mathematica 代码

```python
# 计算 10 的阶乘
res = session.evaluate(wlexpr("Factorial[10]"))
```

### 在 Python 中使用 Mathematica 函数

```python
# 计算 10 的阶乘
res = session.evaluate(wl.Factorial(10))
```

注意：此处代码中的函数名 `Factorial` 是没有代码高亮的。

### 清空

```python
session.terminate()
```

### 结束

```python
session.stop()
```

### 关于计算结果

如果算出来的是整数，那么会直接变成 Python 中的 `int`：

```python
a = session.evaluate(wlexpr("Factorial[10]"))
print(type(a))

# 输出：<class 'int'>
```

如果算出来的不是整数，那么会保留 Mathematica 格式：

```python
c = session.evaluate(wlexpr("1/3"))
print(c)
# 输出：Rational[1, 3]
print(type(c))
# 输出：<class 'wolframclient.language.expression.WLFunction'>
```

## 示例代码

```python
from wolframclient.evaluation import WolframLanguageSession
from wolframclient.language import wl, wlexpr

KERNEL_PATH = r"D:\Program Files\Wolfram Research\Mathematica\13.2\WolframKernel.exe"
session = WolframLanguageSession(KERNEL_PATH)

res = session.evaluate(wlexpr("Sum[x, {x, 1, 10^18}]"))
print(res)

session.stop()

# 输出：500000000000000000500000000000000000
```

## 参考资料

- [Wolfram Client Library for Python](https://reference.wolfram.com/language/WolframClientForPython/)
- [在Python中使用Mathematica - 知乎](https://zhuanlan.zhihu.com/p/645865950)