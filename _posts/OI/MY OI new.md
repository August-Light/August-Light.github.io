# Basic

- 考虑答案是否仅与**差分**数组有关。
- 考虑答案是否与**顺序**有关。
  - 若否，则排序 / 开桶。
- 考虑答案是否可以**二分**。
- 考虑值域数组能否变为 $01$ 数组。

# 序列上统计

- 对于所有子区间
  - 分治。
  - 固定一个端点，另一个端点扩展。
    - 固定 $r$ 扩展 $l$，统计出某些本质不同的扩展位置。然后 $r$ 移动到 $r+1$ 时继承。[P3794 签到题IV](https://www.luogu.com.cn/problem/P3794)

# Binary

- **贪心**。
- 五个套路：
  - **拆位**。
  - **01 Trie**。
  - **线性基**。
  - **SOSDP**。
  - **FWT**。
- $a \ge b$，则 $\gcd(a,b) \le a-b \le a \oplus b \le a+b$。
- 把一个数 $x$ 一直做 $x \gets x \text{ and } k_i$，则 $x$ 发生变化的次数是 $O(\log V)$。$\text{or}$ 也一样。对于区间扩展类问题有用。
- 经典模型 TODO: 放链接
  - 集合的最大异或对
    - 01Trie 裸题。
  - 集合的最小异或对
    - 01Trie 裸题。
    - 根据结论【$x < y < z$，则 $\min(x \oplus y, y \oplus z) < x \oplus z$】。因此把集合排序，答案只会在相邻位置对出现。
  - 单点修改 & 高维前缀和
    - 有单次操作 $O(\sqrt W)$ 的做法。
- $x \oplus y \oplus z = k$ 等价于 $(x \oplus k) \oplus (y \oplus k) = (z \oplus k)$。

# DS

- 并查集
  - 启发式合并的并查集树高 $O(\log n)$。
  - 变种
    - 种类并查集
    - 可持久化并查集
      - 可撤销并查集
    - 序列并查集 [P1840 Color the Axis](https://www.luogu.com.cn/problem/P1840)
      - 上树 [P4092 [HEOI2016/TJOI2016] 树](https://www.luogu.com.cn/problem/P4092)
    - 倍增并查集 [P3295 [SCOI2016] 萌萌哒](https://www.luogu.com.cn/problem/P3295)
      - 上树 TODO:

# Tree

- LCA
  - 多点 LCA
    - $\text{LCA}(a_1, a_2), \cdots, \text{LCA}(a_{n-1}, a_n)$ 中深度最小的那个即为答案。一般用于区间 LCA 查询。
    - 按 $dfn$ 排序，$\text{LCA}(a_1, a_n)$ 即为答案。
- 树的直径
  - **边权非负**时，选择一条直径，离点 $u$ 最远的点必定是该直径端点。
  - TODO:
- 树的重心
  - TODO:
- 点集的导出子树
  - 把点集按 DFS 序排序。
- 随机树
  - 随机树树高 $\Theta(\sqrt n)$。
  - 随机父亲树树高 $\Theta(\log n)$。

# Graph

- 平面图
  - 是稀疏图，$m \le 3n-6$。
  - 转对偶图。
    - 平面图最小割等于对偶图最短路。
  - 网格图是特殊的平面图。

# Math

- $\gcd$
  - 多个数 $\gcd$
    - 辗转相除，时间复杂度 $O(n + \log V)$，不是 $O(n \log V)$。
  - 把一个数 $x$ 一直做 $x \gets \gcd(x, k_i)$，则 $x$ 发生变化的次数是 $O(\log V)$。对于区间扩展类问题有用。
- Vandermonde determinant $\prod\limits_{i<j} (a_i - a_j)$
  - 值域小，对于值域数组 FFT。
  - 值域大没有实用做法。

# Prob

- 期望
  - 设随机变量，推出随机变量之间的关系，然后一起取期望。