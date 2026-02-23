https://artofproblemsolving.com/wiki/index.php?title=2026_AIME_II

# Problem 1

> 设首项为 $4$ 且包含 $24, 34$ 的等差数列的第 $10$ 项为 $a_{10}$。对 $a_{10}$ 的所有可能值求和。

$$d \mid 10 \iff d \in \{1, 2, 5, 10\}$$

$$a_{10} = 4 + 9d$$

$$13 + 22 + 49 + 94 = \boxed{178}$$

# Problem 2

$$\begin{cases}
    f_n = f_{n-1} + 2 g_{n-1} \\
    g_n = f_{n-1} + 2 g_{n-1} \\
\end{cases}$$

$f_0 = g_0 = 1$

$$f_n = g_n = 3^n$$

$$\sqrt{3^{10}} = 3^5 = \boxed{243}$$

# Problem 3

# Problem 4

> 定义 $f(n)$：令 $b$ 为 $n$ 在十进制下所有数位的最大值 $+1$，$f(n)$ 为把 $n$ 直接放在 $b$ 进制下看的结果。
>
> 求 $\sum_{n=1}^{1000} [f(n) = n]$。

首先 $n \in [1,9]$ 都对，特判掉。

对于其它 $n$，$f(n) = n$ 当且仅当 $b = 10$，即 $n$ 中含有数位 $9$。

正难则反，考虑数不含有 $9$ 的 $n$ 的个数。$9 \times 9 \times 9 = 729$。$1000 - 729 = 271$ 个含 $9$ 的数。

把特判放回来，$\boxed{279}$ 个。

# Problem 5

> 有 $n$ 个球，每个球都是红色或蓝色，每种颜色至少 $7$ 个。
>
> 当我随机取 $7$ 个球时，恰好有 $4$ 个红球的概率等于恰好有 $5$ 个红球的概率。
>
> 求出 $n$ 的 $5$ 个可能的最小值之和。

设红球蓝球各 $a,b$ 个：

$$\begin{cases}
    a + b = n \\
    \binom a 4 \binom b 3 = \binom a 5 \binom b 2 \\
\end{cases}$$

$$\frac {b-2} 3 = \frac {a-4} 5$$

$$5b = 3a - 2$$

$$a + \frac {3a - 2} 5 = n$$

$$8a - 2 = 5n$$

$$a = \frac {5n + 2} 8, b = \frac {3n - 2} 8$$

$$5n+2 \equiv 0 \pmod 8$$

$$n \equiv 6 \pmod 8$$

$$\frac {3n-2} 8 \ge 7$$

$$n \ge 20$$

$n = 22, 30, 38, 46, 54$

答案为 $\boxed{190}$。

# Problem 6

> 有一个圆心在 $(4, 39)$ 半径为 $r$ 的圆，与抛物线 $y = f(x) = \frac 1 2 x^2 - 4x + 6$ 相切。
>
> 求 $r$ 的所有可能值之和。

$$f'(x) = x - 4$$

设切点 $(x_0, f(x_0))$，则半径斜率为

$$\frac {f(x_0) - 39} {x_0 - 4}$$

乘起来为 $-1$，等会儿考虑 $x_0 = 4$：

$$f(x_0) - 39 = -1$$

$$f(x_0) = 38$$

$$x_0 = 4 \pm 4 \sqrt 5$$

$$r^2 = (\pm 4 \sqrt 5)^2 + (38 - 39)^2 = 81$$

$$r = 9$$

对于 $x_0 = 4$，顶点为 $(4, -2)$，$r = 41$。

因此答案为 $9 + 41 = \boxed{050}$。

# Problem 7

> 每一轮游戏，A,B,C 三人均匀随机一人拿到 $1$ 个 coin。求 A,B 均在 C 拿到任何 coin 前拿到至少 $2$ coin 的概率。

俩 AI 都算出 $\frac 7 {54}$。





# Problem 8

$$\frac {1 + \sec 2 \theta} {1 + \sec \theta} = \frac {125} 6$$

$$\sec 2 \theta = \frac {\sec^2 \theta} {2 - \sec^2 \theta}$$

令 $s = \sec \theta$：

$$\frac 2 {(2 - s^2) (1 + s)} = \frac {125} 6$$

$$s^3 + s^2 - 2 s - \frac {238} {125} = 0$$

唯一的有理数解为 $s = \frac 7 5$。

$$\sec \theta = \frac 7 5 \implies \sec 2 \theta = 49$$

$5 \times 49 = \boxed{245}$

# Problem 9