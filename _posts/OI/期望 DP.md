# [P1943 Local Maxima](https://www.luogu.com.cn/problem/P1943)

> 给定 $n$。均匀随机一个长为 $n$ 的排列 $p$，若一个数 $p_i$ 比前面的数都大，称其为局部最大值。求局部最大值的期望个数，**保留 $8$ 位小数**。
>
> $n < 2^{31}$。

构造指示器随机变量 $x_i \in \{0,1\}$，表示 $p_i$ 是否是局部最大值。答案即为

$$\mathbb E[\sum x_i] = \sum \mathbb E[x_i]$$

$p_{[1,i]}$ 这一段中任何一个数成为最大值的概率是相等的，都是 $\frac 1 i$，因此 $p_i$ 是局部最大值的概率是 $\frac 1 i$，即 $\mathbb E[x_i] = \frac 1 i$。答案即为

$$\sum\limits_{i=1}^n \frac 1 i = H_n$$

$n$ 较小时可以直接计算；$n$ 较大时使用 $H_n = \ln n + \gamma + O(\frac 1 n)$ 估算，其中 $\gamma$ 是 Euler-Mascheroni 常数 [OEIS A001620](https://oeis.org/A001620)。如果这题要求取模，有科技做法 [P5702 调和级数求和](https://www.luogu.com.cn/problem/P5702)，可以认为考场上不可做。