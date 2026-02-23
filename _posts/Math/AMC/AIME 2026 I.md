# Problem 1 (Too Easy)

小学题。

# Problem 2 (Easy)

> 求不含 $0$ 的、数位和为 $13$ 的、回文数个数。

肯定是奇数位。中间位是奇数。

枚举中间位 $m$，并用插板法：

$$\begin{aligned}
    & \sum_{m \in \{1,3,5,7,9\}} \sum_{n=1}^\infty \binom {\frac {13-m} 2 - 1} {n - 1} \\
    =& \sum_{m \in \{1,3,5,7,9\}} 2^{\frac {13-m} 2 - 1} \\
    =& \sum_{k=0}^4 2^{5-k} & m = 2k+1 \\
    =& \boxed{62} \\
\end{aligned}$$

# Problem 3 (Too Easy)

傻逼几何。

# Problem 4 (Easy)

> 求 $100$ 以内可以被表示为 $ab + a + b$ 形式的整数个数。此处 $a,b$ 是**不同的**正整数。

$$\begin{aligned}
    n &= ab + a + b \\
    n+1 &= (a+1) (b+1) \in [2, 101] \\
\end{aligned}$$

不 OK 的 $n+1$ 只有 $p$ 和 $p^2$ 这两种可能。因此答案为 $100 - (\pi(101) + \pi(\lfloor \sqrt{101} \rfloor)) = \boxed{70}$。

# Problem 5 (Too Easy)

傻逼几何。

# Problem 6 (Easy)

$$\begin{aligned}
    \sqrt[20]{x^{\log_{2026} x}} &= 26 x \\
    \frac 1 {20} \log_{2026} x \ln x &= \ln 26 + \ln x \\
    \frac 1 {20 \ln 2026} \ln^2 x - \ln x - \ln 26 &= 0 \\
    \ln x_1 + \ln x_2 &= 20 \ln 2026 \\
    x_1 x_2 &= 2026^{20} \\
\end{aligned}$$

$$\begin{aligned}
    & d(2026^{20}) \\
    =& d(2^{20}) \times d(1013^{20}) \\
    =& \boxed{441} \\
\end{aligned}$$

# Problem 7 (Easy, Enum)

所有置换环大小 $\in \{1,2,3,6\}$

$$\begin{aligned}
    6 &= 6 \\
    &= 3 + 3 \\
    &= 2 + 2 + 2 \\
    &= 1 + 1 + 1 + 1 + 1 + 1 \\
    &= 1 + 1 + 1 + 1 + 2 \\
    &= 1 + 1 + 2 + 2 \\
    &= 1 + 1 + 1 + 3 \\
    &= 1 + 2 + 3 \\
\end{aligned}$$

大分讨即可。最后答案为 $\boxed{396}$。

# Problem 8 (Easy)

> $$\left( \sum_{d \mid 17017^{17}} [d \bmod 12 = 5] \right) \bmod 1000$$

$$17017 = 7 \times 11 \times 13 \times 17$$

$$d \bmod 12 = 5 \iff \begin{cases}
    d \bmod 4 = 1 \\
    d \bmod 3 = 2 \\
\end{cases}$$

$7 = (-1, 1), 11 = (-1, -1), 13 = (1, 1), 17 = (1, -1)$

太漂亮了，问题解耦：

$$\begin{cases}
    7^a 11^b 13^c 17^d \equiv (-1)^{b+d} \pmod 3 \\
    7^a 11^b 13^c 17^d \equiv (-1)^{a+c} \pmod 4 \\
\end{cases}$$

答案为 $\boxed{244}$。





# Problem 13

> 定义
>
> $$S_r = \sum_{m=0}^\infty \binom {10000} {502m + r}$$
>
> 求
>
> $$\sum_{r=0}^{501} [503 \mid S_r]$$
>
> 为了减少你的计算量：$503$ 是质数。

$$\begin{aligned}
    S_r &= \sum_{502 \mid m} [x^{m+r}] (1 + x)^{10000} \\
    &= \frac 1 {502} \sum_{k=0}^{501} \omega_{502}^{-kr} (1 + \omega_{502}^k)^{10000} \\
\end{aligned}$$

在 $\bmod 503$ 下考虑。用原根 $g$ 代替 $\omega_{502}$，并且 Fermat 小定理降幂：

$$\begin{aligned}
    S_r \equiv & \frac 1 {502} \sum_{k=0}^{501} g^{-kr} (1 + g^k)^{462} \\
    \equiv & \frac 1 {502} \sum_{k=0}^{501} g^{-kr} \sum_{i=0}^{461} \binom {462} i g^{ik} \\
    \equiv & \sum_{i=0}^{461} \binom {462} i \frac 1 {502} \sum_{k=0}^{501} (g^{i-r})^k \\
    \equiv & \sum_{i=0}^{461} \binom {462} i [502 \mid (i - r)] \\
    \equiv & \binom {462} r
\end{aligned}$$

要让它为 $0$，必须是下指标大于上指标。因此 $r = 463, \cdots, 501$ 符合条件，共有 $\boxed{39}$ 个。

# Problem 15

> 求出用 $5$ 个方块环精确覆盖 $10 \times 10$ 棋盘的方案数。
>
> 方块环定义为 $a \times b$ 矩形挖掉中间 $(a-2) \times (b-2)$ 的一块。

