# Basic

- 考虑答案是否仅与**差分**数组有关。
  - $a_{i-1} + a_{i+1} - 2 a_i = (a_{i+1} - a_i) - (a_i - a_{i-1})$。
- 考虑答案是否与**顺序**有关。
  - 若否，则排序 / 开桶。
- 考虑答案是否可以**二分**。
- **调和级数**：$\sum_{i=1}^n \frac 1 i \in \Theta(\log n)$。
- **最小不同和**：若干个正整数之和为 $n$，则去重之后只有 $O(\sqrt n)$ 个。
  - $> \sqrt n$ 的只有 $O(\sqrt n)$ 个；$\le \sqrt n$ 的通常可以预处理。

# Brute Force

- 枚举所有两两配对
  - 枚举全排列，将 $a_i$ 和 $a_{i \oplus 1}$ 配对。

# Calculation on a Sequence

- 偏序
  - 二维偏序
    - 对于每一对偏序关系 $(x_i, y_i) \prec (x_j, y_j)$，删除掉较小的 $(x_i, y_i)$。则剩余的元素中，按照 $x$ 递增排序后 $y$ 递减。[P2900 [USACO08MAR] Land Acquisition G](https://www.luogu.com.cn/problem/P2900)
      - 把区间嵌套视为二维偏序，也适用这个结论。左端点递增时，右端点也递增。[P14255 列车（train）](https://www.luogu.com.cn/problem/P14255)
  - Dilworth 定理。
- $f(1), \cdots, f(n)$ 不同的元素个数
  - 若 $f$ 具有单调性，则等价于求 $f(i) \ne f(i+1)$ 的个数。
- **对于所有子区间**
  - 固定一个端点，另一个端点扩展。
    - 固定 $r$ 扩展 $l$，统计出某些本质不同的扩展位置。然后 $r$ 移动到 $r+1$ 时继承。[P3794 签到题IV](https://www.luogu.com.cn/problem/P3794)
  - 通过前缀信息推区间信息。[P9753 [CSP-S 2023] 消消乐](https://www.luogu.com.cn/problem/P9753)
  - DP，设 $f_i$ 为所有以 $i$ 为右端点的区间的答案。
  - 分治。
  - 摊贡献。TODO:
    - 对所有子区间数颜色求和：$\sum_{i=1}^n (n-i+1) (i - pre_i)$。[[ABC371E] I Hate Sigma Problems](https://www.luogu.com.cn/problem/AT_abc371_e)
- 绝对众数
  - **摩尔投票** [P2397 yyy loves Maths VI (mode) / 摩尔投票](https://www.luogu.com.cn/problem/P2397)
    - 区间摩尔投票
      - TODO:
  - **在绝对众数存在的前提下**（因此要验证答案），拆二进制位，每一位上的绝对众数就是绝对众数的这一位。[P11882 [RMI 2024] 彩虹糖 / Skittlez](https://www.luogu.com.cn/problem/P11882)
  - **随机化**。**在绝对众数存在的前提下**（因此要验证答案），随机取一个数有 $\frac 1 2$ 以上概率取到绝对众数，多取几次即可。[P3567 [POI 2014] KUR-Couriers](https://www.luogu.com.cn/problem/P3567)
  - 把一个区间均分成两半，那么绝对众数一定至少在一半里是绝对众数。
  - 前缀本质不同绝对众数的量级是 $O(\log n)$ 的。
- 括号匹配
  - 栈。
    - 若 $[l,r]$ 形成合法括号序列，则 $[1,l)$ 和 $[1,r]$ 的栈相同。[P9753 [CSP-S 2023] 消消乐](https://www.luogu.com.cn/problem/P9753)
  - 合法括号序列形成树结构。
- 方差
  - $\frac 1 n \sum (x_i - \bar x)^2 = \frac 1 n \sum x_i^2 - \bar x^2$，转化为一次方和和二次方和的问题。
  - 方差只和差分数组有关。
    - 对于一个已知差分数组元素但不知顺序的序列，方差最小时差分数组必定先减后增。[P7962 [NOIP2021] 方差](https://www.luogu.com.cn/problem/P7962)
- 任意排列与前缀和值域
  - 若一列数的值域在 $[L,R]$ 内，且它们的和也在 $[L,R]$ 内，则必定存在一种排列方式，使得每一个前缀和（除了第一个 $S_0 = 0$ 以外）都落在 $[L,R]$ 内。[P9207 灭罪「正直者之死」](https://www.luogu.com.cn/problem/P9207) [P14508 猜数游戏 guess](https://www.luogu.com.cn/problem/P14508)

# DP

- 背包
  - 背包删除物品 [P4141 消失之物](https://www.luogu.com.cn/problem/P4141)
    - 把要删除的物品当成最后一个加入的物品，然后倒着做一次转移。
    - 可行性背包删除物品
      - 随机化。在大模数 $p$ 意义下做计数的背包，然后 check 是否 $=0$。该技巧来自 [CF 文章](https://codeforces.com/blog/entry/100910)。
  - 生成函数。
- 期望
  - 设随机变量，推出随机变量之间的关系，然后一起取期望。
- 转移只依赖于一项的 DP，构成一棵树。[P11770 檐牙覆雪](https://www.luogu.com.cn/problem/P11770)

# Greedy

- 多重排队接水 [P7391 「TOCO Round 1」自适应 PVZ](https://www.luogu.com.cn/problem/P7391)
  - 设区间左闭右开 $[l,r)$，按右端点排序，用 multiset 维护，每次找到第一个 $\le l$ 的右端点来接替。

# Binary

- 五个套路：
  - **拆位**。
  - **01 Trie**。
    - 01 Trie 可以合并，类似线段树合并。
    - 01 Trie 全局 $\pm 1$
      - 01 Trie 全局 $\pm k$ [P11160 【MX-X6-T6】機械生命体](https://www.luogu.com.cn/problem/P11160)
      - TODO:
  - **线性基**。
  - **SOSDP**。
  - **FWT**。
- 从高位到低位**贪心**。
- $\gcd(a,b) \le \lvert a-b \rvert \le a \oplus b \le a+b$。
- 前缀本质不同 $\text{and}$ 和本质不同 $\text{or}$ 都只有 $O(\log V)$ 个。[P3794 签到题IV](https://www.luogu.com.cn/problem/P3794)
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
    - 处理 $pre_i$ 数组表示 $i$ 左侧第一个与 $i$ 同色的位置。颜色数等于 $\sum_{i=l}^r [pre_i < l]$。
  - 区间第 $k$ 大
    - 二分。
      - TODO: 整体二分
    - 可持久化值域线段树。
- 中位数
  - 二分答案，小于等于的设成 $-1$，大于的设成 $+1$，转变成加法的问题。[P11761 [IAMOI R1] 明码标价](https://www.luogu.com.cn/problem/P11761)
- 偏序降维变时间轴
  - TODO:
- **分块**
  - TODO:
- $\text{mex}$
  - TODO:
- 区间询问对于所有子区间
  - 历史和线段树
    - TODO: [P14523 【MX-S11-T4】Ice Drop](https://www.luogu.com.cn/problem/P14523)
- 并查集
  - **并查集生成树**
    - 原理：并查集启发式合并不破坏树结构。
    - 树高 $O(\log n)$。
      - 树高很小，所以可以可持久化。
    - 合理设计边权，当图论题做。[BZOJ4668 冷战](https://hydro.ac/p/bzoj-P4668)
  - **并查集操作树**
    - 类似 Kruskal 重构树的有新建节点的树。[T360101 大茶馆](https://www.luogu.com.cn/problem/T360101)
  - 变种
    - 种类并查集
    - 可持久化并查集
    - 可撤销并查集
    - **序列并查集** [P1840 Color the Axis](https://www.luogu.com.cn/problem/P1840)
      - 上树 [P4092 [HEOI2016/TJOI2016] 树](https://www.luogu.com.cn/problem/P4092)
    - **ST 表并查集** [P3295 [SCOI2016] 萌萌哒](https://www.luogu.com.cn/problem/P3295)
      - 上树（**倍增并查集**） [P13528 [OOI 2023] Gasoline prices / 油价](https://www.luogu.com.cn/problem/P13528)
- 颜色段均摊
  - 每次操作会减少很多颜色段，但只会增加 $O(1)$ 个颜色段。[P4690 [Ynoi2016] 镜中的昆虫](https://www.luogu.com.cn/problem/P4690)
  - TODO: [P11833 [省选联考 2025] 推箱子](https://www.luogu.com.cn/problem/P11833)

# Tree

- LCA
  - $\text{LCA}(u,v)$ 可以看作：把根到 $u$ 的路径上全部节点染色，求 $v$ 的最近染色祖先。
    - $dep_{\text{LCA}(u,v)}$ 可以看成根到 $v$ 的路径上的染色节点个数。[P4211 [LNOI2014] LCA](https://www.luogu.com.cn/problem/P4211)
  - $O(1)$ LCA
    - DFS 序上 ST 表。
  - 多点 LCA
    - $\text{LCA}(a_1, a_2), \cdots, \text{LCA}(a_{n-1}, a_n)$ 中深度最小的那个即为答案。一般用于区间 LCA 查询。[P11364 [NOIP2024] 树上查询](https://www.luogu.com.cn/problem/P11364)
    - 按 $dfn$ 排序，$\text{LCA}(a_1, a_n)$ 即为答案。
  - LCT 求 LCA
    - TODO:
- 子树
  - 子树在 DFS 序上是连续区间。
- 树的直径（树的最长链）
  - 边权非负时，选择一条直径，树上离任意点 $u$ 最远的点必定是该直径的一个端点。
  - TODO:
- 树的重心（以它为根时最大子树最小的点）
  - 重心有 $1$ 个或 $2$ 个，若有 $2$ 个则相邻。
  - 以树的重心为根时，所有子树的大小都 $\le \frac n 2$。
  - 重心到所有点的距离和最小。[P1395 会议](https://www.luogu.com.cn/problem/P1395)
  - 把两棵树加一条边连起来，新树重心在原来两树各自重心的连线上。
  - 在树上添加或删除一个叶子，重心最多移动一条边的距离。
- 树上背包时间复杂度是 $O(nm)$ 的。
- 点集的导出子树
  - 把点集按 DFS 序排序。
- 树上删边后形成连通块
  - 树上连通块数等于 $V - E$。
    - 树上一个子图是连通块，当且仅当 $V - E = 1$。
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
  - 对于一条不出现在最小生成树上的边，再多加边它也不会出现在最小生成树上。[P14362 [CSP-S 2025] 道路修复](https://www.luogu.com.cn/problem/P14362)
  - LCT 可以动态维护最小生成树，支持加边操作。
- 最短路
  - 最短路 DAG。
  - 数据量小的图上 DP 题可能会直接开头跑个多源最短路作为预处理。
- 不要忘记建反图。
- 可达性
  - 稠密图 Floyd $O(\frac {n^3} w)$，稀疏图 Tarjan $O(\frac {nm} w)$。
  - TODO:
- 瓶颈路
  - 最小生成树是最小瓶颈树。
  - 离线按边权排序加边。
  - Kruskal 重构树。
- 环路空间
  - 用线性代数思想刻画图里的欧拉子图结构。
  - 和异或运算可以出在一起。[P4151 [WC2011] 最大XOR和路径](https://www.luogu.com.cn/problem/P4151)
  - 随机化。[P10778 BZOJ3569 DZY Loves Chinese II](https://www.luogu.com.cn/problem/P10778)
  - 有向图也可以做。[CF1515G Phoenix and Odometers](https://www.luogu.com.cn/problem/CF1515G)
- 平面图
  - 是稀疏图，$m \le 3n-6$。
  - 转对偶图。
    - 平面图最小割等于对偶图最短路。[P4001 [ICPC-Beijing 2006] 狼抓兔子](https://www.luogu.com.cn/problem/P4001)
  - 网格图是特殊的平面图。

# String

- Border 与 Period 理论
  - Border 和 period 一一对应。
  - 一个长为 $n$ 的字符串的所有 border 长度构成 $\lfloor \log_2 n \rfloor$ 个等差数列。
    - 可以直接按二进制最高位分组，每一组里一定是等差数列。
    - 用于 DP 等问题中对 border 批量处理。[P1393 Mivik 的标题](https://www.luogu.com.cn/problem/P1393)
  - (Weak) Periodicity Lemma
    - 本质是 Math 模块里的双模数结构。
- **子串是后缀的前缀**。
  - $A$ 的子串是 $B$ 的前缀，相当于 $A$ 的某个后缀和 $B$ 有公共前缀。这是 exKMP 的结构。[P3893 [GDOI2014] Beyond](https://www.luogu.com.cn/problem/P3893)
- **SA 与 SAM**
  - **有字典序的需求用 SA；只关心数学结构用 SAM**。
    - 特别地，SA 的 height 数组也给出了一部分数学结构。所以**涉及到 LCP 的问题也可以考虑 SA**。
  - SAM 不仅是后缀自动机，更是子串自动机。
  - 最小表示法 / $k$ 小表示法
    - SA。
- 回文子串
  - **枚举回文中心**。
    - 很多时候可以**二分**。
  - PAM。
    - 本质不同回文子串数量是 $O(n)$ 的。

# Math

- 有一个量很小的时候，可能是容斥原理。
- 二项式反演
  - 设出要求的 $f$ 后，考虑 $\sum \binom n i f_i$（**至多**）或 $\sum \binom i n f_i$（**至少**）的组合意义。
- $\gcd$
  - 求和式中往往可以枚举 $\gcd$。
  - 对不同质因数分开考虑，每个质因数当成指数上的 $\min$。
  - 多个数 $\gcd$
    - 辗转相除，时间复杂度 $O(n + \log V)$，不是 $O(n \log V)$。[P3794 签到题IV](https://www.luogu.com.cn/problem/P3794)
  - 前缀本质不同 $\gcd$ 只有 $O(\log V)$ 个。[P3794 签到题IV](https://www.luogu.com.cn/problem/P3794)
- $\lfloor \frac n x \rfloor$
  - 有 $O(\sqrt n)$ 个取值。数论分块。
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

# Network Flow

TODO:

- 常见建模
  - $n \times n$ 棋盘，选出不同行不同列的 $n$ 个格子
    - 相当于行和列的二分图匹配。

# Game Theory

- Sprague–Grundy 函数
  - 适合处理的情况：
    - 游戏有明显的子问题结构
    - 多个游戏一起玩
  - 很可能打表能看出规律。
    - 会出现类似“$n > 68$ 后有长度为 $34$ 的循环节”的抽象规律。[HDU4664 Triangulation](https://vjudge.net/problem/HDU-4664)
  - 把 SG 转移式看成 DP，使用普通的 DP 优化。
  - Anti 游戏 [P4279 [SHOI2008] 小约翰的游戏](https://www.luogu.com.cn/problem/P4279)
- SG 函数搞不定的话，应该就是 Ad-hoc 了。祝好运！

# Ad-hoc

- 一个问题的加法版本有简单解法，现在要解决乘法版本时，可以考虑对数。[P4926 [1007] 倍杀测量者](https://www.luogu.com.cn/problem/P4926)
  - 模意义下可以用原根取对数。[CF487C Prefix Product Sequence](https://www.luogu.com.cn/problem/CF487C)
- $\forall k \in [1, \frac {n (n+1)} 2]$，$k$ 可以被表示为不重复的 $[1,n]$ 中数的和。[P11895 「LAOI-9」Sequence](https://www.luogu.com.cn/problem/P11895)