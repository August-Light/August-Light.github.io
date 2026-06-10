# 辅助角公式

在 $a > 0$ 时：

$$\boxed{
    a \sin x + b \cos x = \sqrt{a^2 + b^2} \sin\left( x + \arctan \frac b a \right)
}$$

在 $b > 0$ 时：

$$\boxed{
    b \cos x + a \sin x = \sqrt{a^2 + b^2} \cos\left( x - \arctan \frac a b \right)
}$$

💡若将 $\arctan$ 修改为 $\operatorname{atan2}$，则无需判断 $a,b$ 的正负号。

# $15°$ 与 $75°$

$$\begin{cases}
    \tan 15° = 2 - \sqrt 3 \\
    \tan 75° = 2 + \sqrt 3 \\
\end{cases}$$

# 三角函数解三次方程

> 证明 $\cos \alpha$ 是以下方程的解：
>
> $$4x^3 - 3x - \cos 3 \alpha = 0$$
>
> 并找到剩余的两解。

熟知结论

$$\cos 3 \alpha = 4 \cos^3 \alpha - 3 \cos \alpha$$

显然与 $\alpha$ 对应的一倍角恰好有 $3$ 个：

$$x = \cos \left( \alpha + \frac {2 \pi} 3 k \right), \quad k \in \{0, 1, 2\}$$

> 解方程 $y^3 - 3y - \sqrt 2 = 0$。

对于 $y^3 - a y$ 的结构，我们考虑用一个 $y = kx$ 的换元配出 $4:3$ 的系数：

$$\begin{aligned}
    y^3 - ay &= k^3 x^3 - a k x \\
    \frac {k^3} {ak} &= \frac 4 3 \\
    k^2 &= \frac 4 3 a \\
    k &= \pm \sqrt{\frac 4 3 a} \\
\end{aligned}$$

换元 $y = \sqrt{\frac 4 3 a} x$，其中 $a = 3$：

$$\begin{aligned}
    8 x^3 - 6 x - \sqrt 2 = 0 \\
    4 x^3 - 3 x - \frac {\sqrt 2} 2 &= 0 \\
\end{aligned}$$

$$\alpha = \frac 1 3 \arccos \frac {\sqrt 2} 2 = \frac 1 {12} \pi$$

解得

$$\begin{aligned}
    x_1 &= \cos \left( \alpha \right) &&= \frac {\sqrt 2 + \sqrt 6} 4 \\
    x_2 &= \cos \left( \alpha + \frac 2 3 \pi \right) &&= - \frac {\sqrt 2} 2 \\
    x_3 &= \cos \left( \alpha + \frac 4 3 \pi \right) &&= \frac {\sqrt 2 - \sqrt 6} 4 \\
\end{aligned}$$

换元回来 $y = 2x$：

$$\begin{aligned}
    y_1 &= \frac {\sqrt 2 + \sqrt 6} 2 \\
    y_2 &= - \sqrt 2 \\
    y_3 &= \frac {\sqrt 2 - \sqrt 6} 2 \\
\end{aligned}$$

💡这种解法依赖于常数项 $- \frac {\sqrt 2} 2$ 的绝对值 $\le 1$，否则 $\arccos$ 会坏掉。对于这类情况，可以使用 $\cosh$ 的方法。

# TODO: