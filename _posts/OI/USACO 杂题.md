# [P6010 [USACO20JAN] Falling Portals P](https://www.luogu.com.cn/problem/P6010)

TODO:

# [P5853 [USACO19DEC] Tree Depth P](https://www.luogu.com.cn/problem/P5853)

TODO:

# [P8098 [USACO22JAN] Tests for Haybales G](https://www.luogu.com.cn/problem/P8098)

> 已知一个长为 $n$ 的数组 $a_{1 \cdots n}$。
>
> 构造一个数组 $x_{1 \cdots n}$ 和一个整数 $k$，使得：
> - $x$ 单调不降。
> - 对于每个 $i$，满足 $x_j \le x_i + k$ 的最大索引 $j$ 是 $a_i$。保证 $i \le a_i$。
> - $x_i \in [0, 10^{18}]$，$k \in [1, 10^{18}]$。
>
> 数据范围：
>
> - 对于 50pts，$n \le 5 \times 10^3$。
> - 对于 100pts，$n \le 10^5$。

题目条件的 $a$ 可以写作差分约束的形式：

$$i \to a_i \iff \begin{cases}
    x_{a_i} \le x_i + k \\
    x_i \le x_{a_i + 1} + (-k - 1) \\
\end{cases}$$

除此以外还有 $x_i \le x_{i+1} + 0$ 的条件。



TODO:

# [P5155 [USACO18DEC] Balance Beam P](https://www.luogu.com.cn/problem/P5155)

[我自己写的洛谷题解](https://www.luogu.com.cn/article/tta3avey)

> 给定一个长为 $n$ 的数组 $a_{1 \cdots n}$。
>
> 有一个 $n$ 格长的平衡木，范围为 $[1, n]$。你要从 $k$ 格的位置开始。你可以做以下两种操作：
> - 跳下平衡木，获得 $a_k$ 的奖励。
> - 抛硬币，$\frac 1 2$ 概率左移一格，$\frac 1 2$ 概率右移一格。并再选一次这两种操作，一直重复。
>
> 特别地，若离开了 $[1,n]$ 范围，则游戏直接结束，奖励为 $0$。
>
> 设 $f_k$ 为从第 $k$ 格位置开始，能获得的最大期望奖励。求出 $f_{1 \cdots n}$，精确到 $5$ 位小数。

神题。

我们可以得到显然的 DP 方程：

$$f_i = \max\left(\frac {f_{i-1} + f_{i+1}} 2, a_i\right)$$

（约定 $f_0 = f_{n+1} = 0$）

此时看似无法下手了。但是如果能注意到：

$$\begin{aligned}
    f_i &= \max\left(\frac {f_{i-1} + f_{i+1}} 2, a_i\right) \\
    0 &= \max\left(\frac {f_{i-1} - 2 f_i + f_{i+1}} 2, a_i - f_i \right) \\
    &= \max\left(\frac {(f_{i+1} - f_i) - (f_i - f_{i-1})} 2, a_i - f_i \right) \\
    &= \max\left(\frac {\Delta^2 f_{i-1}} 2, a_i - f_i \right) \\
\end{aligned}$$

（$\Delta$ 是前向差分算子，即 $\Delta f_i = f_{i+1} - f_i$）

这一步的动机是：式子里存在 $f_{i-1} + f_{i+1}$，还有系数 $2$，或许能配出 $f_{i-1} - 2f_i + f_{i+1}$，进一步改写为二阶差分。

这等价于：

$$\begin{cases}
    \Delta^2 f_{i-1} \le 0 \\
    f_i \ge a_i \\
    \Delta^2 f_{i-1} = 0 \text{ or } f_i = a_i \\
\end{cases}$$

第一条性质非常重要：这意味着把 $(i, f_i)$ 画在坐标系中，形状是一个上**凸壳**。

我们现在要根据 $(i, a_i)$ 的散点图，求出 $(i, f_i)$。

- 根据第三条性质，每个 $(i, f_i)$ 的点要么本身就是一个 $(i, a_i)$ 点，要么在凸壳上是一个斜率不改变的点。
- 根据第二条性质，凸壳要在所有 $(i, a_i)$ 的上方。

因此可以很轻松地得到结论：约定 $a_0 = a_{n+1} = 0$，对于 $i \in [0, n+1]$ 画出 $(i, a_i)$，求出这些点的**凸包**。凸包的拐点直接选上，剩下的点作一条竖线连到凸包上求出交点。

<img src="https://cdn.luogu.com.cn/upload/image_hosting/67jvvf9a.png" width=400/>

以这个图为例，$A \cdots H$ 是 $(i, a_i)$ 的点，$O,I$ 是约定的边界。对于这些点求出凸包，$\textcolor{red}{B,E,G}$ 在凸包上直接保留，剩余点找到它们在凸包上的线段的位置。最后凸包上的一排 $J,\textcolor{red}{B},K,L,\textcolor{red}{E},M,\textcolor{red}{G},N$ 的纵坐标就是答案。

用 Graham 求凸包，时间复杂度 $O(n \log n)$。

实现细节：
- 这题卡浮点精度，因此所有运算都用 `long long` 即可，只有最后一步根据斜率算坐标用浮点方便一点。
- 为了方便遍历凸包的边，可以让 Graham 顺时针求出凸包，而不是平时习惯的逆时针。