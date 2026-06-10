# Cyclotomic polynomial

https://en.wikipedia.org/wiki/Cyclotomic_polynomial

$$\Phi_n(x) := \prod_{k \perp n} (x - \omega_n^k)$$

可以证明：

$$\boxed{
    x^n - 1 = \prod_{d \mid n} \Phi_d(x)
}$$

可以证明：

$$\boxed{
    \Phi_n(x) \in \mathbb Z[x]
}$$

$$\boxed{
    \Phi_n(x) \text{ is irreducible on } \mathbb Q[x]
}$$

# Fermat Numbers

https://en.wikipedia.org/wiki/Fermat_number

考虑 $2^m + 1$ 形式的质数，不难发现 $m$ 不能含有任何奇质数因子。因此只能是这样的形式：

$$F_n := 2^{2^n} + 1$$

这些 $F$ 被称为 Fermat numbers，其中的质数被称为 Fermat primes。

有一个很简单的递推：

$$F_n = 2 + \prod_{k=0}^{n-1} F_k$$

反证法可以证明 $\boxed{\forall n \ne m, F_n \perp F_m}$。

# Euler product formula

$$\boxed{
    \sum_{n=1}^\infty \frac 1 {n^s} = \prod_{p \text{ prime}} \frac 1 {1 - p^{-s}}
}$$

证明：显然

$$\sum_{n=1}^\infty \frac 1 {n^s} = \prod_{p \text{ prime}} \sum_{k=0}^\infty \frac 1 {p^{sk}}$$

等比数列求和即可。