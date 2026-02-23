# 离散微积分

## 分部求和

$$\Delta(uv) = u \Delta v + \mathrm E v \Delta u$$

$$\sum u \Delta v = uv - \sum \mathrm Ev \Delta u$$

**注意后面那项总是 $\mathrm E v$ 而不是 $v$**。

## 组合数常用公式

上指标反转：

$$\binom {-x} n = (-1)^n \binom {x + n - 1} n$$

差分 / 求和：

$$\Delta \binom x n = \binom x {n-1}$$

$$\sum \binom x n \delta x = \binom x {n+1} + C$$

## Hockey-Stick Identity

$$\sum_{k = r}^n \binom k r = \binom {n+1} {r+1}$$

<img src="https://upload.wikimedia.org/wikipedia/commons/d/d3/HockeyStick.jpg" width=300>

# Example 3.16 [AIME I 2017 #7](https://artofproblemsolving.com/wiki/index.php?title=2017_AIME_I_Problems/Problem_7) (Easy)

> $$\sum_{a+b \le 6} \binom 6 a \binom 6 b \binom 6 {a+b}$$

$$\begin{aligned}
    & \sum_{a+b \le 6} \binom 6 a \binom 6 b \binom 6 {a+b} \\
    =& \sum_{a,b} \binom 6 a \binom 6 b \binom 6 {6 - (a+b)} \\
    =& \binom {18} 6 = \boxed{18564} \\
\end{aligned}$$

# Example 3.17 [AIME I 2018 #12](https://artofproblemsolving.com/wiki/index.php?title=2018_AIME_I_Problems/Problem_12) (Easy)

> 从 $\{1, \cdots, 18\}$ 中均匀随机抽一个子集，求子集内所有元素之和恰好为 $3$ 的倍数的概率。

OGF：

$$f(x) = \left( (1 + x^0) (1 + x^1) (1 + x^2) \right)^6$$

单位根反演：

$$\sum_{3 \mid m} [x^m] f(x) = \frac 1 3 \sum_{k=0}^2 f(\omega_3^k)$$

$$\begin{cases}
    f(\omega_3^0) = 2^{18} \\
    f(\omega_3^1) = f(\omega_3^2) = 2^6 \\
\end{cases}$$

$$\frac 1 {2^{18}} \frac {2^{18} + 2^6 + 2^6} 3 = \boxed{\frac {683} {2048}}$$

# Example 3.18 [AIME I 2015 #12](https://artofproblemsolving.com/wiki/index.php?title=2015_AIME_I_Problems/Problem_12) (Easy)

> 从 $\{1, \cdots, 2015\}$ 均匀随机抽一个 $1000$ 元子集，求子集内所有元素最小值的期望。

$$\begin{aligned}
    & \sum_{k=1}^{1016} k \times \frac {\binom {2015 - k} {999}} {\binom {2015} {1000}} \\
    =& \frac 1 {\binom {2015} {1000}} \sum_{k=1}^{1016} k \binom {2015 - k} {999} \\
    =& \frac 1 {\binom {2015} {1000}} \sum_{k=999}^{2014} (2015 - k) \binom k {999} \\
\end{aligned}$$

有恒等式

$$\sum_{k=m}^{n-1} (n - k) \binom k m = \binom {n + 1} {m + 2}$$

代入：

$$\begin{aligned}
    & \frac 1 {\binom {2015} {1000}} \sum_{k=999}^{2014} (2015 - k) \binom k {999} \\
    =& \frac {\binom {2015 + 1} {999 + 2}} {\binom {2015} {1000}} = \boxed{\frac {288} {143}} \\
\end{aligned}$$

## 恒等式的推导

$$\begin{aligned}
    & \sum (n - k) \binom k m \delta k \\
    =& (n - k) \binom k {m + 1} - \sum (-1) \binom {k + 1} {m+1} \delta k \\
    =& (n - k) \binom k {m + 1} + \binom {k + 1} {m + 2} + C \\
\end{aligned}$$

$$\begin{aligned}
    & \sum_m^n (n - k) \binom k m \delta k \\
    =& \left. (n - k) \binom k {m + 1} + \binom {k + 1} {m + 2} \right\vert_{k=m}^{k=n} \\
    =& ((n - n) \binom n {m + 1} + \binom {n + 1} {m + 2}) - ((n - m) \binom m {m + 1} + \binom {m + 1} {m + 2}) \\
    =& \binom {n + 1} {m + 2}
\end{aligned}$$

# Example 3.19 [AIME II 2020 #14](https://artofproblemsolving.com/wiki/index.php?title=2020_AIME_II_Problems/Problem_14) (Ad-hoc)

> $\{x\} = x - \lfloor x \rfloor$。
>
> 定义 $f(x) = x \{x\}$。求 $f(f(f(x))) = 17$ 在 $[0, 2020]$ 上的实数解个数 $\bmod 1000$。

注意到对于每个 $n \ge \lfloor y \rfloor$，$f(x) = y$ 在 $[n, n+1)$ 上有且仅有一解。

令 $y = f(x), z = f(y)$。有 $f(z) = 17$。任何 $17 \le \lfloor x \rfloor \le \lfloor y \rfloor \le \lfloor z \rfloor < 2020$ 范围内的整数三元组 $(\lfloor x \rfloor, \lfloor y \rfloor, \lfloor z \rfloor)$ 都是 OK 的。

计数 $\binom {2005} 3 \bmod 1000 = \boxed{10}$。

# Example 3.20 [MPFG 2019 #11](https://mathprize.atfoundation.org/resources/past-tests/2019/mathprize2019problems.pdf) (Easy)

> 我有 $12$ 个 $+1$ 和 $10$ 个 $-1$。选出 $10$ 个数（共有 $\binom {22} {10}$ 种方案）求出它们的乘积。求所有方案算出来的乘积的和。

$$\begin{aligned}
    & [x^{10}] (1 + (+1)x)^{12} (1 - (-1)x)^{10} \\
    =& [x^{10}] (1 + x)^2 (1 - x^2)^{10} \\
    =& - \binom {10} 5 + \binom {10} 4 = \boxed{-42} \\
\end{aligned}$$

# Example 3.21 [BMO1 2022 #3](https://bmos.ukmt.org.uk/home/bmo1-2022.pdf) (Normal)

[官方答案视频](https://bmos.ukmt.org.uk/solutions/bmo1-2022/q3.mp4)

> 对于每个整数 $n \in [0,11]$，Eliza 有 $3$ 个重 $2^n$ 克的**相同**金条。
>
> 求选出若干金条使总重量为 $2021$ 克的方案数。

注意到 $11$ 的上界是没用的，我们直接改成 $\infty$ 增加优雅性。

$$\begin{aligned}
    & [x^m] \prod_{n=0}^\infty (1 + x^{2^n} + x^{2 \times 2^n} + x^{3 \times 2^n}) \\
    =& [x^m] \prod_{n=0}^\infty \frac {1 - x^{4 \times 2^n}} {1 - x^{2^n}} \\
    =& [x^m] \frac 1 {(1 - x) (1 - x^2)} \\
    =& [x^m] \frac 1 {(1 - x)^2 (1 + x)} \\
    =& [x^m] \left( \frac 1 {4 (1 - x)} + \frac 1 {2 (1 - x)^2} + \frac 1 {4 (1 + x)} \right) \\
    =& \frac 1 4 + \frac 1 2 (m + 1) + \frac 1 4 (-1)^m \\
    =& \frac {2m + 3 + (-1)^m} 4 \\
\end{aligned}$$

代入 $m = 2021$ 得 $\boxed{1011}$。

