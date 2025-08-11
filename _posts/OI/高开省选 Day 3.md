# 数据结构优化 DP

## [P2605 [ZJOI2010] 基站选址](https://www.luogu.com.cn/problem/P2605)

首先发现 $D$ 和 $S$ 是假的，可以先二分求出每个村庄基站的村庄覆盖范围 $[l_i,r_i]$。

看一下数据范围估计是 $O(n k \log n)$ 的，那就是先要一个 $O(n^2 k)$ 再优化，这很扫描线。

TODO:

## [P6773 [NOI2020] 命运](https://www.luogu.com.cn/problem/P6773)

考虑一棵定好边的子树。将限制分为三类：子树内，子树往上已满足，子树往上未满足。我们重点关注最后一类。

我们发现往上的话只会是 $u \leftrightsquigarrow \text{root}$ 的路径，所以只要最低的那个限制被满足即可。

令 $f_{u,i}$ 表示 $u$ 的子树内都定好，最深限制是 $dep_i$ 的方案数（没有就是 $i=0$）。

树上 DP 考虑子树合并要怎么做。TODO:

- 填 1：TODO:
- 填 0：$f_{u,i} \times f_{v,j}$ 会对 $f_{u,\max(i,j)}$ 造成贡献。
  - 是 $\max$ 卷积的形式。

优化：对每个 $f_u$ 开一个线段树，做线段树合并。

TODO: 

[题解 P6773 【[NOI2020]命运】](https://www.luogu.com.cn/article/j3li2al4)

# 单调性 / 凸性优化 DP

Slope trick

## [CF1534G A New Beginning](https://www.luogu.com.cn/problem/CF1534G)

第一步切比雪夫转曼哈顿。看成每次往上走，并且往左或往右走一步。

把点按新的纵坐标排序。

$f_{i,j}$ 表示标记了 $i$ 个点，自己横坐标在 $j$。

TODO:

## [CF573E Bear and Bowling](https://www.luogu.com.cn/problem/CF573E)

> 给定序列 $a_{[1,n]}$，你要取出一个长度为 $m$ 的子序列 $b_{[1,m]}$，最大化 $\sum i \times b_i$。
>
> $n \le 10^5$。

$f_{i,j}$ 是前 $i$ 个选了 $j$ 个的答案。答案是 $f_{n,m}$。

$$f_{i,j} = \max(f_{i-1,j}, f_{i-1,j-1} + a_i \times j)$$

**结论：存在最优解使得前 $i-1$ 个数的集合是前 $i$ 个数的集合的子集**。（TODO: 对于一些更复杂的贡献形式也有这个结论，一些二次的）

TODO:

后缀加一次函数 & 单点插入，平衡树维护

## [[ARC168E] Subsegments with Large Sums](https://www.luogu.com.cn/problem/AT_arc168_e)



TODO:
TODO:
TODO:

# 杂 Trick

## CF1810G Maximum Prefix

## [P9132 [USACO23FEB] Watching Cowflix P](https://www.luogu.com.cn/problem/P9132)

> n 个点的树上，有黑点，白点
> 给定 k，你需要选择若干个连通块，使得覆盖所有黑点，每个连通块代价为 size+k
> 对于 k=1…n 求出最小代价
> n <= 2e5

单个 $k$ 怎么做？
- 选一个点覆盖 $+k+1$
- 选一个边覆盖 $-k$

$f_{u,0/1}$ DP，单个 $k$ 可以做到 $O(n)$。

两个连通块距离 $\le k$ 时可以直接合并。

考虑一个根号分治做法，
- $k \le B$ 跑原来的做法
- $k > B$ 做一个背包，$g_{u,j}$ 表示 $u$ 的子树里选了 $j$ 个连通块（$j \le B$）

令 $B = \Theta(\sqrt n)$ 时间复杂度 $O(n \sqrt n)$，空间复杂度 $O(n)$（树形背包）

polylog 做法：$O(\frac n k)$ 个连通块，建出虚树做 DP，调和级数 $O(n \ln n)$。

## [[ARC165E] Random Isolation](https://www.luogu.com.cn/problem/AT_arc165_e)

> 给一棵 n 个节点的树和一个整数 K。每次操作，等概率随机选一个所在连通块大小大于 K 的点，并删掉这个点和与之相连的所有边。重复操作直到图上所有连通块大小不超过 K，求期望操作次数，答案对 998244353 取模。
> $1 \le K < n \le 100$
> Bonus: 做到 $O(n^3)$

点分治，只统计经过根的连通块


TODO:
TODO:
TODO: