---
layout: default
title: "EN.553.761 — Nonlinear Optimization I"
parent: "Module D — Optimization & Operations Research"
nav_order: 1
permalink: /module_d/nonlinear_optimization_1/
---

# EN.553.761 — Nonlinear Optimization I

> *Unconstrained optimization theory and algorithms. This course develops the mathematical foundations — optimality conditions, convergence analysis, and practical algorithms (steepest descent, Newton, Quasi-Newton) — that underpin machine learning, statistical estimation, and engineering design.*

---

## Learning Objectives

1. **State and verify first- and second-order optimality conditions** for unconstrained problems.
2. **Analyze convergence rates** (linear, superlinear, quadratic) of iterative methods.
3. **Implement and compare** line search and trust region frameworks.
4. **Derive and apply Newton's method** and its modifications.
5. **Understand Quasi-Newton methods** (BFGS, L-BFGS) and their superlinear convergence.

---

## Core Theory

### Unit 1: Optimality Conditions

#### 1.1 The Unconstrained Optimization Problem

$$\min_{x \in \mathbb{R}^n} f(x)$$

where $f: \mathbb{R}^n \to \mathbb{R}$ is sufficiently smooth (at least $C^2$).

#### 1.2 First-Order Necessary Conditions

**Theorem**: If $x^*$ is a local minimizer of $f$ and $f$ is differentiable at $x^*$, then:

$$\nabla f(x^*) = 0$$

*Proof*: For any direction $d$, $g(t) = f(x^* + td)$ has a local minimum at $t = 0$, so $g'(0) = \nabla f(x^*)^T d = 0$. Since $d$ is arbitrary, $\nabla f(x^*) = 0$.

#### 1.3 Second-Order Conditions

**Necessary condition**: If $x^*$ is a local minimizer and $f \in C^2$, then $\nabla f(x^*) = 0$ and $\nabla^2 f(x^*) \succeq 0$ (positive semidefinite).

**Sufficient condition**: If $\nabla f(x^*) = 0$ and $\nabla^2 f(x^*) \succ 0$ (positive definite), then $x^*$ is a **strict local minimizer**.

*Proof of sufficiency*: By Taylor's theorem, for $\|d\|$ small:

$$f(x^* + d) = f(x^*) + \nabla f(x^*)^T d + \frac{1}{2} d^T \nabla^2 f(x^*) d + o(\|d\|^2) = f(x^*) + \frac{1}{2} d^T \nabla^2 f(x^*) d + o(\|d\|^2)$$

Since $\nabla^2 f(x^*) \succ 0$, we have $d^T \nabla^2 f(x^*) d \geq \lambda_{\min} \|d\|^2 > 0$ for $d \neq 0$, so $f(x^* + d) > f(x^*)$ for small $\|d\| > 0$.

#### 1.4 Convexity

**Definition**: $f$ is **convex** if $f(\alpha x + (1-\alpha)y) \leq \alpha f(x) + (1-\alpha) f(y)$ for all $x, y$ and $\alpha \in [0,1]$.

**Key Results**:
- $f \in C^2$ is convex $\Leftrightarrow$ $\nabla^2 f(x) \succeq 0$ for all $x$.
- For convex $f$: every local minimizer is a global minimizer.
- For **strictly convex** $f$: at most one global minimizer exists.

---

### Unit 2: Line Search Methods

#### 2.1 The Line Search Framework

```
Given: starting point x_0, convergence tolerance ε
For k = 0, 1, 2, ...
    1. Choose a search direction d_k
    2. Compute step length α_k > 0 by (approximately) minimizing f(x_k + α d_k)
    3. Set x_{k+1} = x_k + α_k d_k
    Check convergence: if ‖∇f(x_{k+1})‖ < ε, stop
```

#### 2.2 Wolfe Conditions

A step length $\alpha_k$ satisfies the **Wolfe conditions** if:

1. **Sufficient decrease (Armijo)**: $f(x_k + \alpha_k d_k) \leq f(x_k) + c_1 \alpha_k \nabla f_k^T d_k$
2. **Curvature condition**: $\nabla f(x_k + \alpha_k d_k)^T d_k \geq c_2 \nabla f_k^T d_k$

with $0 < c_1 < c_2 < 1$ (typical: $c_1 = 10^{-4}$, $c_2 = 0.9$).

**Theorem (Zoutendijk)**: If $d_k$ is a descent direction and $\alpha_k$ satisfies the Wolfe conditions, then:

$$\sum_{k=0}^\infty \cos^2 \theta_k \|\nabla f_k\|^2 < \infty$$

where $\theta_k$ is the angle between $d_k$ and $-\nabla f_k$. This implies $\nabla f_k \to 0$ if $\cos\theta_k$ is bounded away from zero.

#### 2.3 Steepest Descent

**Direction**: $d_k = -\nabla f(x_k)$.

**Convergence**: For a quadratic $f(x) = \frac{1}{2}x^T A x - b^T x$ with $0 < \lambda_1 \leq \cdots \leq \lambda_n$ eigenvalues of $A$:

$$f(x_{k+1}) - f(x^*) \leq \left(\frac{\kappa - 1}{\kappa + 1}\right)^2 (f(x_k) - f(x^*))$$

where $\kappa = \lambda_n / \lambda_1$ is the **condition number**. Convergence is **linear** but can be very slow for ill-conditioned problems ($\kappa \gg 1$).

---

### Unit 3: Newton's Method and Modifications

#### 3.1 Newton's Method

**Direction**: Solve $\nabla^2 f(x_k) d_k = -\nabla f(x_k)$, i.e., $d_k = -[\nabla^2 f(x_k)]^{-1} \nabla f(x_k)$.

**Convergence**: Near a minimizer $x^*$ with $\nabla^2 f(x^*) \succ 0$, Newton's method converges **quadratically**:

$$\|x_{k+1} - x^*\| \leq C \|x_k - x^*\|^2$$

*Proof Sketch*: Using $\nabla f(x^*) = 0$ and Taylor expansion:

$$x_{k+1} - x^* = x_k - x^* - [\nabla^2 f(x_k)]^{-1}\nabla f(x_k) = [\nabla^2 f(x_k)]^{-1}\left[\nabla^2 f(x_k)(x_k - x^*) - \nabla f(x_k)\right]$$

The bracketed term is $O(\|x_k - x^*\|^2)$ by the mean value theorem applied to $\nabla f$.

#### 3.2 Modified Newton Methods

When $\nabla^2 f(x_k)$ is not positive definite, pure Newton may move toward a saddle or maximum. Remedies:

- **Modified Cholesky**: Replace $H_k$ with $H_k + \tau I$ for small $\tau > 0$ to ensure positive definiteness.
- **Trust region Newton**: Solve $\min_d m_k(d) = f_k + \nabla f_k^T d + \frac{1}{2} d^T H_k d$ subject to $\|d\| \leq \Delta_k$.

---

### Unit 4: Quasi-Newton Methods

#### 4.1 Motivation

Newton's method requires computing and factoring $\nabla^2 f(x_k)$ — an $O(n^2)$ storage, $O(n^3)$ computation cost per step. Quasi-Newton methods build approximate Hessians using only gradient information.

#### 4.2 The Secant Equation

Require the approximate Hessian $B_{k+1}$ to satisfy:

$$B_{k+1} s_k = y_k$$

where $s_k = x_{k+1} - x_k$ and $y_k = \nabla f_{k+1} - \nabla f_k$.

#### 4.3 The BFGS Update

The **Broyden-Fletcher-Goldfarb-Shanno** update:

$$B_{k+1} = B_k - \frac{B_k s_k s_k^T B_k}{s_k^T B_k s_k} + \frac{y_k y_k^T}{y_k^T s_k}$$

Or equivalently, maintaining the inverse Hessian approximation $H_k = B_k^{-1}$:

$$H_{k+1} = \left(I - \frac{s_k y_k^T}{y_k^T s_k}\right) H_k \left(I - \frac{y_k s_k^T}{y_k^T s_k}\right) + \frac{s_k s_k^T}{y_k^T s_k}$$

**Key Properties**:
- If $B_k \succ 0$ and $y_k^T s_k > 0$ (guaranteed by Wolfe conditions), then $B_{k+1} \succ 0$.
- **Superlinear convergence**: Under mild conditions, BFGS converges superlinearly: $\|x_{k+1} - x^*\| = o(\|x_k - x^*\|)$.
- No Hessian computation needed — only gradient evaluations.

#### 4.4 Limited-Memory BFGS (L-BFGS)

For large-scale problems ($n \gg 1$), store only the last $m$ pairs $\{s_k, y_k\}$ and compute $H_k \nabla f_k$ implicitly using the **two-loop recursion**. Storage: $O(mn)$ instead of $O(n^2)$.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Numerical Optimization* (2nd ed.) | Jorge Nocedal & Stephen J. Wright | **Primary** — Chapters 2–7 |
| *Nonlinear Programming* (3rd ed.) | Dimitri P. Bertsekas | **Alternative** — Rigorous theory |
| *Introductory Lectures on Stochastic Optimization* | John C. Duchi | **Supplementary** — Modern stochastic methods |
| *Convex Optimization* | Stephen Boyd & Lieven Vandenberghe | **Supplementary** — Convex theory |

---

## Problem Sets

### Problem Set 1: Optimality Conditions

1. **(Nocedal & Wright 2.1)** Verify the first- and second-order conditions for $f(x) = x_1^2 + x_2^2 - 2x_1 x_2 + x_1$ at all critical points.
2. **(Exam-style)** Let $f(x,y) = x^4 + y^4 - 2x^2 y^2$. Find all critical points and classify them.
3. **(Exam-style)** Prove: if $f$ is convex and differentiable, then $\nabla f(x^*) = 0 \Rightarrow x^*$ is a global minimizer.
4. **(Proof)** Show that for $f \in C^2$, $\nabla^2 f(x) \succeq 0$ for all $x$ $\Leftrightarrow$ $f$ is convex.
5. **(Challenge)** Construct a $C^1$ function $f: \mathbb{R}^2 \to \mathbb{R}$ with $\nabla f(0) = 0$ and $\nabla^2 f(0) \succ 0$ but where $0$ is not a global minimizer.

### Problem Set 2: Line Search and Steepest Descent

1. **(Nocedal & Wright 3.1)** Prove that a step length satisfying the Wolfe conditions exists for any descent direction.
2. **(Exam-style)** Derive the convergence rate of steepest descent for $f(x) = \frac{1}{2}x^T A x$ and show it depends on $\kappa(A)$.
3. **(Implementation)** Implement steepest descent with backtracking line search in Python. Test on the Rosenbrock function $f(x,y) = (1-x)^2 + 100(y-x^2)^2$.
4. **(Proof)** Prove Zoutendijk's theorem.
5. **(Application)** Explain why steepest descent exhibits "zigzag" behavior on ill-conditioned problems.

### Problem Set 3: Newton and BFGS

1. **(Nocedal & Wright 6.1)** Prove the quadratic convergence of Newton's method near a strict local minimizer.
2. **(Exam-style)** Verify that the BFGS update preserves positive definiteness when $y_k^T s_k > 0$.
3. **(Implementation)** Implement BFGS with Wolfe line search. Compare convergence to steepest descent on the Rosenbrock function.
4. **(Proof)** Show that the BFGS secant condition $B_{k+1} s_k = y_k$ is satisfied.
5. **(Challenge)** Prove superlinear convergence of BFGS (outline the Dennis-Moré characterization theorem).
