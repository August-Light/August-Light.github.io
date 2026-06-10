$$\begin{aligned}
    G_{X_i}(t) &= P(X_i = 0) t^0 + P(X_i = 1) t^1 \\
    &= (1 - p_i) + p_i t \\
    &= 1 + p_i (t - 1) \\
\end{aligned}$$

$$\begin{aligned}
    G_X(t) &= \prod_{i=1}^n G_{X_i}(t) \\
    \ln G_X(t) &= \sum_{i=1}^n \ln G_{X_i}(t) \\
    &= \sum_{i=1}^n \left( p_i(t-1) + o(p_i) \right) \\
    &= \lambda (t-1) + \sum_{i=1}^n o(p_i) \\
\end{aligned}$$

$$\lim_{n \to \infty} \ln G_X(t) = \lambda (t-1)$$

$$\lim_{n \to \infty} G_X(t) = e^{\lambda (t-1)}$$

$$\begin{aligned}
    G_X(t) &= e^{\lambda (t-1)} \\
    &= e^{-\lambda} e^{\lambda t} \\
    &= \sum_{k=0}^n \left( \frac {\lambda^k e^{-\lambda}} {k!} \right) t^k
\end{aligned}$$