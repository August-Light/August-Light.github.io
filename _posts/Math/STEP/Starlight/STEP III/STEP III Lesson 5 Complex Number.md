# 基本对称多项式

欧拉定理：

$$\boxed{
    P_3 - 3 \sigma_3 = \sigma_1 (P_2 - \sigma_2)
}$$

# Problem：分圆多项式

> 若 $a$ 满足 $a^n = 1$ 且不存在 $0 < m < n$ 使得 $a^m = 1$，则称 $a$ 是一个 $n$ 次本原单位根。
>
> 定义第 $n$ 个分圆多项式 $\Phi_n(x)$ 为以所有 $n$ 次本原单位根为根的多项式。

不难发现

$$\Phi_n(x) = \prod_{k \perp n} (x - \omega_n^k)$$

> 已知对于某个 $n$ 有
>
> $$\Phi_n(x) = x^4 + 1$$
>
> 求 $n$。

$$\begin{aligned}
    & x^4 + 1 \\
    =& (x^2 - i) (x^2 + i) \\
    =& \prod_{k \in \{1,3,5,7\}} (x - e^{\frac {2 \pi k} 8})
\end{aligned}$$

恰好符合 $n = 8$。

> 对于质数 $p$，求 $\Phi_p(x)$。

$$\begin{aligned}
    & \Phi_p(x) \\
    =& \frac {x^p - 1} {x - 1} \\
    =& \sum_{k=0}^{p-1} x^k \\
\end{aligned}$$

> 证明分圆多项式不可能被分解为两个分圆多项式的乘积。
>
> 即不存在 $q,r,s$ 使得
>
> $$\Phi_q(x) = \Phi_r(x) \Phi_s(x)$$

反证法。令 $\Phi_q(x) = \Phi_r(x) \Phi_s(x)$。

设 $\alpha$ 为 $\Phi_q$ 的根。WLOG，让 $\alpha$ 是 $\Phi_r(x)$ 的根。

根据定义，$\alpha$ 同时是 $q$ 次和 $r$ 次的本原单位根，这说明 $q = r$。这要求 $\Phi_s(x) = 1$，但这是不可能的。