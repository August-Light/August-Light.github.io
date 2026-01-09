# Lucas

> 求
>
> $$\binom n m \bmod p$$
>
> 保证 $p$ 为质数。**不保证** $n, m < p$。

$$n = \sum n_i p^i$$

$$m = \sum m_i p^i$$

则

$$\binom n m \equiv \prod_i \binom {n_i} {m_i} \pmod p$$

证明：

$$(1 + x)^p \equiv 1 + x^p \pmod p$$

$$(1 + x)^n = \prod (1 + x)^{n_i p^i} \equiv \prod (1 + x^{p^i})^{n_i} \pmod p$$

$$\binom n m = [x^m] (1 + x)^n \equiv [x^m]\prod (1 + x^{p^i})^{n_i} = \prod \binom {n_i} {m_i} \pmod p$$

# Kummer

当 $p \nmid \binom n m$ 时，我们通过 Lucas 定理可以求出 $\binom n m \bmod p$ 的值。但是当 Lucas 给出 $0$ 的答案时，我们只知道 $p \mid \binom n m$，但有时我们还希望知道它里面有多少个 $p$。

以下为了 $n,m$ 的对称性，把 $\binom n m$ 修改为 $\binom {n+m} m$。

> 求
>
> $$\nu_p\left( \binom {n+m} m \right)$$

在 $p$ 进制下 $n + m$ 的加法产生的进位次数

