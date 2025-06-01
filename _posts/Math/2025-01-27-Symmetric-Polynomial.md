---
title: 'Symmetric Polynomial'
date: 2025-01-27
permalink: /posts/2025/01/Symmetric-Polynomial/
excerpt: "对称多项式的引入。"
tags:
  - Math
  - Math 专题笔记
---

约定：本文中的多项式（polynomial）都指整式，即包括单项式。

# 对称多项式 Symmetric polynomial

$P(x_1, x_2, \cdots, x_n)$ 是一个 $n$ 元多项式，如果任意交换两个变量 $x_i, x_j$ 多项式不变，则 $P$ 是对称多项式。

等价定义：对于任意变量的置换，多项式都不变，则是对称多项式。

# 基本对称多项式 Elementary symmetric polynomial

对于 $n$ 个变量 $x_1, x_2, \cdots, x_n$，它们的 $n$ 个基本对称多项式 $\sigma_1, \sigma_2, \cdots, \sigma_n$ 为：

$$\sigma_k = \sum\limits_{1 \le i_1 < i_2 < \cdots < i_k \le n} x_{i_1} x_{i_2} \cdots x_{i_k}$$

不难发现 $\sigma_1$ 就是所有变量之和，$\sigma_n$ 就是所有变量之积。

为方便后文一些公式形式好看，定义 $\sigma_0 = 1$，以及 $k > n$ 时 $\sigma_k = 0$。

# 对称多项式基本定理 Fundamental theorem of symmetric polynomials

> Theorem. 任何 $n$ 元对称多项式 $P$ 都能表示成关于 $\sigma_1, \sigma_2, \cdots, \sigma_n$ 的多项式。

证明不会 哈哈哈。

# 韦达定理 Vieta's formulas

令 $f(x) = \sum\limits_{i=0}^n a_i x^i$（$a_n = 1$），其 $n$ 个根为 $x_1, x_2, \cdots, x_n$。

> $$\sigma_k = (-1)^k a_{n-k}$$

特别地，$\sigma_1 = - a_{n-1}$，$\sigma_n = (-1)^n a_0$。

## Proof

根据代数基本定理：

$$\begin{aligned}
    \sum\limits_{i=0}^n a_i x^i &= \prod\limits_{i=1}^n (x - x_i) \\
    &= \sum\limits_{i=0}^n (-1)^{n-i} \sigma_{n-i} x^i \\
\end{aligned}$$

对比左右两边系数即可。

# 牛顿恒等式 Newton's Sums / Newton's identities

令 $f(x) = \sum\limits_{i=0}^n a_i x^i$（$a_n = 1$），其 $n$ 个根为 $x_1, x_2, \cdots, x_n$。

令 $P_k$ 为这 $n$ 个根的 $k$ 次方和 $\sum\limits_{i=1}^n x_i^k$。

> $$\sum\limits_{i=0}^k a_{n-k+i} P_i = 0$$
>
> $$P_k = - \sum\limits_{i=0}^{k-1} a_{n-k+i} P_i = \boxed{\sum\limits_{i=0}^{k-1} (-1)^{k-i-1} \sigma_{k-i} P_i}$$
>
> 由于 $\sigma_{k-i}$ 仅在 $0 \le k-i \le n$ 不为 $0$，因此对于 $k > n$：
>
> $$P_k = - \sum\limits_{i=k-n}^{k-1} a_{n-k+i} P_i = \boxed{\sum\limits_{i=k-n}^{k-1} (-1)^{k-i-1} \sigma_{k-i} P_i}$$
>
> 也可写成
>
> $$P_k = \boxed{\sum\limits_{i=1}^n (-1)^{i-1} \sigma_i P_{k-i}}$$

这个柿子建立了 $P$ 与 $a$ 以及 $P$ 与 $\sigma$ 的关系。

Newton's Sums 告诉我们，$P_k$ 满足一个 $n$ 阶常系数齐次线性递推，可以用数列中的办法处理。

## Proof

<https://brilliant.org/wiki/newtons-identities/>

# Example 1: 一个 OI 题

> [UVA10655](https://www.luogu.com.cn/problem/UVA10655) 已知 $a+b$ 与 $ab$，求 $a^n + b^n$。

**【识别 Pattern】** 对称多项式 + 高次之和，用 Newton's Sums。

$$P_n = \sigma_1 P_{n-1} - \sigma_2 P_{n-2} = (a+b) P_{n-1} - ab \times P_{n-2}$$

# Example 2: 2019 AIME I Problem 8

> $\sin^{10} x + \cos^{10} x = \frac {11} {36}$，求 $\sin^{12} x + \cos^{12}$。

**【识别 Pattern】** 高次之和用 Newton's Sums。

注意力再差都能发现柿子是关于 $\sin^2 x$ 和 $\cos^2 x$ 的。相当于已知 $P_5 = \frac {11} {36}$。

把 Example 1 的式子直接拿来用：（设 $C = \sin^2 x \cos^2$）

$$\begin{aligned}
    P_n &= (\sin^2 x + \cos^2 x) P_{n-1} - \sin^2 x \cos^2 x \times P_{n-2} \\
    &= P_{n-1} - C \times P_{n-2}
\end{aligned}$$

$P_0 = 2, P_1 = 1$。

递推上去，$P_5$ 是一个关于 $C$ 的二次多项式，可以解得 $C$ 的值为 $\frac 1 6$。

递推上去知 $P_6 = \boxed{\frac {13} {54}}$。

# Example 3：三角函数综合题

> 求 $\cos^5 \frac 1 9 \pi + \cos^5 \frac 5 9 \pi + \cos^5 \frac 7 9 \pi$。
>
> 因为和出题人对脑电波非常无聊，所以：
>
> **【Hint】** 注意到原式相当于 $\cos^5 \frac 1 9 \pi + \cos^5 \frac 7 9 \pi + \cos^5 \frac {13} 9 \pi$，三个角度的特征为角度之差为 $\frac 2 3 \pi$。

令 $a = \cos \frac 1 9 \pi, b = \cos \frac 7 9 \pi, c = \cos \frac {13} 9 \pi$。原式即为 $a^5 + b^5 + c^5$。

**【识别 Pattern】** 五次方和，用 Newton's Sums。

为了递推到 $P_5$，我们需要 $\sigma_1, \sigma_2, \sigma_3$ 的值。

（下面三角函数知识与主题无关）

## $\sigma_1$

**【识别 Pattern】** 三个角画到单位圆上，是夹角为 $\frac 2 3 \pi$ 的三个单位根，和为 $0$。因此实部和也为 $0$，于是原来的三个 $\cos$ 和也为 $0$。即 $P_1 = \sigma_1 = 0$。

注意不到的话可以积化和差。

## $\sigma_2$

$P_2 = \sigma_1^2 - 2 \sigma_2$，因此算 $\sigma_2$ 和 $P_2$ 的难度一样，算 $P_2$。

**【识别 Pattern】** $\cos^2$ 用二倍角公式，转成一次。

$$\cos^2 \theta = \frac {\cos 2 \theta + 1} 2$$

然后发现这三个角的两倍依然满足夹角为 $\frac 2 3 \pi$，$\cos$ 和为 $0$。因此 $P_2 = \frac 3 2$。

$\sigma_2 = \frac 1 2 (\sigma_1^2 - P_2) = - \frac 3 4$。

## $\sigma_3$

**【识别 Pattern】** 三元对称多项式的 $\sigma_3$ 或 $P_3$，用公式

$$\boxed{a^3 + b^3 + c^3 - 3abc = (a + b + c)(a^2 + b^2 + c^2 -ab - ac - bc)}$$

即

$$P_3 - 3\sigma_3 = \sigma_1 (P_2 - \sigma_2)$$

因此和 $\sigma_2$ 转成 $P_2$ 一样，将问题转化为 $P_3$。

**【识别 Pattern】** $\cos^3$ 用三倍角公式，转成一次。

$$\cos^3 \theta = \frac {\cos 3 \theta + 3 \cos \theta} 4$$

然后发现这三个角的三倍都是 $\frac 1 3 \pi$，好算。

最终得到 $\sigma_3 = \frac 1 8$。

得到三阶递推式：

$$P_k = \frac 3 4 P_{k-2} + \frac 1 8 P_{k-3}$$

初值 $P_0 = 3, P_1 = 0, P_2 = \frac 3 2$。

递推得到 $P_5 = \boxed{\frac {15} {32}}$。