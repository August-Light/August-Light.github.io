# Example: 求解部分数据丢失的单摆运动

$$\theta'' + \alpha \theta' + \beta \sin \theta = 0$$

$$\theta = 0 \implies \theta_{\text{prev}} \times \theta_{\text{next}} < 0$$

从左右两边往中间数值解 ODE，交点即为施加 $F$ 的时间。

---

令

$$f(\theta, \theta') = - \alpha \theta' - \beta \sin \theta$$

可以尝试这么最优化：

$$\min_{\alpha, \beta_1, \beta_2} \lVert \theta'' - f(\theta, \theta') \rVert^2$$

