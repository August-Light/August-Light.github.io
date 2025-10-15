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

