---
title: 'Fibonacci 全家桶'
date: 2025-12-30
permalink: /posts/2025/12/2025-12-30-Fibonacci-全家桶/
excerpt: "Fibonacci 数列的恒等式……抛弃死记硬背！"
tags:
  - Math
---

# Fibonacci 数列

[OEIS A000045](https://oeis.org/A000045)

$$F_n = \begin{cases}
    0 & n = 0 \\
    1 & n = 1 \\
    F_{n-1} + F_{n-2} & n \ge 2 \\
\end{cases}$$

# Fibonacci 数列的矩阵表示

设矩阵

$$A = \begin{bmatrix}
    1 & 1 \\
    1 & 0 \\
\end{bmatrix}$$

该矩阵具有以下性质：
- $\det A = -1$
- $\text{tr} A = 1$
- $A^2 - A - I = 0$，即 $A^2 = A + I$（Cayley–Hamilton 定理）

Fibonacci 数列可被表示为该矩阵的幂：

$$\boxed{
    A^n = \begin{bmatrix}
    F_{n+1} & F_n \\
    F_n & F_{n-1} \\
\end{bmatrix}}$$

这个矩阵表示是全文的核心。

# Cassini 恒等式——$\det (A^n)$

$$\begin{aligned}
    \det (A^n) &= (\det A)^n = (-1)^n \\
    F_{n+1} F_{n-1} - F_n^2 &= (-1)^n \\
\end{aligned}$$

## 邻项互质：$F_n \perp F_{n+1}$

反证。设 $d = \gcd(F_n, F_{n+1}) \ne 1$，根据递推公式可知 $d \mid F_{n-1}$。根据 Cassini 恒等式

$$F_{n+1} F_{n-1} - F_n^2 = (-1)^n$$

等式左边是 $d^2$ 倍数，这意味着等式右边 $d^2 \mid (-1)^n$，而这不可能。

# 加法公式——$A^n A^m$

$$A^{n+m} = A^n A^m$$

$$\boxed{
    F_{n+m} = F_{n+1} F_m + F_n F_{m-1}
}$$

特别地，当 $n = m$ 时，我们会得到**倍增公式**：

$$\boxed{
    F_{2n} = F_n (F_{n-1} + F_{n+1})
}$$

一会儿在学习了 Lucas 数列 $L$ 后，我们知道 $L_n = F_{n-1} + F_{n+1}$：

$$\boxed{
    F_{2n} = F_n L_n
}$$

更关键地：

$$\boxed{
    L_n = \frac {F_{2n}} {F_n}
}$$

例题：[2024 AMC12B #18](https://artofproblemsolving.com/wiki/index.php?title=2024_AMC_10B_Problems/Problem_23)

# $F_n \mid F_{kn}$——对角阵的封闭性

我们有

$$A^n \equiv \begin{bmatrix}
    ? & 0 \\
    0 & ? \\
\end{bmatrix} \pmod {F_n}$$

对角阵的幂还是对角阵，即

$$A^{kn} \equiv \begin{bmatrix}
    ? & 0 \\
    0 & ? \\
\end{bmatrix} \pmod {F_n}$$

观察 $F_{kn}$ 对应的位置是 $0$，因此 $F_n \mid F_{kn}$。

# $\gcd(F_n, F_m) = F_{\gcd(n,m)}$

把 $m$ 拆解为 $qn + r$，其中 $r = m \bmod n$：

$$\begin{aligned}
    & \gcd(F_n, F_m) \\
    =& \gcd(F_n, F_{qn + r}) \\
    =& \gcd(F_n, \textcolor{red}{F_{qn} F_{r+1}} + F_{qn - 1} F_r) \\
    =& \gcd(F_n, \textcolor{limegreen}{F_{qn - 1}} F_r) \\
    =& \gcd(F_n, F_r) \\
\end{aligned}$$

- 第三行：$F_n \mid F_{qn}$
- 第四行：$F_n \mid F_{qn} \perp F_{qn-1}$

因此我们得到了

$$\gcd(F_n, F_m) = \gcd(F_n, F_{m \bmod n})$$

进行 Euclid 算法，可得

$$\gcd(F_n, F_m) = \gcd(F_{\gcd(n, m)}, F_0)$$

$$\boxed{
    \gcd(F_n, F_m) = F_{\gcd(n,m)}
}$$

# Lucas 数列——$\text{tr}(A^n)$

[OEIS A000032](https://oeis.org/A000032)

$$\boxed{
    L_n := \text{tr}(A^n) = F_{n-1} + F_{n+1}
}$$

## 递推公式——$A^2 = A + I$

$$\begin{aligned}
    A^2 &= A + I \\
    A^n &= A^{n-1} + A^{n-2} \\
    \text{tr}(A^n) &= \text{tr}(A^{n-1}) + \text{tr}(A^{n-2}) \\
    L_n &= L_{n-1} + L_{n-2} \\
\end{aligned}$$

$$\boxed{
    L_n = \begin{cases}
        2 & n = 0 \\
        1 & n = 1 \\
        L_{n-1} + L_{n-2} & n \ge 2 \\
    \end{cases}
}$$

# Lucas 数列加法公式——$\text{tr}(A^n A^m)$

对于 $2 \times 2$ 矩阵 $X,Y$，有

$$\text{tr}(XY) = \text{tr} X \text{tr} Y - \det Y \text{tr}(X Y^{-1})$$

> 证明：对 $2 \times 2$ 矩阵 $Y$ 运用 Cayley–Hamilton 定理尝试把 $Y$ 拆成和差，以便于 $\text{tr}$ 运算。
>
> $$\begin{aligned}
>     Y^2 - \text{tr}(Y) Y + \det (Y) I &= 0 \\
>     Y (Y - \text{tr}(Y) I) &= - \det (Y) I \\
>     Y - \text{tr}(Y) I &= - \det(Y) Y^{-1} \\
>     Y &= \text{tr}(Y) I - \det(Y) Y^{-1} \\
> \end{aligned}$$
>
> $$\begin{aligned}
>     & \text{tr}(XY) \\
>     =& \text{tr}(X (\text{tr}(Y) I - \det(Y) Y^{-1})) \\
>     =& \text{tr} X \text{tr} Y - \det Y \text{tr}(X Y^{-1}) \\
> \end{aligned}$$

我们用这个公式可以拆开 $\text{tr}(XY)$ 的结构：

$$\begin{aligned}
    & \text{tr}(A^{n+m}) \\
    =& \text{tr}(A^n A^m) \\
    =& \text{tr} (A^n) \text{tr} (A^m) - \det (A^m) \text{tr}(A^{n-m}) \\
\end{aligned}$$

$$\boxed{
    L_{n+m} = L_n L_m - (-1)^m L_{n-m}
}$$

当 $n = m$ 时，得**倍增公式**：

$$\boxed{
    L_{2n} = L_n^2 - 2 (-1)^n
}$$

# 其他内容

## 生成函数

$$\boxed{
    F(x) = \frac x {1 - x - x^2}
}$$

$$\boxed{
    L(x) = \frac {2 - x} {1 - x - x^2}
}$$

## Binet 公式

利用矩阵相似对角化或直接把生成函数部分分式分解等知识（推导不难但繁杂，略去），可以得到：

$$\boxed{
    F_n = \frac 1 {\sqrt 5} \left(\left(\frac {1 + \sqrt 5} 2 \right)^n - \left(\frac {1 - \sqrt 5} 2 \right)^n \right)
}$$

$$\boxed{
    L_n = \left(\frac {1 + \sqrt 5} 2 \right)^n + \left(\frac {1 - \sqrt 5} 2 \right)^n
}$$