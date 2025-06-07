---
title: "AP E&M Chapter 14-16 Part 4: Maxwell’s Equations"
date: 2025-06-01
permalink: /posts/2025/06/AP-E_M-Chapter-14-16-Part-4-Maxwells-Equations/
excerpt: "Maxwell’s equations: the Holy Grail of electricity and magnetism."
tags:
  - AP Physics C E&M
---

# 💡 Ampere's Law is not Perfect

We take the divergence of both sides of the formula of Ampere's Law:

$$\begin{aligned}
    \nabla \times \vec{B} &= \mu_0 \vec{J} \\
    \nabla \cdot (\nabla \times \vec{B}) &= \mu_0 (\nabla \cdot \vec{J}) \\
    \nabla \cdot \vec{J} &= 0
\end{aligned}$$

This result is inconsistent with **the law of charge conservation (电荷守恒定律)**:

$$\boxed{
    \frac {\partial \rho} {\partial t} + \nabla \cdot \vec{J} = 0
}$$

Therefore, Maxwells added a term into the formula:

$$\colorbox{#424242}{$
    \color{white}\boxed{
        \nabla \times \vec{B} = \mu_0 (\vec{J} + \varepsilon_0 \frac {\partial \vec{E}} {\partial t})
    }
$}$$

We can verify the validity by taking the divergence on both sides again:

$$\begin{aligned}
    \nabla \times \vec{B} &= \mu_0 (\vec{J} + \varepsilon_0 \frac {\partial \vec{E}} {\partial t}) \\
    \nabla \cdot (\nabla \times \vec{B}) &= \mu_0 (\nabla \cdot \vec{J} + \varepsilon_0 \frac {\partial (\nabla \cdot \vec{E})} {\partial t}) \\
    \nabla \cdot \vec{J} + \frac {\partial \rho} {\partial t} &= 0 & \nabla \cdot \vec{E} = \frac \rho {\varepsilon_0} \\
\end{aligned}$$

Therefore, the new Ampere's Law is consistent with charge conservation.

Notably, the added term is not unique, as long as it does not affect the divergence. For example, $\varepsilon_0 \frac {\partial \vec{E}} {\partial t} + \nabla \times \vec{F}$ (where $\vec{F}$ is any vector field) is also valid. However, the correctness of this particular formula is guaranteed by experiment (which means this is a _law_), and therefore this formula is added into the Maxwell's Equations.

The name of this new law is **Ampere-Maxwell Law**.

#  Ampere-Maxwell Law

The integral form of Ampere-Maxwell Law is:

$$\colorbox{#424242}{$
    \color{white}\boxed{
        \displaystyle \oint \vec{B} \cdot d\vec{l} = \mu_0 (I_{\text{enc}} + \varepsilon_0 \frac {\partial \Phi_E} {\partial t})
    }
$}$$

The term $\varepsilon_0 \frac {\partial \Phi_E} {\partial t}$ is called **displacement current (位移电流)**. 

# Maxwell's Equations

TODO:

$$\colorbox{#424242}{$
    \color{white}\boxed{
        \begin{cases}
            \displaystyle \oint \vec{E} \cdot d\vec{A} = \frac {Q_{\text{enc}}} {\varepsilon_0} \\
            \displaystyle \oint \vec{B} \cdot d\vec{A} = 0 \\
            \displaystyle \oint \vec{E} \cdot d\vec{l} = - \frac {\partial \Phi_B} {\partial t} \\
            \displaystyle \oint \vec{B} \cdot d\vec{l} = \mu_0 (I_{\text{enc}} + \varepsilon_0 \frac {\partial \Phi_E} {\partial t}) \\
        \end{cases}
    }
$}$$

$$\colorbox{#424242}{$
    \color{white}\boxed{
        \begin{cases}
            \nabla \cdot \vec{E} = \frac \rho {\varepsilon_0} \\
            \nabla \cdot \vec{B} = 0 \\
            \nabla \times \vec{E} = - \frac {\partial \vec{B}} {\partial t} \\
            \nabla \times \vec{B} = \mu_0 (\vec{J} + \varepsilon_0 \frac {\partial \vec{E}} {\partial t}) \\
        \end{cases}
    }
$}$$

$$\colorbox{#424242}{$
    \color{white}\boxed{
        \vec{F} = q (\vec{E} + \vec{v} \times \vec{B})
    }
$}$$