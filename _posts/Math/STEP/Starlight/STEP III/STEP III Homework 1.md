# Problem 1

> Using the series
>
> $$e^x = \sum_{n=0}^\infty \frac {x^n} {n!}$$
>
> show that $e > \frac 8 3$.

Setting $x = 1$ in the series:

$$\begin{aligned}
    e &= \sum_{n=0}^\infty \frac 1 {n!} \\
    &> \sum_{n=0}^3 \frac 1 {n!} \\
    &= \frac 8 3 \\
\end{aligned}$$

> Show that $n! > 2^n$ for $n \ge 4$ and hence show that $e < \frac {67} {24}$.

We prove the statement by mathematical induction.

Base case: when $n = 4$, $n! = 24$ and $2^n = 16$. Since $24 > 16$, the inequality holds.

Inductive step: Assume $n! > 2^n$ for some $n \ge 4$. For $n+1$:

$$\begin{aligned}
    n! &> 2^n \\
    n! \times (n+1) &> 2^n \times 2 \\
    (n+1)! &> 2^{n+1} \\
\end{aligned}$$

$\square$

$$\begin{aligned}
    e &= \frac 8 3 + \sum_{n=4}^\infty \frac 1 {n!} \\
    &< \frac 8 3 + \sum_{n=4}^\infty \frac 1 {2^n} \\
    &= \frac 8 3 + \frac 1 {16} \frac 1 {1 - \frac 1 2} \\
    &= \frac {67} {24} \\
\end{aligned}$$

$\square$

> Show that the curve with equation
>
> $$y = 3 e^{2x} + 14 \ln \left( \frac 4 3 - x \right), \quad x < \frac 4 3$$
>
> has a minimum turning point between $x = \frac 1 2$ and $x = 1$ and give a sketch to show the shape of the curve.

Take the derivative of $y$:

$$y' = 6 (e^{2x} + \frac 7 {3x-4})$$

Plug in $x = \frac 1 2$ and $x = 1$:

$$\begin{aligned}
    y'\left( \frac 1 2 \right) &= 6 (e - \frac {14} 5) \\
    &< 6 \left( \frac {67} {24} - \frac {14} 5 \right) \\
    &= - \frac 1 {20} < 0 \\
\end{aligned}$$

$$\begin{aligned}
    y'(1) &= 6 (e^2 - 7) \\
    &> 6 \left( \left( \frac 8 3 \right)^2 - 7 \right) \\
    &= \frac 2 3 > 0 \\
\end{aligned}$$

Since $y'$ is a continuous function on the interval $[\frac 1 2, 1]$, by the Intermediate Value Theorem, there exists $\xi \in [\frac 1 2, 1]$ so that $y'(\xi) = 0$. Furthermore, the sign of $y'(x)$ flips from negative to positive when passing $x = \xi$, so $x = \xi$ is a local minimum.

$\square$

# Problem 2

> In this question, you may assume that the infinite series
>
> $$\ln(1+x) = \sum_{n=1}^\infty (-1)^{n+1} \frac {x^n} n$$
>
> is valid for $\lvert x \rvert < 1$.

> Let $n$ be an integer greater than $1$. Show that, for any positive integer $k$,
>
> $$\frac 1 {(k+1) n^{k+1}} < \frac 1 {k n^k}$$
>
> Hence show that $\ln\left( 1 + \frac 1 n \right) < \frac 1 n$. Deduce that
>
> $$\left( 1 + \frac 1 n \right)^n < e$$

$$\begin{aligned}
    n &> \frac k {k+1} \\
    (k+1) n^{k+1} &> k n^k \\
    \frac 1 {(k+1) n^{k+1}} &< \frac 1 {k n^k} \\
\end{aligned}$$

$\square$

Plug in $x = \frac 1 n$:

$$\begin{aligned}
    \ln\left( 1 + \frac 1 n \right) =& \sum_{k=1}^\infty (-1)^{k+1} \frac 1 {k n^k} \\
    =& \frac 1 n - \left( \frac 1 {2n^2} - \frac 1 {3n^3} \right) - \left( \frac 1 {4n^4} - \frac 1 {5n^5} \right) - \cdots \\
    <& \frac 1 n
\end{aligned}$$

$$\begin{aligned}
    \ln\left( 1 + \frac 1 n \right) &< \frac 1 n \\
    \left( 1 + \frac 1 n \right)^n &< e \\
\end{aligned}$$

$\square$

> Show, using an expansion in powers of $\frac 1 y$, that $\ln\left( \frac {2y+1} {2y-1} \right) > \frac 1 y$ for $y > \frac 1 2$.
>
> Deduce that, for any positive integer $n$,
>
> $$e < \left( 1 + \frac 1 n \right)^{n + \frac 1 2}$$

$$\begin{aligned}
    & \ln\left( \frac {2y+1} {2y-1} \right) \\
    =& \ln\left( \frac {1 + \frac 1 {2y}} {1 - \frac 1 {2y}} \right) \\
    =& \ln\left( 1 + \frac 1 {2y} \right) - \ln\left( 1 - \frac 1 {2y} \right) \\
    =& \sum_{k=1}^\infty (-1)^{k+1} \frac 1 k \left( \frac 1 {(2y)^k} - \frac 1 {(-2y)^k} \right) \\
    =& \sum_{t=0}^\infty \frac 1 {2t+1} \frac 2 {(2y)^{2t+1}} \\
    >& \frac 1 y \\
\end{aligned}$$

$\square$

$$\begin{aligned}
    \ln\left( \frac {2y+1} {2y-1} \right) >& \frac 1 y \\
    \ln\left( 1 + \frac 1 {y - \frac 1 2} \right) >& \frac 1 y \\
    \left( 1 + \frac 1 {y - \frac 1 2} \right)^y >& e
\end{aligned}$$

Plug in $y = n + \frac 1 2$:

$$e < \left( 1 + \frac 1 n \right)^{n + \frac 1 2}$$

$\square$

> Use parts (i) and (ii) to show that as $n \to \infty$
>
> $$\left( 1 + \frac 1 n \right)^n \to e$$

$$\begin{aligned}
    & \lim_{n \to \infty} \left( 1 + \frac 1 n \right)^{n + \frac 1 2} \\
    =& \lim_{n \to \infty} \left( 1 + \frac 1 n \right)^n \times \lim_{n \to \infty} \sqrt{1 + \frac 1 n} \\
    =& \lim_{n \to \infty} \left( 1 + \frac 1 n \right)^n \\
\end{aligned}$$

We know

$$\left( 1 + \frac 1 n \right)^n < e < \left( 1 + \frac 1 n \right)^{n + \frac 1 2}$$

By the Squeeze Theorem, they must tend to the same limit, which is $e$.

$\square$

# Problem 3

> If $s_1, s_2, s_3, \cdots$ and $t_1, t_2, t_3, \cdots$ are sequences of positive numbers, we write
>
> $$(s_n) \le (t_n)$$
>
> to mean "there exists a positive integer $m$ such that $s_n \le t_n$ whenever $n \ge m$".
>
> Determine whether each of the following statements is true or false. In the case of a true statement, you should give a proof which includes an explicit determination of an appropriate $m$; in the case of a false statement, you should give a counterexample.

> $$(1000n) \le (n^2)$$

**True**. Choose $m = 1000$, then for any $n \ge m$ we have

$$1000n \le n^2$$

> If it is not the case that $(s_n) \le (t_n)$, then it is the case that $(t_n) \le (s_n)$.

**False**. Choose $s_n = 2 + (-1)^n$ and $t_n = 2 + (-1)^{n+1}$. Since they are always alternating, there is no appropriate $m$.

> If $(s_n) \le (t_n)$ and $(t_n) \le (u_n)$, then $(s_n) \le (u_n)$.

**True**. Let $m_1$ and $m_2$ be the appropriate $m$ for the former two statements. Choose $m = \max\{m_1, m_2\}$. For any $n \ge m$, we have

$$s_n \le t_n \le u_n$$

which meets the definition.

> $$(n^2) \le (2^n)$$

**True**. Choose $m = 4$.

We prove the statement by mathematical induction.

Base case: when $n = 4$, $n^2 = 16$ and $2^n = 16$. Since $16 \le 16$, the inequality holds.

Inductive step: Assume $n^2 < 2^n$ for some $n \ge 4$. For $n+1$:

$$\begin{aligned}
    n^2 &\le 2^n \\
    n^2 \times \left( \frac {n+1} n \right)^2 &\le 2^n \times 2 \\
    (n+1)^2 &\le 2^{n+1}
\end{aligned}$$

The middle step holds because

$$\left( \frac {n+1} n \right)^2 \le \left( \frac 5 4 \right)^2 < 2$$

$\square$

# Problem 4

> Given that $f''(x) > 0$ when $ a \le x \le b$, explain with the aid of a sketch why
>
> $$(b - a) f\left( \frac {a + b} 2 \right) < \int_a^b f(x) dx < (b - a) \frac {f(a) + f(b)} 2$$

The curve of $f$ is under the line segment from $(a, f(a))$ to $(b, f(b))$, so the area under the curve is less than the trapezoid under the line segment:

$$\int_a^b f(x) dx < (b - a) \frac {f(a) + f(b)} 2$$

Draw a tangent line of the curve at the point $(\frac {a+b} 2, f(\frac {a+b} 2))$. The area of trapezoid under the tangent line is less than the area under the curve:

$$(b - a) f\left( \frac {a + b} 2 \right) < \int_a^b f(x) dx$$

> By choosing suitable $a$, $b$ and $f(x)$, show that
>
> $$\frac 4 {(2n-1)^2} < \frac 1 {n-1} - \frac 1 n < \frac 1 2 \left( \frac 1 {n^2} + \frac 1 {(n-1)^2} \right)$$
>
> where $n$ is an integer greater than $1$.

Choose $a = n-1, b = n, f(x) = \frac 1 {x^2}$:

$$\begin{aligned}
    f\left( \frac {2n-1} 2 \right) < \int_{n-1}^n f(x) dx < \frac {f(n-1) + f(n)} 2 \\
    \frac 4 {(2n - 1)^2} < \frac 1 {n-1} - \frac 1 n < \frac 1 2 \left( \frac 1 {n^2} + \frac 1 {(n-1)^2} \right)
\end{aligned}$$

> Deduce that
>
> $$4 \left( \frac 1 {3^2} + \frac 1 {5^2} + \frac 1 {7^2} + \cdots \right) < 1 < \frac 1 2 + \left( \frac 1 {2^2} + \frac 1 {3^2} + \frac 1 {4^2} + \cdots \right)$$

$$\begin{aligned}
    4 \sum_{n=2}^\infty \frac 1 {(2n-1)^2} &< \sum_{n=2}^\infty \left( \frac 1 {n-1} - \frac 1 n \right) < \frac 1 2 \sum_{n=2}^\infty \left( \frac 1 {n^2} + \frac 1 {(n-1)^2} \right) \\
    4 \sum_{n=2}^\infty \frac 1 {(2n-1)^2} &< 1 < \frac 1 2 + \sum_{n=2}^\infty \frac 1 {n^2} \\
\end{aligned}$$

$\square$

> Show that
>
> $$\frac 1 2 \left( \frac 1 {3^2} + \frac 1 {4^2} + \frac 1 {5^2} + \frac 1 {6^2} + \cdots \right) < \frac 1 {3^2} + \frac 1 {5^2} + \frac 1 {7^2} + \cdots$$
>
> and hence show that
>
> $$\frac 3 2 < \sum_{n=1}^\infty \frac 1 {n^2} < \frac 7 4$$

$$\begin{aligned}
    \frac 1 {4^2} + \frac 1 {6^2} + \cdots &< \frac 1 {3^2} + \frac 1 {5^2} + \cdots \\
    \frac 1 {3^2} + \frac 1 {4^2} + \frac 1 {5^2} + \frac 1 {6^2} + \cdots &< 2 \left( \frac 1 {3^2} + \frac 1 {5^2} + \cdots \right) \\
    \frac 1 2 \left( \frac 1 {3^2} + \frac 1 {4^2} + \frac 1 {5^2} + \frac 1 {6^2} + \cdots \right) &< \frac 1 {3^2} + \frac 1 {5^2} + \frac 1 {7^2} + \cdots
\end{aligned}$$

$\square$

$$1 < \frac 1 2 + \sum_{n=2}^\infty \frac 1 {n^2} \implies \frac 3 2 < \sum_{n=1}^\infty \frac 1 {n^2}$$

$$\begin{aligned}
    4 \sum_{n=2}^\infty \frac 1 {(2n-1)^2} &< 1 \\
    \sum_{n=3}^\infty \frac 1 {n^2} < 2 \sum_{n=2}^\infty \frac 1 {(2n-1)^2} < \frac 1 2 \\
    \sum_{n=1}^\infty \frac 1 {n^2} < \frac 7 4 \\
\end{aligned}$$

$\square$