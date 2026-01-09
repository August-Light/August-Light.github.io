# 光速不变

$$ct = \sqrt{x^2 + y^2 + z^2}$$

$$c^2 t^2 - x^2 - y^2 - z^2 = 0$$

自然单位制 $c=1$

$$\boxed{
    t^2 - x^2 - y^2 - z^2 = 0
}$$

# 线性变换

只能是线性变换

$$\begin{bmatrix}
    t' \\ x' \\ y' \\ z'
\end{bmatrix} = \Lambda \begin{bmatrix}
    t \\ x \\ y \\ z
\end{bmatrix}$$

$$x^\mu \eta_{\mu \nu} x^\nu = 0$$

$s^2$ 不变

度规 $\eta$

# 双曲、快度

把运动方向限制在 $x$ 轴

$$t^2 - x^2 = s^2$$

是双曲线。

Lorentz boost:

$$\begin{bmatrix} t' \\ x' \end{bmatrix}
 = \begin{bmatrix}
    \cosh \phi & - \sinh \phi \\
    - \sinh \phi & \cosh \phi \\
\end{bmatrix}
\begin{bmatrix} t \\ x \end{bmatrix}$$

快度 $\phi = \operatorname{artanh} v$

boost 复合，快度相加。

为什么光速达不到？切回普通的单位制，因为 $\phi = \operatorname{artanh} \frac v c$，$v \to c$ 时 $\phi \to \infty$。