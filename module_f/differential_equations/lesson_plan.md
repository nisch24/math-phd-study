---
layout: default
title: "F.1 — Ordinary & Partial Differential Equations"
parent: "Module F — Differential Equations & Numerical Analysis"
nav_order: 1
permalink: /module_f/differential_equations/
---

# F.1 — Ordinary &amp; Partial Differential Equations

> *A differential equation is a local rule: given the present state, it says how the state changes. This course asks the global questions: does a solution exist, is it unique, where does it end up, and how do disturbances spread? Most of the answers come from analysis (Module A) and linear algebra (eigenvalues), not from memorized solution recipes.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Prove existence and uniqueness** of solutions to initial value problems (Picard–Lindelöf), and recognize when uniqueness or global existence fails.
2. **Solve linear systems** $\dot{x} = Ax$ via the matrix exponential and classify equilibria by the eigenvalues of $A$.
3. **Analyze nonlinear systems qualitatively** using linearization and Lyapunov functions.
4. **Solve the heat, wave, and Laplace equations** in model settings, and prove uniqueness with maximum principles and energy methods.
5. **Connect the heat equation to Brownian motion**, and gradient flows to optimization.

---

## Core Theory

### Unit 1: Existence, Uniqueness, and Well-Posedness

Consider the **initial value problem** $\dot{x} = f(t, x)$, $x(t_0) = x_0$, with $x \in \mathbb{R}^n$. It is equivalent to the integral equation

$$x(t) = x_0 + \int_{t_0}^t f(s, x(s))\,ds.$$

**Theorem (Picard–Lindelöf)**: Suppose $f$ is continuous on $R = \{|t - t_0| \leq a,\ \|x - x_0\| \leq b\}$, bounded there by $M$, and **Lipschitz in $x$**: $\|f(t,x) - f(t,y)\| \leq L\|x - y\|$. Then the IVP has a unique solution on $|t - t_0| \leq h$, where $h = \min(a, b/M)$.

*Proof idea*: The **Picard operator** $(Tx)(t) = x_0 + \int_{t_0}^t f(s, x(s))\,ds$ maps the closed ball of continuous curves staying within $b$ of $x_0$ into itself (that is why $h \leq b/M$). On a short enough interval ($hL < 1$) it is a contraction in the sup norm, so the Banach Fixed-Point Theorem from Module A gives a unique fixed point. A weighted sup norm (or iterating $T$) removes the $hL < 1$ restriction.

**Grönwall's inequality and continuous dependence**: two solutions with initial values $x_0, y_0$ satisfy

$$\|x(t) - y(t)\| \leq \|x_0 - y_0\|\, e^{L|t - t_0|}.$$

**Intuition**: the Lipschitz constant bounds how fast nearby solutions can separate. They can diverge exponentially, which is chaos in miniature, but they cannot cross or split. Existence, uniqueness, and continuous dependence on the data together make a problem **well-posed**.

**When the hypotheses fail**:
- **Non-uniqueness**: $\dot{x} = 3x^{2/3}$, $x(0) = 0$ has the solutions $x \equiv 0$ and $x = t^3$, because $x^{2/3}$ is not Lipschitz at $0$.
- **Finite-time blow-up**: $\dot{x} = x^2$, $x(0) = 1$ has the solution $x = 1/(1 - t)$, which exists only for $t < 1$. Picard–Lindelöf is a *local* theorem.

---

### Unit 2: Linear Systems

For $\dot{x} = Ax$ with constant $A \in \mathbb{R}^{n \times n}$:

$$x(t) = e^{At}x_0, \qquad e^{At} = \sum_{k=0}^\infty \frac{(At)^k}{k!}.$$

If $A = V\Lambda V^{-1}$ is diagonalizable, then $e^{At} = V e^{\Lambda t} V^{-1}$, so every solution is a combination of modes $e^{\lambda_i t} v_i$. For a Jordan block, $e^{At}$ also contains terms like $t e^{\lambda t}$.

**Stability Theorem**: The origin is asymptotically stable (all solutions $\to 0$) iff **every eigenvalue of $A$ has negative real part**.

**Intuition**: each eigen-direction evolves independently, growing or decaying at rate $\operatorname{Re}\lambda$ and rotating at rate $\operatorname{Im}\lambda$. The slowest-decaying mode dominates in the long run, exactly as the smallest eigenvalue controls the convergence of gradient descent in Module D.

**Planar classification** with $\tau = \operatorname{tr} A$ and $\Delta = \det A$ (eigenvalues solve $\lambda^2 - \tau\lambda + \Delta = 0$):

| Region | Equilibrium type |
|--------|------------------|
| $\Delta < 0$ | Saddle (real eigenvalues of opposite sign) |
| $\Delta > 0$, $\tau < 0$ | Stable: node if $\tau^2 \geq 4\Delta$, spiral if $\tau^2 < 4\Delta$ |
| $\Delta > 0$, $\tau > 0$ | Unstable: node or spiral, by the same test |
| $\Delta > 0$, $\tau = 0$ | Center (closed orbits) |

**Forced systems (variation of parameters)**: $\dot{x} = Ax + g(t)$ has $x(t) = e^{At}x_0 + \int_0^t e^{A(t-s)}g(s)\,ds$.

---

### Unit 3: Nonlinear Systems and Stability

An **equilibrium** $x^*$ satisfies $f(x^*) = 0$. Its **linearization** is $\dot{y} = Df(x^*)\,y$.

**Theorem (Hartman–Grobman)**: If no eigenvalue of $Df(x^*)$ has zero real part (a **hyperbolic** equilibrium), the nonlinear flow near $x^*$ is topologically equivalent to its linearization. In particular, if all eigenvalues have negative real part, $x^*$ is asymptotically stable. When some eigenvalue has zero real part, linearization is inconclusive: $\dot{x} = -x^3$ and $\dot{x} = x^3$ have the same linearization at $0$ but opposite stability.

**Lyapunov's method**: Let $V$ be positive definite near $x^*$ (i.e. $V(x^*) = 0$ and $V > 0$ elsewhere), with $\dot{V} = \nabla V \cdot f$.
- If $\dot{V} \leq 0$, then $x^*$ is stable.
- If $\dot{V} < 0$ away from $x^*$, then $x^*$ is asymptotically stable.
- **LaSalle's invariance principle**: if $\dot{V} \leq 0$ on a compact forward-invariant set, trajectories approach the largest invariant subset of $\{\dot{V} = 0\}$.

**Intuition**: a Lyapunov function is an "energy" that can only go down. You don't need to solve the equation, only to show that something always decreases.

**Gradient flows**: for $\dot{x} = -\nabla f(x)$,

$$\frac{d}{dt} f(x(t)) = -\|\nabla f(x(t))\|^2 \leq 0,$$

so $f$ itself is a Lyapunov function, and every nondegenerate local minimizer ($\nabla f(x^*) = 0$, $\nabla^2 f(x^*) \succ 0$) is asymptotically stable: the linearization $\dot{y} = -\nabla^2 f(x^*)\,y$ has only negative eigenvalues. Gradient descent with step $h$ is the forward-Euler discretization of this flow; see F.2 for why the step size must satisfy $h < 2/\lambda_{\max}(\nabla^2 f)$.

---

### Unit 4: Partial Differential Equations

A second-order linear PDE $a u_{xx} + 2b u_{xy} + c u_{yy} + \cdots = 0$ is **elliptic** if $b^2 - ac < 0$, **parabolic** if $b^2 - ac = 0$, and **hyperbolic** if $b^2 - ac > 0$. The prototypes behave very differently:

| Equation | Type | Behavior |
|----------|------|----------|
| Heat: $u_t = k u_{xx}$ | Parabolic | Smoothing, irreversible, infinite propagation speed |
| Wave: $u_{tt} = c^2 u_{xx}$ | Hyperbolic | Signals travel at speed $c$; no smoothing; reversible |
| Laplace: $u_{xx} + u_{yy} = 0$ | Elliptic | Equilibrium states; values determined by the boundary |

#### 4.1 The Heat Equation

On $[0, L]$ with $u(0,t) = u(L,t) = 0$ and $u(x, 0) = \varphi(x)$, **separation of variables** gives

$$u(x,t) = \sum_{n=1}^\infty b_n\, e^{-k(n\pi/L)^2 t} \sin\!\left(\frac{n\pi x}{L}\right), \qquad b_n = \frac{2}{L}\int_0^L \varphi(x)\sin\!\left(\frac{n\pi x}{L}\right)dx.$$

**Intuition**: the $n$-th frequency decays like $e^{-cn^2 t}$, so the high-frequency detail disappears almost instantly. That is why heat smooths any initial condition, and why running it backward in time is ill-posed.

**Weak maximum principle**: a solution on $[0,L] \times [0,T]$ attains its maximum on the initial line $t = 0$ or on the boundary $x \in \{0, L\}$. **Energy method**: $E(t) = \int_0^L u^2\,dx$ satisfies $E'(t) = -2k\int_0^L u_x^2\,dx \leq 0$. Either fact gives uniqueness and stability: apply it to the difference of two solutions.

**Connection to probability**: $u(t,x) = E[g(x + B_t)]$, where $B$ is Brownian motion, solves $u_t = \tfrac{1}{2}u_{xx}$ with $u(0, x) = g(x)$. Heat spreading is the averaged behavior of random walkers, and the Gaussian heat kernel is the density of $B_t$.

#### 4.2 The Wave Equation

On $\mathbb{R}$, with $u(x,0) = \varphi(x)$ and $u_t(x,0) = \psi(x)$, **d'Alembert's formula** is

$$u(x,t) = \frac{1}{2}\big[\varphi(x + ct) + \varphi(x - ct)\big] + \frac{1}{2c}\int_{x - ct}^{x + ct} \psi(s)\,ds.$$

The value at $(x,t)$ depends only on the data in $[x - ct, x + ct]$ (the **domain of dependence**): information travels at finite speed $c$, and singularities in the data propagate without smoothing.

#### 4.3 Laplace's Equation

Solutions of $\Delta u = 0$ are **harmonic**. They have the **mean value property** (the value at a point equals the average over any circle centered there), which implies the **maximum principle**: a nonconstant harmonic function has no interior maximum. Consequently the Dirichlet problem ($\Delta u = 0$ in $\Omega$, $u = g$ on $\partial\Omega$) has at most one solution.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Nonlinear Dynamics and Chaos* (2nd ed.) | Steven Strogatz | **Primary (ODE)** — The most intuitive introduction to qualitative dynamics |
| *Differential Equations, Dynamical Systems, and an Introduction to Chaos* | Hirsch, Smale &amp; Devaney | **Primary (ODE theory)** — Linear systems and existence theory with proofs |
| *Partial Differential Equations: An Introduction* (2nd ed.) | Walter Strauss | **Primary (PDE)** — Standard first PDE course |
| *Partial Differential Equations* (2nd ed.) | Lawrence C. Evans | **Advanced** — The graduate reference |

---

## Problem Sets

### Problem Set 1: Existence and Uniqueness

1. **(Core)** Compute the Picard iterates for $\dot{x} = x$, $x(0) = 1$, and show they are the partial sums of $e^t$.
2. **(Core)** Show that $\dot{x} = 3x^{2/3}$, $x(0) = 0$ has infinitely many solutions. *(Hint: stay at $0$ until an arbitrary time $c$, then follow $(t-c)^3$.)* Identify the hypothesis of Picard–Lindelöf that fails.
3. **(Proof)** Prove Grönwall's inequality in the form: if $u$ is continuous, nonnegative, and $u(t) \leq C + L\int_0^t u(s)\,ds$, then $u(t) \leq Ce^{Lt}$. Deduce continuous dependence on initial data.
4. **(Core)** Solve $\dot{x} = 1 + x^2$, $x(0) = 0$, and show the solution cannot be extended past $t = \pi/2$, even though the right-hand side is smooth.
5. **(Challenge)** Prove Picard–Lindelöf on an interval with $hL < 1$ by showing the Picard operator is a contraction on a suitable complete metric space of continuous functions.

### Problem Set 2: Linear and Nonlinear Systems

1. **(Core)** Solve $\dot{x} = Ax$ for $A = \begin{pmatrix} 0 & 1 \\ -2 & -3 \end{pmatrix}$ and classify the origin.
2. **(Core)** Show that $\exp\!\left(t\begin{pmatrix} \lambda & 1 \\ 0 & \lambda \end{pmatrix}\right) = e^{\lambda t}\begin{pmatrix} 1 & t \\ 0 & 1 \end{pmatrix}$.
3. **(Proof)** Prove that if $A$ is diagonalizable and every eigenvalue has negative real part, then $\|e^{At}x_0\| \to 0$ for every $x_0$. Then explain how the argument changes when $A$ is not diagonalizable.
4. **(Core)** Find and classify all equilibria of the Lotka–Volterra competition model $\dot{x} = x(3 - x - 2y)$, $\dot{y} = y(2 - x - y)$.
5. **(Challenge)** For the damped pendulum $\ddot{\theta} + b\dot{\theta} + \sin\theta = 0$ ($b > 0$), show that $E = \tfrac{1}{2}\dot{\theta}^2 + (1 - \cos\theta)$ is nonincreasing. Use LaSalle's principle to show that every trajectory with $E(0) < 2$ and $|\theta(0)| < \pi$ converges to $(\theta, \dot{\theta}) = (0, 0)$. (Why are both conditions needed? What happens if $\theta(0)$ is near $2\pi$?)

### Problem Set 3: PDEs

1. **(Core)** Solve the heat equation $u_t = u_{xx}$ on $[0, \pi]$ with zero boundary values and $u(x, 0) = x(\pi - x)$. Show that $b_n = \frac{8}{\pi n^3}$ for odd $n$ and $0$ for even $n$.
2. **(Proof)** Use the energy method to prove uniqueness for the heat equation with Dirichlet boundary conditions.
3. **(Core)** Derive d'Alembert's formula by factoring $\partial_t^2 - c^2\partial_x^2 = (\partial_t - c\partial_x)(\partial_t + c\partial_x)$, and sketch the solution for $\varphi = \mathbf{1}_{[-1,1]}$, $\psi = 0$.
4. **(Proof)** Prove the mean value property for harmonic functions in the plane, and deduce the maximum principle.
5. **(Challenge)** Verify that $u(t,x) = E[g(x + B_t)] = \int g(y)\frac{1}{\sqrt{2\pi t}}e^{-(x-y)^2/(2t)}\,dy$ solves $u_t = \tfrac{1}{2}u_{xx}$ for bounded continuous $g$, and that $u(t,x) \to g(x)$ as $t \downarrow 0$. Explain the smoothing effect probabilistically.

---

## Study Guide

{: .important }
> **Key results**
>
> - **Picard–Lindelöf** — Lipschitz $\Rightarrow$ local existence and uniqueness, via the Contraction Mapping Principle
> - **Grönwall** — continuous dependence; nearby solutions separate at most exponentially
> - **Linear stability** — $\operatorname{Re}\lambda_i < 0$ for all $i$ $\iff$ asymptotic stability; the trace–determinant classification
> - **Lyapunov / LaSalle** — stability without solving the equation
> - **Heat / Wave / Laplace** — smoothing vs. finite speed vs. equilibrium; maximum principles and energy methods for uniqueness

**Habits that pay off**: before solving any ODE, find the equilibria and their stability. Before solving any PDE, ask what is conserved or what decreases. Those two questions usually reveal the long-time behavior before you compute anything.
