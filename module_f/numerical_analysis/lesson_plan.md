---
layout: default
title: "F.2 — Numerical Analysis"
parent: "Module F — Differential Equations & Numerical Analysis"
nav_order: 2
permalink: /module_f/numerical_analysis/
---

# F.2 — Numerical Analysis

> *A computer answers a slightly different question from the one you asked: the numbers are rounded, the infinite is truncated, and the continuous is discretized. Numerical analysis asks how far the computed answer can be from the true one, and it splits that error into two parts: the problem's sensitivity (**conditioning**) and the algorithm's robustness (**stability**).*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Separate conditioning from stability**, and use the rule of thumb *forward error ≲ condition number × backward error*.
2. **Analyze root-finding methods** (bisection, fixed-point iteration, Newton, secant) and their orders of convergence.
3. **Bound interpolation and quadrature errors**, and explain the Runge phenomenon and the advantage of Chebyshev nodes.
4. **Analyze ODE solvers** for accuracy (order) and stability (absolute stability regions, stiffness).
5. **Choose numerical linear algebra methods** (LU, Cholesky, QR, SVD, conjugate gradients) based on structure and conditioning.

---

## Core Theory

### Unit 1: Floating Point, Conditioning, and Stability

IEEE double precision stores about 16 significant decimal digits. Every basic operation satisfies

$$\operatorname{fl}(x \circ y) = (x \circ y)(1 + \delta), \qquad |\delta| \leq u = 2^{-53} \approx 1.1 \times 10^{-16}.$$

(Machine epsilon, the gap between $1$ and the next larger double, is $2^{-52} \approx 2.2 \times 10^{-16} = 2u$.)

**Conditioning (a property of the problem)**: the relative condition number of evaluating $f$ at $x$ is

$$\kappa_f(x) = \left|\frac{x f'(x)}{f(x)}\right|,$$

the factor by which relative input errors are amplified. For solving $Ax = b$, the condition number is $\kappa(A) = \|A\|\|A^{-1}\|$.

**Stability (a property of the algorithm)**: an algorithm is **backward stable** if its computed answer is the *exact* answer for slightly perturbed data (relative perturbation $O(u)$).

**The fundamental rule**: for a backward-stable algorithm, $\text{relative forward error} \lesssim \kappa \cdot u$. Losing digits on an ill-conditioned problem is unavoidable; losing them on a well-conditioned problem means the algorithm is at fault.

**Catastrophic cancellation**: subtracting nearly equal numbers wipes out the leading digits. Two examples:
- For $x = 10^{-8}$, $\operatorname{fl}(\cos x) = 1$ exactly, so $(1 - \cos x)/x^2$ evaluates to $0$ instead of $\approx 0.5$. The identity $1 - \cos x = 2\sin^2(x/2)$ avoids the subtraction.
- The one-pass variance formula $\frac{1}{n}\sum x_i^2 - \bar{x}^2$ fails badly for data with a large mean and a small spread. Use the two-pass formula or Welford's algorithm. Every statistician should know this.

---

### Unit 2: Nonlinear Equations

| Method | Iteration | Convergence near a simple root |
|--------|-----------|-------------------------------|
| Bisection | Halve a sign-change bracket | Linear; error $\leq (b-a)/2^{n+1}$; always converges |
| Fixed point | $x_{k+1} = g(x_k)$ | Linear with rate $\lvert g'(x^*) \rvert$, if $\lvert g'(x^*) \rvert < 1$ |
| Newton | $x_{k+1} = x_k - f(x_k)/f'(x_k)$ | Quadratic: $e_{k+1} \approx \frac{f''(x^*)}{2f'(x^*)} e_k^2$ |
| Secant | Newton with $f'$ replaced by a difference quotient | Order $\frac{1+\sqrt{5}}{2} \approx 1.618$ |

**Intuition**: quadratic convergence means the number of correct digits roughly **doubles** each step. Newton's weakness is locality: far from the root it can diverge or cycle, and at a multiple root it degrades to linear convergence. Robust solvers combine bisection's guarantee with Newton's speed.

**Fixed-point theory**: if $g$ maps $[a,b]$ into itself and $|g'| \leq \rho < 1$ there, then $g$ is a contraction, and the Banach Fixed-Point Theorem (Module A) gives convergence from any starting point in $[a,b]$.

---

### Unit 3: Interpolation and Approximation

There is a unique polynomial $p_n$ of degree $\leq n$ through $n+1$ distinct points $(x_i, f(x_i))$, and

$$f(x) - p_n(x) = \frac{f^{(n+1)}(\xi)}{(n+1)!}\prod_{i=0}^n (x - x_i) \quad \text{for some } \xi \text{ in the span of } x, x_0, \ldots, x_n.$$

**Runge phenomenon**: for $f(x) = 1/(1 + 25x^2)$ on $[-1,1]$, interpolation at **equally spaced** nodes diverges near the endpoints as $n \to \infty$. The cause is the node polynomial $\prod(x - x_i)$, which is huge near the ends.

**Chebyshev nodes** $x_i = \cos\!\left(\frac{(2i+1)\pi}{2(n+1)}\right)$ minimize $\max_{[-1,1]}\left|\prod_{i=0}^n(x - x_i)\right|$, achieving $2^{-n}$. For smooth $f$, Chebyshev interpolants converge rapidly. **Lesson**: where you sample matters as much as how many samples you take.

**Splines**: piecewise cubics with continuous second derivatives avoid high degree altogether, and are the usual practical choice.

---

### Unit 4: Numerical Integration

| Rule (composite, step $h$) | Error | Exact for polynomials of degree |
|----------------------------|-------|---------------------|
| Trapezoid | $-\frac{(b-a)h^2}{12}f''(\xi)$ | $\leq 1$ |
| Simpson | $-\frac{(b-a)h^4}{180}f^{(4)}(\xi)$ | $\leq 3$ |
| Gauss–Legendre, $n$ nodes | $O\big(f^{(2n)}\big)$ | $\leq 2n - 1$ |
| Monte Carlo, $n$ samples | $\approx \sigma/\sqrt{n}$ (random) | — |

**Intuition**: deterministic rules achieve high order by exploiting smoothness, but in $d$ dimensions a grid needs $m^d$ points. Monte Carlo's $n^{-1/2}$ rate does not depend on $d$ at all (Module B's CLT), which is why it wins for high-dimensional integrals such as Bayesian posteriors.

---

### Unit 5: Numerical Methods for ODEs

For $y' = f(t, y)$ with step $h$:
- **Forward Euler**: $y_{n+1} = y_n + h f(t_n, y_n)$. The local truncation error is $O(h^2)$ and the global error $O(h)$, so this is a first-order method.
- **Classical Runge–Kutta (RK4)**: four stages per step; global error $O(h^4)$.
- **Backward Euler**: $y_{n+1} = y_n + h f(t_{n+1}, y_{n+1})$. It is implicit (each step solves an equation) and first order.

**Absolute stability**: apply each method to the test equation $y' = \lambda y$ with $\operatorname{Re}\lambda < 0$, whose true solution decays.
- Forward Euler gives $y_{n+1} = (1 + h\lambda)y_n$, which decays only if $|1 + h\lambda| < 1$. For real $\lambda < 0$, this requires $h < 2/|\lambda|$.
- Backward Euler gives $y_{n+1} = y_n/(1 - h\lambda)$, which decays for **every** $h > 0$ (the method is **A-stable**).

**Stiffness**: when a system has both fast-decaying and slow modes (eigenvalues of very different sizes), explicit methods need $h < 2/|\lambda_{\text{fast}}|$ for stability, even after the fast mode has died out and accuracy no longer requires it. Implicit methods remove that restriction.

**Connection to optimization**: gradient descent $x_{k+1} = x_k - h\nabla f(x_k)$ is forward Euler on the gradient flow. On a quadratic with Hessian eigenvalues in $[\mu, L]$, it is stable iff $h < 2/L$. This is the familiar step-size limit, seen as a numerical stability condition.

**Convergence = consistency + stability**: a linear multistep method converges iff it is consistent and zero-stable (Dahlquist); a consistent linear finite-difference scheme for a well-posed linear PDE converges iff it is stable (Lax equivalence theorem). Accuracy of each step is not enough; errors must also not be amplified from step to step.

---

### Unit 6: Numerical Linear Algebra

| Task | Method | Cost | Notes |
|------|--------|------|-------|
| Solve $Ax = b$ | LU with partial pivoting | $\tfrac{2}{3}n^3$ | Pivoting is what makes it stable in practice |
| Solve $Ax = b$, $A \succ 0$ | Cholesky $A = R^T R$ | $\tfrac{1}{3}n^3$ | Stable without pivoting |
| Least squares | Householder QR | $\approx 2mn^2$ | Backward stable |
| Least squares | Normal equations $A^TA x = A^T b$ | cheaper | Squares the condition number: $\kappa(A^TA) = \kappa(A)^2$ |
| Rank-deficient least squares | SVD | most expensive | Most robust; reveals numerical rank |
| Large sparse $A \succ 0$ | Conjugate gradients | per-iteration matvec | Error in the $A$-norm shrinks at least like $2\left(\frac{\sqrt{\kappa}-1}{\sqrt{\kappa}+1}\right)^k$ |

**Practical rule**: never form $A^{-1}$ explicitly to solve a system. Factor once and solve by substitution.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *An Introduction to Numerical Analysis* | Endre Süli &amp; David Mayers | **Primary** — Rigorous and well-paced, with proofs |
| *Numerical Linear Algebra* | Lloyd N. Trefethen &amp; David Bau III | **Primary (linear algebra)** — Conditioning and stability explained beautifully |
| *Accuracy and Stability of Numerical Algorithms* (2nd ed.) | Nicholas J. Higham | **Reference** — The definitive treatment of rounding error |
| *Finite Difference Methods for Ordinary and Partial Differential Equations* | Randall J. LeVeque | **Supplementary** — Stability of ODE/PDE discretizations |

---

## Problem Sets

### Problem Set 1: Conditioning, Stability, and Root Finding

1. **(Core)** Compute the condition number of $f(x) = \sqrt{x}$ and of $f(x) = x - 1$. Which is ill-conditioned, and where?
2. **(Implementation)** Evaluate $(1 - \cos x)/x^2$ and $2\sin^2(x/2)/x^2$ in double precision for $x = 10^{-1}, 10^{-2}, \ldots, 10^{-10}$. Explain the results.
3. **(Implementation)** Compute the variance of $\{10^9 + 1, 10^9 + 2, 10^9 + 3\}$ with the one-pass formula and with Welford's algorithm. Explain the discrepancy.
4. **(Proof)** Prove that Newton's method converges quadratically to a simple root $x^*$ of a $C^2$ function, for starting points close enough to $x^*$.
5. **(Challenge)** Show that Newton's method converges only linearly to the double root of $f(x) = (x-1)^2$, find the rate, and show that the modified iteration $x_{k+1} = x_k - 2f(x_k)/f'(x_k)$ restores fast convergence.

### Problem Set 2: Interpolation and Quadrature

1. **(Proof)** Prove the interpolation error formula. *(Hint: apply Rolle's theorem repeatedly to $f - p_n - c\prod(x - x_i)$.)*
2. **(Implementation)** Interpolate $1/(1 + 25x^2)$ at $n+1$ equispaced and at $n+1$ Chebyshev nodes for $n = 5, 10, 20$. Plot the max error against $n$.
3. **(Core)** Derive the composite trapezoid error $O(h^2)$, and verify it numerically on $\int_0^1 e^x\,dx$ by halving $h$ repeatedly.
4. **(Proof)** Show that an $n$-point quadrature rule cannot be exact for all polynomials of degree $2n$. *(Hint: integrate $\prod(x - x_i)^2$.)*
5. **(Challenge)** Estimate $\int_{[0,1]^{10}} e^{-\|x\|^2}\,dx$ by Monte Carlo and by a tensor-product trapezoid rule with the same number of function evaluations. Compare the errors.

### Problem Set 3: ODE Solvers and Linear Algebra

1. **(Core)** Show that forward Euler applied to $y' = -50y$ with $h = 0.05$ produces growing oscillations, and that backward Euler with the same $h$ decays.
2. **(Implementation)** Solve $y' = y$, $y(0) = 1$ on $[0,1]$ with Euler and RK4 for $h = 0.1, 0.05, 0.025$. Verify the orders 1 and 4 from a log-log plot of error versus $h$.
3. **(Proof)** Derive the stability region of forward Euler, $\{z \in \mathbb{C} : |1 + z| \leq 1\}$, and show backward Euler is A-stable.
4. **(Core)** For $A$ with $\kappa(A) = 10^8$ and a small residual $\|Ax^* - b\|$, explain why solving least squares by the normal equations can lose all 16 digits, while QR loses only about 8. (With a large residual, the problem's own sensitivity involves $\kappa^2$, and both methods suffer.)
5. **(Challenge)** Show that gradient descent with step $h$ on $f(x) = \tfrac{1}{2}x^T A x$ ($A \succ 0$) converges iff $h < 2/\lambda_{\max}(A)$, and that the optimal fixed step $h = 2/(\lambda_{\min} + \lambda_{\max})$ gives the contraction factor $\frac{\kappa - 1}{\kappa + 1}$.

---

## Study Guide

{: .important }
> **Key ideas**
>
> - **Forward error ≲ κ × backward error**: separate the problem's sensitivity from the algorithm's quality
> - **Orders of convergence**: bisection (linear), Newton (quadratic), secant (≈1.618)
> - **Interpolation error formula**; Chebyshev nodes vs. Runge
> - **Absolute stability and stiffness**: why implicit methods exist
> - **Normal equations square κ**: use QR or the SVD for least squares

**Always check numerically**: for every error bound you prove, write five lines of code that confirm the predicted rate on a log-log plot. When the slope is wrong, either the code or the analysis has a bug, and finding out which is how this subject is learned.
