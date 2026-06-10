# 切线

## Problem 1.1 (剑桥面试)

> 已知 $y = kx$ 与 $y = \sin x$ 有 $5$ 个交点。求 $k$。

若 $k > 0$，随手画一下可知 $y = kx$ 必然是一条切线。

$$\begin{cases}
    \sin x = kx \\
    \cos x = k \\
\end{cases}$$

$$x = \tan x$$

解析解求不出，画图。

若 $k < 0$，那么是一个范围，求解过程一样。

## Problem 1.2

> 找一个圆心在 $(0,2)$ 的圆与 $y = x^2$ 相切。

隐函数求导能做但是比较麻烦。考虑圆的切线的特殊性质——切线与半径垂直。

设切点为 $(x, x^2)$。切线斜率为 $2x$，半径斜率为 $\frac {x^2 - 2} x$。

$$\begin{aligned}
    2x \times \frac {x^2 - 2} x &= -1 \\
    x &= \pm \sqrt{\frac 3 2}
\end{aligned}$$

后续算 $r$ 就直接距离公式，很简单。

> 找一个圆与 $y = x^2$ 的底部相切。求出圆心 $(0,a)$（$a > 0$）。

$$\begin{aligned}
    2x \times \frac {x^2 - a} x &= -1 \\
    x &= \pm \sqrt{a - \frac 1 2}
\end{aligned}$$

与底部相切，就是使它未定义或等于 $0$。因此答案为 $a \le \frac 1 2$。

# 画图

## Problem 2.1

> 画图
>
> $$\sqrt{y^2 + 1} = \frac {e^x + e^{-x}} 2$$

💡注意到右侧是 $\cosh$，因此 $y = \pm \sinh x$。

$$y = \pm \frac {e^x - e^{-x}} 2$$

## Problem 2.2

> 画图
>
> $$y = \frac {x^2 + x + 1} {x - 1}$$

$$\frac {x^2 + x + 1} {x - 1} = x+2 + \frac 3 {x-1}$$

我们从对勾函数 $x + \frac 3 x$ 的基础上作图：

$$(y - 3) = (x-1) + \frac 3 {x-1}$$

## Problem 2.3

> 画图（$a > 0$）
>
> $$x (x^2 + y^2) = 2 a y^2$$

$$y^2 = \frac {x^3} {2a - x}$$

求一下定义域：

$$\begin{aligned}
    \frac {x^3} {2a - x} \ge 0 \\
    x^3 (2a - x) \ge 0 \\
    x \in [0, 2a) \\
\end{aligned}$$

注意到 $\frac {x^3} {2a - x}$ 是增函数，所以非常好画。注意 $2a$ 处竖直渐近线。

画完之后 $(x, y) \to (x, \sqrt y)$。

## Problem 2.4

> 画图
>
> $$y = \sin \frac 1 x$$

是奇函数。

先画 $y = \sin x$，然后 $(x, y) \to (\frac 1 x, y)$。可以画出零点来帮忙。

$x \to \pm \infty$ 有 $y = 0$。

> 画图
>
> $$y = \begin{cases}
>     x \sin \frac 1 x, & x \ne 0 \\
>     0, & x = 0 \\
> \end{cases}$$

是偶函数。

$$\lim_{x \to \infty} x \sin \frac 1 x = \lim_{x \to \infty} \frac {\sin \frac 1 x} {\frac 1 x} = 1$$

有渐近线 $y = 1$。

$$\lim_{x \to 0} x \sin \frac 1 x = \lim_{x \to 0} \frac {\sin \frac 1 x} {\frac 1 x} = 0$$

是连续函数。

### 奇函数与偶函数

设 $f$ 是奇函数，$g$ 是偶函数：

$$\begin{cases}
    f(-x) f(-x) = f(x) f(x) & \text{even} \\
    f(-x) g(-x) = - f(x) g(x) & \text{odd} \\
    g(-x) g(-x) = g(x) g(x) & \text{even} \\
\end{cases}$$

$$\begin{cases}
    f(f(-x)) = f(-f(x)) = -f(f(x)) & \text{odd} \\
    f(g(-x)) = f(g(x)) & \text{even} \\
    g(f(-x)) = g(-f(x)) = g(f(x)) & \text{even} \\
    g(g(-x)) = g(g(x)) & \text{even} \\
\end{cases}$$

# 取整函数

## Problem 3.1

> 在 $x \in [0,3]$ 上画图
>
> $$y = \lfloor x^2 \rfloor$$

分段讨论。

> 求
>
> $$\int_0^3 \lfloor x^2 \rfloor dx$$

$$\begin{aligned}
    & \int_0^3 \lfloor x^2 \rfloor dx \\
    =& \sum_{i=1}^8 \int_{\sqrt i}^{\sqrt {i+1}} i dx \\
    & \sum_{i=1}^8 i (\sqrt{i+1} - \sqrt i) \\
    =& 8 \sqrt 9 - \sum_{i=1}^8 \sqrt i \\
\end{aligned}$$

> 求
>
> $$\int_0^{\ln n} \lfloor e^x \rfloor dx$$

$$\begin{aligned}
    & \int_0^{\ln n} \lfloor e^x \rfloor dx \\
    =& \sum_{i=1}^{n-1} \int_{\ln i}^{\ln(i+1)} i dx \\
    & \sum_{i=1}^{n-1} i (\ln(i+1) - \ln i) \\
    =& (n-1) \ln n - \sum_{i=1}^{n-1} \ln i \\
    =& \ln \frac {n^{n-1}} {(n-1)!} =  \ln \frac {n^n} {n!} \\
\end{aligned}$$

# （推广）介值定理 IVT

## Problem 4.1

> 证明 $2x^3 - 5x + 2 = 0$ 在 $x \in [0,1]$ 上有根。

令 $f(x) = 2x^3 - 5x + 2$。$f(0) = 2, f(1) = -1$。IVT 即可。

## Problem 4.2

> 证明一元奇数次多项式必有实根。

WLOG，设最高项系数为正。

$f(\infty) = \infty, f(-\infty) = -\infty$。推广 IVT 即可。

# 求导

乘积求导：

$$\left( \prod u_i \right)' = \left( \prod u_i \right) \left( \sum \frac {u_i'} {u_i} \right)$$

Leibniz rule：

$$(u v)^{(n)} = \sum_{k=0}^n \binom n k u^{(k)} v^{(n-k)}$$

$$\left( \prod_{i=1}^m u_i \right)^{(n)} = \sum_{\sum_{i=1}^m k_i = n} \binom n {k_1, \cdots, k_m} \prod u_i^{(k_i)}$$