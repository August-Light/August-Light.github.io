# 10/12 [[NOIP2024 T4] 树上查询](https://www.luogu.com.cn/problem/P11364)

首先注意到 $\ge k$ 是假的，直接写成 $= k$ 即可。

$l \ne r$ 时有经典转化：

$$\text{dep}_{\text{LCA}(u_l, \cdots, u_r)} = \min\limits_{i \in [l,r)} \text{dep}_{\text{LCA}(u_i, u_{i+1})}$$

（注意不要用那个 $dfn$ 最小最大 LCA 的结论，在这里没用）

即原题排除 $k = 1$ 后答案为：

$$\max\limits_{p \in [l, r-k]} \min\limits_{i \in [p, p+k)} \text{dep}_{\text{LCA}(u_i, u_{i+1})}$$

（$k=1$ 用 RMQ 处理）

令 $v_i = \text{LCA}(u_i, u_{i+1})$。

对于每一个 $v_i$，求出一个极长段 $[x_i, y_i]$ 使得 $\text{LCA}(x_i, x_i+1, \cdots, y_i) = v_i$。这一步是单调栈。TODO:



# 10/14 [[NOIP2021 T2] 数列](https://www.luogu.com.cn/problem/P7961)

TODO:

# 10/20 [P9755 [CSP-S 2023] 种树](https://www.luogu.com.cn/problem/P9755) (Normal)

这个题肯定不是 DP，性质也太差了。估计是个贪心。

一眼二分答案。设我们要验证 $m$ 天是否可行。

我们对于每个点 $u$ 求一个最大的 $t_u$ 使得

$$\sum\limits_{x = t_u}^m \max(b_u + x c_u, 1) \ge a_u$$

这一步可以二分，求和可以分类讨论 $O(1)$ 求。

此时问题和 $a,b,c$ 已经无关。

问题转化为：我们要从 $1$ 开始种树，每个点 $u$ 有一个最晚种树时间 $t_u$，求是否可行。

正着做不好做，考虑反着贪心。最后种的树一定是叶子节点，因此我们从叶子中选择一个 $t$ 最大的节点删掉，对于剩下的节点求解子问题。这可以用优先队列 $O(n \log n)$ 维护。

卡常：注意到我们关心的 $t_u$ 其实只在 $n$ 的范围内，所以二分 $t_u$ 的时候上界设成 $n$ 即可。

时间复杂度 $O(n \log n \log V)$。注意卡常，不要滥用 `long long`。

总体来说没有思维难度吧，但是为什么做不出呢？

# 10/21 [[NOIP2021] 方差 T3](https://www.luogu.com.cn/problem/P7962)

首先有非常平凡的性质，$a_{i-1} \le a_{i-1} + a_{i+1} - a_i \le a_{i+1}$，即变换完后序列依然弱增。

按照套路，我们观察答案是否只和差分有关。我们发现**一次操作等价于交换差分数组的两个相邻值**。而且**方差只和差分数组有关**。

因此我们完全不在意原数组了，我们只看差分数组。令 $d_i = a_i - a_{i-1}$。

部分分：此时直接暴力时间复杂度 $O(n!)$。

此时这个东西看起来不像能 DP，先找性质。

$$\begin{aligned}
    & n^2 \times \frac 1 n \sum (a_i - \bar a)^2 \\
    =& n \sum a_i^2 - (\sum a_i)^2 \\
    =& n \sum_{i=1}^n (\sum_{j=1}^i d_j)^2 - (\sum_{i=1}^n \sum_{j=1}^i d_j)^2 \\
    =& n \sum_{i=1}^n \sum_{j=1}^i \sum_{k=1}^i d_j d_k - (\sum_{i=1}^n (n-i+1) d_i)^2 \\
    =& n \sum_{j=1}^n \sum_{k=1}^n d_j d_k (n-\max(j,k)+1) - \sum_{j=1}^n \sum_{k=1}^n (n-j+1) (n-k+1) d_j d_k \\
    =& \sum_{j=1}^n \sum_{k=1}^n d_j d_k (n(n+1) - n \max(j,k) - (n+1)^2 + (n+1)(j+k) - jk) \\
    =& \sum_{j=1}^n \sum_{k=1}^n d_j d_k (-n-1 - n \max(j,k) + (n+1)(j+k) - jk) \\
    =& \sum_{j=1}^n \sum_{k=1}^n d_j d_k (n \min(j,k) - (j-1)(k-1) - n) \\
    =& \sum_{i=1}^n d_i^2 (n-i+1)(i-1) + 2 \sum_{j=1}^n \sum_{k=1}^{j-1} d_j d_k (n-j+1)(k-1) \\
\end{aligned}$$



TODO:

# 10/23 [[CSP-S 2022 T1] 假期计划](https://www.luogu.com.cn/problem/P8817) (Normal)

这个题没有蓝的难度，顶多只有绿。

首先跑个多源最短路是不亏的，$O(n^2)$。此时原图已经没用，我们只考虑这张新图的情况。

$1 \to A \to B \to C \to D \to 1$ 这个条件不太好处理，肯定不能全枚举。我们考虑拆成 $1 \to A \to B$ 和 $C \to D \to 1$，这样两边就对称了，枚举 $B,C$ 统计答案。

具体怎么统计呢？我们发现一个严重的问题，若我们只保留最优解，则可能出现 $A=D$ 或 $A=C$ 或 $B=D$ 的情况，然后就寄了。所以我们存前 $3$ 优的解。

时间复杂度 $O(n^2)$。

注意判图不连通的情况，不判只有 55pts。

# 10/27 [P14255 列车（train）](https://www.luogu.com.cn/problem/P14255)

记录 $f_i$ 表示，停开区间左端点 $\le i$ 时右端点的最大值。$f$ 是单调弱增的。

对于点 $i$，从点 $i$ 出发能到达的第一个终点是 $f_i + 1$。

- 新增一个停开区间 $[l,r]$ 时，二分找到 $x$，使得 $x$ 是最大的使 $f_x < r$ 的位置。
  - 我们对 $i \in [l,x]$ 执行 $f_i \gets r$。
- 查询区间 $[l,r]$ 时，我们希望 $\min\limits_{i=1}^l (p_{\max(f_i + 1, r)} - p_i)$。二分找到 $x$，使得 $x$ 是最大的使 $f_x + 1 \le r$ 的位置。
  - 若选择列车的初始位置 $i \le x$，答案为 $\min\limits_{i=1}^x (p_r - p_i) = p_r - p_x$。
  - 若选择列车的初始位置 $i > x$，答案为 $\min\limits_{i=x+1}^l (p_{f_i + 1} - p_i)$。

线段树维护 $f_i$ 和 $p_{f_i + 1} - p_i$ 即可。

时间复杂度 $O(n \log n)$。

TODO: 有没有下标写错啊？
