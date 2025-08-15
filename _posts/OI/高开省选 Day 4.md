- 点双连通图
  - 任意两点 $u,v$ 之间至少有两条不相交简单路径

# 无向图 Tarjan

$low_u$ 是点 $u$ 至多经过一条非树边，所能到达的 $dfn$ 最小的节点对应的 $dfn$

（DFS 树要看成有向的）

DFS 树的非树边都是返祖边

对于边 $u \to v$：
- 若这条边是树边：$low_u \gets \min(low_u, low_v)$
- 若这条边是返祖边：$low_u \gets \min(low_u, dfn_v)$

割点：[P3388 【模板】割点（割顶）](https://www.luogu.com.cn/problem/P3388)
- 若 $u$ 是根，若 $u$ 有不止一个儿子，则 $u$ 是割点。
- 否则，若存在 $u$ 的一个儿子 $v$ 满足 $low_v \ge dfn_u$，则 $u$ 是割点。

点双：[P8435 【模板】点双连通分量](https://www.luogu.com.cn/problem/P8435)
- 在 DFS 过程中把点压进一个栈。
- 若 $u$ 是非根的割点，则不断弹栈，直到弹出 $v$；此时刚弹出的点和 $u$ 构成一个点双。
- DFS 结束后栈中剩下的点构成一个点双。TODO:

割边：
- 返祖边不是割边。
- 对于树边 $u \to v$：
  - 若 $low_v > dfn_u$，则 $u \to v$ 是割边。
  - 或者是，若 $low_u = dfn_u$，则 $fa_u \to u$ 是割边。TODO:

边双：[P8436 【模板】边双连通分量](https://www.luogu.com.cn/problem/P8436)
- 在 DFS 过程中把点压进一个栈。
- 若 $low_u = dfn_u$，则 $fa_u \to u$ 是割边。则不断弹栈，直到弹出 $u$；此时刚弹出的点构成一个边双。

# 有向图 Tarjan

DFS 出四类边：树边、前向边、返祖边、横叉边。

- 横叉边 $u \to v$ 满足 $dfn_u > dfn_v$。

强连通分量：[P3387 【模板】缩点](https://www.luogu.com.cn/problem/P3387)
- 在 DFS 过程中把点压进一个栈。
- TODO:
- 当

# Tarjan 例题

## [P4494 [HAOI2018] 反色游戏](https://www.luogu.com.cn/problem/P4494) (Normal)

- 树的方案若存在则唯一，存在方案的充要条件是黑点数量为偶数。
- 连通图若黑点数量为偶数，则方案数为 $2^{m - (n-1)}$。
- 非连通图的方案数为 $2^{m-n+c}$，其中 $c$ 为黑点为偶数的连通块数量。

## [Counting The Important Pairs](https://vjudge.net/problem/CodeChef-TAPAIR) (Hard)

> 给定一个有 $n$ 个点 $m$ 条边的无向连通图，可以删掉两条边，问有多少种方案使得这个连通图不连通。
>
> $n,m \le 3 \times 10^5$。

相同套路的问题：[P10778 BZOJ3569 DZY Loves Chinese II](https://www.luogu.com.cn/problem/P10778)

随机化。

对于每条非树边 $v \to u$ 随机一个权 $w$，把树上 $u \rightsquigarrow v$ 的边都 $\oplus w$。

割掉的两条边合法的必要（且大概率充分）条件是：**存在一条边的权值为 $0$（即这条边是割边）或两条边权值相同**。

~~所以这个树上差分也是求割边的另一种做法。~~

## [CF1515G Phoenix and Odometers](https://www.luogu.com.cn/problem/CF1515G) (Hard)

神题！

> 给定一个有 $n$ 个点 $m$ 条边的有向图，边带边权。
> 有 $q$ 次询问，每次询问会给出三个参数 $v,s,t$，你需要回答是否存在一条从 $v$ 出发回到 $v$ 的路径使得，该路径的边权和对 $t$ 取模后为 $s$。
>
> $1 \le n,m,q \le 2 \times 10^5$。

这是一个和 [P4151 [WC2011] 最大XOR和路径](https://www.luogu.com.cn/problem/P4151) 类似的环路空间题，因为一个回路走 $t$ 遍相当于没有走过。

因此强连通分量内答案一致，缩点。接下来考虑强连通分量内的求解。

找到一组环路空间的基，令基中每个环的长度为 $x_i$，根据 Bézout 定理可知则一组询问有解当且仅当 $\gcd(\gcd\limits_i (x_i), t) \mid s$。

有向图环路空间的基和无向图也没什么两样，依然是 DFS 树上的非树边。可以这样写：对于每条非树边 $u \to v$ 权值为 $w$，把 $dis_u + w - dis_v$ TODO:

## [P5163 WD与地图](https://www.luogu.com.cn/problem/P5163)

> 给出一个 $n$ 个点 $m$ 条边的有向图，第 $i$ 个点有点权 $a_i$。
> 你需要支持 $q$ 次操作：
> - 删除图中的一条边。
> - 把一个点的点权增加 $x$。
> - 询问一个点所在的强连通分量中点权前 $k$ 大之和。
>
> $1 \le n,m,q \le 2 \times 10^5$。

首先时光倒流，删边变加边，加权变减权。

整体二分。TODO:

## [P8426 [JOI Open 2022] 放学路 / School Road](https://www.luogu.com.cn/problem/P8426) (Hard)

> 给出一个 $n$ 个点 $m$ 条边的带权无向图，边权均为正，判断是否所有从 $1$ 出发到 $n$ 的简单路径长度均相同。
>
> $n \le 10^5$，$m \le 2 \times 10^5$。

先考虑所有点都在一个点双内的情况（这个是部分分）。

有一个这样的结构：

```
1
 \
  a-b
  |/|
  c-d
     \
      n
```

中间那条 `/` 是不可能存在的。

所以说整个图就是一个串并联的样子。以 $1,n$ 为正极和负极，整个图都是串联和并联，我们不妨把这种图叫杏仁图 hhh。

一直缩 degree 为 $2$ 的点，TODO:

最终合法当且仅当 TODO:

似乎和广义串并联图有关？

# 圆方树 例题

## [P4606 [SDOI2018] 战略游戏](https://www.luogu.com.cn/problem/P4606) (Easy)

> 给出一个简单无向连通图，有 $Q$ 次询问：
> 每次给出一个点集 $S$，求有多少个点 $u$ 满足 $u \not \in S$ 且删去 $u$ 后 $S$ 中的点不连通。
>
> $T \le 10, n \le 10^5, m \le 2 \times 10^5, Q \le 10^5, \sum \lvert S \rvert \le 2 \times 10^5$。

圆方树上 [P3320 [SDOI2015] 寻宝游戏](https://www.luogu.com.cn/problem/P3320)。做完了。

~~SDOI 真的很喜欢虚树呢，[P2495 [SDOI2011] 消耗战](https://www.luogu.com.cn/problem/P2495) 也是 SDOI~~。

## [P4630 [APIO2018] 铁人两项](https://www.luogu.com.cn/problem/P4630) (Easy)

> 给出一个简单无向图，求有多少三元组 $(x,y,z)$ 满足：
> - $x, y, z$ 两两不相等。
> - 存在一条从 $x$ 到 $z$ 的简单路径经过 $y$。
>
> $n \le 10^5, m \le 2 \times 10^5$。

感觉太简单了做法不用写了，$O(n+m)$。

## [P8331 [ZJOI2022] 简单题](https://www.luogu.com.cn/problem/P8331)

> 首先给出一张简单连通无向图，每条边有一个正整数边权。特别地，保证图上任意两个简单环的边权和相等。
> 然后修改图中每条边的边权。
> 给出修改后的图，同时给出多组询问，每次询问两点 $S,T$ 间所有简单路径权值和。答案对 $998244353$ 取模。
>
> $n, q \le 5 \times 10^5$，$n-1 \le m \le 6.4 \times 10^5$。

题目的性质非常强，手玩可以发现这又是前面那个杏仁图。

TODO:

# 2-SAT

[P4782 【模板】2-SAT](https://www.luogu.com.cn/problem/P4782)

对于每个变量 $x_i$，在图上创建两个点 $x_i = 0$ 和 $x_i = 1$。有向边 $u \to v$ 的含义为 $u \implies v$。

## 解法 1：字典序最小解

依次确定 $x_i$ 并 DFS check，复杂度 $O(n (n+m))$。

虽然效率很低，但是可以求出字典序最小的解（对于这样的问题似乎没有更好的解法）。

## 解法 2：缩点

先缩点。若 $u$ 和 $\neg u$ 在同一 SCC 内无解，否则选择**拓扑序较大**的点，这样一定不会推出另一个。

复杂度 $O(n+m)$，效率很高，但是只能求出一组解。

# 2-SAT 例题

## [CF1657F Words on Tree](https://www.luogu.com.cn/problem/CF1657F) (Normal)

TODO:

## [CF1697F Too Many Constraints](https://www.luogu.com.cn/problem/CF1697F) (Normal)

对每个 $a_i$ 建 $k$ 个状态，$a_i$ 的第 $j$ 个状态 $b_{i,j}$ 表示 $a_i \le j$。

- 根据 $b_{i,j}$ 天生的限制：首先 $b_{i,j} \to b_{i,j+2}$，还有 反过来 $\neg b_{i,j} \to \neg b_{i,j-1}$。
- 对于单调性的限制：TODO:
- 对于额外的限制：TODO:

时间复杂度 $O((n+m) k)$。

常见问题：建模建的是 $b_{i,j}$ 表示 $a_i = j$，这样是不好处理的。

## [P7216 [JOISC 2020] 美味しい美味しいハンバーグ](https://www.luogu.com.cn/problem/P7216) (Lunatic)

> 平面上有n个矩形，要选出k个点使得每个矩形内都有至少一个点。**保证有解**。
>
> $n \le 2 \times 10^5$，$k \le 4$。

TODO:

# 差分约束

[P5960 【模板】差分约束](https://www.luogu.com.cn/problem/P5960)

$x_v - x_u \le w$，移项 $x_v \le x_u + w$，用一条边 $u \to v$ 权值为 $w$ 的边表示。

跑 SPFA，求出的最短路即为一组可行解。若存在负环说明无解。时间复杂度 $O(nm)$（同 SPFA），但是特殊性质图可能有奇效。

## [P7515 [省选联考 2021 A 卷] 矩阵游戏](https://www.luogu.com.cn/problem/P7515) (Normal)



注意到确定了第一行第一列整个矩阵就被完全确定，接下来试图调整。考虑这样的

TODO:

时间复杂度上界 $O(T n m (n+m))$，玄学地能过。

## [CF1450E Capitalism](https://www.luogu.com.cn/problem/CF1450E) (Hard)

>

- 有向边：一正一反两条边即可。
- 无向边：$dis_u - 1 \le dis_v \le dis_u + 1$，但是奇偶性分析可知必然能求出合法解。

第二问改成 Floyd。

# 最小环

[P6175 无向图的最小环问题](https://www.luogu.com.cn/problem/P6175)

我们魔改 Floyd。在外层循环到点 $k$ 开始计算前，$dis_{u,v}$ 表示 $u \rightsquigarrow v$ 仅经过 $[1,k)$ 内的点的最短路。我们把这个最短路和 $w_{v,k} + w_{k,u}$ 拼起来。

# 最小环 例题

## [#2832. 「JOISC 2018 Day 1」栅栏](https://loj.ac/p/2832) (Hard)

爱来自 LOJ。神奇的题！

> 有一个坐标系，给定 $n$ 条线段栅栏和一个边长为 $2S$ 的正方形，保证栅栏不经过正方形，且线段之间不相交（最多在端点处重合）。
>
> 你再加入一些栅栏，使得这些栅栏能够形成一个多边形包住正方形。求加入的栅栏长度和的最小值。
>
> $n \le 100$。

首先对每个栅栏的两个端点和正方形的四个顶点连边，边权是欧氏距离。问题转化为包含正方形的最小环。

光线投射法。从正方形中心引一条随机射线，射线穿过环上的奇数条边。所以 Floyd 再加一维 $0/1$ 代表穿过次数的奇偶次。

时间复杂度 $O(n^3)$。

# Hall 定理

二分图是否存在完美匹配？

令 $G$ 是一个二分图，$X$ 是左部，$Y$ 是右部，且 $\lvert X \rvert \le \lvert Y \rvert$。

对 $W \subseteq X$，记 $N_G(W)$ 为 $Y$ 中所有和 $X$ 中点有边的顶点集合。

**Hall 定理**：**二分图 $G$ 存在完美匹配，当且仅当 $\lvert W \rvert \le \lvert N_G(W) \rvert$ 对于所有 $W \subseteq X$ 都成立**。

## 证明

必要性显然，证明充分性。

TODO:

# Hall 定理 例题

## [[AGC029F] Construction of a tree](https://www.luogu.com.cn/problem/AT_agc029_f)



## [CF1408H Rainbow Triples](https://www.luogu.com.cn/problem/CF1408H)