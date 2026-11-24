---
layout: default
title: "EN.553.762 — Nonlinear Optimization II"
parent: "Module D — Optimization & Operations Research"
nav_order: 2
permalink: /module_d/nonlinear_optimization_2/
---

# EN.553.762 — Nonlinear Optimization II

> *Constrained optimization: Lagrangian duality, the Karush-Kuhn-Tucker conditions, penalty and barrier methods, and interior-point algorithms. These tools are essential for constrained statistical estimation, support vector machines, portfolio optimization, and engineering design.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Formulate constrained optimization problems** and identify the active constraint set at a candidate solution.
2. **Derive and apply the KKT conditions** as necessary (and, under convexity, sufficient) conditions for optimality.
3. **Understand Lagrangian duality** and verify strong duality using Slater's condition.
4. **Analyze penalty, barrier, and augmented Lagrangian methods** and their convergence properties.
5. **Describe interior-point methods** for linear and convex programs and their polynomial-time iteration complexity.
6. **Formulate and dualize semidefinite programs**, using the Schur complement to model nonlinear constraints as linear matrix inequalities.

---

## Core Theory

### Unit 1: Constrained Optimization Formulation

#### 1.1 The General Nonlinear Program

$$\min_{x \in \mathbb{R}^n} f(x) \quad \text{subject to} \quad c_i(x) = 0,\; i \in \mathcal{E}; \quad c_j(x) \geq 0,\; j \in \mathcal{I},$$

where $\mathcal{E}$ indexes equality constraints and $\mathcal{I}$ indexes inequality constraints, and all functions are assumed sufficiently smooth ($C^1$ or $C^2$).

#### 1.2 Constraint Qualifications

The **Linear Independence Constraint Qualification (LICQ)** holds at $x^*$ if the gradients

$$\{\nabla c_i(x^*) : i \in \mathcal{E} \cup \mathcal{A}(x^*)\}$$

are linearly independent, where $\mathcal{A}(x^*) = \{j \in \mathcal{I} : c_j(x^*) = 0\}$ is the **active set** of inequality constraints at $x^*$.

---

### Unit 2: KKT Conditions

#### 2.1 The Lagrangian

$$\mathcal{L}(x, \lambda, \mu) = f(x) - \sum_{i \in \mathcal{E}} \lambda_i c_i(x) - \sum_{j \in \mathcal{I}} \mu_j c_j(x).$$

#### 2.2 KKT Necessary Conditions

**Theorem (Karush-Kuhn-Tucker)**: If $x^*$ is a local minimizer of $f$ and LICQ holds at $x^*$, then there exist multipliers $\lambda_i^*$ ($i \in \mathcal{E}$) and $\mu_j^*$ ($j \in \mathcal{I}$) satisfying:

1. **Stationarity**: $\nabla_x \mathcal{L}(x^*, \lambda^*, \mu^*) = 0$, i.e.,

$$\nabla f(x^*) = \sum_{i \in \mathcal{E}} \lambda_i^* \nabla c_i(x^*) + \sum_{j \in \mathcal{I}} \mu_j^* \nabla c_j(x^*).$$

2. **Primal feasibility**: $c_i(x^*) = 0$ for $i \in \mathcal{E}$; and $c_j(x^*) \geq 0$ for $j \in \mathcal{I}$.
3. **Dual feasibility**: $\mu_j^* \geq 0$ for all $j \in \mathcal{I}$.
4. **Complementary slackness**: $\mu_j^* c_j(x^*) = 0$ for all $j \in \mathcal{I}$.

#### 2.3 KKT Sufficient Conditions

**Theorem**: Suppose the KKT conditions hold at $(x^*, \lambda^*, \mu^*)$ and

$$d^T \nabla^2_{xx}\mathcal{L}(x^*, \lambda^*, \mu^*)\, d > 0 \quad \text{for all nonzero } d \in \mathcal{C}(x^*, \mu^*),$$

where the **critical cone** is

$$\mathcal{C}(x^*, \mu^*) = \left\{ d \;:\; \begin{aligned} &\nabla c_i(x^*)^T d = 0, && i \in \mathcal{E}, \\ &\nabla c_j(x^*)^T d = 0, && j \in \mathcal{A}(x^*) \text{ with } \mu_j^* > 0, \\ &\nabla c_j(x^*)^T d \geq 0, && j \in \mathcal{A}(x^*) \text{ with } \mu_j^* = 0 \end{aligned} \right\}.$$

Then $x^*$ is a strict local minimizer. Under **strict complementarity** ($\mu_j^* > 0$ for every active $j$), the cone reduces to the subspace $\{d : \nabla c_i(x^*)^T d = 0,\ i \in \mathcal{E} \cup \mathcal{A}(x^*)\}$. In general it is a cone, not a subspace, so checking positive definiteness on that subspace alone is not sufficient.

---

### Unit 3: Lagrangian Duality

#### 3.1 The Lagrange Dual Function

$$g(\lambda, \mu) = \inf_{x \in \mathbb{R}^n} \mathcal{L}(x, \lambda, \mu).$$

The dual function is always **concave** as a pointwise infimum of affine functions of $(\lambda, \mu)$, regardless of the convexity of the primal.

**Weak Duality**: For any primal feasible $x$ and dual feasible $(\lambda, \mu)$ with $\mu \geq 0$:

$$g(\lambda, \mu) \leq f(x).$$

The **dual problem** is $\max_{\lambda,\, \mu \geq 0} g(\lambda, \mu)$, and weak duality gives $\max g \leq \min f$.

#### 3.2 Strong Duality and Slater's Condition

**Theorem (Slater)**: For a **convex** optimization problem (convex $f$, affine equality constraints, concave inequality constraints), if there exists a **strictly feasible** point (i.e., $c_j(\bar{x}) > 0$ for all $j \in \mathcal{I}$), then **strong duality** holds:

$$\max_{\lambda,\, \mu \geq 0} g(\lambda, \mu) = \min_{x} f(x),$$

and the dual optimum is attained.

#### 3.3 Saddle Point Interpretation

$(x^*, \lambda^*, \mu^*)$ is a **saddle point** of $\mathcal{L}$ if:

$$\mathcal{L}(x^*, \lambda, \mu) \leq \mathcal{L}(x^*, \lambda^*, \mu^*) \leq \mathcal{L}(x, \lambda^*, \mu^*)$$

for all $x$, all $\lambda$, and all $\mu \geq 0$. Under convexity and a constraint qualification:

$$\text{KKT conditions} \;\Longleftrightarrow\; \text{saddle point} \;\Longleftrightarrow\; \text{primal-dual optimality}.$$

---

### Unit 4: Algorithmic Methods for Constrained Optimization

#### 4.1 Penalty Methods

Replace the constrained problem by a sequence of unconstrained subproblems:

$$\min_x\; f(x) + \frac{\rho}{2}\!\left(\sum_{i \in \mathcal{E}} c_i(x)^2 + \sum_{j \in \mathcal{I}} [\min(0, c_j(x))]^2\right).$$

As $\rho \to \infty$, solutions converge to the constrained optimum. **Drawback**: increasing $\rho$ causes increasingly ill-conditioned subproblems.

**Augmented Lagrangian (method of multipliers)**: For equality constraints, minimize

$$\mathcal{L}_A(x; \lambda, \rho) = f(x) - \sum_{i \in \mathcal{E}} \lambda_i c_i(x) + \frac{\rho}{2}\sum_{i \in \mathcal{E}} c_i(x)^2,$$

then update $\lambda_i \leftarrow \lambda_i - \rho\, c_i(x)$. Because the multiplier estimates absorb the constraint violation, the iterates converge for a fixed, moderate $\rho$. This avoids the ill-conditioning of the pure penalty method, and it is the basis of ADMM.

#### 4.2 Logarithmic Barrier (Interior-Point) Methods

For inequality-constrained problems, introduce the **log-barrier**:

$$\min_x\; f(x) - \frac{1}{t} \sum_{j \in \mathcal{I}} \log c_j(x).$$

As $t \to \infty$, the solution traces the **central path** converging to the constrained optimum. The log-barrier prevents iterates from violating $c_j(x) > 0$.

**Central Path Conditions**: The path $x^*(t)$ satisfies the perturbed stationarity:

$$\nabla f(x) = \sum_{j \in \mathcal{I}} \frac{1}{t \cdot c_j(x)} \nabla c_j(x),$$

which approaches the KKT stationarity conditions as $t \to \infty$.

#### 4.3 Sequential Quadratic Programming (SQP)

At each iterate $x_k$, solve a **quadratic program (QP)** approximating the original problem:

$$\min_d\; \nabla f_k^T d + \frac{1}{2} d^T W_k d \quad \text{s.t.} \quad \nabla c_i(x_k)^T d + c_i(x_k) = 0,\; \text{etc.}$$

where $W_k \approx \nabla^2_{xx}\mathcal{L}$ is a Hessian approximation. SQP achieves superlinear convergence and is the method of choice for medium-scale nonlinear programming.

#### 4.4 Primal-Dual Interior-Point Methods for LP

For $\min c^T x$ subject to $Ax = b$, $x \geq 0$, the primal-dual method solves the perturbed KKT system:

$$\begin{aligned} Ax &= b, \\ A^T y + s &= c, \\ X S e &= \tau e, \end{aligned}$$

where $X = \operatorname{diag}(x)$, $S = \operatorname{diag}(s)$, and $\tau \to 0$. Short-step path-following variants reach an $\varepsilon$-accurate solution in $O(\sqrt{n} \log(1/\varepsilon))$ Newton iterations.

---

### Unit 5: Semidefinite Programming

#### 5.1 Standard Form and Duality

Let $\mathbb{S}^n$ be the space of symmetric $n \times n$ matrices with inner product $\langle A, B \rangle = \operatorname{tr}(AB)$. A **semidefinite program (SDP)** in standard form is

$$\min_{X \in \mathbb{S}^n} \; \langle C, X \rangle \quad \text{s.t.} \quad \langle A_i, X \rangle = b_i,\; i = 1, \ldots, m, \qquad X \succeq 0,$$

with dual

$$\max_{y \in \mathbb{R}^m} \; b^T y \quad \text{s.t.} \quad S = C - \sum_{i=1}^m y_i A_i \succeq 0.$$

**Weak duality**: For feasible $X$ and $(y, S)$, $\langle C, X \rangle - b^T y = \langle S, X \rangle \geq 0$. The inequality holds because the PSD cone is **self-dual**: $\operatorname{tr}(SX) \geq 0$ whenever $S, X \succeq 0$.

**Strong duality**: If both problems are strictly feasible (some $X \succ 0$ and some $(y, S)$ with $S \succ 0$), both optima are attained and equal. Unlike LP, strong duality can fail for SDPs without such a condition.

#### 5.2 Modeling Tools

- **LP as a special case**: if $C$ and all $A_i$ are diagonal, the SDP reduces to an LP in the diagonal entries of $X$.
- **Schur complement lemma**: if $A \succ 0$, then $\begin{pmatrix} A & B \\ B^T & D \end{pmatrix} \succeq 0 \iff D - B^T A^{-1} B \succeq 0$. This turns nonlinear constraints such as $x^T x \leq t$ into linear matrix inequalities.
- **Eigenvalue optimization**: $\lambda_{\max}(A) = \min\{t : tI - A \succeq 0\}$.
- **Relaxations**: the Goemans–Williamson MAX-CUT relaxation replaces $x x^T$ (with $x \in \{\pm 1\}^n$) by $X \succeq 0$ with $X_{ii} = 1$. Shape-constrained estimation problems (e.g. requiring a Hankel or Toeplitz matrix to be PSD) are also SDPs.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Numerical Optimization* (2nd ed.) | Jorge Nocedal &amp; Stephen J. Wright | **Primary** — Chapters 12–19 |
| *Convex Optimization* | Stephen Boyd &amp; Lieven Vandenberghe | **Primary** — Duality, barrier methods, semidefinite programming |
| *Nonlinear Programming* (3rd ed.) | Dimitri P. Bertsekas | **Alternative** — Rigorous constrained optimization theory |
| *Linear and Nonlinear Programming* (4th ed.) | David Luenberger &amp; Yinyu Ye | **Supplementary** — Interior-point methods for LP and QP |

---

## Problem Sets

### Problem Set 1: KKT Conditions

1. **(cf. Nocedal &amp; Wright Ch. 12)** Solve $\min x_1 + x_2$ subject to $x_1^2 + x_2^2 \leq 2$. Identify KKT points and verify optimality.
2. **(Exam-style)** State the KKT conditions for $\min \frac{1}{2}\|x\|^2$ subject to $Ax = b$. Show the solution is $x = A^T(AA^T)^{-1}b$.
3. **(Exam-style)** Derive the KKT conditions for the SVM primal: $\min \frac{1}{2}\|w\|^2$ subject to $y_i(w^T x_i + b) \geq 1$. Derive the dual problem.
4. **(Proof)** Prove the KKT necessary conditions under LICQ using the Fritz John conditions as an intermediate step.
5. **(Challenge)** Show that a constraint qualification cannot be dropped from the KKT theorem: for $\min x_1$ subject to $x_1^3 - x_2 \geq 0$ and $x_2 \geq 0$, show that $x^* = (0, 0)$ is the global minimizer, that LICQ fails there, and that **no** KKT multipliers exist.

### Problem Set 2: Duality

1. **(cf. Boyd &amp; Vandenberghe §5.2)** Derive the dual of the linear program $\min c^T x$ subject to $Ax \leq b$.
2. **(Exam-style)** Prove weak duality.
3. **(Exam-style)** Verify Slater's condition and derive the Lagrange dual for: $\min x^2 + y^2$ subject to $x + y \geq 1$.
4. **(Proof)** Prove that the Lagrange dual function $g(\lambda, \mu)$ is concave.
5. **(Application)** Derive the dual of ridge regression: $\min_\beta \|y - X\beta\|^2 + \lambda\|\beta\|^2$.

### Problem Set 3: Algorithms

1. **(cf. Nocedal &amp; Wright Ch. 17)** Implement a quadratic penalty method for a simple constrained problem. Observe the growth in condition number as $\rho$ increases.
2. **(Exam-style)** Derive the central path conditions for a log-barrier method applied to a standard LP in inequality form.
3. **(Implementation)** Implement a basic log-barrier interior-point method for a small LP with 3 variables and 5 inequality constraints. Plot the primal central path.
4. **(Proof)** Show that the log-barrier function $-\sum_j \log c_j(x)$ is convex when each $c_j$ is affine (or more generally, concave and positive).
5. **(Challenge)** Analyze the $O(\sqrt{n}\log(1/\varepsilon))$ iteration complexity of primal-dual interior-point methods for LP.

### Problem Set 4: Semidefinite Programming

1. **(Proof)** Prove that $\operatorname{tr}(SX) \geq 0$ for all $S, X \succeq 0$, and that the PSD cone is self-dual.
2. **(Exam-style)** Write $\lambda_{\max}(A)$ as an SDP and show that its dual is $\max\{\operatorname{tr}(AX) : \operatorname{tr}(X) = 1,\ X \succeq 0\}$. Interpret the dual using the spectral theorem.
3. **(Proof)** Prove the Schur complement lemma, then use it to write $\min_x \|Ax - b\|_2$ as an SDP.
4. **(Application)** Show that every LP is an SDP with diagonal data matrices, and verify that SDP duality reduces to LP duality in that case.
5. **(Challenge)** Construct an SDP with a finite, unattained optimal value or a nonzero duality gap, showing that strict feasibility is genuinely needed.

---

## Study Guide &amp; Exam Preparation

{: .important }
> **Key Theorems for Nonlinear Optimization II**
>
> - **KKT Necessary Conditions** — four conditions: stationarity, primal feasibility, dual feasibility, complementary slackness; LICQ is required
> - **KKT Sufficient Conditions** — positive definiteness of the Lagrangian Hessian on the critical cone
> - **Weak Duality** — $g(\lambda, \mu) \leq f(x)$ for all feasible $x$ and dual-feasible $(\lambda, \mu)$; proof is a one-line application of feasibility
> - **Strong Duality (Slater)** — strictly feasible point + convexity $\Rightarrow$ duality gap = 0
> - **Saddle Point Theorem** — KKT $\Leftrightarrow$ saddle point $\Leftrightarrow$ primal-dual optimality under convexity
> - **Central Path** — the log-barrier solution path $x^*(t)$; converges to a KKT point as $t \to \infty$ (barrier weight $1/t \to 0$)
> - **SDP Duality** — weak duality from self-duality of the PSD cone; strong duality needs strict feasibility

**Proof-Writing Tips**:
- For KKT proofs, always state the constraint qualification (LICQ or MFCQ) that ensures multiplier existence.
- For duality gap proofs: weak duality follows from feasibility + dual non-negativity ($\mu \geq 0$). Strong duality requires Slater's condition and a separating-hyperplane argument (separate the convex set of achievable (constraint, objective) values from the point at the optimal value).
- The complementary slackness condition $\mu_j^* c_j(x^*) = 0$ is the key to understanding which inequality constraints are "active" at optimality.
