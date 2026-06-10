# Problem 1

> 证明曲线
>
> $$\cosh y = 2 e^{-x} - 1$$
>
> 的渐近线为
>
> $$y = \pm (-x + \ln 4)$$

$$\begin{aligned}
    \frac {e^y + e^{-y}} 2 &= 2 e^{-x} - 1 \\
    e^y + e^{-y} &= 4 e^{-x} - 2 \\
\end{aligned}$$

$$\lim_{x \to - \infty} (4 e^{-x} - 2) = \infty$$

分类讨论。若 $y \to \infty$，则 $e^y$ 成为主导项：

$$\begin{aligned}
    e^y \sim 4 e^{-x} - 2 \\
    y \sim \ln 4 - x
\end{aligned}$$

同理，若 $y \to - \infty$，则得到

$$y \sim x - \ln 4$$

# Problem 2

> 令 $y' = \frac {dy} {dx}$。
>
> $$y = y'^2 + 2 x y'$$
>
> 证明
>
> $$\frac {dx} {d(y')} = -2 - \frac {2x} {y'}$$
>
> 进一步证明
>
> $$x = - \frac 2 3 y' + \frac C {(y')^2}$$

$$\begin{aligned}
    y &= (2x + y') y' \\
    y' &= (2 + y'') y' + (2x + y') y'' \\
    y'' &= - \frac {y'} {2x + 2 y'} \\
    \frac {dx} {d(y')} &= - \frac {2x + 2 y'} {y'} \\
    &= -2 - \frac {2x} {y'} \\
\end{aligned}$$

$$\begin{aligned}
    \frac {dx} {d(y')} + \frac 2 {y'} x &= -2 \\
    \int \frac 2 {y'} d(y') &= 2 \ln(y') + C \\
    \frac d {d(y')} \left( e^{2 \ln (y')} \times x \right) &= -2 e^{2 \ln (y')} \\
    (y')^2 x &= - \frac 2 3 (y')^3 + C \\
    x &= - \frac 2 3 y' + \frac C {(y')^2} \\
\end{aligned}$$