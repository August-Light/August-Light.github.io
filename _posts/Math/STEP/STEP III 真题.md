# 2019

## 3：精巧的线性代数题

> 令
>
> $$\mathbf A = \begin{bmatrix}
>     a & b \\
>     c & d \\
> \end{bmatrix}$$

> 直线 $L_1$（不一定经过原点）上的向量 $\vec x$ 都满足 $\mathbf A \vec x = \vec x$。证明 $(a-1)(d-1) = bc$。

$$(\mathbf A - \mathbf I) \vec x = \vec 0$$

若 $\det(\mathbf A - \mathbf I) \ne 0$，则可解出唯一解 $\vec x = 0$，矛盾。因此 $\det(\mathbf A - \mathbf I) = 0$ 得证。

> 若 $L_1$ 不经过原点，求出 $\mathbf A$。

猜测 $\mathbf A = \mathbf I$，试图证明对于任意 $\vec z$ 有 $\mathbf A \vec z = \vec z$。

在直线上任取两点 $\vec x, \vec y$ 有

$$\begin{cases}
    \mathbf A \vec x = \vec x \\
    \mathbf A \vec y = \vec y \\
\end{cases}$$

由于 $L_1$ 不过原点有 $\vec x, \vec y$ 线性无关，把 $\vec z$ 分解成 $a \vec x + b \vec y$ 有

$$\begin{aligned}
    \mathbf A \vec z &= a \mathbf A \vec x + b \mathbf A \vec y \\
    &= a \vec x + b \vec y \\
    &= \vec z
\end{aligned}$$

得证。

> 不过原点的直线 $L_2$ 上的任意一点都满足经过变换 $\mathbf A$ 后仍然停留在 $L_2$ 上。仍然证明 $(a-1)(d-1) = bc$。

$\mathbf A \vec x - \vec x$ 与 $\mathbf A \vec y - \vec y$ 线性相关，即存在系数 $k_1, k_2$ 使得

$$\begin{aligned}
    k_1 (\mathbf A \vec x - \vec x) + k_2 (\mathbf A \vec y - \vec y) &= \vec 0 \\
    (\mathbf A - \mathbf I) (k_1 \vec x + k_2 \vec y) &= \vec 0 \\
\end{aligned}$$

由于 $k_1 \vec x + k_2 \vec y \ne \vec 0$，$\det(\mathbf A - \mathbf I) = 0$。

## 7：无穷小看低次项，无穷大看高次项

> 求 $x^2 (x^2-4) = y^2 (y^2-5)$ 在原点附近的行为。

$$\begin{aligned}
    -4 x^2 + x^4 = -5 y^2 + y^4 \\
    -4 x^2 \approx -5 y^2 \\
    y \approx \pm \frac 2 {\sqrt 5} x \\
\end{aligned}$$

> 求 $x^2 (x^2-4) = y^2 (y^2-5)$ 在离原点很远处的行为。

$$\begin{aligned}
    x^4 -4 x^2 = y^4 -5 y^2 \\
    x^4 \approx y^4 \\
    y \approx \pm x \\
\end{aligned}$$

## 10：无穷区间上的最大值

> $e$ 是 coefficient of restitution。已知 $\alpha$ 是锐角，求最大值：
>
> $$\frac {(e+1) \tan \alpha} {2 \tan^2 \alpha + 1 - e}$$
>
> 用 $e$ 表示。

求一阶导后不难发现 $\tan \alpha = \sqrt{\frac {1-e} 2}$ 是驻点，重点在于如何说明这是最大值。注意到 $\tan \alpha \to 0$ 和 $\to \infty$ 时原式都 $\to 0$，且原式恒正，因此唯一的极值点只能是全局最大值。

另一种方法，使用均值不等式规避二阶导：

$$\begin{aligned}
    & \frac {(e+1) \tan \alpha} {2 \tan^2 \alpha + 1 - e} \\
    &= (e+1) \frac 1 {2 \tan \alpha + \frac {1 - e} {\tan \alpha}} \\
    & \le (e+1) \frac 1 {2 \sqrt {2 (1-e)}} & \text{when } \tan \alpha = \sqrt{\frac {1-e} 2}
\end{aligned}$$

## 11：Poisson 分布基础练习题

Poisson 分布相关的说理可以不按定义说，直接式子算出来就行了。

> 一个店铺一天中来的顾客人数服从期望为 $\lambda$ 的 Poisson 分布。每个客人都有 $p$ 的概率从店铺获得沙子。
>
> 证明一天中获得沙子的人数服从期望为 $p \lambda$ 的 Poisson 分布。

$$\begin{aligned}
    & \sum_{i=r}^\infty \frac {\lambda^i e^{-\lambda}} {i!} \times \binom i r p^r (1-p)^{i-r} \\
    =& \frac {e^{-\lambda} p^r} {r!} \sum_{i=r}^\infty \frac {\lambda^i} {(i-r)!} (1-p)^{i-r} \\
    =& \frac {e^{-\lambda} (p\lambda)^r} {r!} e^{\lambda (1-p)} \\
    =& \frac {(p \lambda)^r e^{- p \lambda}} {r!} \\
\end{aligned}$$

> 每个获得沙子的顾客获得当前沙子的 $k$ 的比例（$0 \le k < 1$）。
>
> 证明被拿走的沙子总比例的期望为 $1 - e^{-kp\lambda}$。

$$\begin{aligned}
    & \sum_{i=1}^\infty \frac {(p \lambda)^i e^{- p \lambda}} {i!} \times \left( 1 - (1 - k)^i \right) \\
    =& e^{-p\lambda} \left( \left( e^{p \lambda} - 1 \right) - \left( e^{(1-k) p \lambda} - 1 \right) \right) \\
    =& 1 - e^{-kp\lambda}
\end{aligned}$$

> 在巨量的沙子中有一个沙子是金的。当一天过去之后，店主的助手也获得当前沙子的 $k$ 的比例，求出店主助手获得金沙子的概率。

$$\begin{aligned}
    & \sum_{r=0}^\infty \frac {(p\lambda)^r e^{-p\lambda}} {r!} \times k (1-k)^r \\
    =& k e^{-p\lambda} e^{p \lambda (1-k)} \\
    =& k e^{-kp \lambda} \\
\end{aligned}$$

# 2020

## 5：部分分式分解模板

> $$\frac 1 {x^n (x-k)} = \frac A {x-k} + \frac {f(x)} {x^n}$$
>
> $A$ 是一个常数，$f(x)$ 是一个多项式。求出 $A$。

去分母：

$$1 = A x^n + f(x) (x - k)$$

代入 $x=k$ 得

$$1 = A k^n \implies A = \frac 1 {k^n}$$

## 6：先反解再 Taylor 展开；极坐标转直角坐标 Taylor 展开

> $\theta \in [- \frac \pi 4, \frac \pi 4]$
>
> $$r^2 - 2r \cos \theta + \sin^2 \theta = 0$$
>
> 证明：当 $r$ 很小时，$r \approx \frac 1 2 \theta^2$。

先说明自变量是无穷小量，然后再 Taylor 展开。

解二次方程得

$$r = \cos \theta \pm \sqrt{\cos 2 \theta}$$

$r = 0$ 的唯一可能是 $\theta = 0$ 且原式取减号。因此 $r$ 很小时 $\theta$ 也很小。

$$\begin{aligned}
    r &= \cos \theta - \sqrt{\cos 2 \theta} \\
    &= 1 - \frac 1 2 \theta^2 + o(\theta^2) - \sqrt{1 - \frac 1 2 (2 \theta)^2 + o(\theta^2)} \\
    &= 1 - \frac 1 2 \theta^2 - \left( 1 + \frac 1 2 \times (- 2 \theta^2) \right) + o(\theta^2) \\
    &= \frac 1 2 \theta^2 + o(\theta^2)
\end{aligned}$$

> 绘制该极坐标方程图像，尤其注意 $r = 0$ 附近的表现。

转到直角坐标系下看得更清晰。

考虑作一个近似：

$$\begin{cases}
    x = r \cos \theta \approx \frac 1 2 \theta^2 \\
    y = r \sin \theta \approx \frac 1 2 \theta^3 \\
\end{cases}$$

消去 $\theta$ 得：

$$y^2 \approx 2 x^3$$

$$x = 2^{\frac 1 3} y^{\frac 2 3}$$

这个图象在原点处是一个尖点。

## 10

> $$N = m \left( \frac {a \Omega^2} k + \Omega^2 (a + x - h) + \omega^2 (b - x) \right)$$
>
> 对于任意 $x \in [0, 2b]$ 都有 $N \ge 0$。已知角速度 $\omega < \Omega$，证明：
>
> $$h \le a \left( 1 + \frac 1 k \right) + \frac {\omega^2} {\Omega^2} b$$

注意到 $N$ 是关于 $x$ 的一次函数：

$$\frac {dN} {dx} = m (\Omega^2 - \omega^2) > 0$$

因此 $x = 0$ 时 $N$ 最小，$x = 2b$ 时 $N$ 最大。

由于要求的是 $h$ 的上界，而 $h$ 的系数 $- m \Omega^2$ 是负的，因此观察 $N$ 最小的情况即可，即代入 $x = 0$。化简后得证。

# 2021

未完工

## 2：普通放缩

> 已知 $a,b,c > 0$，证明
> 
> $$\frac a {b+c} + \frac b {a+c} + \frac c {a+b} > 1$$

通分可以做，但是计算太烦。

$$\begin{aligned}
    & \frac a {b+c} + \frac b {a+c} + \frac c {a+b} \\
    >& \frac a {a+b+c} + \frac b {a+b+c} + \frac c {a+b+c} \\
    =& 1 \\
\end{aligned}$$

## 3：鬼题？！

第一题非常简单，但是第二题怎么做？？？官方解法似乎是错的。TODO:

> 对自然数 $n$ 和 $\beta \in (0, \frac \pi 2)$ 定义
>
> $$I_n = \int_0^\beta (\sec x + \tan x)^n dx$$
>
> 对 $n \ge 1$，证明
>
> $$\frac {I_{n+1} + I_{n-1}} 2 = \frac 1 n ((\sec \beta + \tan \beta)^n - 1)$$
>
> 证明
>
> $$I_n < \frac 1 n ((\sec \beta + \tan \beta)^n - 1)$$

>  对自然数 $n$ 和 $\beta \in (0, \frac \pi 2)$ 定义
>
> $$J_n = \int_0^\beta (\cos \beta \sec x + \tan x)^n dx$$
>
> 对 $n \ge 1$，证明
>
> $$J_n < \frac 1 n ((1 + \tan \beta)^n - \cos^n \beta)$$

## 5：极坐标曲线相切

> 求常数 $a$ 使得极坐标中的曲线 $r = a + 2 \cos \theta$ 与 $r = 2 + \cos 2 \theta$ 相切。

两条曲线相切当且仅当它们交点处的 $\frac {dr} {d \theta}$ 相等。列方程求解即可。

# 2022

## 4：复数？！

> 对于实数 $x \ne 0$ 有
> 
> $$\frac {\sinh x} x = \prod_{r=1}^\infty \cosh \frac x {2^r}$$
>
> 证明
>
> $$\frac 2 \pi = \frac {\sqrt 2} 2 \times \frac {\sqrt {2 + \sqrt 2}} 2 \times \frac {\sqrt {2 + \sqrt {2 + \sqrt 2}}} 2 \times \cdots$$

代入 $x = i \frac \pi 2$

TODO:

避免复数开根号多值性，转回三角函数 $\cosh(ix) = \cos x$

# 2023

## 11：带依赖求和符号交换的解释

> $$\mathbb E(D) = \sum_{d=1}^\infty d \sum_{k=d}^\infty \frac 1 k \frac {n^k e^{-n}} {k!}$$
>
> 证明
>
> $$\mathbb E(D) = \sum_{k=1}^\infty \frac 1 k \frac {n^k e^{-n}} {k!} \sum_{d=1}^k d$$

TODO:

## 12：组合意义的解释

- **对于古典概型的概率，分子和分母分开解释**；
- **计数问题，把握加法原理和乘法原理**。

> 从 $n$ 双袜子（共 $2n$ 个袜子，每双袜子均不同）中等概率随机抽取 $2k$ 个袜子，其中 $2k \le n$。
>
> 求出抽出的袜子中没有完整一对的概率。

- E1: There are $\binom {2n} {2k}$ ways of choosing $2k$ socks from $2n$.
- E1: If there is no pair of socks, then the $2k$ socks must be of different colours; the collours can be chosen $\binom n {2k}$ ways and for each colour there are $2$ ways of choosing a sock of that colour.
- B1: Hence the probability of no pairs is $\frac {\binom n {2k} 2^{2k}} {\binom {2n} {2k}}$.

> 令 $X_{n,k}$ 为取出的完整袜子对数。证明
>
> $$P(X_{n,k} = r) = \frac {\binom n r \binom {n-r} {2(k-r)} 2^{2(k-r)}} {\binom {2n} {2k}}$$

- E1: For $X_{n,k} = r$, there must be $2r$ socks that are pairs and $2 (k - r)$ that are of different colours.
- E1: The colours of the pairs can be chosen $\binom n r$ ways and the colours of the remaining $2 (k - r)$ individual socks can be chosen from the remaining $n - r$ colours $\binom {n - r} {2 (k - r)}$ ways.
- E1: For each colour chosen for an individual sock there are $2$ choices of which sock of the pair is chosen.
- A1: 

$$P(X_{n,k} = r) = \frac {\binom n r \binom {n-r} {2(k-r)} 2^{2(k-r)}} {\binom {2n} {2k}}$$

# 2024

TODO:

# 2025

未完工

## 3：增减性不只有导数

**本题的函数没说可导！一切使用导数的做法都是错的。**

> 对于 $0 < a < b$ 和恒正的函数 $f$，
> 
> $$m = \frac {f(a) b + f(b) a} {f(a) + f(b)}$$
>
> 当 $f$ 取函数 $g_1$ 时 $m$ 的值为 $M_1$，取函数 $g_2$ 时 $m$ 的值为 $M_2$。
>
> 证明：若 $\frac {g_1(x)} {g_2(x)}$ 是严格减函数，则 $M_1 > M_2$。

ChatGPT 给出的思路：

$$\begin{aligned}
    \frac {g_1(a)} {g_2(a)} &> \frac {g_1(b)} {g_2(b)} \\
    \iff \frac {g_1(a)} {g_1(b)} &> \frac {g_2(a)} {g_2(b)} \\
\end{aligned}$$

考虑直接在 $m$ 中凑出 $r = \frac {f(a)} {f(b)}$：

$$\begin{aligned}
    m &= \frac {f(a) b + f(b) a} {f(a) + f(b)} \\
    &= \frac {rb + a} {r + 1} \\
    &= b + \frac {a - b} {r + 1} \\
    &= b - \frac {b - a} {r + 1} \\
\end{aligned}$$

$r$ 越大 $m$ 越大，得证。

## 7：无穷远 Taylor 展开

套路：倒代换。

> 对于绝对值很大的 $x$，证明：
>
> $$\sqrt{x^2 + 1} \approx \lvert x \rvert + \frac 1 {2 \lvert x \rvert}$$

$$\begin{aligned}
    & \sqrt{x^2 + 1} \\
    \xlongequal{t = \lvert x \rvert^{-1}} & \frac {\sqrt{1 + t^2}} t \\
    =& \frac 1 t \left( 1 + \frac 1 2 t^2 + O(t^4) \right) \\
    =& \frac 1 t + \frac 1 2 t + O(t^3) \\
    =& \lvert x \rvert + \frac 1 {2 \lvert x \rvert} + O(\lvert x \rvert^{-3})
\end{aligned}$$

