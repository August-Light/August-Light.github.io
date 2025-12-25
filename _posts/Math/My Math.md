# Algebra

- $\sqrt \cdot + \sqrt \cdot$
  - 看到 $\sqrt {x^2 - a^2} + \sqrt {y^2 - a^2}$，构造高为 $a$ 的三角形。[2006 AIME II #15](https://artofproblemsolving.com/wiki/index.php?title=2006_AIME_II_Problems/Problem_15)
- 二次曲线切线
  - 构造方程使 $\Delta = 0$。[2005 AIME II #15](https://artofproblemsolving.com/wiki/index.php?title=2005_AIME_II_Problems/Problem_15)
  - 通法：求法向量，切线与法向量垂直，用点积刻画。

## Conic Section

- 椭圆 $\frac {x^2} {a^2} + \frac {y^2} {a^2 - k} = 1$ [2022 AIME II #12](https://artofproblemsolving.com/wiki/index.php?title=2022_AIME_II_Problems/Problem_12)
  - $\sqrt k$ 是焦距一半。

# Polynomials

## Factorizing

- $a^2 + (ab + ac + bc) = (a+b) (a+c)$ [HMMT 2025 Feb AN #7](https://hmmt-archive.s3.amazonaws.com/tournaments/2025/feb/algnt/problems.pdf)
- $a^3 + b^3 + c^3 - 3abc = (a + b + c) (a^2 + b^2 + c^2 - ab - ac - bc)$

# Geometry

## Triangle

- 已知三边求面积
  - Heron 公式 $A = \sqrt{p (p-a) (p-b) (p-c)}$
  - 三边带根号 或 两边固定只动第三边
    - 秦九韶公式 $A = \frac 1 2 \sqrt {a^2 b^2 - (\frac {a^2 + b^2 - c^2} 2)^2}$ [2025 AMC12B #21](https://artofproblemsolving.com/wiki/index.php?title=2025_AMC_12B_Problems/Problem_21)
    - 对称形式 $A = \frac 1 4 \sqrt{(a^2 + b^2 + c^2)^2 - 2 (a^4 + b^4 + c^4)}$
- 正弦定理
  - $\sin A : \sin B : \sin C = a : b : c$
    - 边长为 $\sin A, \sin B, \sin C$ 的三角形和原三角形是相似的。[2013 AIME II #15](https://artofproblemsolving.com/wiki/index.php?title=2013_AIME_II_Problems/Problem_15)
- 外接圆
  - 正弦定理 $2R = \frac a {\sin A} = \frac b {\sin B} = \frac c {\sin C}$
  - 有垂线：考虑 Simson 线
- 中线
  - 中线长公式 $AD^2 = \frac 1 2 (AB^2 + AC^2) - \frac 1 4 BC^2$
- Stewart 定理
- Fermat 点
  - 若原三角形最大内角 $\ge 120°$，则 Fermat 点退化为这个内角的顶点。
  - 对于非退化的 Fermat 点 $P$，$AP, BP, CP$ 两两夹角 $120°$。
- Miquel 定理：<img src="https://cdn.luogu.com.cn/upload/image_hosting/xu936wmm.png" width=200/>

## Circle

- 切线
  - 圆幂定理。
- 两圆公切线
  - 根轴（公共弦）平分公切线。

### Cyclic Quadrilateral

- 圆周角
- 对角互补
- Brahmagupta 公式 $A = \sqrt{(p-a) (p-b) (p-c) (p-d)}$

### Cyclic Polygon

- 保持面积不变的变换：像切 pizza 一样把每根弦切在一个三角形内，然后重新组合。[2022 AIME II #15](https://artofproblemsolving.com/wiki/index.php?title=2022_AIME_II_Problems/Problem_15)

# Other

- 四边形 Fermat 点
  - 凹四边形的 Fermat 点退化为凹进去的那个顶点。
  - 凸四边形的 Fermat 点为对角线交点。[2022 AIME II #12](https://artofproblemsolving.com/wiki/index.php?title=2022_AIME_II_Problems/Problem_12)

# Trigonometric Function

- $\tan a + \tan b$ 和 $\cot a + \cot b$
  - $\tan a + \tan b = \frac {\sin(a + b)} {\cos a \cos b}$
  - $\cot a + \cot b = \frac {\sin(a + b)} {\sin a \sin b}$

# Number Theory

- $\bmod$ 合数，尝试用 CRT 拆开。
- 缩系
  - 任何数 $m$（$m \ne 2$）的缩系内所有元素求和在 $\bmod m$ 下一定是 $0$。