---
title: 'Mathematica Partial Fraction Decomposition'
date: 2024-06-10
permalink: /posts/2024/06/Mathematica-Partial-Fraction-Decomposition/
excerpt: "Mathematica 的部分分式分解函数。"
tags:
  - Mathematica
---

## 遇到的问题

Mathematica 中有一个自带的部分分式分解函数 [`Apart`](https://reference.wolfram.com/language/ref/Apart.html)。

```Mathematica
In := Apart[(-3 + x)/((-1 + x) (1 + x))]
Out := -(1/(-1 + x)) + 2/(1 + x)
```

但是 `Apart` 遇到分解结果中带无理数的就会摆烂：

```Mathematica
In := Apart[x/(1 - x - x^2)]
Out := -(x/(-1 + x + x^2))
```

## 解决方案 1

我们有一个函数 ``Integrate`ComplexApart`` 可以使用：

```Mathematica
In := Integrate`ComplexApart[x/(1 - x - x^2), x]
Out := -((-1 + Sqrt[5])/(2 Sqrt[5] (1/2 (1 - Sqrt[5]) + x))) + (-1 - Sqrt[
  5])/(2 Sqrt[5] (1/2 (1 + Sqrt[5]) + x))
```

它不是官方文档内的函数，但是似乎可以正常使用。

## 解决方案 2

使用 `ResourceFunction` 中的函数 [`ApartAll`](https://resources.wolframcloud.com/FunctionRepository/resources/ApartAll/)：

```Mathematica
In := ApartAll = ResourceFunction["ApartAll"];

In := ApartAll[x/(1 - x - x^2)]
Out := (5 + Sqrt[5])/(10 (1/2 (-1 - Sqrt[5]) - x)) + (5 - Sqrt[5])/(
 10 (1/2 (-1 + Sqrt[5]) - x))
```

也可以使用函数 [`ExtendedApart`](https://resources.wolframcloud.com/FunctionRepository/resources/ExtendedApart/)：

```Mathematica
In := ExtendedApart = ResourceFunction["ExtendedApart"];
```

似乎 `ExtendedApart` 更强大一些。

## 参考资料

- [equation solving - Apart for complex roots? - Mathematica Stack Exchange](https://mathematica.stackexchange.com/questions/68824/apart-for-complex-roots)