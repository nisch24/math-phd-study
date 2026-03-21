---
layout: default
title: "Qualifying Exam Simulation"
nav_order: 8
permalink: /qualifying_exam/
---

# Qualifying Exam Simulation

> *The JHU Introductory Exam covers Real Analysis, Linear Algebra, and Probability. These three mock exams simulate the format, difficulty, and scope of the qualifying exam. Each problem requires a complete, rigorous proof.*

<div class="info-card">
  <div class="info-row"><span class="info-label">⏱ Duration</span> 4 hours</div>
  <div class="info-row"><span class="info-label">📝 Problems</span> 6 problems (choose 5)</div>
  <div class="info-row"><span class="info-label">📂 Sections</span> Analysis (2) · Linear Algebra (2) · Probability (2)</div>
  <div class="info-row"><span class="info-label">📊 Scoring</span> Each problem 0–10. Pass requires ≥ 30/50.</div>
  <div class="info-row"><span class="info-label">✍️ Style</span> Formal proofs required. State any theorems you use.</div>
</div>

---

## Mock Exam 1

<details open>
<summary>📘 Analysis — Problems 1 & 2</summary>

**Problem 1.** Let $f: [0,1] \to \mathbb{R}$ be continuous with $f(0) = f(1)$.

(a) Prove that for each $n \in \mathbb{N}$, there exists $x_n \in [0, 1 - 1/n]$ such that $f(x_n + 1/n) = f(x_n)$.

(b) Does the result hold if $[0,1]$ is replaced by $(0,1)$? Prove or give a counterexample.

**Problem 2.** Let $\{f_n\}$ be a sequence of continuous functions on $[0,1]$ and suppose $f_n \to f$ uniformly.

(a) Prove that $f$ is continuous.

(b) Prove that $\int_0^1 f_n(x)\,dx \to \int_0^1 f(x)\,dx$.

(c) Give an example where $f_n \to f$ pointwise, each $f_n$ is continuous, but $f$ is not continuous.

</details>

<details>
<summary>📗 Linear Algebra — Problems 3 & 4</summary>

**Problem 3.** Let $A \in \mathbb{R}^{n \times n}$ be symmetric with eigenvalues $\lambda_1 \leq \lambda_2 \leq \cdots \leq \lambda_n$.

(a) Prove that $\lambda_1 = \min_{\|x\|=1} x^T A x$ and $\lambda_n = \max_{\|x\|=1} x^T A x$.

(b) Let $B$ be obtained from $A$ by deleting the $n$-th row and column. Show that the eigenvalues of $B$ interlace those of $A$.

**Problem 4.** Let $A \in \mathbb{R}^{m \times n}$.

(a) Prove that $\text{rank}(A) = \text{rank}(A^T A) = \text{rank}(AA^T)$.

(b) Show that the nonzero eigenvalues of $A^T A$ and $AA^T$ are the same.

(c) Define the Singular Value Decomposition and state its existence theorem.

</details>

<details>
<summary>📙 Probability — Problems 5 & 6</summary>

**Problem 5.** Let $X_1, X_2, \ldots$ be i.i.d. random variables with $E[X_1] = \mu$ and $\text{Var}(X_1) = \sigma^2 < \infty$.

(a) State and prove the Weak Law of Large Numbers.

(b) State the Strong Law of Large Numbers (proof not required).

(c) State and prove the Central Limit Theorem using characteristic functions.

**Problem 6.** Let $(\Omega, \mathcal{F}, P)$ be a probability space.

(a) State the Monotone Convergence Theorem and Dominated Convergence Theorem.

(b) Compute $\lim_{n \to \infty} \int_0^\infty \frac{n \sin(x/n)}{x(1 + x^2)}\,dx$ using the DCT.

(c) Prove Borel-Cantelli Lemma I: if $\sum P(A_n) < \infty$, then $P(\limsup A_n) = 0$.

</details>

---

## Mock Exam 2

<details>
<summary>📘 Analysis — Problems 1 & 2</summary>

**Problem 1.** Let $(X, d)$ be a compact metric space and $f: X \to X$ a continuous function satisfying $d(f(x), f(y)) < d(x, y)$ for all $x \neq y$.

(a) Prove that $f$ has a unique fixed point.

(b) Show that the compactness assumption is necessary by giving a counterexample on a non-compact space.

**Problem 2.** Consider the function $g: \mathbb{R}^2 \to \mathbb{R}^2$ defined by $g(x, y) = (e^x \cos y - 1, e^x \sin y)$.

(a) Show that $g(0, 0) = (0, 0)$ and compute the Jacobian $Dg(0, 0)$.

(b) Use the Inverse Function Theorem to show $g$ is locally invertible near $(0, 0)$.

(c) Express $D(g^{-1})(0, 0)$ explicitly.

</details>

<details>
<summary>📗 Linear Algebra — Problems 3 & 4</summary>

**Problem 3.** Let $A$ be a real $n \times n$ matrix (not necessarily symmetric).

(a) Prove that all eigenvalues of $A^T A$ are nonnegative.

(b) Prove that $A$ is invertible if and only if all singular values of $A$ are positive.

(c) Show that $\|A\|_2 = \sigma_{\max}(A)$, the largest singular value.

**Problem 4.** Let $P$ be an $n \times n$ matrix satisfying $P^2 = P$ (idempotent).

(a) Prove that the eigenvalues of $P$ are 0 or 1.

(b) Prove that $\text{rank}(P) = \text{trace}(P)$.

(c) If additionally $P = P^T$, prove that $P$ is the orthogonal projection onto $\text{Col}(P)$.

</details>

<details>
<summary>📙 Probability — Problems 5 & 6</summary>

**Problem 5.** Let $(M_n, \mathcal{F}_n)_{n \geq 0}$ be a martingale with $M_0 = 0$.

(a) Prove that $E[M_n] = 0$ for all $n$.

(b) Prove that if $E[M_n^2] < \infty$, then $E[M_n^2] = \sum_{k=1}^n E[(M_k - M_{k-1})^2]$.

(c) Let $X_i$ be i.i.d. with $P(X_i = 1) = P(X_i = -1) = 1/2$. Show $S_n = X_1 + \cdots + X_n$ is a martingale and $S_n^2 - n$ is a martingale.

**Problem 6.** Let $X$ and $Y$ be jointly distributed with $X \sim N(0, 1)$ and $Y | X \sim N(X, 1)$.

(a) Compute $E[Y]$, $\text{Var}(Y)$, and $\text{Cov}(X, Y)$.

(b) Compute $E[X | Y = y]$ and $\text{Var}(X | Y = y)$.

(c) Is $(X, Y)$ jointly normal? Prove your claim.

</details>

---

## Mock Exam 3

<details>
<summary>📘 Analysis — Problems 1 & 2</summary>

**Problem 1.** Let $K \subset \mathbb{R}^n$ be compact and $\{U_\alpha\}_{\alpha \in A}$ an open cover.

(a) Prove that there exists a **Lebesgue number** $\delta > 0$ such that every set of diameter $< \delta$ is contained in some $U_\alpha$.

(b) Use part (a) to prove: every continuous function on a compact metric space is uniformly continuous.

**Problem 2.** Let $f_n(x) = \frac{nx}{1 + n^2 x^2}$ for $x \in [0, 1]$.

(a) Find $f(x) = \lim_{n \to \infty} f_n(x)$ and determine whether convergence is uniform.

(b) Compute $\lim_{n \to \infty} \int_0^1 f_n(x)\,dx$ and $\int_0^1 f(x)\,dx$. Are they equal? Explain.

(c) Does this contradict the theorem on term-by-term integration? Why or why not?

</details>

<details>
<summary>📗 Linear Algebra — Problems 3 & 4</summary>

**Problem 3.** (Positive definite matrices)

(a) Prove that $A \succ 0$ (positive definite) if and only if all eigenvalues of $A$ are positive.

(b) Prove that if $A \succ 0$ and $B \succeq 0$, then $\lambda_i(A + B) \geq \lambda_i(A)$ for all $i$.

(c) Prove that the set of positive definite matrices is an open subset of the space of symmetric matrices.

**Problem 4.** Let $A$ be an $m \times n$ matrix with $m \geq n$ and $\text{rank}(A) = n$.

(a) Prove that $A^T A$ is invertible and positive definite.

(b) Show that $P = A(A^T A)^{-1} A^T$ is the orthogonal projection onto $\text{Col}(A)$.

(c) Prove that the least squares solution to $Ax = b$ is $x^* = (A^T A)^{-1} A^T b$.

</details>

<details>
<summary>📙 Probability — Problems 5 & 6</summary>

**Problem 5.** (Convergence)

(a) Prove: almost sure convergence implies convergence in probability.

(b) Prove: convergence in probability implies convergence in distribution.

(c) Give an example showing convergence in probability does NOT imply almost sure convergence.

(d) Prove: if $X_n \xrightarrow{d} c$ (a constant), then $X_n \xrightarrow{P} c$.

**Problem 6.** Let $X_1, X_2, \ldots$ be i.i.d. Exponential($\lambda$) random variables.

(a) Find the MLE $\hat{\lambda}_n$ of $\lambda$.

(b) Compute the Fisher Information $I(\lambda)$ and verify that $\hat{\lambda}_n$ achieves the Cramér-Rao bound asymptotically.

(c) Find the asymptotic distribution of $\sqrt{n}(\hat{\lambda}_n - \lambda)$.

(d) Construct an approximate 95% confidence interval for $\lambda$.

</details>

---

## Grading Rubric

| Score | Description |
|-------|-------------|
| 9–10  | Complete, rigorous proof with clear exposition |
| 7–8   | Correct proof with minor gaps or unclear steps |
| 5–6   | Correct approach, significant gaps in rigor |
| 3–4   | Partial understanding, major errors or omissions |
| 1–2   | Relevant ideas mentioned but no coherent proof |
| 0     | Blank or completely incorrect |

---

## Preparation Tips

<div class="steps-grid">
  <div class="step-card">
    <div class="step-number">1</div>
    <div class="step-title">Start with Definitions</div>
    <div class="step-desc">Begin every answer by stating the relevant definitions. This grounds your proof and earns partial credit.</div>
  </div>
  <div class="step-card">
    <div class="step-number">2</div>
    <div class="step-title">State Theorems</div>
    <div class="step-desc">When invoking a theorem (e.g., Bolzano-Weierstrass, Courant-Fischer), state it explicitly before using it.</div>
  </div>
  <div class="step-card">
    <div class="step-number">3</div>
    <div class="step-title">Time Management</div>
    <div class="step-desc">Allocate ~45 minutes per problem. Skip and return if stuck — don't lose time on one problem.</div>
  </div>
  <div class="step-card">
    <div class="step-number">4</div>
    <div class="step-title">Practice Proof Writing</div>
    <div class="step-desc">Work through Rudin Ch. 2, 3, 7, 9 and Horn & Johnson Ch. 1, 4, 7 for exam-style practice.</div>
  </div>
  <div class="step-card">
    <div class="step-number">5</div>
    <div class="step-title">Review Past Exams</div>
    <div class="step-desc">JHU departmental past qualifying exams are the best preparation resource for format and difficulty.</div>
  </div>
</div>
