$$z = \frac {\bar x - \mu} {\sigma / \sqrt n}$$

不知道 $\sigma$，用 $s$ 代替：

$$t = \frac {\bar x - \mu} {s / \sqrt n}$$

我们关心此时 $t$ 的分布。

$$\begin{aligned}
    t &= \frac z {\sqrt {\frac {s^2} {\sigma^2}}} \\
    &= \frac z {\sqrt {\frac {(n-1) s^2 / \sigma^2} {n-1}}} \\
    &= \frac z {\sqrt {U / (n-1)}}
\end{aligned}$$

$$\begin{aligned}
    U &= (n-1) \frac {s^2} {\sigma^2} \\
    &= \sum \left(\frac {x_i - \bar x} \sigma \right)^2 \\
\end{aligned}$$

因此 $U \sim \chi^2(n-1)$。

TODO: $U$ 和 $z$ 独立。

TODO: 推导


$$f(x) = \frac 1 {\sqrt k B(\frac k 2, \frac 1 2)} \left(\frac k {k + x^2} \right)^{\frac {k+1} 2}$$

## Welch's t-test

TODO: