---
title: 'Cycle Space 与 Cut Space'
date: 2025-08-15
permalink: /posts/2025/08/2025-08-15-Cycle-Space-与-Cut-Space/
excerpt: "讲解了无向图的 cycle space 和 cut space 的性质，并且尝试在有向图的情况进行类比。"
tags:
  - OI
---

# About This Post

我学线性基的时候，被这题 [P4151 [WC2011] 最大XOR和路径](https://www.luogu.com.cn/problem/P4151) 创死过一次（毕竟是线性基的经典例题）。我感觉到这题背后有很精妙的数学结构，但是看题解区并没有让我理解。

后来学物理学到 Kirchhoff 定律，平面电路只要分析网眼就行。我感觉这两者背后似乎是同一种结构，但是我依然没有搞明白为什么这么构造就是对的。

上高开的 OI 课的时候，被这两题 [P10778 BZOJ3569 DZY Loves Chinese II](https://www.luogu.com.cn/problem/P10778) & [CF1515G Phoenix and Odometers](https://www.luogu.com.cn/problem/CF1515G) 再次创飞。前一题的随机化令我印象非常深刻，后一题则是扩展了这种模型在有向图上的情况。

一气之下，这篇笔记就诞生了。

# Prerequisite Knowledge

- 无向图和有向图的 Euler 回路：[P7771 【模板】欧拉路径](https://www.luogu.com.cn/problem/P7771)
- 图论中关于生成树的基本知识。
- 线性代数的基本知识。
- 例题中需要的内容：
  - 异或线性基：[P3812 【模板】线性基](https://www.luogu.com.cn/problem/P3812)。
  - 电路的 Kirchhoff 定律的基本表述。
  - 数论的 Bézout 定理。

# Insight

> [P4151 [WC2011] 最大XOR和路径](https://www.luogu.com.cn/problem/P4151)
>
> 给定一张无向图，边有边权，求一条 $1 \rightsquigarrow n$ 的路径，使得路径上的所有边的异或和最大。
>
> $n \le 5 \times 10^4$，$m \le 10^5$，值域 $10^{18}$。

注意到一条路径走两遍可以抵消。假设我们已有一条路径，可以先走到一个环上，走一遍环，然后再原路返回，这样就只增加了环的贡献。也就是说，我们可以在一条路径的基础上，异或任意环。（初始路径是可以任选的，因为假设有一条路径比原路径更优，我们总能异或上一个环变成新路径）

定义 Euler 图为每个连通块都存在 Euler 回路的图。刚才的问题也可以看出是再一条路径上加了一个 Euler 子图。

这就引出了本文的主要目标：**我们希望刻画一个图中的所有 Euler 子图组成的数学结构**。

btw，这个结构在物理学中也是有用处的。Kirchhoff 电压定律的计算就是基于相关的理论，等会儿详细分析。

# Cycle Space & Fundamental Cycle Basis

为了方便分析，我们假设图连通。

遵循上面那题的想法，定义一张图的两张子图之间的异或运算 $A \oplus B$：仅保留要么出现在 $A$ 中要么出现在 $B$ 中的边，$A,B$ 的公共边删除。

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Cycle_space_addition.svg/720px-Cycle_space_addition.svg.png" width=400>

（图源：Wikipedia）

不难发现 **Euler 子图对 $\oplus$ 运算封闭**。一个偶度数节点异或上对应的偶度数节点，一定还是偶度数节点。

寻找 Euler 子图空间的其他性质：
- 令加法定义为 $\oplus$。
  - 封闭性已经满足。
  - 结合律显然。
  - 交换律显然。
  - 加法单位元是空图。
  - 加法逆元是元素自身。
- 令数乘基于 $\mathbb F_2$ 的域。性质是平凡的。

这让 Euler 图的集合构成了一个**线性空间**，因此这个结构被称为 **cycle space（环空间 / 环路空间）**。

要研究一个线性空间我们就要~~搞基~~，找到它的一组基。

一个经典的构造：**任选一棵生成树，所有仅包含一条非树边的环（基环 / 本原环）构成这个空间的一组基，称为 fundamental cycle basis**。记为 $B$，每个基环记作 $B_1, B_2, \cdots$。

如何证明？考虑基的定义：
- 线性无关。
- 生成律：张成整个空间，即空间中的每个元素都是基的线性组合。

逐一证明。

- 线性无关：我们要说明 $\sum\limits_i \alpha_i B_i = \vec{0}$ 只能 $\alpha = \vec{0}$。考察某一条非树边，这条非树边在左侧只有来自自己基环的贡献，而在右侧是 $0$。说明这个基环不能选。对所有非树边都这样分析，得到所有基环都不能选，即 $\alpha = \vec{0}$，得证。

- 生成律：可以证明，一张 Euler 子图 $E$ 可以由它经过的那些非树边对应的基环 $\oplus$ 得到。证明是，先把 $E$ 异或上刚刚提到的所有环，此时 $E$ 是一张只有树边的 Euler 子图。但是树是没有环的，所以这样的图只能是空图。

推论：连通图的 cycle space 的 dimension 为 $m-n+1$（非连通图为 $m-n+c$，$c$ 为连通块数）。

总结：
- Euler 子图对 $\oplus$ 运算封闭。
- Euler 子图构成线性空间，称为 cycle space。
- 通过一棵任意的生成树，可以构造 cycle space 的一组基，这组通过生成树构造的基名为 fundamental cycle basis。

由于异或这个运算天然带有 $\bmod 2$，因此 fundamental cycle basis 对于跟奇偶性和位运算相关的题杀伤力很强。

# Related Questions

## [P4151 [WC2011] 最大XOR和路径](https://www.luogu.com.cn/problem/P4151)

开篇例题。

我们找到 fundamental cycle basis，把每个环自己的异或和扔进一个异或线性基，用初始路径的异或和查询出最大值即可。

## Kirchhoff's Voltage Law

> 令 $n$ 为电路的点数，$m$ 为电路的边数。为什么平面上的 Kirchhoff 电压定律只要取所有网眼分析？在任何情况下为什么只需要 $m-n+1$ 个方程，非平面情况下如何选取这些方程？

对于平面的情况，所有网眼就构成 fundamental cycle basis，可以组合出任意回路。

对于非平面的情况，按照非树边选择 fundamental cycle basis 即可。~~但是脑子正常的题目是不会出现这种东西的~~。

一般的电路只有一个连通块，非树边数量是 $m-n+1$，也就恰好只能写出这个数量的方程。再配合 Kirchhoff 电流定律的 $n-1$ 条方程和 Ohm 定律，就可以刚好解出整个电路的情况。

如果你非要弄一个 $c$ 个连通块的电路，你就需要 $m-n+c$ 个方程。

## [CF19E Fairy](https://www.luogu.com.cn/problem/CF19E)

> 给出一张稀疏无向图，求删除一条边后此图变成二分图的所有方案。
>
> 没有重边和自环。
>
> 需要一个 $O(n)$ 的做法。

首先排除掉一个平凡的情况：原图已经是二分图，删任何一条边都对。

二分图就是不存在奇环的图。因此，我们要删掉一条边破坏掉所有奇环，即这条边属于所有奇环的交集（必要条件）。

只有一个奇环的情况也是平凡的，奇环上任选一条边删掉即可，排除掉。

注意到一些性质：对于两个有交的环，
- 偶环异或偶环是偶环。
- 偶环异或奇环是奇环。
- 奇环异或奇环是偶环。

对于一条非树边，称其基环中的树边被其覆盖。

定义基环为奇环的非树边为“坏边”，为偶环的非树边为“好边”。删掉的边必定被所有坏边覆盖（因此删掉的必为树边）。但这只是必要条件，我们尝试找到充要条件。

考虑一条**被所有坏边覆盖**但**不被任何好边覆盖**的边 $e$。若一个环 $R$ 是奇环，则必定含有 $e$ 这条边，因为 $R$ 的分解包含奇数个奇环，异或之后必定会留下 $e$。

特意考虑“不被任何好边覆盖”是因为：偶环不会对 $R$ 的奇偶性造成贡献，但是对 $e$ 是否留在 $R$ 上有贡献。

事实上这就是充要条件：**排除掉两种平凡情况时，不被任何好边覆盖且被所有坏边覆盖的边是答案**。

为什么答案边**不能被好边覆盖**：我们可以构造一个没有被删掉的奇环。假设有一条边 $e$ 又被好边覆盖又被坏边覆盖，对于经过这条边的偶环 $E_e$ 和奇环 $E_o$，$E_e \oplus E_o$ 必然是一个奇环而且不包含 $e$，也就是说奇环没删干净。

证完了。维护坏边好边的覆盖情况用树上差分即可。选择生成树时使用 DFS 树，保证所有非树边都是返祖边就免掉求 LCA 了，时间复杂度 $O(n)$。

# Cut Space

这个地方引入有点突兀，但是限于我的线代知识我不知道怎么合适的引出接下来的内容。后面会展示 cycle space 和 cut space 的联系——它们互为 orthogonal complement。

把图 $G$ 的点集 $V$ 分为两份 $V_1 \sqcup V_2$，我们把所有横跨 $V_1,V_2$ 的边组成的集合称为 $G$ 的一个**割集**。

我们依然只考虑连通图。

和 cycle space 一样，我们考虑找出连通图的一棵生成树，然后研究非树边。

对于这棵生成树自身，我们发现树的边集 $E$ 的任何自己都是一个割集，而且对应划分 $V_1,V_2$ 是唯一的。

也就是说，通过寻找 $E' \subseteq E$，我们唯一确定 $V_1, V_2$ 的划分，同时也确定了非树边是否属于这个割集（覆盖了奇数条 $E'$ 中的边的非树边属于这个割集）。

很显然我们已经发现生成树上的每条边互相独立，割集组成的集合应该和环路空间一样是一个线性空间。我们尝试依然使用 $\oplus$ 运算说明这一点：

**割集 $C_1,C_2$ 的异或 $C_1 \oplus C_2$ 仍然是割集。若两个生成树的子集 $E_1,E_2$ 对应的割集分别为 $C_1,C_2$，则 $E_1 \oplus E_2$ 对应的割集为 $C_1 \oplus C_2$**。

证明：若一条非树边 $e$ 满足要么覆盖奇数条 $E_1$ 的边（$e \in C_1$）要么覆盖奇数条 $E_2$ 的边（$e \in C_2$），则它一定属于 $C_1 \oplus C_2$，而且覆盖奇数条 $E_1 \oplus E_2$ 的边。得证。Cut space 的 dimension 是 $n-1$（对于不连通图是 $n-c$，$c$ 为连通块数量）。

因此，**割集构成线性空间**，称为 **cut space**。我们对生成树的每条边 $e$ 定义 $f(e)$ 为 $e$ 和覆盖 $e$ 的非树边组成的边集，则所有 $f(e)$ 构成 cut space 的一组基。

接下来有一个很重要的性质，把上下文串了起来：**cycle space 和 cut space 互为 orthogonal complement**。

考虑一条树边 $e_1$ 和一条非树边 $e_0$，对应的 cut space 和 cycle space 的 basis 上的元素分别为 $v_1$ 和 $v_2$。若 $e_1$ 不被 $e_0$ 覆盖，则 $v_1 \cap v_2 = \varnothing$；反之，$v_1 \cap v_2 = \{e_1, e_0\}$。不论哪种情况，$\vec{v_1} \cdot \vec{v_2} = 0$，满足 orthogonal。同时两个空间的 dimension 之和为 $m$，因此两个空间构成 orthogonal complement。

总结：
- 割集对 $\oplus$ 封闭。
- 割集构成线性空间，称为 cut space。
- Cut space 的基也可以通过生成树构造。
- Cycle space 和 cut space 互为 orthogonal complement。

## [P10778 BZOJ3569 DZY Loves Chinese II](https://www.luogu.com.cn/problem/P10778)（论文题）

> 给定一张无向图，$q$ 次询问每次给定一个边集，求删除该边集后图是否连通。保证边集大小不超过 $15$。
>
> $n \le 10^5$，$m \le 5 \times 10^5$，$q \le 5 \times 10^4$。**强制在线**。
>
> 注：若可以离线，有线段树分治+可撤销并查集的确定性做法。而且似乎不受边集大小限制。
>
> 更热闹的多倍经验题，都可以离线：[P5227](https://www.luogu.com.cn/problem/P5227)、[P10075](https://www.luogu.com.cn/problem/P10075)。

我们要判断一个边集是否**包含**割集。包含有点困难，我们先考虑怎么判断一个边集是否是割集。

一个边集属于 cut space，当且仅当它和任意环的 $\bmod 2$ 下内积为 $0$，这是 orthogonal complement 的性质。

我们希望我们的边集投影在任何一个基环上都是 $0$。这意味着对于每一个基环，我们的边集在奇环上的出现边数是偶数。

令 $t$ 为 cycle space 的 dimension。我们可以给每一条边 $e$ 设置一个 $t$ 维向量 $v(e)$ 表示 $e$ 在 cycle space 下的坐标，$v(e)_i$ 表示 $e$ 是否出现在第 $i$ 个基环内。若一个边集是割集，则其所有边的 $v$ 向量之和是 $0$ 向量。这是一个充要条件。

但是代码中我们无法这么实现，因为 $t$ 非常大。我们使用**随机化**——给每一维一个 $2^{64}$ 以内的随机权，一个向量使用所有 $1$ 位的权值异或和表示。如果最终一个边集的异或和是 $0$（**必要不充分条件**），我们就认为它是一个割集。由于这题询问的边集非常小，只有 $15$，所以错误率并不高，可以忽略。

回到原题，怎么判断有没有包含割集？异或线性基，搞定。

# Cycle Space on Directed Graph

我们修改 Euler 图的定义为**每个结点的入度等于出度的图**。可以证明这样的图可以表示为若干个简单环的不交并。

考虑到强连通分量缩点之后得到的是 DAG 没有环，所以接下来我们只考虑强连通图。

有向图的 cycle space 没有特别好的性质，但是在特殊的条件之下（例如边权 $\bmod m$）还是有和无向图的类比的。结合例题一起看：

> [CF1515G Phoenix and Odometers](https://www.luogu.com.cn/problem/CF1515G)（论文题）
>
> 给定一个有 $n$ 个点 $m$ 条边的有向图，边带边权。
> 有 $q$ 次询问，每次询问会给出三个参数 $v,s,t$，你需要回答是否存在一条含有 $v$ 的环使得该环的边权和对 $t$ 取模后为 $s$。
>
> $1 \le n,m,q \le 2 \times 10^5$。

首先依然是缩点之后只考虑强连通图的情况。

**结论：强连通图中，对任意模数 $m$，若路径 $u \rightsquigarrow v$ 在 $\bmod m$ 的长度为 $s$，则必定存在 $v \rightsquigarrow u$ 在 $\bmod m$ 长度为 $-s$**。也就是说走过的路可以无损地走回来。

- 构造性证明：任意找一条路径 $v \rightsquigarrow u$。考虑一条路径包含 $m-1$ 个 $u \rightsquigarrow v$ 和 $m$ 个 $v \rightsquigarrow u$，显然边权和为 $-s$。

此时其实已经某种程度上变成无向图问题了，我们要求环的线性组合。而且此题天生带有线性空间的结构——Bézout 定理揭示了这一点。此时问题转化为求所有 Euler 子图长度的 $\gcd$。

我们在这个无向图上找一棵根为 $r$ 的生成树（$r$ 是随便定的），仿照前面的做法选择仅包含一条非树边的简单环。我们猜测**任何一个 Euler 子图的长度可以被表示为这些简单环长度的线性组合**。

证明：对于一条非树边 $u \to v$ 边权为 $w$，它的“有向”基环长为 $dep_u + w - dep_v$（$r \leftrightsquigarrow \text{LCA}(u,v)$ 这段来回被抵消）。考虑一个 Euler 子图经过 $k$ 条非树边，则这个图的长度为 $\sum\limits_i dep_{u_i} + w_i - dep_{v_{i+1}}$（特别地 $v_{k+1} = v_1$）。我们发现把 $v$ 整个平移一下整个式子就变成 $\sum\limits_i dep_{u_i} + w_i - dep_{v_i}$，恰好就是这些“有向”基环的权值和。

因此，对树上的每一个“有向”基环求出环长 $dep_u + w - dep_v$，取 $\gcd$，即为树上所有 Euler 子图的权值 $\gcd$。

总结：
- 无向图对每个连通块（或者每个边双连通分量）考虑问题，有向图对每个强连通分量考虑问题。
- 有向图的 Euler 子图性质不如无向图，但是在 $\bmod$ 意义下有类似的结论。
- $\bmod$ 意义下，寻找非树边构造基的思路依然成立。

# References

- [国家集训队 2023 论文集 - 万成章《综述图论中连通性及相关问题的一些处理方法》](https://github.com/enkerewpo/OI-Public-Library/blob/master/IOI%E4%B8%AD%E5%9B%BD%E5%9B%BD%E5%AE%B6%E5%80%99%E9%80%89%E9%98%9F%E8%AE%BA%E6%96%87/%E5%9B%BD%E5%AE%B6%E9%9B%86%E8%AE%AD%E9%98%9F2023%E8%AE%BA%E6%96%87%E9%9B%86.pdf)
  - 国内对于这方面的资料不是很多，事实上这篇文章很大一部分内容来源是这篇论文。orz
  - [【学习笔记】《综述图论中连通性及相关问题的一些处理方法》 - APJifengc](https://www.cnblogs.com/apjifengc/p/18034638)
- Wikipedia
  - [Cycle space - Wikipedia](https://en.wikipedia.org/wiki/Cycle_space)
  - [Cycle basis - Wikipedia](https://en.wikipedia.org/wiki/Cycle_basis)
  - [Cut (graph theory) - Wikipedia](https://en.wikipedia.org/wiki/Cut_(graph_theory))
- [题解 CF19E 【Fairy】 - command_block](https://www.luogu.com.cn/article/c9mfsmzr)
- [环路与割、图的同调，以及不可思议的生活 - yyc樱初音](https://zhuanlan.zhihu.com/p/681987899)
  - [DZY Loves Chinese II 证明 - 博客 - rushcheyo的博客](https://rushcheyo.blog.uoj.ac/blog/6704)
- 感谢 ChatGPT，在读论文的过程中给了我很大帮助。