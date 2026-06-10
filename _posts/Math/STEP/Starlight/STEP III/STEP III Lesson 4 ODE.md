# 一阶 ODE

$$\boxed{
    \frac {dy} {dx} + p(x)y = q(x) \implies y = e^{-\int p(x) dx} \int q(x) e^{\int p(x) dx} dx
}$$

证明：

$$\begin{aligned}
    \frac {dy} {dx} + p(x)y &= q(x) \\
    e^{\int p(x) dx} \frac {dy} {dx} + e^{\int p(x) dx} p(x) y &= q(x) e^{\int p(x) dx} \\
    e^{\int p(x) dx} \frac {dy} {dx} + y \frac d {dx} (e^{\int p(x) dx}) &= q(x) e^{\int p(x) dx} \\
    \frac d {dx} (e^{\int p(x) dx} \times y) &= q(x) e^{\int p(x) dx} \\
    y &= e^{-\int p(x) dx} \int q(x) e^{\int p(x) dx} dx \\
\end{aligned}$$

# ODE 通解结构

以二阶为例。

**Definition.** 函数的线性无关：对于函数 $f,g$，方程

$$C_1 f(x) + C_2 g(x) \equiv 0$$

的唯一解为 $C_1 = 0, C_2 = 0$，则称 $f,g$ 线性无关。

💡 可以使用 Wronskian 系统判断多个函数的线性无关。

**Theorem.** 对于二阶 ODE

$$y'' + a(x) y' + b(x) = 0$$

若已知其有线性无关解 $y = f_1(x), y = f_2(x)$，则其通解为 $y = C_1 f_1(x) + C_2 f_2(x)$。

# 常系数齐次 ODE

## 特征方程

对于常系数齐次 ODE

$$\sum_{k=0}^n a_k y^{(k)} = 0$$

其特征方程为

$$\sum_{k=0}^n a_k \lambda^k = 0$$

## 二阶常系数齐次 ODE

解特征方程得到 $\lambda_1, \lambda_2$。

（不同实根）若 $\lambda_1 \ne \lambda_2 \in \mathbb R$：

$$y = C_1 e^{\lambda_1 x} + C_2 e^{\lambda_2 x}$$

（相同实根）若 $\lambda_1 = \lambda_2$：记 $\lambda = \lambda_1 = \lambda_2$，

$$y = (C_1 + C_2 x) e^{\lambda x}$$

（共轭复根）若 $\lambda_1 \ne \lambda_2 \not \in \mathbb R$：令 $\lambda_{1,2} = \alpha \pm i \beta$，

$$y = e^{\alpha x} (C_1 \cos \beta x + C_2 \sin \beta x)$$

# 一阶常系数齐次 ODE 组

> 解一阶常系数齐次 ODE 组：
>
> $$\begin{cases}
>     \dot y = - 2y + 2z \\
>     \dot z = 2y - 5z \\
> \end{cases}$$

## 【超纲】线性代数做法

$$\frac{d}{dt}
\begin{bmatrix}
y \\ z
\end{bmatrix}
=
\begin{bmatrix}
-2 & 2 \\
2 & -5
\end{bmatrix}
\begin{bmatrix}
y \\ z
\end{bmatrix}$$

$$\implies \begin{cases}
    \lambda_1 = -1 \\
    v_1 = \begin{bmatrix} 2 \\ 1 \end{bmatrix}
\end{cases}, \quad \begin{cases}
    \lambda_2 = -6 \\
    v_2 = \begin{bmatrix} 1 \\ -2 \end{bmatrix} \\
\end{cases}$$

$$\begin{bmatrix} y \\ z \end{bmatrix} = A e^{-t} \begin{bmatrix} 2 \\ 1 \end{bmatrix} + B e^{-6t} \begin{bmatrix} 1 \\ -2 \end{bmatrix}$$

## $n$ 阶 ODE 做法

先用第一个式子，用 $y$ 表示 $z$：

$$\dot y = - 2y + 2z \implies z = \frac {\dot y + 2y} 2$$

$$\dot z = \frac {\ddot y + 2 \dot y} 2$$

代入第二个式子：

$$\frac {\ddot y + 2 \dot y} 2 = 2y - 5 \times \frac {\dot y + 2y} 2$$

$$\ddot y + 7 \dot y + 6y = 0$$

$$\lambda^2 + 7 \lambda + 6 = 0 \implies \lambda_1 = -1, \lambda_2 = -6$$

$$y = A e^{-t} + B e^{-6t}$$

$$\dot y = -A e^{-t} - 6B e^{-6t} \implies z = \frac 1 2 A e^{-t} - 2 B e^{-6t}$$