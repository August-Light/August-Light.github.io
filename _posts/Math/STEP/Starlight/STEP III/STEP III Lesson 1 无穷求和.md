# Generalized binomial theorem

$$(1 + x)^r = \sum_{i=0}^\infty \binom r i x^i, \quad \lvert x \rvert < 1$$

证明可以直接 Taylor 展开。

## 证明

令该数列为 $a$。取其上确界 $L = \sup a$（说明该上确界存在需要数学分析的知识）。

对于任意 $\varepsilon > 0$，根据上确界的定义，存在 $N$ 使得

$$a_N > L - \varepsilon$$

对于任意 $n \ge N$，有

$$a_n \ge a_N > L - \varepsilon$$

$$\lvert a_n - L \rvert < \varepsilon$$

为极限定义，证毕。

# 题目



## Problem 3 (Easy)

有点普通，纯粹为了考试而出的题目。

> 此问题中 $\lvert x \rvert < 1$。
>
> 可以证明，接下来的论证中你不必考虑敛散性的问题。

> 对于正整数 $n$，化简
>
> $$(1-x) \prod_{k=1}^n (1 + x^{2^k})$$

$$1 - x^{2^{n+1}}$$

> 证明
>
> $$\frac 1 {1-x} = \frac {x^{2^{n+1}}} {1-x} + \prod_{k=1}^n (1 + x^{2^k})$$

$$\begin{aligned}
    (1-x) \prod_{k=1}^n (1 + x^{2^k}) &= 1 - x^{2^{n+1}} \\
    \prod_{k=1}^n (1 + x^{2^k}) &= \frac {1 - x^{2^{n+1}}} {1-x} \\
    \frac 1 {1-x} &= \frac {x^{2^{n+1}}} {1-x} + \prod_{k=1}^n (1 + x^{2^k})
\end{aligned}$$

> 证明
>
> $$\ln(1 - x) = - \sum_{k=0}^\infty \ln(1 + x^{2^k})$$

上一题结论两边同时取 $\lim_{n \to \infty}$ 后同时取 $\ln$ 得证。

> 证明
>
> $$\frac 1 {1-x} = \sum_{k=0}^\infty \frac {2^k x^{2^k - 1}} {1 + x^{2^k}}$$

上一题结论两边同时取 $\frac d {dx}$ 得证。

> 证明
>
> $$\frac {1 + 2x} {1 + x + x^2} = \sum_{k=0}^\infty \frac {2^k x^{2^k-1} - 2^{k+1} x^{2^{k+1}-1}} {1 - x^{2^k} + x^{2^{k+1}}}$$

两边积分：

$$\ln(1 + x + x^2) = - \sum_{k=0}^\infty \ln(1 - x^{2^k} + x^{2^{k+1}})$$

$$\begin{aligned}
    & \ln(1 + x + x^2) \\
    =& \ln(1 - x^3) - \ln(1 - x) \\
    =& - \sum_{k=0}^\infty \left( \ln(1 + x^{3 \times 2^k}) - \ln(1 + x^{2^k}) \right) \\
\end{aligned}$$

得证。

## Problem 4 (Normal)

常幂多项式转下降幂多项式模板题。

> 证明
>
> $$\sum_{n=1}^\infty \frac {n+1} {n!} = 2e - 1$$
>
> $$\sum_{n=1}^\infty \frac {(n+1)^2} {n!} = 5e - 1$$
>
> 并求
>
> $$\sum_{n=1}^\infty \frac {(2n-1)^3} {n!}$$

引理：

$$\sum_{n=0}^\infty \frac {n^{\underline k}} {n!} = e$$

$$\sum_{n=1}^\infty \frac {n^{\underline k}} {n!} = e - [k = 0]$$

---

$$\begin{aligned}
    & \sum_{n=1}^\infty \frac {n+1} {n!} \\
    =& \sum_{n=1}^\infty \frac {n^{\underline 1} + n^{\underline 0}} {n!} \\
    =& e + (e-1) \\
    =& 2 e - 1 \\
\end{aligned}$$

$$\begin{aligned}
    & \sum_{n=1}^\infty \frac {(n+1)^2} {n!} \\
    =& \sum_{n=1}^\infty \frac {n^{\underline 2} + 3 n^{\underline 1} + n^{\underline 0}} {n!} \\
    =& e + 3 e + (e - 1) \\
    =& 5 e - 1 \\
\end{aligned}$$

$$\begin{aligned}
    & \sum_{n=1}^\infty \frac {(2n-1)^3} {n!} \\
    =& \sum_{n=1}^\infty \frac {8 n^{\underline 3} + 12 n^{\underline 2} + 2 n^{\underline 1} - n^{\underline 0}} {n!} \\
    =& 8e + 12e + 2e - (e-1) \\
    =& 21e + 1 \\
\end{aligned}$$

## Problem 6 (Normal)

定求和往往和 Taylor 级数有关。

> 求出下列收敛的和：
>
> $$\sum_{r=1}^\infty \frac r {2^{r-1}}$$
>
> $$\sum_{r=1}^\infty \frac 1 {r \times 2^{r-1}}$$
>
> $$\sum_{k=2}^\infty \frac {(2k-1)!!} {k! \times 3^{k-1}}$$

$$\begin{aligned}
    f(x) &:= \sum_{r=1}^\infty \frac r {2^{r-1}} x^{r-1} \\
    &= \frac d {dx} \sum_{r=1}^\infty \frac {x^r} {2^{r-1}} \\
    &= \frac d {dx} \frac {2x} {2-x} \\
    &= \frac 4 {(2-x)^2} \\
\end{aligned}$$

$$f(1) = 4$$

---

$$\begin{aligned}
    f(x) &:= \sum_{r=1}^\infty \frac 1 {r \times 2^{r-1}} x^r \\
    &= \int_0^x \sum_{r=1}^\infty \frac {t^{r-1}} {2^{r-1}} dt \\
    &= \int_0^x \frac 2 {2 - t} dt \\
    &= -2 \ln (2 - t) \vert_0^x \\
    &= -2 \ln \left( 1 - \frac x 2 \right) \\
\end{aligned}$$

$$f(1) = 2 \ln 2$$

---

第三题 Taylor 依然可以做，但是用广义二项式很简单（其实还是 Taylor 嘛）。

$$\begin{aligned}
    & \sum_{k=2}^\infty \frac {(2k-1)!!} {k!} \frac 1 {3^{k-1}} \\
    =& \sum_{k=2}^\infty \binom {- \frac 1 2} k (-2)^k \frac 1 {3^{k-1}} \\
    =& 3 \left( - 1 - \frac 1 3 + \sum_{k=0}^\infty \binom {- \frac 1 2} k \left( - \frac 2 3 \right)^k \right) \\
    =& 3 \left( - \frac 4 3 + \frac 1 {\sqrt {1 + (- \frac 2 3)}} \right) \\
    =& -4 + 3 \sqrt 3 \\
\end{aligned}$$

关于双阶乘的处理手法可以看 Problem 7。

## Problem 7 (Normal)

双阶乘与中心二项式系数模板题。

> 证明：
>
> $$\binom {2r} r = \frac {(2r-1)!!} {r!} \times 2^r$$

显然的吧。

> 证明：
>
> $$\sum_{r=0}^\infty \binom {2r} r \frac 1 {8^r} = \sqrt 2$$

核心的引理：

$$\boxed{
    \binom {2n} n = \binom {- \frac 1 2} n (-4)^n
}$$

代入：

$$\begin{aligned}
    & \sum_{r=0}^\infty \binom {2r} r \frac 1 {8^r} \\
    =& \sum_{r=0}^\infty \binom {- \frac 1 2} r (-4)^r \frac 1 {8^r} \\
    =& \frac 1 {\sqrt{1 + (- \frac 1 2)}} \\
    =& \sqrt 2
\end{aligned}$$

> 证明：
>
> $$\sum_{r=0}^\infty \binom {2r} r \frac {2r + 1} {5^r} = 5^{\frac 3 2}$$

$$\boxed{
    \binom {- \frac 3 2} r = \frac {(2r + 1)!!} {r!} \left( - \frac 1 2 \right)^r
}$$

$$\begin{aligned}
    & \sum_{r=0}^\infty \binom {2r} r \frac {2r + 1} {5^r} \\
    =& \sum_{r=0}^\infty \frac {(2r + 1)!!} {r!} \left( \frac 2 5 \right)^r \\
    =& \sum_{r=0}^\infty \binom {- \frac 3 2} r \left( - \frac 4 5 \right)^r \\
    =& \left(1 + (- \frac 4 5) \right)^{- \frac 3 2} \\
    =& 5^{\frac 3 2} \\
\end{aligned}$$