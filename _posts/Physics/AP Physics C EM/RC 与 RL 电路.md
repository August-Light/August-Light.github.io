# RC & RL 电路

这两个都会得到一阶常系数 ODE。令 $x$ 的系数为 $- \frac 1 \tau$：

$$\dot x = - \frac 1 \tau x + C$$

整理：

$$\dot x = - \frac 1 \tau (x - C)$$

在 $t = \infty$ 时 $\dot x = 0$，因此第二个 $C$ 就是 $x$ 在 $t = \infty$ 的取值：

$$\dot x = - \frac 1 \tau (x - x_\infty)$$

化成

$$\frac d {dt} (x - x_\infty) = - \frac 1 \tau (x - x_\infty)$$

显然这个方程的解为

$$\begin{aligned}
    x(t) &= x_\infty + (x_0 - x_\infty) e^{- \frac t \tau} \\
    &= x_0 e^{- \frac t \tau} + x_\infty \left( 1 - e^{- \frac t \tau} \right)
\end{aligned}$$

## RC 电路

$$R \frac {dQ} {dt} + \frac Q C = 0$$

$$\boxed{\textcolor{lightgreen}{
    \tau = RC
}}$$

| 物理量 | 充电 | 放电 |
| - | - | - |
| $Q$ | $Q = C \mathcal E \left( 1 - e^{- \frac t \tau} \right)$ | $Q = Q_0 e^{- \frac t \tau}$ |
| $I = \frac {dQ} {dt}$ | $I = \frac {\mathcal E} R e^{- \frac t \tau}$ | $I = I_0 e^{- \frac t \tau}$ |

## RL 电路

$$- L \frac {dI} {dt} - RI = 0$$

$$\boxed{\textcolor{lightgreen}{
    \tau = \frac L R
}}$$

| 物理量 | 充电 | 放电 |
| - | - | - |
| $I$ | $I = \frac {\mathcal E} R \left( 1 - e^{- \frac t \tau} \right)$ | $I = I_0 e^{- \frac t \tau}$ |
| $V = L \frac {dI} {dt}$ | $V = \mathcal E e^{- \frac t \tau}$ | $V = V_0 e^{- \frac t \tau}$ |