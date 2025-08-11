# 组合意义

组合意义可以简化很多问题，组合数的上指标求和与 Vandermonde 卷积都有组合意义。

## 一道题

> 给定一个 $\texttt{01}$ 串，每次删掉一个位置直至删空，问有多少种删除方案。
>
> 两种删除方案不同，当且仅当某一步后得到的字符串不同。
>
> $n \le 400$。

首先跟连续段有关，但是直接做不好做，做一个这样的转化：每次删一个 $S_i \ne S_{i-1}$ 的位置 $i$，求删空方案数。

$n \le 400$ 做区间 DP。注意到，一个能被删除位置被删除之前，它的左右问题是独立的。

设 $f_{l,r}$ 为删去这个区间的方案数，且 $s_{l-1}$ 没删。

合并的时候要把左右两边的操作归并起来。

# 容斥原理 / 二项式反演

> 对于每个限制开一个集合，存下所有满足这个限制的方案。
>
> 令 $g_i$ 表示任意 $i$ 个集合的并的大小之和。
>
> 计算恰好在 $k$ 个集合内的数的个数 $f_k$。
>
> $k=0$ 对应了容斥原理，更一般的情况对应了二项式反演。

我们写出 $f,g$ 的关系：

$$g_k = \sum\limits_{i=k}^n \binom i k f_i$$

可以证明：

$$f_k = \sum\limits_{i=k}^n (-1)^{i-k} \binom i k g_i$$



# 二项式反演 例题

## [CF1228E Another Filling the Grid](https://www.luogu.com.cn/problem/CF1228E)

> 给定一个 $n \times n$ 的正方形网格和一个整数 $k$。在每个格子中填入一个整数，满足以下条件：
> - 网格中所有数字都在 $1$ 到 $k$ 之间（包含 $1$ 和 $k$）。
> - $\forall i \in [1,n]$，第 $i$ 行的最小值为 $1$。
> - $\forall j \in [1,n]$，第 $j$ 列的最小值为 $1$。
>
> 计数。对 $10^9+7$ 取模。
>
> 需要一个 $O(n^2)$ 的解法，实际上能更优。

TODO:

$$\sum\limits_{i,j} (-1)^{i+j} \binom n i \binom n j k^{(n-i)(n-j)} (k-1)^{n(i+j) -ij}$$

时间复杂度 $O(n^2)$。

## [[ARC156E] Non-Adjacent Matching](https://www.luogu.com.cn/problem/AT_arc156_e)

TODO:

## [[ARC159F] Good Division](https://www.luogu.com.cn/problem/AT_arc159_f)

>

良好数列的充要条件为 $\lvert X \rvert$ 为偶数，且 $X$ 不存在绝对众数（出现次数 $> \frac {\lvert X \rvert} 2$）。

TODO:

## [[ABC236Ex] Distinct Multiples](https://www.luogu.com.cn/problem/AT_abc236_h)

TODO:

## ABC236Ex 改

TODO:

# DP 套 DP

