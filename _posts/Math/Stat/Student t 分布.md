# Student’s t-distribution

> 你是 William Sealy Gosset，Guinness 啤酒厂的统计师。现在你要统计麦芽的参数。
>
> （以下案例为 ChatGPT 编写）
>
> - 麦芽的标准*糖化力*为 $\mu_0 = 80$。你现在有一批麦芽，你想知道其糖化力是否正常。
> - 假定麦芽的糖化力符合正态分布。
> - 由于原料价格原因，你只能抽取**很少**样本进行统计。你抽取了 $n=5$ 份样本，统计出 $\bar x = 82.1$，$s = 4.8$。
>
> **拒绝或接受**：这批麦芽的糖化力均值 $\mu$，等于麦芽的标准糖化力 $\mu_0 = 80$。（显著性水平 $\alpha = 5\%$）
>
> 你当年已经有了通过正态分布进行显著性检验的方案。但很可惜，**你并不知道总体标准差**，因此无法使用。
>
> 你必须在不知道总体标准差的情况下，对均值进行显著性检验。

把问题形式化：

> 我有一个来自 $\mathcal N(\mu, \sigma^2)$ 的样本。但是我不知道具体的 $\mu$ 和 $\sigma^2$。
>
> 我们考虑均值 $\bar x$ 的标准化变量 $z$
>
> $$z = \frac {\bar x - \mu} {\sigma / \sqrt n}$$
>
> 应该服从 $\mathcal N(0,1)$。
>
> 但是很遗憾我们并不知道 $\sigma$ 的值。但是我们可以知道 $\hat \sigma$，即 $s$。因此我们用 $s$ 代替未知的 $\sigma$，定义新的“标准化变量”为 $t$：
>
> $$t = \frac {\bar x - \mu} {s / \sqrt n}$$
>
> 我们关心此时 $t$ 的分布。这被称为自由度为 $n-1$ 的 **Student’s t-distribution** $t_{n-1}$。

$$\begin{aligned}
    t &= \frac z {\sqrt {\frac {s^2} {\sigma^2}}} \\
    &= \frac z {\sqrt {\frac {(n-1) s^2 / \sigma^2} {n-1}}} \\
    &= \frac z {\sqrt {V / (n-1)}}
\end{aligned}$$

$$\begin{aligned}
    V &= (n-1) \frac {s^2} {\sigma^2} \\
    &= \sum \left(\frac {x_i - \bar x} \sigma \right)^2 \\
\end{aligned}$$

因此 $V \sim \chi^2(n-1)$。

我们又知道 $\bar x$ 与 $s^2$ 独立，因此 $V$ 和 $z$ 独立。

于是我们可以重新定义 $t$ 分布的表述：对于独立随机变量 $z \sim \mathcal N(0,1)$ 和 $V \sim \mathcal \chi^2(\nu)$，以下变量 $t$ 服从自由度为 $\nu$ 的 $t$ 分布：

$$t = \frac {z} {\sqrt{\frac {V} \nu}} \sim t_\nu$$

## 更高妙的视角

TODO:

## PDF

$$f_{\nu}(x) = \frac 1 {\sqrt \nu B(\frac \nu 2, \frac 1 2)} \left(\frac \nu {\nu + x^2} \right)^{\frac {\nu+1} 2}$$

证明略。

注意到其只和 $x^2$ 有关，因此：
- $f(x)$ 关于 $x=0$ 对称。
- 在 $\nu$ 是正整数的时候，PDF 的积分（即 CDF）总是初等的。

通过这种 Beta 函数的形式，我们可以把这个 PDF 扩展到 $\nu \not \in \mathbb N^+$ 的情形，对于近似计算有一定用处，在后文会聊到。

### 小例子

| $\nu$ | $f_\nu(x)$ |
| - | - |
| $1$ | $\frac 1 {\pi (1 + x^2)}$ |
| $2$ | $\frac 1 {(2 + x^2)^{\frac 3 2}}$ |
| $3$ | $\frac {6 \sqrt 3} {\pi (3 + x^2)^2}$ |
| $4$ | $\frac {12} {(4 + x^2)^{\frac 5 2}}$ |
| $\infty$ | $\frac 1 {\sqrt{2 \pi}} e^{- \frac {x^2} 2}$ |

当 $\nu \to \infty$ 时，t 分布趋于正态分布。

由于 $t$ 的定义中分母提供了更大的随机程度，因此 t 分布会比正态分布尾巴更大一点，看起来也就更扁一点。

# t 检验

> 回到啤酒厂的例子。
>
> 你抽取了 $n=5$ 份样本，统计出 $\bar x = 82.1$，$s = 4.8$。
>
> 设定显著性水平 $\alpha = 5\%$。拒绝或接受：$\mu = \mu_0 = 80$。

$$t = \frac {\bar x - \mu_0} {s / \sqrt n} = \frac {82.1 - 80} {4.8 / \sqrt 5} \approx 0.978$$

在卡方分布的章节中已经聊过，$n=5$ 对应的自由度 $\nu = n-1 = 4$。

$$\begin{aligned}
    & p \\
    =& P(\lvert t \rvert > 0.978) \\
    =& 2 P(t > 0.978) \\
    =& 2 \int_{0.978}^\infty \frac {12} {(4 + x^2)^{\frac 5 2}} dx \\
    \approx & 0.383 \\
\end{aligned}$$

也就是说，产生比目前结果更加离谱结果的概率有足足 $38.3\%$，远远大于 $\alpha = 5\%$。所以我们接受原假设，我们的样本和标准的 $80$ 之间没有显著差异。

## 置信区间计算

> 还是刚才的这份样本，我希望找到总体平均 $\mu$ 的一个 $95\%$ 置信区间。这个区间一定会是这样的形式：
>
> $$\bar x \pm t^* \times SE(\bar x)$$
>
> 即
>
> $$\bar x \pm t^* \times \frac s {\sqrt n}$$

定义 $\text{invT}(x)$ 函数，为 CDF 的反函数。即 $P(t \le \text{invT}(x)) = x$。

$$t^* = \text{invT}(1 - \frac \alpha 2)$$

---

对于这份样本，我们计算 $t^*$：

$$t^* =\text{invT}(1 - \frac {0.05} 2) \approx 2.776$$

$$t^* \times \frac s {\sqrt n} \approx 2.776 \times \frac {4.8} {\sqrt 5} \approx 5.96$$

置信区间即为

$$82.1 \pm 5.96$$

反过来再看，$\mu_0 = 80$ 落在这个区间内，也能说明我们前面选择接受假设是正确的。也就是说前面那个题其实有两个做法：
- 显式算出 $p$，和 $\alpha$ 比较。
- 从 $\alpha$ 反过来算出置信区间，和 $\mu$ 比较。

# Behrens–Fisher problem

https://en.wikipedia.org/wiki/Behrens%E2%80%93Fisher_problem

> 有两个正态总体 $\mathcal N(\mu_1, \sigma_1^2)$ 和 $\mathcal N(\mu_2, \sigma_2^2)$。**你不知道 $\mu_1, \mu_2, \sigma_1, \sigma_2$ 的任何一个参数。不保证 $\sigma_1^2 = \sigma_2^2$**。
>
> 你从两个总体分别取了两个样本：$x_1, \cdots, x_{n_1}$ 和 $y_1, \cdots, y_{n_2}$。
>
> 给定显著性水平 $\alpha$，支持或拒绝：$H_0: \mu_1 = \mu_2$。

根据 t 检验的思路，我希望求出以下统计量的分布：

$$T = \frac {\bar x - \bar y} {\sqrt{\frac {s_1^2} {n_1} + \frac {s_2^2} {n_2}}}$$

但是这种两个卡方线性组合放在分母上的形式极难处理。所以统计学家们开发了很多近似计算方法。以下介绍一个考试会用的 Welch's t-test。

## Welch's t-test

https://en.wikipedia.org/wiki/Welch%27s_t-test

> Example 7.6 一位社会学家随机抽取了 $30$ 名大学教授和 $30$ 名警察，调查他们计划的退休年龄。在大学教授的样本中，平均计划退休年龄为 $66$ 岁，标准差为 $3.5$；而在警察的样本中，平均计划退休年龄为 $55$ 岁，标准差为 $5.1$。
>
> - 两组样本独立。
> - 每组样本来自近似正态的总体（$n \ge 30$，可以近似看作正态），可以使用正态分布的方法。
>
> 确定大学教授和警察平均计划退休年龄之差的（近似）$95\%$ 置信区间。

TODO: 重写这一段。

我们要考察 $\bar x_1 - \bar x_2$ 的行为。置信区间可以被表示为这样的形式：

$$(\bar x_1 - \bar x_2) \pm t^* \times \text{SE}(\bar x_1 - \bar x_2)$$

即

$$(\bar x_1 - \bar x_2) \pm t^* \times \sqrt{\frac {s_1^2} {n_1} + \frac {s_2^2} {n_2}}$$

我们可以方便地计算

$$\bar x_1 - \bar x_2 = 11$$

$$\sqrt{\frac {s_1^2} {n_1} + \frac {s_2^2} {n_2}} \approx 1.12931$$

我们还需要求 $t^* = \text{invT}_\nu(1 - \frac {0.05} 2)$，但是我们不知道 t 分布的自由度 $\nu$。

> Welch's t-test：
>
> 设 $a = \frac {s_1^2} {n_1}$ 和 $b = \frac {s_2^2} {n_2}$，分别为两组均值的方差估计。
>
> $$\nu \approx \frac {(\frac {s_1^2} {n_1} + \frac {s_2^2} {n_2})^2} {\frac {s_1^4} {n_1^2 (n_1 - 1)} + \frac {s_2^4} {n_2^2 (n_2 - 1)}} = \frac {(a + b)^2} {\frac {a^2} {n_1 - 1} + \frac {b^2} {n_2 - 1}}$$
>
> 对于 $n_1 = n_2$ 的情况，有简化公式：
>
> $$\nu \approx (n-1) \frac {(s_1^2 + s_2^2)^2} {s_1^4 + s_2^4}$$

$$\begin{aligned}
    \nu \approx & (n-1) \frac {(s_1^2 + s_2^2)^2} {s_1^4 + s_2^4} \\
    =& (30 - 1) \frac {(3.5^2 + 5.1^2)^2} {3.5^4 + 1.5^4} \\
    =& 51.3572 \\
\end{aligned}$$

这样我们就可以计算 $\text{invT}_{51.3572}(0.975) \approx 2.00724$。

最后计算出答案区间：

$$\begin{aligned}
    & 11 \pm 2.00724 \times 1.12931 \\
    \approx & 11 \pm 2.26679 \\
    = & [8.73321, 13.2668] \\
\end{aligned}$$

对于 TI-NSpire 计算器，有一个捷径：`tInterval_2Samp` 选择“统计”，输入 $\bar x_1, s_1, n_1, \bar x_2, s_2, n_2$，即可获得全部数据：
- $[\text{CLower}, \text{CUpper}]$ 是置信区间。
- $\bar x \text{Diff}$ 是 $\bar x_1 - \bar x_2$。
- $\text{ME}$ 是 Margin of Error。

TODO: 能不能用 paired data

## Paired Data

> TODO:

令 $\mu = \mu_1 - \mu_2, \sigma^2 = \sigma_1^2 + \sigma_2^2$。

$$z_i = x_i - y_i \sim \mathcal N(\mu, \sigma^2)$$

$$\bar z \sim \mathcal N(\mu, \frac {\sigma^2} n)$$

$$\frac {\bar z - \mu} {\sigma / \sqrt n} \sim \mathcal N(0,1)$$

这个很熟悉啊，我们用 $s = \sqrt{\frac 1 {n-1} \sum (z_i - \bar z)^2}$ 代替 $\sigma$ 就得到 t 分布：

$$\frac {\bar z - \mu} {s / \sqrt n} \sim t_{n-1}$$

TODO: 我写的真的对吗？

https://math.fandom.com/zh/wiki/Behrens-Fisher_%E9%97%AE%E9%A2%98