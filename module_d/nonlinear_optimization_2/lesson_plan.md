---
layout: default
title: "EN.553.762 — Nonlinear Optimization II"
parent: "Module D — Optimization & Operations Research"
nav_order: 2
permalink: /module_d/nonlinear_optimization_2/
---

# EN.553.762 — Nonlinear Optimization II

> *Constrained optimization: Lagrangian duality, the Karush-Kuhn-Tucker conditions, penalty and barrier methods, and interior-point algorithms. These tools are essential for constrained statistical estimation, support vector machines, and engineering design.*

---

## Learning Objectives

1. **Formulate constrained optimization problems** and identify active constraints.
2. **Derive and apply KKT conditions** for optimality in constrained problems.
3. **Understand Lagrangian duality** and the conditions for strong duality.
4. **Analyze penalty, barrier, and augmented Lagrangian methods**.
5. **Describe interior-point methods** and their polynomial-time convergence.

---

## Core Theory

### Unit 1: Constrained Optimization Formulation

#### 1.1 The General Problem

$$\min_{x \in \mathbb{R}^n} f(x) \quad \text{subject to} \quad c_i(x) = 0, \; i \in \mathcal{E}; \quad c_j(x) \geq 0, \; j \in \mathcal{I}$$

where $\mathcal{E}$ is the set of equality constraint indices and $\mathcal{I}$ is the set of inequality constraint indices.

#### 1.2 Constraint Qualifications

**Linear Independence Constraint Qualification (LICQ)**: The gradients $\{\nabla c_i(x^*) : i \in \mathcal{E} \cup \mathcal{A}(x^*)\}$ are linearly independent, where $\mathcal{A}(x^*) = \{j \in \mathcal{I} : c_j(x^*) = 0\}$ is the **active set**.

---

### Unit 2: KKT Conditions

#### 2.1 The Lagrangian

$$\mathcal{L}(x, \lambda, \mu) = f(x) - \sum_{i \in \mathcal{E}} \lambda_i c_i(x) - \sum_{j \in \mathcal{I}} \mu_j c_j(x)$$

#### 2.2 KKT Necessary Conditions

**Theorem (Karush-Kuhn-Tucker)**: If $x^*$ is a local minimizer and LICQ holds at $x^*$, then there exist multipliers $\lambda_i^*$ ($i \in \mathcal{E}$) and $\mu_j^*$ ($j \in \mathcal{I}$) such that:

1. **Stationarity**: $\nabla_x \mathcal{L}(x^*, \lambda^*, \mu^*) = 0$, i.e.:

$$\nabla f(x^*) = \sum_{i \in \mathcal{E}} \lambda_i^* \nabla c_i(x^*) + \sum_{j \in \mathcal{I}} \mu_j^* \nabla c_j(x^*)$$

2. **Primal feasibility**: $c_i(x^*) = 0$ for $i \in \mathcal{E}$; $c_j(x^*) \geq 0$ for $j \in \mathcal{I}$.
3. **Dual feasibility**: $\mu_j^* \geq 0$ for $j \in \mathcal{I}$.
4. **Complementary slackness**: $\mu_j^* c_j(x^*) = 0$ for $j \in \mathcal{I}$.

#### 2.3 KKT Sufficient Conditions

**Theorem**: If the KKT conditions hold and the Lagrangian Hessian $\nabla^2_{xx}\mathcal{L}(x^*, \lambda^*, \mu^*)$ is positive definite on the tangent space of active constraints:

$$\{d : \nabla c_i(x^*)^T d = 0 \text{ for } i \in \mathcal{E} \cup \mathcal{A}(x^*)\}$$

then $x^*$ is a strict local minimizer.

---

### Unit 3: Lagrangian Duality

#### 3.1 The Lagrange Dual Function

$$g(\lambda, \mu) = \inf_{x \in \mathbb{R}^n} \mathcal{L}(x, \lambda, \mu)$$

The **dual function** is always concave, even if the primal problem is nonconvex.

**Weak Duality**: For any feasible $x$ and dual feasible $(\lambda, \mu)$ with $\mu \geq 0$:

$$g(\lambda, \mu) \leq f(x)$$

The **dual problem**: $\max_{\lambda, \mu \geq 0} g(\lambda, \mu) \leq \min_x f(x)$.

#### 3.2 Strong Duality

**Theorem (Slater's Condition)**: For a **convex** optimization problem (convex $f$, affine equalities, concave inequalities), if there exists a strictly feasible point (i.e., $c_j(x) > 0$ for all $j \in \mathcal{I}$), then **strong duality** holds:

$$\max_{\lambda, \mu \geq 0} g(\lambda, \mu) = \min_x f(x)$$

and the dual optimum is attained.

#### 3.3 Saddle Point Interpretation

$(x^*, \lambda^*, \mu^*)$ is a **saddle point** of $\mathcal{L}$ if:

$$\mathcal{L}(x^*, \lambda, \mu) \leq \mathcal{L}(x^*, \lambda^*, \mu^*) \leq \mathcal{L}(x, \lambda^*, \mu^*)$$

for all $x$, $\lambda$, and $\mu \geq 0$. Under convexity + constraint qualification, KKT $\Leftrightarrow$ saddle point $\Leftrightarrow$ primal-dual optimality.

---

### Unit 4: Algorithmic Methods for Constrained Optimization

#### 4.1 Penalty Methods

Replace the constrained problem with a sequence of unconstrained problems:

$$\min_x f(x) + \frac{\rho}{2}\left(\sum_{i \in \mathcal{E}} c_i(x)^2 + \sum_{j \in \mathcal{I}} [\min(0, c_j(x))]^2\right)$$

As $\rho \to \infty$, solutions converge to the constrained optimum. **Drawback**: Increasing $\rho$ makes subproblems ill-conditioned.

#### 4.2 Barrier (Interior-Point) Methods

For inequality-constrained problems, add a **logarithmic barrier**:

$$\min_x f(x) - \frac{1}{t} \sum_{j \in \mathcal{I}} \log c_j(x)$$

As $t \to \infty$, the solution traces the **central path** toward the constrained optimum. The barrier prevents iterates from violating constraints.

**Central Path Conditions**: The central path $x^*(t)$ satisfies:

$$\nabla f(x) = \sum_j \frac{1}{t \cdot c_j(x)} \nabla c_j(x)$$

which approaches the KKT conditions as $t \to \infty$.

#### 4.3 Sequential Quadratic Programming (SQP)

At each iteration, solve a **quadratic program (QP)** that approximates the constrained problem:

$$\min_d \nabla f_k^T d + \frac{1}{2} d^T W_k d \quad \text{s.t.} \quad \nabla c_i(x_k)^T d + c_i(x_k) = 0, \; etc.$$

where $W_k \approx \nabla^2_{xx}\mathcal{L}$. SQP can achieve superlinear convergence.

#### 4.4 Interior-Point Methods for Linear and Convex Programming

For LP: $\min c^T x$ s.t. $Ax = b, x \geq 0$, the primal-dual interior-point method solves the perturbed KKT system:

$$\begin{aligned} Ax &= b \\ A^T y + s &= c \\ X S e &= \tau e \end{aligned}$$

where $X = \text{diag}(x)$, $S = \text{diag}(s)$, and $\tau \to 0$. The method converges in $O(\sqrt{n} \log(1/\varepsilon))$ iterations.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Numerical Optimization* (2nd ed.) | Jorge Nocedal & Stephen J. Wright | **Primary** — Chapters 12–19 |
| *Convex Optimization* | Stephen Boyd & Lieven Vandenberghe | **Primary** — Duality, interior-point methods |
| *Nonlinear Programming* (3rd ed.) | Dimitri P. Bertsekas | **Alternative** — Rigorous constrained optimization |
| *Linear and Nonlinear Programming* (4th ed.) | David Luenberger & Yinyu Ye | **Supplementary** |

---

## Problem Sets

### Problem Set 1: KKT Conditions

1. **(Nocedal & Wright 12.1)** Solve: $\min x_1 + x_2$ s.t. $x_1^2 + x_2^2 \leq 2$. Find KKT points and verify optimality.
2. **(Exam-style)** State the KKT conditions for $\min \frac{1}{2}\|x\|^2$ s.t. $Ax = b$. Show the solution is $x = A^T(AA^T)^{-1}b$.
3. **(Exam-style)** Solve the SVM primal: $\min \frac{1}{2}\|w\|^2$ s.t. $y_i(w^T x_i + b) \geq 1$ by deriving the KKT conditions and the dual problem.
4. **(Proof)** Prove the KKT necessary conditions under LICQ using the Fritz John conditions.
5. **(Challenge)** Construct an example where KKT conditions hold but LICQ fails, and the KKT point is not a minimizer.

### Problem Set 2: Duality

1. **(Boyd & Vandenberghe 5.1)** Derive the dual of the LP: $\min c^T x$ s.t. $Ax \leq b$.
2. **(Exam-style)** Prove weak duality.
3. **(Exam-style)** Verify Slater's condition and derive the dual for: $\min x^2 + y^2$ s.t. $x + y \geq 1$.
4. **(Proof)** Prove that the Lagrange dual function is concave.
5. **(Application)** Derive the dual of ridge regression: $\min \|y - X\beta\|^2 + \lambda\|\beta\|^2$.

### Problem Set 3: Algorithms

1. **(Nocedal & Wright 17.1)** Implement a penalty method for a simple constrained problem. Observe the ill-conditioning as $\rho$ grows.
2. **(Exam-style)** Derive the central path conditions for a barrier method applied to an LP.
3. **(Implementation)** Implement an interior-point method for a small LP and plot the central path.
4. **(Proof)** Show that the barrier function $-\sum \log c_j(x)$ is convex when each $c_j$ is concave.
5. **(Challenge)** Analyze the iteration complexity $O(\sqrt{n}\log(1/\varepsilon))$ of primal-dual interior-point methods for LP.
