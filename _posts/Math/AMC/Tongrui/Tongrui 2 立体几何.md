# 点到平面的距离公式

2D: 点 $(x_0, y_0)$ 到直线 $A x + B y + C = 0$ 的距离为

$$d = \frac {\lvert A x_0 + B y_0 + C \rvert} {\sqrt{A^2 + B^2}}$$

3D: 点 $(x_0, y_0, z_0)$ 到平面 $A x + B y + C z + D = 0$ 的距离为

$$d = \frac {\lvert A x_0 + B y_0 + C z_0 + D \rvert} {\sqrt{A^2 + B^2 + C^2}}$$

3D 版本的证明：

$Ax + By + Cz + D = 0$ 的一个法向量为 $(A,B,C)$。在平面上取任意一点 $(x_1, y_1, z_1)$，和 $(x_0, y_0, z_0)$ 作差之后和法向量点积除以法向量长度即可：

$$\begin{aligned}
    & \frac {A(x_0 - x_1) + B(y_0 - y_1) + C(z_0 - z_1)} {\sqrt{A^2 + B^2 + C^2}} \\
    =& \frac {A x_0 + B y_0 + C z_0 + D} {\sqrt{A^2 + B^2 + C^2}}
\end{aligned}$$

当然，由于 $(x_0, y_0, z_0)$ 可能在 $(A,B,C)$ 的另一面，最后取个绝对值。

# 平行六面体的体积

三个向量组成的平行六面体的有向体积为：

$$V = \begin{vmatrix}
    x_1 & x_2 & x_3 \\
    y_1 & y_2 & y_3 \\
    z_1 & z_2 & z_3 \\
\end{vmatrix}$$

$$V = (x_1 y_2 z_3 + x_2 y_3 z_1 + x_3 y_1 z_2) - (x_3 y_2 z_1 + y_3 z_2 x_1 + z_3 x_2 y_1)$$

# 三角形面积

$A,B,C$ 组成的三角形的面积为

$$\lvert \overrightarrow{AB} \times \overrightarrow{AC} \rvert = \begin{vmatrix}
    \vec i & \vec j & \vec k \\
    \Delta x_{1,2} & \Delta y_{1,2} & \Delta z_{1,2} \\
    \Delta x_{1,3} & \Delta y_{1,3} & \Delta z_{1,3} \\
\end{vmatrix}$$