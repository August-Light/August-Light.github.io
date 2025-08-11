# [10378: 区间逆序对](https://www.xmoj.tech/problem.php?id=10378)

绿。

唐题

# [10379: 写作业](https://www.xmoj.tech/problem.php?id=10379)

紫。

Kubic: Hall 定理可能也能做，但是麻烦一点。

$\min +$ 卷积的 Minkowski 和

# [10380: 异或](https://www.xmoj.tech/problem.php?id=10380)

> 有一个空集合 $S$。给定一个参数 $m$。
> $n$ 次操作，每次操作给定两个参数 $a_i, b_i$（$0 \le a_i < 2^m, -1 \le b_i < 2^m$）：
> - 向 $S$ 插入 $a_i$，保证在此之前 $a_i \not \in S$。
> - 求：
> $$\min\limits_{d=0}^{b_i} \min\limits_{x,y \in S, x \ne y} (x + d) \oplus (y + d)$$
>
> 特别地，若 $\lvert S \rvert < 2$ 或 $b_i = -1$ 则答案为 $-1$。
>
> $n \le 10^5$，$m \le 40$。

**异或最小值，来自 [ABC308G](https://www.luogu.com.cn/problem/AT_abc308_g) 的结论：$x < y < z$，则 $\min(x \oplus y, y \oplus z) < x \oplus z$**。熟悉的排序取相邻值。



对于 $x < y$，有 $(x + d) \oplus (y + d) \ge y - x$。



