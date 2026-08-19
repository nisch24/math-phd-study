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

**Theorem**: If the KKT conditions hold at $(x^*, \lambda^*, \mu^*)$ and the Lagrangian Hessian $\nabla^2_{xx}\mathcal{L}(x^*, \lambda^*, \mu^*)$ is positive definite on the **critical cone**:

$$\mathcal{C}(x^*) = \bigl\{d : \nabla c_i(x^*)^T d = 0 \text{ for } i \in \mathcal{E} \cup \mathcal{A}(x^*)\bigr\},$$

then $x^*$ is a strict local minimizer.

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

where $X = \operatorname{diag}(x)$, $S = \operatorname{diag}(s)$, and $\tau \to 0$. The algorithm converges in $O(\sqrt{n} \log(1/\varepsilon))$ Newton iterations.

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

1. **(Nocedal &amp; Wright 12.1)** Solve $\min x_1 + x_2$ subject to $x_1^2 + x_2^2 \leq 2$. Identify KKT points and verify optimality.
2. **(Exam-style)** State the KKT conditions for $\min \frac{1}{2}\|x\|^2$ subject to $Ax = b$. Show the solution is $x = A^T(AA^T)^{-1}b$.
3. **(Exam-style)** Derive the KKT conditions for the SVM primal: $\min \frac{1}{2}\|w\|^2$ subject to $y_i(w^T x_i + b) \geq 1$. Derive the dual problem.
4. **(Proof)** Prove the KKT necessary conditions under LICQ using the Fritz John conditions as an intermediate step.
5. **(Challenge)** Construct an example where the KKT conditions hold but LICQ fails, and the KKT point is not a local minimizer.

### Problem Set 2: Duality

1. **(Boyd &amp; Vandenberghe 5.1)** Derive the dual of the linear program $\min c^T x$ subject to $Ax \leq b$.
2. **(Exam-style)** Prove weak duality.
3. **(Exam-style)** Verify Slater's condition and derive the Lagrange dual for: $\min x^2 + y^2$ subject to $x + y \geq 1$.
4. **(Proof)** Prove that the Lagrange dual function $g(\lambda, \mu)$ is concave.
5. **(Application)** Derive the dual of ridge regression: $\min_\beta \|y - X\beta\|^2 + \lambda\|\beta\|^2$.

### Problem Set 3: Algorithms

1. **(Nocedal &amp; Wright 17.1)** Implement a quadratic penalty method for a simple constrained problem. Observe the growth in condition number as $\rho$ increases.
2. **(Exam-style)** Derive the central path conditions for a log-barrier method applied to a standard LP in inequality form.
3. **(Implementation)** Implement a basic log-barrier interior-point method for a small LP with 3 variables and 5 inequality constraints. Plot the primal central path.
4. **(Proof)** Show that the log-barrier function $-\sum_j \log c_j(x)$ is convex when each $c_j$ is affine (or more generally, concave and positive).
5. **(Challenge)** Analyze the $O(\sqrt{n}\log(1/\varepsilon))$ iteration complexity of primal-dual interior-point methods for LP.

---

## Study Guide &amp; Exam Preparation

> [!IMPORTANT]
> **Key Theorems for Nonlinear Optimization II**
>
> - **KKT Necessary Conditions** — four conditions: stationarity, primal feasibility, dual feasibility, complementary slackness; LICQ is required
> - **KKT Sufficient Conditions** — positive definiteness of the Lagrangian Hessian on the critical cone
> - **Weak Duality** — $g(\lambda, \mu) \leq f(x)$ for all feasible $x$ and dual-feasible $(\lambda, \mu)$; proof is a one-line application of feasibility
> - **Strong Duality (Slater)** — strictly feasible point + convexity $\Rightarrow$ duality gap = 0
> - **Saddle Point Theorem** — KKT $\Leftrightarrow$ saddle point $\Leftrightarrow$ primal-dual optimality under convexity
> - **Central Path** — the log-barrier solution path; converges to KKT point as barrier parameter $\to 0$

**Proof-Writing Tips**:
- For KKT proofs, always state the constraint qualification (LICQ or MFCQ) that ensures multiplier existence.
- For duality gap proofs: weak duality follows from feasibility + dual non-negativity ($\mu \geq 0$). Strong duality requires Slater's condition and a fixed-point argument.
- The complementary slackness condition $\mu_j^* c_j(x^*) = 0$ is the key to understanding which inequality constraints are "active" at optimality.
