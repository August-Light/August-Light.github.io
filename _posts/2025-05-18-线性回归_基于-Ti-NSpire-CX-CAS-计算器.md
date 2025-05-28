---
title: '线性回归，基于 Ti-NSpire CX CAS 计算器'
date: 2025-05-18
permalink: /posts/2025/05/线性回归_基于-Ti-NSpire-CX-CAS-计算器/
excerpt: "在 Ti-NSpire CX CAS 计算器中算出线性回归的数值解与解析解。"
---

一元线性回归：假设你有若干个坐标 $(x_i, y_i)$，你要拟合一条最优直线。

为了方便，假设我们有 $3$ 个坐标。

Step 1. 设定矩阵 $p$：

$$p := \begin{bmatrix}
    1 & x_1 \\
    1 & x_2 \\
    1 & x_3 \\
\end{bmatrix}$$

Step 2. 计算：

$$(p^T p)^{-1} p^T \begin{bmatrix} y_1 \\ y_2 \\ y_3 \end{bmatrix}$$

（注：转置运算 $()^T$ 可以在菜单栏的 2 中的矩阵一栏中找到，求逆直接写 $-1$ 次方即可）

算出来的结果记为

$$\begin{bmatrix}
    b \\ k
\end{bmatrix}$$

最终，得到的最优直线就是

$$y = k x + b$$