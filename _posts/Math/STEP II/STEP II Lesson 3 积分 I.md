# $\int \cos^n x dx$

用 $\cos(kx)$ 表示 $\cos^n x$。

# 苦命鸳鸯 $\tan$ 与 $\sec$

$$\begin{cases}
    \tan^2 x + 1 = \sec^2 x \\
    \tan' x = \sec^2 x \\
    \sec' x = \tan x \sec x \\
\end{cases}$$

> 积分表扩充：
>
> $$\int \sec x dx, \int \csc x dx$$

$$\begin{aligned}
    & \int \sec x dx \\
    =& \int \frac {\sec x (\textcolor{red}{\sec x + \tan x})} {\textcolor{red}{\sec x + \tan x}} dx \\
    =& \int \frac {d(\sec x + \tan x)} {\sec x + \tan x} \\
    =& \ln \lvert \sec x + \tan x \rvert + C \\
\end{aligned}$$

$$\begin{aligned}
    & \int \csc x dx \\
    =& \int \frac {\csc x (\textcolor{red}{\csc x - \cot x})} {\textcolor{red}{\csc x - \cot x}} dx \\
    =& \int \frac {d(\csc x - \cot x)} {\csc x - \cot x} \\
    =& \ln \lvert \csc x - \cot x \rvert + C \\
\end{aligned}$$

这个解法可以背下来。

> STEP 原题：
>
> $$\int \sec^n \tan x dx$$

$$\begin{aligned}
    & \int \sec^n \tan x dx \\
    =& \int \sec^{n-1} d(\sec x) \\
    =& \frac {\sec^n x} n + C \\
\end{aligned}$$

> 令
>
> $$I_n = \int \tan^n x dx$$
>
> 求一个 $I_n$ 关于 $I_{n-2}$ 的递推公式。

$$\begin{aligned}
    I_n &= \int \tan^n x dx \\
    &= \int \tan^{n-2} x (\sec^2 x - 1) dx \\
    &= \int \tan^{n-2} x \sec^2 x dx - \int \tan^{n-2} x dx \\
    &= \frac {\tan^{n-1} x} {n-1} - I_{n-2} \\
\end{aligned}$$

$I_n = \int \sec^n dx$ 也可以通过类似方法解决。

# $\arctan$

$$\int \frac 1 {a + b x^2} dx = \frac 1 {\sqrt{ab}} \arctan\left( \sqrt{\frac b a} x \right) + C$$

> 「一次比二次，分母无实根」的通用解法：
>
> $$\int \frac {3x-2} {x^2 + 2x + 2} dx$$

$$\begin{aligned}
    & \int \frac {3x-2} {x^2 + 2x + 2} dx \\
    =& \int \frac {\frac 3 2 (2x+2) - 5} {x^2 + 2x + 2} dx \\
    =& \frac 3 2 \ln \lvert x^2 + 2x + 2 \rvert - 5 \arctan(x+1) + C \\
\end{aligned}$$

# 三角换元

$$\begin{cases}
    \sqrt{1 - x^2} \to \sin \theta \text{ or } \cos \theta \\
    \sqrt{x^2 + 1} \to \tan \theta \\
    \sqrt{x^2 - 1} \to \sec \theta \\
\end{cases}$$

# Problem 1

> $$\int \frac x {x \cot x - 1} dx$$
>
> 提示：$u = x \cos x - \sin x$。

$u' = \cos x - x \sin x - \cos x = - x \sin x$

$$\begin{aligned}
    & \int \frac x {x \cot x - 1} dx \\
    =& \int \frac {x \sin x} u dx \\
    =& - \int \frac {u'} u dx \\
    =& - \ln |u| + C \\
    =& - \ln \lvert x \cos x - \sin x \rvert + C \\
\end{aligned}$$

> $$\int \frac x {x \tan x + 1} dx$$

$$u = x \sin x + \cos x$$

$$u' = \sin x + x \cos x - \sin x = x \cos x$$

$$\begin{aligned}
    & \int \frac x {x \tan x + 1} dx \\
    =& \int \frac {x \cos x} u dx \\
    =& \int \frac {u'} u dx \\
    =& \ln |u| + C \\
    =& \ln \lvert x \sin x + \cos x \rvert + C \\
\end{aligned}$$

> $$\int \frac {x \sec^2 x \tan x} {x \sec^2 x - \tan x} dx$$

考虑 generalize 一下刚才构造的结构：

$$\boxed{
    u = x \times f - F \implies u' = x \times f' + f - f = x \times f'
}$$

我们一眼就能在分母中看到这个结构：

$$u = x \sec^2 x - \tan x \implies u' = 2 x \sec^2 x \tan x$$

$$\begin{aligned}
    & \int \frac {x \sec^2 x \tan x} {x \sec^2 x - \tan x} dx \\
    =& \frac 1 2 \int \frac {u'} u dx \\
    =& \frac 1 2 \ln |u| + C \\
    =& \frac 1 2 \ln \lvert x \sec^2 x - \tan x \rvert + C \\
\end{aligned}$$

# Problem 2

> $$\int \frac 1 {\sqrt x + \sqrt[3] x} dx$$

$$\begin{aligned}
    & \int \frac 1 {x^{\frac 1 2} + x^{\frac 1 3}} dx \\
    =& \int \frac {6 t^5} {t^3 + t^2} dt & t = x^{\frac 1 6} \\
    =& 6 \int \frac {t^3} {t^2 + 1} dt \\
    =& \cdots \\
\end{aligned}$$

# 一些值得注意的变形

$$\begin{aligned}
    & \cos^4 x - \sin^4 x \\
    =& (\cos^2 x + \sin^2 x) (\cos^2  x - \sin^2 x) \\
    =& \cos 2x \\
\end{aligned}$$

$$\begin{aligned}
    & \cos^4 x + \sin^4 x \\
    =& (\cos^2 x + \sin^2 x)^2 - 2 \sin^2 x \cos^2 x \\
    =& 1 - \frac {\sin^2 2x} 2 \\
    =& \frac {3 + \cos 4x} 4 \\
\end{aligned}$$

$$\begin{aligned}
    & 1 \pm \sin 2x \\
    =& \sin^2 x + \cos^2 x \pm 2 \sin x \cos x \\
    =& (\sin x + \cos x)^2 \\
\end{aligned}$$

$$1 \pm \sin x = \left( \sin \frac x 2 \pm \cos \frac x 2 \right)^2$$