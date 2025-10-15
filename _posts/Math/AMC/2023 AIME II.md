[题目链接](https://artofproblemsolving.com/wiki/index.php/2023_AIME_II_Problems)

# Problem 6 (Normal)

（积分算概率）

> 令这个图形为 $Q$。在 $Q$ 内部均匀独立随机取两点 $A,B$，问 $AB$ 中点落在 $Q$ 内部的概率。
>
> <img src="https://latex.artofproblemsolving.com/3/5/e/35e5685ec38ac2940e2bd21b651c8faa1f022f57.png" width=200/>
>
> 可以证明答案是 $\frac m n$ 的形式，输出 $m+n$。

“枚举”点 $A$ 的位置。

若 $A$ 落在左下角的方格，$B$ 在哪都合法。$\frac 1 3$。

若 $A$ 落在左上角的方格，令 $(x,y)$ 为以左上角为原点 $A$ 的坐标（$x$ 向右 $y$ 向下）。画图可知 $B$ 不能落的区域的大小是 $x (1-y)$。

$$1 - \int_0^1 \int_0^1 \frac {x (1-y)} 3 dx dy = \frac {11} {12}$$

这里的 $\frac {11} {12}$ 指的是 **点 $A$ 落在左上角方格的前提下，点 $B$ 点 随机落在整个图形 $Q$ 中，使得中点仍在 $Q$ 内的平均概率**。

右下角的情况和左上角完全一致。

$$ans = \frac 1 3 + \frac {11} {12} \times \frac 2 3 = \frac {17} {18}$$

输出 $17 + 18 = \boxed{035}$。

# Problem 8 (Normal)

（单位根、计算易出错）

> 求
>
> $$\prod\limits_{k=0}^6 (\omega_7^{3k} + \omega_7^k + 1)$$
>
> 其中 $\omega_7 = \cos \frac {2 \pi} 7 + i \sin \frac {2 \pi} 7$。

[2024 AIME II Problem 13](https://artofproblemsolving.com/wiki/index.php/2024_AIME_II_Problems/Problem_13) 是此题的削弱版，那一题中 $\prod$ 内的是一个关于 $\omega$ 的二次函数，可以求出简单的解。

题解区除了 Solution 4 以外似乎都是利用了特殊性质的做法。这里写一个显然的 Newton's Sums 做法。

熟知 $\prod\limits_{k=1}^{n} (z - \omega_n^k) = z^n - 1$，我们把 $x^3 + x + 1$ 分解因式就能凑出这个格式。假设 $r,s,t$ 是 $x^3 + x + 1 = 0$ 的三个复根。

$$\begin{aligned}
    & \prod\limits_{k=0}^6 (\omega_7^{3k} + \omega_7^k + 1) \\
    =& - \prod\limits_{k=0}^6 (r - \omega_7^k) (s - \omega_7^k) (t - \omega_7^k) \\
    =& - (r^7 - 1) (s^7 - 1) (t^7 - 1) \\
    =& 1 - (r^7 + s^7 + t^7) + ((rs)^7 + (rt)^7 + (st)^7) - (rst)^7 \\
\end{aligned}$$

高次方和，很明显 Newton's Sums 是很好的选择。

根据 Vieta 定理我们能得到 $r,s,t$ 的关系：

$$\begin{cases}
    \sigma_1 = r + s + t = 0 \\
    \sigma_2 = rs + rt + st = 1 \\
    \sigma_3 = rst = -1 \\
\end{cases}$$

原式的 $(rst)^7 = -1$ 直接能算了，$r^7 + s^7 + t^7$ 也是标准的递推。$0$ 次方和到 $7$ 次方和的结果分别是：$\langle 3, 0, -2, -3, 2, 5, 1, -7 \rangle$，$r^7 + s^7 + t^7 = -7$。

$(rs)^7 + (rt)^7 + (st)^7$ 这一项我们看成 $rs, rt, st$ 的高次方和，要寻找这三者的基本多项式，不妨记作 $\Sigma$。

$$\begin{cases}
    \Sigma_1 = rs + rt + st = \sigma_2 = 1 \\
    \Sigma_2 = rst(r + s + t) = \sigma_3 \sigma_1 = 0 \\
    \Sigma_3 = (rst)^2 = \sigma_3^2 = 1 \\
\end{cases}$$

一样递推：$\langle 3,1,1,4,5,6,10,15 \rangle$，$(rs)^7 + (rt)^7 + (st)^7 = 15$。

$$\begin{aligned}
    & \prod\limits_{k=0}^6 (\omega_7^{3k} + \omega_7^k + 1) \\
    =& 1 - (r^7 + s^7 + t^7) + ((rs)^7 + (rt)^7 + (st)^7) - (rst)^7 \\
    =& 1 - (-7) + 15 - (-1) \\
    =& \boxed{024} \\
\end{aligned}$$

# TODO: