# 三角函数不定积分处理手法

$$\begin{aligned}
    & \int \sin^{2n+1} x \times f(\cos x) dx \\
    =& - \int \sin^{2n} x \times f(\cos x) d(\cos x) \\
    =& - \int (1 - \cos^2 x)^n \times f(\cos x) d(\cos x) \\
\end{aligned}$$

$$\begin{aligned}
    & \int \cos^{2n+1} x \times f(\sin x) dx \\
    =& \int \cos^{2n} x \times f(\sin x) d(\sin x) \\
    =& \int (1 - \sin^2 x)^n \times f(\sin x) d(\sin x) \\
\end{aligned}$$

# 定积分变形

对于定积分变形问题：
- **分部积分不变上下限**。
- **换元积分变上下限**。

## King's Rule (区间再现)

不在 syllabus 之内，但是非常重要。

对于任意 $[a,b]$ 上的可积函数 $f$，有

- 反转区间：

$$\boxed{
    \int_a^b f(x) dx = \int_a^b f(a + b - x) dx
}$$

- 首尾相加：

$$\boxed{
    \int_a^b f(x) dx = \frac 1 2 \int_a^b (f(x) + f(a + b - x)) dx
}$$

简单推论——$[0, \frac \pi 2]$ 上 $\sin$ 与 $\cos$ 可以互换：

$$\boxed{
    \int_0^{\frac \pi 2} f(\sin x, \cos x) dx = \int_0^{\frac \pi 2} f(\cos x, \sin x) dx
}$$

# Wallis Integrals (点火公式)

$$W_n := \int_0^{\frac \pi 2} \sin^n x dx$$

我们要求出 $W_n$ 的通项公式，以及其相关性质。

## 先别急着算

> $\int_0^{\frac \pi 2} \sin^n x dx$ 要是会算了，$\int_0^{\frac \pi 2} \cos^n x dx$ 怎么算？

King's Rule 秒了。

## 递推

$$\begin{aligned}
    W_n &= \int_0^{\frac \pi 2} \sin^n x dx \\
    &= \int_0^{\frac \pi 2} \sin^{n-1} x \sin x dx \\
    &= (- \sin^{n-1} x \cos x) \vert_0^{\frac \pi 2} + (n-1) \int_0^{\frac \pi 2} \sin^{n-2} x \cos^2 x dx \\
    &= (n-1) \int_0^{\frac \pi 2} \sin^{n-2} x (1 - \sin^2 x) dx \\
    &= (n-1) (W_{n-2} - W_n) \\
\end{aligned}$$

$$\boxed{
    W_n = \frac {n-1} n W_{n-2}
}$$

## 通项

$$W_{2n} = \frac {(2n-1)!!} {(2n)!!} \times \frac \pi 2$$

$$W_{2n+1} = \frac {(2n)!!} {(2n+1)!!}$$

## 极限

ChatGPT 给出了一个简单的做法：把区间最右边截出长为 $\delta$ 的一段，左边段上界 $\sin^n (\frac \pi 2 - \delta)$ 为指数衰减，右边段上界 $\delta$ 可以任意小，因此总体趋于 $0$：

$$\lim_{n \to \infty} W_n = 0$$

进一步地，利用 Laplace 方法可知其渐进估计

$$W_n \sim \sqrt{ \frac \pi {2 n}}$$

## Wallis 公式

注意到 $0 < \sin x < 1$，因此 $W$ 是单调递减数列。

观察奇数项子列：

$$W_{2n+1} < W_{2n-1}$$

$$1 < \frac {W_{2n-1}} {W_{2n+1}} = \frac {2n-1} {2n}$$

再加入偶数项：

$$1 < \frac {W_{2n}} {W_{2n+1}} < \frac {W_{2n-1}} {W_{2n+1}} = \frac {2n-1} {2n}$$

Squeeze theorem：

$$\lim_{n \to \infty} \frac {W_{2n}} {W_{2n+1}} = 1$$

$$\lim_{n \to \infty} \frac {(2n+1)!!} {(2n)!!} \frac {(2n-1)!!} {(2n)!!} \times \frac \pi 2 = 1$$

这导出 **Wallis Product**：

$$\boxed{
    \prod_{n=1}^\infty \left( \frac {2n} {2n-1} \times \frac {2n} {2n+1} \right) = \frac \pi 2
}$$

直观地写开：

$$\frac 2 1 \times \frac 2 3 \times \frac 4 3 \times \frac 4 5 \times \frac 6 5 \times \frac 6 7 \times \cdots = \frac \pi 2$$

# 💡初识 Beta 函数

这一块原本属于 Problem 4，但是我认为它值得一个专题。

我们采取和主流略微不同的定义：

$$\beta(x, y) := \int_0^1 t^x (1-t)^y dt$$

对称性：

$$\beta(x, y) = \beta(y, x)$$

递推 1：

$$\begin{aligned}
    \beta(x, y) &= \int_0^1 t^x (1-t)^y dt \\
    &= \left. \left( t^x \times - \frac {(1-t)^{y+1}} {y+1} \right) \right\vert_0^1 - \int_0^1 x t^{x-1} \times - \frac {(1-t)^{y+1}} {y+1} dt \\
    &= \frac x {y+1} \int_0^1 t^{x-1} (1-t)^{y+1} dt \\
    &= \frac x {y+1} \beta(x-1, y+1) \\
\end{aligned}$$

递推 2：

$$\begin{aligned}
    \beta(x, y) &= \frac x {y+1} \int_0^1 t^{x-1} (1-t)^{y+1} dt \\
    &= \frac x {y+1} \int_0^1 \left( t^{x-1} (1-t)^y - t^x (1-t)^y \right) dt \\
    &= \frac x {y+1} (\beta(x-1, y) - \beta(x, y)) \\
\end{aligned}$$

$$\begin{aligned}
    (x + y + 1) \beta(x, y) &= x \beta(x-1, y) \\
    \beta(x, y) &= \frac x {x + y + 1} \beta(x-1, y) \\
\end{aligned}$$

# 💡反常积分的 Cauchy 主值

设函数 $f$ 在区间 $[a,b]$ 上在 $x=c$ 处有奇点，定义其在 $[a,b]$ 上的积分的 Cauchy 主值为：

$$\mathrm{PV} \int_a^b f(x)dx := \lim_{\varepsilon\to 0^+} \left( \int_a^{c-\varepsilon} f(x)dx + \int_{c+\varepsilon}^b f(x)dx \right)$$

# Problem 1 (STEP)

$\text{Ei}$ 模板题。

> 令
>
> $$E = \int_0^1 \frac {e^x} {1 + x} dx$$

> 求积分
>
> $$\int_0^1 \frac {x e^x} {1 + x} dx$$
>
> 答案中包含 $E$。

$$\begin{aligned}
    & \int_0^1 \frac {x e^x} {1 + x} dx \\
    =& \int_0^1 \left( 1 - \frac 1 {1 + x} \right) e^x dx \\
    =& (e - 1) - \int_0^1 \frac {e^x} {1 + x} dx \\
    =& e - 1 - E \\
\end{aligned}$$

> 求积分
>
> $$\int_0^1 \frac {x^2 e^x} {1 + x} dx$$
>
> 答案中包含 $E$。

$$\begin{aligned}
    & \int_0^1 \frac {x^2 e^x} {1 + x} dx \\
    =& \int_0^1 \left( x - 1 + \frac 1 {1 + x} \right) e^x dx \\
    =& 1 - (e - 1) + \int_0^1 \frac {e^x} {1 + x} dx \\
    =& 2 - e + E \\
\end{aligned}$$

> 求积分
>
> $$\int_0^1 \frac {e^{\frac {1-x} {1+x}}} {1 + x} dx$$
>
> 答案中包含 $E$。

$$\begin{aligned}
    & \int_0^1 \frac {e^{\frac {1-x} {1+x}}} {1 + x} dx \\
    =& \frac 1 e \int_0^1 \frac {e^{\frac 2 {1+x}}} {1 + x} dx \\
\end{aligned}$$

换元 $t = \frac 2 {1 + x}$。有 $x = \frac 2 t - 1 \implies \frac {dx} {dt} = - \frac 2 {t^2}$。

$$\begin{aligned}
    & \int_0^1 \frac {e^{\frac 2 {1+x}}} {1 + x} dx \\
    =& \int_2^1 \frac {t e^t} 2 \left( - \frac 2 {t^2} \right) dt \\
    =& \int_1^2 \frac {e^t} t dt \\
    =& e \int_0^1 \frac {e^t} {t + 1} dt \\
    =& e E
\end{aligned}$$

答案为 $E$。

> 求积分
>
> $$\int_1^{\sqrt 2} \frac {e^{x^2}} x dx$$
>
> 答案中包含 $E$。

$$\begin{aligned}
    & \int_1^{\sqrt 2} \frac {e^{x^2}} x dx \\
    =& \int_1^2 \frac {e^t} {\sqrt t} \frac 1 {2 \sqrt t} dt \\
    =& \frac 1 2 \int_1^2 \frac {e^t} t dt \\
    =& \frac {e E} 2 \\
\end{aligned}$$

# Problem 2 (STEP)

> $$\int_0^1 \frac 1 {x + \sqrt {1 - x^2}} dx$$

$$\begin{aligned}
    & \int_0^1 \frac 1 {x + \sqrt {1 - x^2}} dx \\
    =& \int_0^{\frac \pi 2} \frac {\cos \theta} {\sin \theta + \cos \theta} d \theta \\
    =& \frac 1 2 \int_0^{\frac \pi 2} \frac {\sin \theta + \cos \theta} {\sin \theta + \cos \theta} d \theta & \text{King's Rule} \\
    =& \frac \pi 4 \\
\end{aligned}$$

> 刚才我们用 King's Rule 逃了课，那么这个不定积分具体怎么求：
>
> $$I = \int \frac {\sin \theta} {\sin \theta + \cos \theta} d \theta$$
>
> $$J = \int \frac {\cos \theta} {\sin \theta + \cos \theta} d \theta$$

$$I + J = \theta + C$$

$$\begin{aligned}
    & J - I \\
    =& \int \frac {\cos \theta - \sin \theta} {\sin \theta + \cos \theta} d \theta \\
    =& \ln \lvert \sin \theta + \cos \theta \rvert + C \\
\end{aligned}$$

$$\begin{cases}
    I = \frac {\theta - \ln \lvert \sin \theta + \cos \theta \rvert} 2 + C \\
    J = \frac {\theta + \ln \lvert \sin \theta + \cos \theta \rvert} 2 + C \\
\end{cases}$$

# Problem 3 (剑桥面试)

> $$I_n = \int_0^1 \frac {x^n} {\sqrt{1 + x^3}} dx$$
>
> 求一个 $I_n$ 关于 $I_{n-3}$ 的递推式。

$$\begin{aligned}
    I_n &= \int_0^1 \frac {x^n} {\sqrt{1 + x^3}} dx \\
    &= \int_0^1 \frac {\frac 1 3 x^{n-2} \times 3x^2} {\sqrt{1 + x^3}} dx \\
    &= \left. \left( \frac 1 3 x^{n-2} \times 2 \sqrt{1 + x^3} \right) \right\vert_0^1 - \frac 2 3 (n-2) \int_0^1 x^{n-3} \sqrt{1 + x^3} dx \\
    &= \frac {2 \sqrt 2} 3 - \frac 2 3 (n-2) \int_0^1 \frac {x^{n-3} (1 + x^3)} {\sqrt{1 + x^3}} dx \\
    &= \frac {2 \sqrt 2} 3 - \frac 2 3 (n-2) (I_{n-3} + I_n) \\
\end{aligned}$$

$$I_n = \frac {2 \sqrt 2 - 2 (n-2) I_{n-3}} {2n-1}$$

# Problem 4

> $$I_n = \int_0^1 x^n (1-x)^n dx$$
>
> 求一个 $I_n$ 关于 $I_{n-1}$ 的递推式。

$$\begin{aligned}
    I_n &= \beta(n, n) \\
    &= \frac n {2n+1} \beta(n-1, n) \\
    &= \frac n {2n+1} \frac n {2n} \beta(n-1, n-1) \\
    &= \frac n {4n+2} I_{n-1} \\
\end{aligned}$$

