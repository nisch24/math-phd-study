---
layout: default
title: "EN.553.761 — Nonlinear Optimization I"
parent: "Module D — Optimization & Operations Research"
nav_order: 1
permalink: /module_d/nonlinear_optimization_1/
---

# EN.553.761 — Nonlinear Optimization I

> *Unconstrained optimization theory and algorithms. This course develops the mathematical foundations — optimality conditions, convergence analysis, and practical algorithms (steepest descent, Newton, quasi-Newton) — that underpin machine learning, statistical estimation, and engineering design.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **State and verify first- and second-order optimality conditions** for unconstrained minimization problems.
2. **Analyze convergence rates** (linear, superlinear, quadratic) of iterative optimization algorithms.
3. **Implement and compare** line search and trust region frameworks.
4. **Derive and apply Newton's method** and understand its local quadratic convergence.
5. **Understand quasi-Newton methods** — particularly BFGS — and their superlinear convergence without explicit Hessian computation.

---

## Core Theory

### Unit 1: Optimality Conditions

#### 1.1 The Unconstrained Optimization Problem

$$\min_{x \in \mathbb{R}^n} f(x),$$

where $f: \mathbb{R}^n \to \mathbb{R}$ is sufficiently smooth (at least $C^2$ near any local minimizer of interest).

#### 1.2 First-Order Necessary Conditions

**Theorem**: If $x^*$ is a local minimizer of $f$ and $f$ is differentiable at $x^*$, then:

$$\nabla f(x^*) = 0.$$

*Proof*: For any direction $d \in \mathbb{R}^n$, the scalar function $g(t) = f(x^* + td)$ has a local minimum at $t = 0$, so $g'(0) = \nabla f(x^*)^T d = 0$. Since $d$ is arbitrary, $\nabla f(x^*) = 0$.

#### 1.3 Second-Order Conditions

**Necessary condition**: If $x^*$ is a local minimizer and $f \in C^2$, then $\nabla f(x^*) = 0$ and $\nabla^2 f(x^*) \succeq 0$ (positive semidefinite).

**Sufficient condition**: If $\nabla f(x^*) = 0$ and $\nabla^2 f(x^*) \succ 0$ (positive definite), then $x^*$ is a **strict local minimizer**.

*Proof of sufficiency*: By Taylor's theorem with remainder, for $\|d\|$ small:

$$f(x^* + d) = f(x^*) + \underbrace{\nabla f(x^*)^T d}_{=\,0} + \frac{1}{2} d^T \nabla^2 f(x^*) d + o(\|d\|^2).$$

Since $\nabla^2 f(x^*) \succ 0$, we have $d^T \nabla^2 f(x^*) d \geq \lambda_{\min} \|d\|^2 > 0$ for $d \neq 0$, so $f(x^* + d) > f(x^*)$ for all sufficiently small $\|d\| > 0$.

#### 1.4 Convexity and Its Consequences

**Definition**: $f$ is **convex** if $f(\alpha x + (1-\alpha)y) \leq \alpha f(x) + (1-\alpha) f(y)$ for all $x, y$ and $\alpha \in [0,1]$.

**Key Results**:
- $f \in C^2$ is convex $\Leftrightarrow$ $\nabla^2 f(x) \succeq 0$ for all $x$.
- For convex $f$: every local minimizer is a global minimizer.
- For **strictly convex** $f$: there is at most one global minimizer.

---

### Unit 2: Line Search Methods

#### 2.1 The General Line Search Framework

```
Given: initial point x_0, convergence tolerance ε
For k = 0, 1, 2, ...
    1. Choose a search direction d_k (descent direction: ∇f_k^T d_k < 0)
    2. Compute step length α_k > 0 by (approximately) solving min_{α>0} f(x_k + α d_k)
    3. Update: x_{k+1} = x_k + α_k d_k
    Convergence check: if ‖∇f(x_{k+1})‖ < ε, terminate
```

#### 2.2 The Wolfe Conditions

A step length $\alpha_k$ satisfies the **Wolfe conditions** if:

1. **Sufficient decrease (Armijo condition)**: $f(x_k + \alpha_k d_k) \leq f(x_k) + c_1 \alpha_k \nabla f_k^T d_k$
2. **Curvature condition**: $\nabla f(x_k + \alpha_k d_k)^T d_k \geq c_2 \nabla f_k^T d_k$

with $0 < c_1 < c_2 < 1$. Typical values: $c_1 = 10^{-4}$, $c_2 = 0.9$.

**Theorem (Zoutendijk)**: Suppose $f$ is bounded below and continuously differentiable on an open set containing the level set $\{x : f(x) \leq f(x_0)\}$, with $\nabla f$ Lipschitz there. If each $d_k$ is a descent direction and each $\alpha_k$ satisfies the Wolfe conditions, then:

$$\sum_{k=0}^\infty \cos^2\!\theta_k \, \|\nabla f_k\|^2 < \infty,$$

where $\theta_k$ is the angle between $d_k$ and $-\nabla f_k$. Consequently, $\nabla f_k \to 0$ whenever $\cos\theta_k$ is bounded away from zero.

#### 2.3 Steepest Descent

**Search direction**: $d_k = -\nabla f(x_k)$ — the direction of most rapid local decrease.

**Convergence on quadratics**: For $f(x) = \frac{1}{2}x^T A x - b^T x$ with $A$ symmetric, eigenvalues $0 < \lambda_1 \leq \cdots \leq \lambda_n$, and **exact** line search ($\alpha_k = \frac{g_k^T g_k}{g_k^T A g_k}$):

$$f(x_{k+1}) - f(x^*) \leq \left(\frac{\kappa - 1}{\kappa + 1}\right)^2 (f(x_k) - f(x^*)),$$

where $\kappa = \lambda_n / \lambda_1$ is the **condition number** of $A$. The convergence is **linear** (geometric), but can be extremely slow for ill-conditioned problems ($\kappa \gg 1$).

---

### Unit 3: Newton's Method and Modifications

#### 3.1 Newton's Method

**Search direction**: Solve the Newton system $\nabla^2 f(x_k) d_k = -\nabla f(x_k)$, i.e., $d_k = -[\nabla^2 f(x_k)]^{-1} \nabla f(x_k)$.

**Convergence**: Suppose $\nabla^2 f$ is Lipschitz continuous near a local minimizer $x^*$ with $\nabla^2 f(x^*) \succ 0$. Then for $x_0$ sufficiently close to $x^*$, Newton's method (with unit steps) converges **quadratically**:

$$\|x_{k+1} - x^*\| \leq C \|x_k - x^*\|^2.$$

*Proof Sketch*: Using $\nabla f(x^*) = 0$ and a Taylor expansion of $\nabla f$:

$$x_{k+1} - x^* = [\nabla^2 f(x_k)]^{-1}\!\left[\nabla^2 f(x_k)(x_k - x^*) - \nabla f(x_k)\right],$$

where the bracketed term equals $\int_0^1 [\nabla^2 f(x_k) - \nabla^2 f(x^* + t(x_k - x^*))](x_k - x^*)\,dt$, which is $O(\|x_k - x^*\|^2)$ by the Lipschitz continuity of $\nabla^2 f$. Since $\nabla^2 f(x^*)$ is invertible, $\|[\nabla^2 f(x_k)]^{-1}\|$ stays bounded near $x^*$.

#### 3.2 Modified Newton Methods

When $\nabla^2 f(x_k)$ is not positive definite, the pure Newton direction may point toward a saddle point or local maximum. Remedies:

- **Modified Cholesky factorization**: Replace $H_k$ with $H_k + \tau I$ for a minimal $\tau > 0$ restoring positive definiteness.
- **Trust region Newton**: Solve $\min_{\|d\| \leq \Delta_k} \bigl[f_k + \nabla f_k^T d + \tfrac{1}{2} d^T H_k d\bigr]$ — restricts the step to a ball of radius $\Delta_k$ within which the quadratic model is trusted.

---

### Unit 4: Quasi-Newton Methods

#### 4.1 Motivation

Newton's method requires computing and factoring $\nabla^2 f(x_k)$ at each iteration — $O(n^2)$ storage and $O(n^3)$ arithmetic. Quasi-Newton methods build approximate Hessians $B_k \approx \nabla^2 f(x_k)$ using only first-derivative information.

#### 4.2 The Secant Equation

Require $B_{k+1}$ to satisfy:

$$B_{k+1} s_k = y_k,$$

where $s_k = x_{k+1} - x_k$ and $y_k = \nabla f_{k+1} - \nabla f_k$. This mimics the finite-difference approximation to the Hessian action.

#### 4.3 The BFGS Update

The **Broyden-Fletcher-Goldfarb-Shanno** update is:

$$B_{k+1} = B_k - \frac{B_k s_k s_k^T B_k}{s_k^T B_k s_k} + \frac{y_k y_k^T}{y_k^T s_k}.$$

Equivalently, maintaining the inverse Hessian approximation $H_k = B_k^{-1}$:

$$H_{k+1} = \left(I - \frac{s_k y_k^T}{y_k^T s_k}\right) H_k \left(I - \frac{y_k s_k^T}{y_k^T s_k}\right) + \frac{s_k s_k^T}{y_k^T s_k}.$$

**Key Properties**:
- If $B_k \succ 0$ and $y_k^T s_k > 0$ (guaranteed by the Wolfe curvature condition), then $B_{k+1} \succ 0$.
- **Superlinear convergence**: $\|x_{k+1} - x^*\| = o(\|x_k - x^*\|)$ under mild conditions — faster than any fixed geometric rate.
- No Hessian computation required — only gradient evaluations.

#### 4.4 Limited-Memory BFGS (L-BFGS)

For large-scale problems ($n \gg 1$), storing $H_k$ explicitly costs $O(n^2)$ memory. L-BFGS retains only the last $m$ curvature pairs $\{(s_j, y_j)\}$ and applies the BFGS formula implicitly via the **two-loop recursion**, reducing storage to $O(mn)$.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Numerical Optimization* (2nd ed.) | Jorge Nocedal &amp; Stephen J. Wright | **Primary** — Chapters 2–7 |
| *Nonlinear Programming* (3rd ed.) | Dimitri P. Bertsekas | **Alternative** — Rigorous theoretical treatment |
| *Introductory Lectures on Stochastic Optimization* | John C. Duchi | **Supplementary** — Modern stochastic and online methods |
| *Convex Optimization* | Stephen Boyd &amp; Lieven Vandenberghe | **Supplementary** — Convex theory and duality |

---

## Problem Sets

### Problem Set 1: Optimality Conditions

1. **(cf. Nocedal &amp; Wright Ch. 2)** (a) Find all critical points of $f(x) = x_1^2 + x_2^2 - x_1 x_2 + x_1$ and verify the second-order sufficient conditions there. (b) Show that $g(x) = x_1^2 + x_2^2 - 2x_1x_2 + x_1 = (x_1 - x_2)^2 + x_1$ has **no** critical points and is unbounded below. Why does the small change in the cross term matter? (Consider the Hessians.)
2. **(Exam-style)** Let $f(x,y) = x^4 + y^4 - 2x^2 y^2 = (x^2 - y^2)^2$. Find all critical points and classify each. Note that the critical set is not isolated, and explain why the second-order test is inconclusive there.
3. **(Exam-style)** Prove: if $f$ is convex and differentiable, then $\nabla f(x^*) = 0 \Rightarrow x^*$ is a global minimizer.
4. **(Proof)** Show that for $f \in C^2$: $\nabla^2 f(x) \succeq 0$ for all $x$ if and only if $f$ is convex.
5. **(Challenge — Peano's example)** Let $f(x,y) = (y - x^2)(y - 3x^2)$. Show that the restriction of $f$ to every line through the origin has a strict local minimum at $0$, yet $0$ is not a local minimizer of $f$ (consider the curve $y = 2x^2$). Compute $\nabla^2 f(0)$ and explain why this does not contradict the second-order sufficient conditions.

### Problem Set 2: Line Search and Steepest Descent

1. **(cf. Nocedal &amp; Wright Lemma 3.1)** Prove that if $f$ is continuously differentiable and bounded below along the ray $\{x_k + \alpha d_k : \alpha > 0\}$, and $d_k$ is a descent direction, then a step length satisfying the Wolfe conditions exists.
2. **(Exam-style)** For steepest descent with exact line search on $f(x) = \frac{1}{2}x^T A x$, $A \succ 0$, prove the bound $f(x_{k+1}) \leq \left(\frac{\kappa-1}{\kappa+1}\right)^2 f(x_k)$ (via the Kantorovich inequality), and show it is attained for a suitable starting point. Conclude that the worst-case rate depends only on $\kappa(A)$.
3. **(Implementation)** Implement steepest descent with backtracking line search in Python. Test on the Rosenbrock function $f(x,y) = (1-x)^2 + 100(y-x^2)^2$.
4. **(Proof)** Prove Zoutendijk's theorem.
5. **(Application)** Explain geometrically why steepest descent exhibits "zigzag" behavior on ill-conditioned quadratics.

### Problem Set 3: Newton and BFGS

1. **(cf. Nocedal &amp; Wright Thm. 3.5)** Prove the quadratic convergence of Newton's method near a local minimizer $x^*$ with $\nabla^2 f(x^*) \succ 0$ and Lipschitz $\nabla^2 f$.
2. **(Exam-style)** Verify that the BFGS update preserves positive definiteness when $y_k^T s_k > 0$.
3. **(Implementation)** Implement BFGS with Wolfe line search. Compare convergence iteration counts with steepest descent on the Rosenbrock function.
4. **(Proof)** Show that the BFGS update satisfies the secant equation $B_{k+1} s_k = y_k$.
5. **(Challenge)** Prove superlinear convergence of BFGS: outline the Dennis-Moré characterization theorem and identify the key approximation condition.

---

## Study Guide &amp; Exam Preparation

{: .important }
> **Key Theorems for Nonlinear Optimization I**
>
> - **First-order necessary conditions** — $\nabla f(x^*) = 0$; proof via directional derivative
> - **Second-order sufficient conditions** — positive definite Hessian at a stationary point $\Rightarrow$ strict local min
> - **Zoutendijk's theorem** — global convergence guarantee for Wolfe line search with descent directions
> - **Quadratic convergence of Newton** — proof via Taylor expansion of $\nabla f$; requires $\nabla^2 f(x^*) \succ 0$
> - **Steepest descent convergence rate** — $((\kappa-1)/(\kappa+1))^2$ per step on quadratics; shows dependence on condition number
> - **BFGS properties** — secant equation, positive definiteness preservation, superlinear convergence

**Exam Preparation Tips**:
- Convergence proofs for Newton require explicit tracking of the $O(\|x_k - x^*\|^2)$ error term.
- For Zoutendijk: the key is that the Wolfe conditions bound $\cos^2\theta_k \|\nabla f_k\|^2$, summing to a finite quantity.
- Know both the $B$-form and $H$-form of the BFGS update and be able to derive the Sherman-Morrison-Woodbury identity connecting them.
