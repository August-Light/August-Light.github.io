# 离散化

不是复杂算法，但是值得背一下。

```cpp
    for (int i = 1; i <= n; i++)
        c[i] = a[i];
    sort(c + 1, c + n + 1);
    int len = unique(c + 1, c + n + 1) - c - 1;
    for (int i = 1; i <= n; i++)
        b[i] = lower_bound(c + 1, c + len + 1, a[i]) - c;
```

# 莫队

分块，令 $bel_i$ 为 $i$ 所在的块。将询问 $[l,r]$ 按照 $bel_l$ 为第一关键字 $r$ 为第二关键字排序。强行移动。

奇偶排序优化：$bel_l$ 为奇数时 $r$ 升序排序，$bel_l$ 为偶数时 $r$ 降序排序。好写的常数优化。

- 莫队的最优时间复杂度是 $O(n \sqrt m)$，在块长为 $\Theta(\frac n {\sqrt m})$ 时取到。

```cpp
    B = ceil(n / sqrt(m));
    rep(i, 1, n)
        bel[i] = i / B;
    sort(q+1, q+m+1, [](Query &A, Query &B) {
        if (bel[A.l] != bel[B.l])
            return bel[A.l] < bel[B.l];
        if (bel[A.l] % 2 == 1)
            return A.r < B.r;
        return A.r > B.r;
    });

    int l = 1, r = 0;
    rep(i, 1, m) {
        while (l > q[i].l) add(--l);
        while (r < q[i].r) add(++r);
        while (l < q[i].l) del(l++);
        while (r > q[i].r) del(r--);
        ans[q[i].id] = res;
    }
```

## 回滚莫队

预处理 $L$ 和 $R$ 数组，代表第 $i$ 块的范围是 $[L_i, R_i]$。总块数记为 $n_B$。

先把所有询问按莫队顺序排序。然后我们枚举块 $i$，依次处理 $bel_l = i$ 的询问。若 $bel_r = i$（即 $[l,r]$ 在同一块），则暴力；否则见下文。

以下用 $l,r$ 代表区间指针，$l_q,r_q$ 代表询问区间。从 $[l,r] = [R_i + 1, R_i]$ 空区间开始移动。每次扩张到 $[l_q, r_q]$ 算出答案，然后把 $l$ 从 $l_q$ 退回到 $R_i + 1$，$r$ 不动。乍一看这里有删除操作，但是只是删除了辅助信息（如桶），但是并未更新关键信息。

细节：扩张到 $[l_q, r_q]$ 这一步中，先把 $r$ 扩张到 $r_q$，保存关键信息副本，然后把 $l$ 扩张到 $l_q$ 算完答案退回时直接把刚才的副本拿过来。

```cpp
    B = ceil(n / sqrt(m));
    int nB = 0;
    for (int i = 1; i <= n; i += B) {
        nB++;
        L[nB] = i, R[nB] = min(i + B - 1, n);
        rep(j, L[nB], R[nB])
            bel[j] = nB;
    }
    sort(q+1, q+m+1, [](Query &A, Query &B) {
        if (bel[A.l] != bel[B.l])
            return bel[A.l] < bel[B.l];
        return A.r < B.r;
    });

    // 实现 add 和 brute_force。
    // 实现 del 函数。只删除辅助信息，关键信息不更新

    int l = 1, r = 0;
    int ptr = 1;
    rep(i, 1, nB) {
        l = R[i] + 1, r = R[i];
        memset(c, 0, sizeof c), res = 0;
        for (; bel[q[ptr].l] == i; ptr++) {
            auto Q = q[ptr];
            if (bel[Q.l] == bel[Q.r]) {
                ans[Q.id] = brute_force(Q.l, Q.r);
                continue;
            }
            while (r < Q.r)
                add(++r);
            ll copy_res = res;
            while (l > Q.l)
                add(--l);
            ans[Q.id] = res;
            res = copy_res;
            while (l < R[i] + 1)
                del(l++);
        }
    }
```

# 树上背包

可以证明[时间复杂度是 $O(nm)$ 的](https://www.luogu.com.cn/article/v8s8o0ft)。

- $i$ 倒序，从 $\min(siz_u, m)$ 枚举到 $1$。
- $j$ 随意，枚举 $1$ 到 $\min(siz_v, m-i)$。

```cpp
    siz[u] = 1;
    f[u][1] = a[u];
    for (auto v : G[u]) {
        dfs(v);
        per(i, min(siz[u], m), 1)
            rep(j, 1, min(siz[v], m-i))
                cmax(f[u][i+j], f[u][i] + f[v][j]);
        siz[u] += siz[v];
    }
```

[U53204 【数据加强版】选课](https://www.luogu.com.cn/problem/U53204)

# Tarjan

## 强连通分量

- 要记 `ins` 数组。
  - 只有 `ins[v]` 时才有 `low[u] = min(low[u], dfn[v]);` 这个转移。

```cpp
int dfn[MAXN], low[MAXN], cnt;
bool ins[MAXN];
vector<int> stk;
int bel[MAXN], tot;
void tarjan(int u) {
    dfn[u] = low[u] = ++cnt;
    stk.push_back(u), ins[u] = true;
    for (auto v : G[u]) {
        if (!dfn[v]) {
            tarjan(v);
            low[u] = min(low[u], low[v]);
        } else if (ins[v])
            low[u] = min(low[u], dfn[v]);
    }
    if (dfn[u] == low[u]) {
        tot++;
        int v; do {
            v = stk.back(), stk.pop_back(), ins[v] = false;
            bel[v] = tot;
        } while (v != u);
    }
}
```

## 边双连通分量

- 要判反边。
- 不用记 `ins` 数组。

```cpp
int dfn[MAXN], low[MAXN], cnt;
vector<int> stk;
int bel[MAXN], tot;
void tarjan(int u, int lst) {
    dfn[u] = low[u] = ++cnt;
    stk.push_back(u);
    for (auto [v, i] : G[u]) if (i != (lst ^ 1)) {
        if (!dfn[v]) {
            tarjan(v, i);
            low[u] = min(low[u], low[v]);
        } else
            low[u] = min(low[u], dfn[v]);
    }
    if (dfn[u] == low[u]) {
        tot++;
        int v; do {
            v = stk.back(), stk.pop_back();
            bel[v] = tot;
        } while (v != u);
    }
}
```

## 点双连通分量

- 当 `low[v] >= dfn[u]` 时，持续弹栈直到把 $v$ 弹出。
- 孤立点要特判。

P.S. 一个点是割点，当且仅当它存在于 $\ge 2$ 个点双连通分量中。

```cpp
int dfn[MAXN], low[MAXN], cnt;
vector<int> stk;
vector<vector<int>> vbccs;
void tarjan(int u, int lst) {
    dfn[u] = low[u] = ++cnt;
    stk.push_back(u);
    for (auto [v, i] : G[u]) if (i != (lst ^ 1)) {
        if (!dfn[v]) {
            tarjan(v, i);
            low[u] = min(low[u], low[v]);
            if (low[v] >= dfn[u]) {
                vector<int> vbcc; vbcc.push_back(u);
                int w; do {
                    w = stk.back(), stk.pop_back();
                    vbcc.push_back(w);
                } while (w != v);
                vbccs.push_back(vbcc);
            }
        } else
            low[u] = min(low[u], dfn[v]);
    }
    if (G[u].empty())
        vbccs.push_back({u});
}
```

# Manacher

维护一个 box $[mid, mx]$。若当前 $i \le mx$，则可以用 $i$ 关于 $mid$ 对面的 $2 \times mid - i$ 的信息来更新（注意和 $mx - i$ 取 $\min$）。不管是否可以更新，都暴力扩展 $r_i$。若当前 box 的 $mx$ 更大则更新现在维护的 box。

- 由于加了间隔字符，`MAXN` 要开 $2$ 倍。

```cpp
int mid = 0, mx = 0;
rep(i, 1, n) {
    if (i <= mx)
        r[i] = min(r[2 * mid - i], mx - i);
    while (i - r[i] >= 1 && i + r[i] <= n && S[i - r[i]] == S[i + r[i]])
        r[i]++;
    if (i + r[i] > mx)
        mid = i, mx = i + r[i];
}
```

# 欧拉路径

## 有向图欧拉路径

从度数符合条件的起点开始一股脑 DFS，每次经过一条边就把这条边删掉（当前弧优化），如果一个点没有出边了则加入 `euler_path`。最终将 `euler_path` 数组 `reverse` 就得到真实欧拉路径。

```cpp
vector<int> euler_path;
int cur[MAXN];
void dfs(int u) {
    while (cur[u] < oud[u])
        dfs(G[u][cur[u]++]);
    euler_path.push_back(u);
}
bool euler() {
    int S = 0, T = 0;
    rep(u, 1, n) {
        if (oud[u] == ind[u] + 1) {
            if (S)
                return false;
            S = u;
        } else if (ind[u] == oud[u] + 1) {
            if (T)
                return false;
            T = u;
        } else if (ind[u] != oud[u])
            return false;
    }
    if (!S)
        S = T = 1;
    dfs(S);
    reverse(euler_path.begin(), euler_path.end());
    return true;
}
```

## 无向图欧拉路径

思路和有向图完全一致，注意判反边。反边的编号设成和原来边一样即可。

- `vis` 的大小是边数的 `MAXM` 而不是点数的 `MAXN`。

```cpp
vector<int> euler_path;
int cur[MAXN];
bool vis[MAXM];
void dfs(int u) {
    while (cur[u] < deg[u]) {
        auto [v, i] = G[u][cur[u]++];
        if (!vis[i]) {
            vis[i] = true;
            dfs(v);
        }
    }
    euler_path.push_back(u);
}
```

这一部分的判定**有待商榷**，可能不是正确的：

```cpp
bool euler() {
    int S = 0, cnt = 0;
    rep(u, 1, n) {
        if (deg[u] % 2 == 1) {
            if (!S) S = u;
            cnt++;
        }
    }
    if (cnt > 2)
        return false;

    if (cnt == 2)
        dfs(S);
    else {
        rep(u, 1, n)
            if (deg[u] != 0) {
                dfs(u);
                break;
            }
    }
    reverse(euler_path.begin(), euler_path.end());
    return (int)euler_path.size() == m+1;
}
```

# 匈牙利算法

`u` 代表某一个左部点，`v` 代表某一个右部点。

`match[v]` 代表右部点 `v` 目前匹配着的左部点。`col[u]` 是一个类似时间戳的东西，如果 `col` 相同代表是同一轮更新。

`dfs(u, c)` 代表在 `c` 这一轮中 `u` 是否能匹配到任何一个右部点。若 `u` 在这一轮已经动过则不变；否则遍历所有与 `u` 相邻的右部点，若 `v` 没有匹配的左部点，或 `dfs(match[v], c)` 成立（即 `v` 原本匹配着的左部点可以让出来），则 `u` 可以和 `v` 匹配。

使用时，对每个左部点调用 `dfs(u, u)`，即直接使用当前节点编号作为时间戳。若 `dfs(u, u)` 返回 `true` 则 `ans++`。

时间复杂度 $O(n_L \times m)$。

```cpp
int match[MAXN], col[MAXN];
bool dfs(int u, int c) {
    if (col[u] == c)
        return false;
    col[u] = c;
    for (auto v : G[u]) {
        if (!match[v] || dfs(match[v], c)) {
            match[v] = u;
            return true;
        }
    }
    return false;
}
```