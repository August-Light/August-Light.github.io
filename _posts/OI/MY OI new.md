# Basic

- 考虑答案是否仅与**差分**数组有关。
  - $a_{i-1} + a_{i+1} - 2 a_i = (a_{i+1} - a_i) - (a_i - a_{i-1})$。
- 考虑答案是否与**顺序**有关。
  - 若否，则排序 / 开桶。
- 考虑答案是否可以**二分**。
- 考虑值域数组能否变为 $01$ 数组。
- 最小不同和：若干个正整数之和为 $n$，则去重之后只有 $O(\sqrt n)$ 个。
  - $> \sqrt n$ 的只有 $O(\sqrt n)$ 个；$\le \sqrt n$ 的通常可以预处理。

# 暴力

- 枚举所有两两配对
  - 枚举全排列，将 $a_i$ 和 $a_{i \oplus 1}$ 配对。

# 序列上统计

- 偏序
  - 二维偏序
    - 对于每一对偏序关系 $(x_i, y_i) \prec (x_j, y_j)$，删除掉较小的 $(x_i, y_i)$。则剩余的元素中，按照 $x$ 递增排序后 $y$ 递减。[P2900 [USACO08MAR] Land Acquisition G](https://www.luogu.com.cn/problem/P2900)
      - 把区间嵌套视为二维偏序，也适用这个结论。左端点递增时，右端点也递增。[P14255 列车（train）](https://www.luogu.com.cn/problem/P14255)
- 中位数
  - 二分答案，小于等于的设成 $-1$，大于的设成 $+1$，转变成加法的问题。[P11761 [IAMOI R1] 明码标价](https://www.luogu.com.cn/problem/P11761)
  - 看成特殊的第 $k$ 小问题。
- 对于所有子区间
  - 固定一个端点，另一个端点扩展。
    - 固定 $r$ 扩展 $l$，统计出某些本质不同的扩展位置。然后 $r$ 移动到 $r+1$ 时继承。[P3794 签到题IV](https://www.luogu.com.cn/problem/P3794)
  - 通过前缀信息推区间信息。[P9753 [CSP-S 2023] 消消乐](https://www.luogu.com.cn/problem/P9753)
  - DP，设 $f_i$ 为所有以 $i$ 为右端点的区间的答案。
  - 分治。
- 绝对众数
  - **摩尔投票** [P2397 yyy loves Maths VI (mode) / 摩尔投票](https://www.luogu.com.cn/problem/P2397)
    - TODO:
  - 随机化。
    - TODO: [P3567 [POI 2014] KUR-Couriers](https://www.luogu.com.cn/problem/P3567)
    - TODO: [P11882 [RMI 2024] 彩虹糖 / Skittlez](https://www.luogu.com.cn/problem/P11882)
- 括号匹配
  - 栈。
    - 若 $[l,r]$ 形成合法括号序列，则 $[1,l)$ 和 $[1,r]$ 的栈相同。[P9753 [CSP-S 2023] 消消乐](https://www.luogu.com.cn/problem/P9753)
  - 合法括号序列形成树结构。
- 方差
  - $\frac 1 n \sum (x_i - \bar x)^2 = \frac 1 n \sum x_i^2 - \bar x^2$，转化为一次方和和二次方和的问题。
  - 方差只和差分数组有关。

# DP

- 背包
  - 生成函数。
  - 背包删除物品 [P4141 消失之物](https://www.luogu.com.cn/problem/P4141)
    - 把要删除的物品当成最后一个加入的物品，然后倒着做一次转移。
- 期望
  - 设随机变量，推出随机变量之间的关系，然后一起取期望。

# Binary

- **贪心**。
- 五个套路：
  - **拆位**。
  - **01 Trie**。
  - **线性基**。
  - **SOSDP**。
  - **FWT**。
- $\gcd(a,b) \le \lvert a-b \rvert \le a \oplus b \le a+b$。
- 把一个数 $x$ 一直做 $x \gets x \text{ and } k_i$，则 $x$ 发生变化的次数是 $O(\log V)$。$\text{or}$ 也一样。对于区间扩展类问题有用。
- 经典模型 TODO: 放链接
  - 集合的最大异或对
    - 01Trie 裸题。
  - 集合的最小异或对
    - 01Trie 裸题。
    - 根据结论【$x < y < z$，则 $\min(x \oplus y, y \oplus z) < x \oplus z$】。因此把集合排序，答案只会在相邻位置对出现。
  - 单点修改 & 高维前缀和
    - 有单次操作 $O(\sqrt V)$ 的做法。

# DS

- 区间查询
  - 能离线就考虑莫队。
  - 区间数颜色
    - TODO:
  - 区间第 $k$ 大 / 中位数
    - 二分。
      - TODO: 整体二分
    - 可持久化值域线段树。
- 并查集
  - **并查集生成树**
    - 原理：并查集启发式合并不破坏树结构。
    - 树高 $O(\log n)$。
      - 树高很小，所以可以可持久化。
    - 合理设计边权，当图论题做。[BZOJ4668 冷战](https://hydro.ac/p/bzoj-P4668)
  - **并查集操作树**
    - 类似 Kruskal 重构树的有新建节点的树。
  - 变种
    - 种类并查集
    - 可持久化并查集
    - 可撤销并查集
    - **序列并查集** [P1840 Color the Axis](https://www.luogu.com.cn/problem/P1840)
      - 上树 [P4092 [HEOI2016/TJOI2016] 树](https://www.luogu.com.cn/problem/P4092)
    - **倍增并查集** [P3295 [SCOI2016] 萌萌哒](https://www.luogu.com.cn/problem/P3295)
      - 上树 TODO:
- 逆序对
  - 长为 $n$ 的排列，逆序对数期望是 $\frac {n (n-1)} 4$。

# Tree

- TODO:
- LCA
  - TODO: [P4211 [LNOI2014] LCA](https://www.luogu.com.cn/problem/P4211)
  - $O(1)$ LCA
    - DFS 序上 ST 表。
  - 多点 LCA
    - $\text{LCA}(a_1, a_2), \cdots, \text{LCA}(a_{n-1}, a_n)$ 中深度最小的那个即为答案。一般用于区间 LCA 查询。[P11364 [NOIP2024] 树上查询](https://www.luogu.com.cn/problem/P11364)
    - 按 $dfn$ 排序，$\text{LCA}(a_1, a_n)$ 即为答案。
  - LCT 求 LCA
    - TODO:
- 树的直径
  - **边权非负**时，选择一条直径，树上离任意点 $u$ 最远的点必定是该直径的一个端点。
  - TODO:
- 树的重心
  - 以树的重心为根时，所有子树的大小都不超过整棵树大小的一半。
  - TODO:
- 树上背包时间复杂度是 $O(nm)$ 的。
- 点集的导出子树
  - 把点集按 DFS 序排序。
- 边 $(u,v)$ 在路径 $x \leftrightsquigarrow y$ 上
  - 以 $u$ 为根，$v$ 的子树中只能有 $x$ 和 $y$ 中的一个。[#207. 共价大爷游长沙](https://uoj.ac/problem/207)
- 树上路径求交
  - 求是否有交 [P3398 仓鼠找 sugar](https://www.luogu.com.cn/problem/P3398)
    - LCA。有交的充要条件是有一条路径 LCA 在另一条路径上。
    - 树剖暴力做。
  - 如果要求具体交的是哪段，[LCA 也可以做](https://www.luogu.com/article/o2cqlmfa)。
- 树上 $2k$ 个关键点配对使得每对的路径无公共边，方法是唯一的。对每条边考虑其两边关键点数奇偶性。[P14309 【MX-S8-T2】配对](https://www.luogu.com.cn/problem/P14309)
- 随机树
  - 随机树树高 $\Theta(\sqrt n)$。
  - 随机父亲树树高 $\Theta(\log n)$。

# Graph

- 最小生成树
  - Prim、Kruskal、和 Borůvka。
    - 特殊性质图，选一个魔改。
    - 有类似 Dijkstra 一样的贪心结构时，使用 Prim。
    - 有修改需要多次求最小生成树时，使用 Kruskal，预先排序。可能结合归并使用。[P14362 [CSP-S 2025] 道路修复](https://www.luogu.com.cn/problem/P14362) [P5633 最小度限制生成树](https://www.luogu.com.cn/problem/P5633)
    - 特殊性质完全图最小生成树，使用 Borůvka。
  - LCT 可以动态维护最小生成树，支持加边操作。
- 最短路
  - 最短路 DAG。
    - 最短路树的计数是最短路 DAG 的树形图计数，Matrix-Tree 定理解决。
- 瓶颈路
  - 最小生成树是最小瓶颈树。
  - 离线按边权排序加边。
  - Kruskal 重构树。
- 平面图
  - 是稀疏图，$m \le 3n-6$。
  - 转对偶图。
    - 平面图最小割等于对偶图最短路。
  - 网格图是特殊的平面图。

# String

- 字符串匹配
  - TODO:
- LCP
  - TODO:
- 回文子串
  - 枚举回文中心。
  - PAM。
    - 本质不同回文子串数量是 $O(n)$ 的。
- Periodicity Lemma
  - 本质是 Math 模块里的双模数结构。

# Math

- 容斥原理
  - TODO:
- $\gcd$
  - 对不同质因数分开考虑，每个质因数当成指数上的 $\min$。
  - 多个数 $\gcd$
    - 辗转相除，时间复杂度 $O(n + \log V)$，不是 $O(n \log V)$。[P3794 签到题IV](https://www.luogu.com.cn/problem/P3794)
  - 把一个数 $x$ 一直做 $x \gets \gcd(x, k_i)$，则 $x$ 发生变化的次数是 $O(\log V)$。对于区间扩展类问题有用。
- 双模数 [P5330 [SNOI2019] 数论](https://www.luogu.com.cn/problem/P5330)
  - 即 $x \bmod p$ 和 $x \bmod q$ 同时出现。在 $\bmod q$ 下考虑，建图 $i \to (i + p) \bmod q$，则形成 $\gcd(p,q)$ 个环。
  - [自己写的文章](https://www.luogu.com.cn/article/cz8shjvu)。
  - 多模数
    - 同余最短路。[P3403 跳楼机](https://www.luogu.com.cn/problem/P3403)
- 没用的东西
  - Catalan 数
    - $C_n = \frac {4n+2} {n+1} C_{n-1} = \frac 1 {n+1} \binom {2n} n$
    - $n$ 个节点的二叉树个数。
  - Vandermonde determinant $\prod\limits_{i<j} (a_i - a_j)$
    - 值域小可以对于值域数组 FFT；值域大没有实用做法。

# 博弈论

# Ad-hoc

- 一个问题的加法版本有简单解法，现在要解决乘法版本时，可以考虑对数。[P4926 [1007] 倍杀测量者](https://www.luogu.com.cn/problem/P4926)
  - 模意义下可以用原根取对数。[CF487C Prefix Product Sequence](https://www.luogu.com.cn/problem/CF487C)
- $\forall k \in [1, \frac {n (n+1)} 2]$，$k$ 可以被表示为不重复的 $[1,n]$ 中数的和。[P11895 「LAOI-9」Sequence](https://www.luogu.com.cn/problem/P11895)