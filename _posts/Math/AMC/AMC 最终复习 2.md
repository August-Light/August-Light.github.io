# 2021 AMC Fall 12A

TODO:


## Problem 20 (Normal)

> 函数 $f(n) = 2 d(n)$。求 $n \in [1,50]$ 有几个数满足 $f^{50}(n) = 12$。

一看就是个图论题。连边 $i \to 2 d(i)$，看一下图长什么样。不难发现，$[1,11]$ 的数走不到 $12$；$12$ 是个自环。

$2 d(i) \ge 12$ 即 $d(i) \ge 6$ 的情况比较少，枚举即可。答案是 $\boxed{10}$。

## Problem 23 (Hard)

> 有一个首一二次多项式 $p(x)$，已知恰有 $3$ 个不同实数满足 $p(p(x))=0$，求所有 $p(x)$ 中一次项系数最小的那个。
>
> 输出 $p(1)$。

设 $p(x) = x^2 + bx + c$。

注意到 $p(p(x))$ 是 $4$ 次多项式，但是只有 $3$ 个根非常奇怪。怎么刻画重根？求导。对于多项式 $f(x)$ 的根 $x_0$，若 $f'(x_0) = 0$，则 $x_0$ 是一个重根。

$$\frac d {dx} p(p(x)) = p'(p(x)) \times p'(x)$$

$p'(x) = 2x + b$。因此 $\frac d {dx} p(p(x)) \rvert_{x=x_0} = 0$ 等价于 $p(x_0) = -\frac b 2$ 或 $x_0 = - \frac b 2$。

前者是不可能的，由于使得 $p(x_0) = - \frac b 2$ 的 $x_0$ 不止一个（如果只有 $1$ 个那只能是 $-\frac b 2$，归入后一种情况）会导致更多重根出现。因此 $x_0 = - \frac b 2$。

因此 $p(- \frac b 2)$ 是 $p$ 的一个根。

怎么刻画“某数是 $p$ 的根”这一条件？我们可以设出其根 $\alpha,\beta$，$p(x) = (x - \alpha) (x - \beta)$。我们让 $\alpha$ 为 $p(- \frac b 2)$。

$$\alpha = p(- \frac b 2) = p(\frac {\alpha + \beta} 2) = - \frac {(\alpha - \beta)^2} 4$$

这个 $(\alpha - \beta)^2$ 很好看，我们尝试把 $b$ 表示为 $\alpha - \beta$ 的函数：

$$\begin{aligned}
    & b \\
    =& - (\alpha + \beta) \\
    =& - 2 \alpha + (\alpha - \beta) \\
    =& \frac {(\alpha - \beta)^2} 2 + (\alpha - \beta) \\
    =& \frac 1 2 ((\alpha - \beta) + 1)^2 - \frac 1 2 \\
    \ge & - \frac 1 2
\end{aligned}$$

在 $\alpha - \beta = -1$ 时取等。

与此同时，当 $b = - \frac 1 2$ 时，$\alpha + \beta = \frac 1 2$。解得

$$\begin{cases}
    \alpha = - \frac 1 4 \\
    \beta = \frac 3 4 \\
\end{cases}$$

因此

$$p(x) = (x + \frac 1 4) (x - \frac 3 4)$$

输出 $p(1) = \boxed{\frac 5 {16}}$。

## Problem 25 (Hard)

生成函数解法可以给到 Hard 上位，组合意义解法 Normal，平均一下评个 Hard。

> $m \ge 5$ 是一个奇正整数。$D(m)$ 是满足以下条件的四元组 $(a_1, a_2, a_3, a_4)$ 的个数：
> - $a_i$ 互不相同。
> - $1 \le a_i \le m$。
> - $m \mid a_1 + a_2 + a_3 + a_4$。
>
> 有一个三次多项式 $q(m)$ 在任何奇正整数处和 $D(m)$ 取值相同，求 $q(m)$ 的表达式。
>
> 输出 $q(m)$ 的一次项系数。

### Sol 1：生成函数解法

我们不妨先排个序：$a_1 < a_2 < a_3 < a_4$，最后答案 $\times 24$ 即可。

**组合意义天地灭，代数推导保平安**！

我们尝试用 GF 做，但是发现 GF 很难刻画条件。若没有“$4$ 个数”这个限制，我们可以写成 $\prod\limits_{i=1}^m (1 + x^i)$。那么怎么刻画“$4$ 个数”呢？我们可以使用二元 GF：

$$f(x) = [t^4] \prod_{i=1}^m (1 + t \times x^i)$$

我们要筛选出 $x^m, x^{2m}, \dots$ 这些项系数之和，显然可以使用单位根的技巧：

$$\frac 1 {24} D(m) = \frac 1 m \sum_{k=0}^{m-1} f(\omega_m^k) = \frac 1 m \sum_{k=0}^{m-1} [t^4] \prod\limits_{i=1}^m (1 + t \times \omega_m^{ki})$$

尝试化简后面的求积。

当 $k=0$ 时，化简为 $(1+t)^m$，其四次项系数为 $\binom m 4$。

当 $k \ne 0$ 时：

$$\begin{aligned}
    & \prod\limits_{i=1}^m (1 + t \times \omega_m^{ki}) \\
    =& (-t)^m \prod\limits_{i=1}^m (- \frac 1 t - \omega_m^{ki}) \\
    =& (-t)^m (\frac 1 {(-t)^{m/\gcd(k,m)}} - 1)^{\gcd(k,m)} \\
    =& (1 - (-t)^{m / \gcd(k,m)})^{\gcd(k,m)} \\
\end{aligned}$$

由于 $m$ 是 $\ge 5$ 的奇数，这个式子不可能组合出 $t^4$ 项。因此四次项系数为 $0$。

总结：

$$f(\omega_m^k) = \begin{cases}
    \binom m 4 & k = 0 \\
    0 & \text{otherwise}
\end{cases}$$

因此 $D(m) = \frac {24} m \binom m 4 = (m-1) (m-2) (m-3)$。做完了。

这个结果好像有点优美，应该有组合意义。看一下 Sol 2。

### Sol 2：组合意义是？

（官方解法 Sol 3）

选 $a_1, a_2, a_3$ 有 $\binom m 3$ 种方案，此时 $m \mid (a_1 + a_2 + a_3) + a_4$ 可以唯一确定 $a_4$。但是有 $\frac 3 m$ 比例的情况中 $a_4$ 已经被占掉了。

$$D(m) = \binom m 3 (1 - \frac 3 m) = (m-1) (m-2) (m-3)$$

### Sol 3（？）：插值

（官方解法 Sol 2）

题目已经说了是三次多项式，找到四个点值插值即可。通过巨大分类讨论不难找出四个点值。难度没有，但是考场上真的算得完吗？

# 2021 AMC Fall 12B

总体来说比较简单的一张卷子。但是不少题目需要一定注意力。全卷没有题目达到 Hard 难度。

## Problem 19 (Normal)

> 有一个圆，画出圆内接正 $5,6,7,8$ 边形各一个，保证没有公共顶点或三线共点。求这些多边形之间的交点数之和。

结论：对于同一圆的内接正 $a,b$ 边形（无公共顶点），它们的交点个数是 $2 \min(a,b)$。

证明：不妨设 $a \le b$。考虑 $a$ 边形的每条边，它都会割过 $b$ 边形，由于其凸性所以总是产生且仅产生 $2$ 个交点，总交点数为 $2a$。

答案为 $2 \times (3 \times 5 + 2 \times 6 + 1 \times 7) = \boxed{68}$。

## Problem 20 (Easy)

> 有一个正方体，给顶点染色，四黑四白，求方案数。通过旋转可以相同的方案视为同种方案。

手玩可以玩出以下方案：

<img src="https://wiki-images.artofproblemsolving.com//thumb/f/f6/Topology.jpg/1900px-Topology.jpg" width=500/>

因此我们可以认为答案就是 $\boxed 7$。

但是怎么证明找全了呢？如果不考虑旋转，则方案数是 $\binom 8 4 = 70$。把这 $7$ 种每种的方案数加起来，算出来正好是 $70$。

# 2021 AMC Spring 12A


## 

# 2021 AMC Spring 12B

## Problem 22 

Sol 1 知识点：Sprague–Grundy Theorem

Sol 2 知识点：Ad-hoc

> 有一个游戏：有若干堆砖头，Alice 和 Bob 轮流操作（Alice 先手），每次可以选择一堆砖头，设有 $n$ 块，拿掉其中的 $1$ 或 $2$ 块把它变成 $x,y$ 块的两堆（即 $x+y \in \{n-1,n-2\}$，$x,y$ 可以为 $0$）。不能操作者败。
>
> 例：$(4,2)$ 这个局面在拿掉后可以成为 $(3,2)$ 或 $(2,1,2)$ 或 $(4)$ 等局面，以此类推。
>
> <img src="https://latex.artofproblemsolving.com/1/a/5/1a5938c90db67cc867d798bb9693e149b9438071.png" width=300/>
>
> 以下哪个初始局面 Bob 有必胜策略？
>
> - $(6,1,1)$
> - $(6,2,1)$
> - $(6,2,2)$
> - $(6,3,1)$
> - $(6,3,2)$

### Sol 1：Sprague–Grundy Theorem

我们发现每堆砖头其实都是独立的游戏，所以考虑用 $SG$ 函数。

令 $SG(n)$ 表示一堆 $n$ 块的砖头的 $SG$ 函数值。边界 $SG(0) = 0$，有以下转移：

$$SG(n) = \operatorname{mex}\limits_{x+y \in \{n-1,n-2\}} (SG(x) \oplus SG(y))$$

暴力算一下：

| $n$ | $SG(n)$ |
| :-: | :-: |
| $0$ | $0$ |
| $1$ | $1$ |
| $2$ | $2$ |
| $3$ | $3$ |
| $4$ | $1$ |
| $5$ | $4$ |
| $6$ | $3$ |

每个选项的 $SG$ 函数就是把三堆的 $SG$ 异或起来。只有 B 选项 $SG(6) \oplus SG(2) \oplus SG(1) = 0$，是必败态，选择 B。

### Sol 1 方法复习

- 终止态 $SG$ 函数为 $0$。对于单个游戏，每个状态的 $SG$ 为其所有后继状态的 $SG$ 之 $\text{mex}$。（Sprague–Grundy Theorem）
- 对于多个独立游戏，它们并起来的 $SG$ 函数值等于各自 $SG$ 函数的异或。

### Sol 2：不会 SG 怎么做？

（官方解法 Sol 2）

博弈论题的一个经典构造：copy 上一次对方的操作。因此，若 Alice 可以把局面变得“对称”，则可以 copy Bob 的策略。

- A 选项 $(6,1,1)$ 可以把第一堆变成 $2,2$，变成 $(2,2,1,1)$ 的对称局面。
- C 选项 $(6,2,2)$ 变成 $(2,2,2,2)$。
- D 选项 $(6,3,1)$ 变成 $(3,1,3,1)$。
- E 选项 $(6,3,2)$ 变成 $(3,2,3,2)$。

排除法选择 B 选项。但是 Sol 2 没有证明 B 选项的正确性。