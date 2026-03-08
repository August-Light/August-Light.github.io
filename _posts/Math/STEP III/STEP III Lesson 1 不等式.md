# Monotone convergence theorem

**单调递增**且**有上界**的数列**存在极限**，且极限为其上确界。

## Problem 2 (Easy)

经典的精巧好题。

> 证明：对任意正整数 $n$ 有
>
> $$\left(1 + \frac 1 n \right)^n < e$$
>
> 提示：$e = \sum_{i=0}^\infty \frac 1 {i!}$。

$$\begin{aligned}
    & \left(1 + \frac 1 n \right)^n \\
    =& \sum_{i=0}^n \binom n i \frac 1 {n^i} \\
    =& \sum_{i=0}^n \frac {n^{\underline{i}}} {n^i} \frac 1 {i!} \\
    < & \sum_{i=0}^n \frac 1 {i!} \\
    < & e \\
\end{aligned}$$

> 定义函数
>
> $$P(n) = \prod_{k=1}^n \frac {2^k + 1} {2^k}$$
>
> 证明：对任意正整数 $n$ 有
>
> $$P(n) < e$$
>
> 提示：AM-GM 不等式。

$$\begin{aligned}
    & \prod_{k=1}^n \frac {2^k + 1} {2^k} \\
    \le & \left( \frac 1 n \sum_{k=1}^n \frac {2^k + 1} {2^k} \right)^n \\
    =& \left( 1 + \frac 1 n (1 - \frac 1 {2^n}) \right)^n \\
    <& \left( 1 + \frac 1 n \right)^n \\
    <& e
\end{aligned}$$

> 说明 $\lim_{n \to \infty} P(n)$ 存在，并证明
>
> $$2 < \lim_{n \to \infty} P(n) \le e$$

$P(n)$ 单调递增且 $< e$，根据 Monotone convergence theorem，存在极限 $\lim_{n \to \infty} P(n)$，且 $\lim P(n) = \sup P(n) \le e$。

而 $P(1) = 2$，故 $\sup P(n) > 2$。证毕。

## Problem 5 (Easy)

虽然简单，但是这种**分组放缩构造几何级数**的思想值得学习。

> $a$ 是一个严格单调递减数列。
>
> 证明：对任意自然数 $n$ 与大于等于 $2$ 的自然数 $k$ 有
>
> $$k^n (k-1) a_{k^{n+1}} < \sum_{r=k^n}^{k^{n+1} - 1} a_r < k^n (k-1) a_{k^n}$$

$r$ 遍历了 $k^n (k-1)$ 个元素，首尾夹一下范围是显然的。

> 证明：
>
> $$\frac {N+1} 2 \le \sum_{r=1}^{2^{N+1} - 1} \frac 1 r \le N+1$$
>
> 并证明 $\sum_{r=1}^\infty \frac 1 r$ 发散。

$$\begin{aligned}
    & \sum_{r=1}^{2^{N+1} - 1} a_r \\
    =& \sum_{n=0}^N \sum_{r=2^n}^{2^{n+1} - 1} a_r \\
\end{aligned}$$

$$\begin{aligned}
    \sum_{n=0}^N 2^n a_{2^{n+1}} & < \sum_{n=0}^N \sum_{r=2^n}^{2^{n+1} - 1} a_r & < & \sum_{n=0}^N 2^n a_{2^n} \\
    \frac {N+1} 2 & < \sum_{n=0}^N \sum_{r=2^n}^{2^{n+1} - 1} \frac 1 r & < & \frac {N+1} 2 \\
\end{aligned}$$

证毕。

> 证明：
>
> $$\sum_{r=1}^\infty \frac 1 {r^3} \le \frac 4 3$$

$$\begin{aligned}
    & \sum_{r=1}^\infty \frac 1 {r^3} \\
    =& \sum_{n=0}^\infty \sum_{r = 2^n}^{2^{n+1} - 1} \frac 1 {r^3} \\
    < & \sum_{n=0}^\infty 2^n \frac 1 {(2^n)^3} \\
    =& \frac 4 3 \\
\end{aligned}$$

> 令 $S(n)$ 表示 $< n$ 的所有正整数中十进制表示不包含 $2$ 的数组成的集合。
>
> 证明 $\lvert S(1000) \rvert = 9^3 - 1$。

三位数，每一位有 $9$ 种取法，共 $9^3$ 个数。去掉 $000$ 即 $9^3 - 1$。

> 证明：对任意正整数 $n$ 有
>
> $$\sum_{r \in S(n)} \frac 1 r < 80$$

$$\begin{aligned}
    & \sum_{r \in S(\infty)} \frac 1 r \\
    =& \sum_{n=0}^\infty \sum_{r \in [10^n, 10^{n+1}) \cap S(\infty)} \frac 1 r \\
    < & \sum_{n=0}^\infty \left( 8 \times 9^n \times \frac 1 {10^n} \right) \\
    =& 80
\end{aligned}$$