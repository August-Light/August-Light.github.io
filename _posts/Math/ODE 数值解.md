# 问题

任意阶 ODE 都等价于一个多元的一阶 ODE。因此我们只考虑一阶 ODE：

$$\begin{cases}
    y'(t) = f(t, y(t)) \\
    y(t_0) = y_0 \\
\end{cases}$$

我们要数值求解该 ODE，这指的是我们要求在一堆等距的 $t$ 上 $y$ 的取值。

我们可以用 $y'$ 的积分来表示相邻 $y$ 之间的增量：

$$y_{k+1} = y_k + \int_{t_k}^{t_k + h} y'(t) dt$$

问题变为求出这个积分的近似值。

## Taylor 展开

$$y'_{k+1} = y'(t_k + h) = \sum_{n=0}^\infty \frac {y^{(n+1)}_k} {n!} h^n$$

$$\begin{aligned}
    \int_{t_k}^{t_k + h} y'(t) dt &= \sum_{n=1}^\infty \frac {y^{(n)}_k} {n!} h^n \\
\end{aligned}$$

我们想要拟合尽量高的 $h^n$ 项。

困难在于：我们只有 $y \mapsto y'$ 的关系，并没有 $y' \mapsto y''$ 之类的关系。这是我们接下来要解决的问题。

# Euler 法

我们打算先摆个烂。

既然不知道二阶导，那我就不用了：

$$\int_{t_k}^{t_k + h} y'(t) dt = y'_k h + O(h^2)$$

每次更新时：

$$\boxed{
    y_{k+1} = y_k + y'_k h
}$$

用题目给的 $y \mapsto y'$ 的函数 $f$ 来表示：

$$\boxed{\begin{cases}
    K = f(y_k, t_k) \\
    y_{k+1} = y_k + K h
\end{cases}}$$

# Heun 法

这次我们的目标是得到二阶导：

$$\int_{t_k}^{t_k + h} y'(t) dt = y'_k h + \frac 1 2 y''_k h^2 + O(h^3)$$

考虑先 Euler 走一步得到一个估计值 $\tilde y_{k+1}$，尝试把它再次代入微分方程得到一个二阶导项：

$$\tilde y_{k+1} := y_k + y'_k h$$

$$\begin{aligned}
    \tilde y'_{k+1} &= f(t_{k+1}, \tilde y_{k+1}) \\
    &= f(t_k, y_k) + h \times \frac {df} {dt} + O(h^2) \\
    &= y'_k + y''_k h + O(h^2) \\
\end{aligned}$$

（注意 $\frac {df} {dt}$ 是一个全导数）

出现了！我们给 $\tilde y''_{k+1}$ 乘上 $h$ 变成二次项，然后配上 $\frac 1 2$ 的系数，并且再用朴素方法配好一次项：

$$\begin{aligned}
    & \frac {\tilde y'_{k+1}} 2 h \\
    =& \frac {y'_k + y''_k h + O(h^2)} 2 h \\
    =& \left( y'_k h + \frac 1 2 y''_k h^2 + O(h^3) \right) - \frac 1 2 y'_k h \\
\end{aligned}$$

$$\frac {y'_k + \tilde y'_{k+1}} 2 h = y'_k h + \frac 1 2 y''_k h^2 + O(h^3)$$

因此我们也就得到了我们对 $y_{k+1}$ 的计算：

$$\boxed{\begin{cases}
    \tilde y_{k+1} = y_k + y'_k h \\
    y_{k+1} = y_k + \dfrac {y'_k + \tilde y'_{k+1}} 2 h
\end{cases}}$$

同样用 $f$ 来表示：

$$\boxed{\begin{cases}
    K_1 = f(t_k, y_k) \\
    K_2 = f(t_k + h, y_k + K_1 h) \\
    y_{k+1} = y_k + \left( \frac 1 2 K_1 + \frac 1 2 K_2 \right) h
\end{cases}}$$

## Heun 法的几何意义

梯形近似积分：

$$\int_{t_k}^{t_k + h} y'(t) dt \approx \frac {y'_k + \tilde y'_{k+1}} 2 h$$

# RK4

根据前面推导 Heun 法的经验，我们的直觉应当可以意识到更高阶精度的方案也是存在的。这一类迭代的框架被称为 Runge–Kutta methods。Euler 法和 Heun 法也落在该框架内。

实践中最好用的是四阶精度（即 $O(h^5)$）的 RK4：

$$\boxed{\begin{cases}
    K_1 = f(t_n, y_n) \\
    K_2 = f(t_n + \frac 1 2 h, y_n + \frac 1 2 K_1 h) \\
    K_3 = f(t_n + \frac 1 2 h, y_n + \frac 1 2 K_2 h) \\
    K_4 = f(t_n + h, y_n + K_3 h) \\
    y_{n+1} = y_n + \left( \frac 1 6 K_1 + \frac 1 3 K_2 + \frac 1 3 K_3 + \frac 1 6 K_4 \right) h \\
\end{cases}}$$

很多系数的选择都是自由的，这是计算量比较小的一种选择。