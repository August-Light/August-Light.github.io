# 抛物线的参数方程

$$\boxed{y^2 = 4ax \implies \begin{cases}
    x = a t^2 \\
    y = 2 a t \\
\end{cases}}$$

$$\frac {dy} {dx} = \frac {\frac {dy} {dt}} {\frac {dx} {dt}} = \frac {2a} {2at} = \frac 1 t \implies \boxed{t = \frac 1 {\frac {dy} {dx}}}$$

## 例题：直线到抛物线距离

> The line $L$ has equation $y = mx + c$, where $m > 0$ and $c > 0$. Show that, in the case $mc > a > 0$, the shortest distance between $L$ and the parabola $y^2 = 4ax$ is
>
> $$\frac {mc - a} {m \sqrt{m^2 + 1}}$$

在抛物线上作一切线平行于直线 $L$，问题变为求切点到 $L$ 的距离。

设切点为 $(at^2, 2at)$，则 $t$ 为该点处切线斜率倒数：

$$t = \frac 1 m \implies \begin{cases}
    x = \frac a {m^2} \\
    y = \frac {2a} m \\
\end{cases}$$

该点到直线 $L$ 即 $mx - y + c = 0$ 的距离为：

$$\frac {\lvert m \frac a {m^2} - \frac {2a} m + c \rvert} {\sqrt{m^2 + 1}} = \frac {mc - a} {m \sqrt{m^2 + 1}}$$

# 曲率与曲率半径

对一条二阶可导的曲线，其切线方向转过的角度 $\theta$ 关于弧长 $s$ 的导数（的绝对值）被称为**曲率 $\kappa$**：

$$\boxed{
    \kappa := \left\lvert \frac {d \theta} {ds} \right\rvert
}$$

对于使用参数方程定义的曲线 $(x(t), y(t))$，其曲率可以这么求：

$$\kappa = \left\lvert \frac {d \theta} {ds} \right\rvert = \left\lvert \frac {\dot \theta} {\dot s} \right\rvert$$

$$\begin{aligned}
    \dot \theta &= \frac d {dt} \arctan \frac {dy} {dx} \\
    &= \frac d {dt} \arctan \frac {\dot y} {\dot x} \\
    &= \frac {\frac d {dt} \frac {\dot y} {\dot x}} {1 + (\frac {\dot y} {\dot x})^2} \\
    &= \frac {\dot x \ddot y - \ddot x \dot y} {\dot x^2 + \dot y^2}
\end{aligned}$$

$$\dot s = \sqrt{\dot x^2 + \dot y^2}$$

$$\boxed{
    \kappa = \left\lvert \frac {\dot x \ddot y - \dot y \ddot x} {(\dot x^2 + \dot y^2)^{\frac 3 2}} \right\rvert
}$$

对于普通的 $y = f(x)$ 的曲线，我们直接令 $x = t$：

$$\boxed{
    \kappa = \left\lvert \frac {y''} {(1 + y')^{\frac 3 2}} \right\rvert
}$$

---

考虑一个半径为 $R$ 的圆。根据定义可以直接求出其曲率

$$\begin{aligned}
    ds &= R d \theta \\
    \frac {ds} {d \theta} &= R \\
    \kappa = \frac {d \theta} {ds} &= \frac 1 R \\
\end{aligned}$$

因此，若一条曲线在某处曲率为 $\kappa$，则那里附近的表现应该类似于一个半径为 $\frac 1 \kappa$ 的圆。我们定义这个值为 **曲率半径 $\rho$**：

$$\boxed{
    \rho := \frac 1 \kappa
}$$

# 例题：与一簇曲线正交的曲线

> $\mathcal C$ 的方程为 $r = f(\theta)$。对于任意 $a$，$\mathcal C$ 与曲线 $r = a (1 + \sin \theta)$ 正交。
>
> $\mathcal C$ 经过点 $r = 4, \theta = \frac \pi 2$。求出 $\mathcal C$ 的方程。

我们首先刻画正交这个条件：在垂足处，有

$$\boxed{
    f(\theta) g(\theta) + f'(\theta) g'(\theta) = 0
}$$

【证明 1】不超纲：

$$\frac {dy} {dx} = \cdots = \frac {r + r' \tan \theta} {-r \tan \theta + r'}$$

$$\frac {f + f' \tan \theta} {-f \tan \theta + f'} \times \frac {g + g' \tan \theta} {-g \tan \theta + g'} = -1$$

省略一大堆繁杂计算后：

$$fg + f'g' = 0$$

【证明 2】：

$$ds = dr \hat r + r d\theta \hat \theta$$

$$\begin{aligned}
    ds_1 \perp ds_2 \implies dr_1 dr_2 + r_1 r_2 d\theta_1 d \theta_2 &= 0 \\
    \frac {dr_1} {d\theta_1} \frac {dr_2} {d\theta_2} + r_1 r_2 &= 0
\end{aligned}$$

---

$$f(\theta) = a (1 + \sin \theta) \implies f'(\theta) = a \cos \theta$$

$$\begin{aligned}
    a (1 + \sin \theta) g(\theta) + a \cos \theta g'(\theta) &= 0 \\
    \frac {g'(\theta)} {g(\theta)} &= - \frac {1 + \sin \theta} {\cos \theta} \\
    \ln \lvert g(\theta) \rvert &= \ln \left\lvert \frac {\cos \theta} {\sec \theta + \tan \theta} \right\rvert + C \\
    g(\theta) &= C (1 - \sin \theta)
\end{aligned}$$

代入 $r = 4, \theta = \frac \pi 2$ 得 $g(\theta) = 2 (1 - \sin \theta)$。



# 双曲函数求导与多倍角

$$\begin{cases}
    \cosh^2 x &- \sinh^2 x &= 1 \\
    1 &- \tanh^2 x &= \operatorname{sech}^2 x \\
    \coth^2 x &- 1 &= \operatorname{csch}^2 x \\
\end{cases}$$

> Let $y = \ln(x^2 - 1)$, where $x > 1$, and let $r$ and $\theta$ be functions of $x$ determined by $r = \sqrt{x^2 - 1}$ and $\coth \theta = x$. Show that
>
> $$\frac {dy} {dx} = \frac {2 \cosh \theta} r$$
>
> and
>
> $$\frac {d^2 y} {dx^2} = - \frac {2 \cosh 2 \theta} {r^2}$$
>
> and find an expression in terms of $r$ and $\theta$ for $\frac {d^3 y} {dx^3}$.
>
> Find, with proof, a similar formula for $\frac {d^n y} {dx^n}$ in terms of $r$ and $\theta$.

$$\begin{aligned}
    \frac {dy} {dx} &= \frac d {dx} \ln(r^2) \\
    &= \frac {dr} {dx} \frac d {dr} \ln(r^2) \\
    &= \frac x {\sqrt{x^2 - 1}} \times \frac 2 r \\
    &= \frac {\coth \theta} {\operatorname{csch} \theta} \times \frac 2 r \\
    &= \frac {2 \cosh \theta} r \\
\end{aligned}$$

注意我们同时还得到了 $r = \operatorname{csch} \theta, \frac {dr} {dx} = \cosh \theta$ 的结论。

---

$$\begin{aligned}
    \frac d {dx} \frac {dy} {dx} &= \frac {2r \frac d {dx} (\cosh \theta) - 2 \cosh \theta \frac {dr} {dx}} {r^2} \\
    &= \frac {2r \sinh \theta \frac {d\theta} {dx} - 2 \cosh^2 \theta} {r^2} \\
    &= \frac {- 2 \sinh^2 \theta - 2 \cosh^2 \theta} {r^2} \\
    &= \frac {-2 - 4 \sinh^2 \theta} {r^2} \\
    &= - \frac {2 \cosh 2 \theta} {r^2}
\end{aligned}$$

---

TODO:

$$\begin{aligned}
    \frac d {dx} \frac {d^n y} {dx^n} &= 
\end{aligned}$$