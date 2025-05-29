---
title: '自主探究：Modular Geometry'
date: 2025-04-24
permalink: /posts/2025/04/自主探究_Modular-Geometry/
excerpt: "尝试研究模意义下的几何问题。"
tags:
  - Math
  - 探究
---

# 前言

全文中的 $p$ 为奇素数。

我们希望研究"平面" $\mathbb F_p^2$ 中几何形状的性质。

# 直线

满足 $ax+by+c=0$ 的形状称为**直线**（其中 $a,b$ 不全为 $0$）。

举个例子：$\mathbb F_7^2$ 中 $y=3x+1$ 长这样：

```
(0,0)            (6,0)
⬛⬛⬜⬛⬛⬛⬛
⬜⬛⬛⬛⬛⬛⬛
⬛⬛⬛⬛⬛⬜⬛
⬛⬛⬛⬜⬛⬛⬛
⬛⬜⬛⬛⬛⬛⬛
⬛⬛⬛⬛⬛⬛⬜
⬛⬛⬛⬛⬜⬛⬛
(0,6)            (6,6)
```

若两条直线的 $(a_1, b_1, c_1)$ 与 $(a_2, b_2, c_2)$ 线性相关，则称这两条直线为**同一条直线**。

## Properties

> **Property 1. 直线有 $p$ 个点。**

证明：WLOG 设 $b \ne 0$。可以解出 $y = - \frac a b x - \frac c b$。对于每一个 $x$ 都有一个对应的 $y$。$\square$

---

> **Property 2. 两点确定一条直线。**

$$\begin{bmatrix}
    x_1 & y_1 \\
    x_2 & y_2 \\
\end{bmatrix}
\begin{bmatrix}
    a \\
    b \\
\end{bmatrix}
=
\begin{bmatrix}
    -c \\
    -c \\
\end{bmatrix}$$

不妨设

TODO:

---

若两条直线的 $(a_1, b_1)$ 与 $(a_2, b_2)$ 线性相关，称这两条直线**平行**，否则称**不平行**。

> **Property 3. 平行的直线没有交点，不平行的直线有且仅有一个交点。**

证明：两条直线的交点 $(x,y)$ 应满足：

$$\begin{bmatrix}
    a_1 & b_1 \\
    a_2 & b_2 \\
\end{bmatrix}
\begin{bmatrix}
    x \\
    y \\
\end{bmatrix}
=
\begin{bmatrix}
    -c_1 \\
    -c_2 \\
\end{bmatrix}$$

令 $A = \begin{bmatrix} a_1 & b_1 \\ a_2 & b_2 \\ \end{bmatrix}$，$\det A = 0$ 当且仅当两直线平行，两直线不平行时原方程的解唯一。$\square$

## 一个定理

> **Theorem. $\mathbb F_p^2$ 中最多可以取出 $p+1$ 个点使得其中不存在三点共线。（2025 CTST 6）**

不妨设原点被取。

所有 $y=kx$ 与 $x=0$ 共 $p+1$ 条直线刚好完美覆盖整个平面（除了 $(0,0)$），因此每条直线上最多再有一个点，最多有 $p+2$。

但是经过尝试，发现最多似乎只能 $p+1$。我们尝试证明 $p+2$ 不行。

每个点都应该符合刚才原点处那个性质。我们可以把任意点都移动到原点处，观察 $x=0$ 上有两个点，因此原平面每条竖线上都有 $2$ 个或 $0$ 个点，总点数只能为偶数。但是 $p+2$ 是奇数，矛盾。

因此最多只有 $p+1$，接下来证明必能取到。

构造：（思路：圆锥曲线不存在三点共线）

构造圆锥曲线 $\Gamma: y^2 = r x^2 + 1$。接下来证明 $r$ 为非二次剩余时 $|\Gamma| = p+1$。

$$\begin{aligned}
    & |\Gamma| \\
    =& \sum\limits_{x \in \mathbb F_p} \left(1 + \left( \frac {rx^2 + 1} p \right) \right) \\
    =& p + \sum\limits_{x \in \mathbb F_p} \left( \frac {rx^2 + 1} p \right) \\
\end{aligned}$$

令 $A = \sum\limits_{x \in \mathbb F_p} \left( \frac {rx^2 + 1} p \right)$。

$$\begin{aligned}
    & A \\
    \equiv& \sum\limits_{x} (rx^2 + 1)^{\frac {p-1} 2} \\
    \equiv& \sum\limits_{x} \sum\limits_{i=0}^{\frac {p-1} 2} \binom {\frac {p-1} 2} i r^i x^{2i} \\
    \equiv& \sum\limits_{i=0}^{\frac {p-1} 2} \binom {\frac {p-1} 2} i r^i \sum\limits_{x} x^{2i} \\
\end{aligned}$$

分析一下 $S \equiv \sum\limits_{x \in \mathbb F_p} x^k$ 的性质。

- 当 $k>0$ 且 $(p-1) \nmid k$，令 $g$ 为一原根，$x = g^j$，求和化为等比数列求和：$\frac {(g^k)^{p-1} - 1} {g^k - 1} \equiv 0$。
- 当 $k=0$，$S$ 为 $0$。
- 当 $k>0$ 且 $(p-1) \mid k$，$S \equiv -1$。

继续推导：

$$\begin{aligned}
    & A \\
    \equiv& - r^{\frac {p-1} 2} \\
    \equiv& - \left( \frac r p \right) \pmod p \\
\end{aligned}$$

令 $r$ 为一个非二次剩余，即可满足 $A \equiv 1$ 即 $|\Gamma| \equiv 1$，不难得到 $|\Gamma| = p+1$。$\square$

# 圆锥曲线

形如 $Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0$ 的形状称为圆锥曲线。

定义判别式 $\Delta = B^2 - 4AC$。
- 若 $\left( \frac \Delta p \right) = 1$，则圆锥曲线是双曲线。
- 若 $\left( \frac \Delta p \right) = -1$，则圆锥曲线是椭圆。
- 若 $\Delta = 0$，TODO:

## Example

### Example 1：抛物线

$\mathbb F_7^2$ 中 $y = x^2$：

```
⬜⬛⬛⬛⬛⬛⬛
⬛⬜⬛⬛⬛⬛⬜
⬛⬛⬛⬜⬜⬛⬛
⬛⬛⬛⬛⬛⬛⬛
⬛⬛⬜⬛⬛⬜⬛
⬛⬛⬛⬛⬛⬛⬛
⬛⬛⬛⬛⬛⬛⬛
```

### Example 2：椭圆

$\mathbb F_7^2$ 中 $y^2 = 3x^2 + 1$：

```
⬛⬛⬛⬜⬜⬛⬛
⬜⬛⬛⬛⬛⬛⬛
⬛⬜⬛⬛⬛⬛⬜
⬛⬛⬛⬛⬛⬛⬛
⬛⬛⬛⬛⬛⬛⬛
⬛⬜⬛⬛⬛⬛⬜
⬜⬛⬛⬛⬛⬛⬛
```

### Example 3

退化的圆锥曲线：$\mathbb F_7^2$ 中 $x^2 - y^2 = 0$：

```
⬜⬛⬛⬛⬛⬛⬛
⬛⬜⬛⬛⬛⬛⬜
⬛⬛⬜⬛⬛⬜⬛
⬛⬛⬛⬜⬜⬛⬛
⬛⬛⬛⬜⬜⬛⬛
⬛⬛⬜⬛⬛⬜⬛
⬛⬜⬛⬛⬛⬛⬜
```

---

> **Property 1. 圆锥曲线上不存在三点共线。**

联立圆锥曲线和直线方程，总共也就二次，不可能有三个解。$\square$

---


TODO:

# References

- [一道极其优雅的平面数论题！ - 哔哩哔哩](https://www.bilibili.com/video/BV1V5Q1YQE5j/)
- [2025中国数学国家集训队第一阶段第一次测试解答 - 哔哩哔哩](https://www.bilibili.com/opus/1042189903326085125)