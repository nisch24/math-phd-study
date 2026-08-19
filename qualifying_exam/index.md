---
layout: default
title: "Qualifying Exam Simulation"
nav_order: 8
permalink: /qualifying_exam/
---

# Qualifying Exam Simulation

> *The JHU Introductory Qualifying Exam covers Real Analysis, Linear Algebra, and Probability Theory. The three mock exams below simulate the format, difficulty level, and scope of the qualifying exam. Each problem requires a complete, rigorous, book-quality proof.*

<div class="info-card">
  <div class="info-row"><span class="info-label">⏱ Duration</span> 4 hours</div>
  <div class="info-row"><span class="info-label">📝 Problems</span> 6 problems presented (choose any 5 to submit)</div>
  <div class="info-row"><span class="info-label">📂 Sections</span> Analysis (2) · Linear Algebra (2) · Probability (2)</div>
  <div class="info-row"><span class="info-label">📊 Scoring</span> Each problem scored 0–10. Pass threshold: ≥ 30 out of 50.</div>
  <div class="info-row"><span class="info-label">✍️ Style</span> Formal proofs required. State every theorem or lemma you invoke.</div>
</div>

---

## Mock Exam 1

<details open>
<summary>📘 Analysis — Problems 1 &amp; 2</summary>

**Problem 1.** Let $f: [0,1] \to \mathbb{R}$ be continuous with $f(0) = f(1)$.

(a) Prove that for each $n \in \mathbb{N}$, there exists $x_n \in [0, 1 - 1/n]$ such that $f(x_n + 1/n) = f(x_n)$.

(b) Does the result hold if $[0,1]$ is replaced by $(0,1)$? Prove or give a counterexample.

---

**Problem 2.** Let $\{f_n\}$ be a sequence of continuous functions on $[0,1]$ converging uniformly to $f$.

(a) Prove that $f$ is continuous.

(b) Prove that $\displaystyle\int_0^1 f_n(x)\,dx \to \int_0^1 f(x)\,dx$.

(c) Give an explicit example where $f_n \to f$ pointwise, each $f_n$ is continuous, but $f$ is discontinuous.

</details>

<details>
<summary>📗 Linear Algebra — Problems 3 &amp; 4</summary>

**Problem 3.** Let $A \in \mathbb{R}^{n \times n}$ be symmetric with eigenvalues $\lambda_1 \leq \lambda_2 \leq \cdots \leq \lambda_n$.

(a) Prove that $\lambda_1 = \min_{\|x\|=1} x^T A x$ and $\lambda_n = \max_{\|x\|=1} x^T A x$.

(b) Let $B$ be obtained from $A$ by deleting the $n$-th row and corresponding column. Prove that the eigenvalues of $B$ interlace those of $A$.

---

**Problem 4.** Let $A \in \mathbb{R}^{m \times n}$.

(a) Prove that $\operatorname{rank}(A) = \operatorname{rank}(A^T A) = \operatorname{rank}(AA^T)$.

(b) Show that the nonzero eigenvalues of $A^T A$ and $AA^T$ coincide.

(c) Define the Singular Value Decomposition of $A$ and state the existence theorem.

</details>

<details>
<summary>📙 Probability — Problems 5 &amp; 6</summary>

**Problem 5.** Let $X_1, X_2, \ldots$ be i.i.d. with $E[X_1] = \mu$ and $\operatorname{Var}(X_1) = \sigma^2 < \infty$.

(a) State and prove the Weak Law of Large Numbers.

(b) State the Strong Law of Large Numbers. (Proof not required.)

(c) State and prove the Central Limit Theorem using characteristic functions (Lévy's Continuity Theorem may be cited without proof).

---

**Problem 6.** Let $(\Omega, \mathcal{F}, P)$ be a probability space.

(a) State the Monotone Convergence Theorem and the Dominated Convergence Theorem.

(b) Compute $\displaystyle\lim_{n \to \infty} \int_0^\infty \frac{n \sin(x/n)}{x(1 + x^2)}\,dx$ using the DCT. Justify every step.

(c) Prove Borel-Cantelli Lemma I: if $\sum_{n=1}^\infty P(A_n) < \infty$, then $P(\limsup A_n) = 0$.

</details>

---

## Mock Exam 2

<details>
<summary>📘 Analysis — Problems 1 &amp; 2</summary>

**Problem 1.** Let $(X, d)$ be a compact metric space and $f: X \to X$ a continuous function satisfying $d(f(x), f(y)) < d(x, y)$ for all $x \neq y$.

(a) Prove that $f$ has a unique fixed point.

(b) Show that compactness is necessary by giving an explicit counterexample on a non-compact metric space.

---

**Problem 2.** Consider $g: \mathbb{R}^2 \to \mathbb{R}^2$ defined by $g(x, y) = (e^x \cos y - 1,\; e^x \sin y)$.

(a) Show that $g(0, 0) = (0, 0)$ and compute the Jacobian $Dg(0, 0)$.

(b) Apply the Inverse Function Theorem to show $g$ is locally invertible near $(0, 0)$.

(c) Compute $D(g^{-1})(0, 0)$ explicitly.

</details>

<details>
<summary>📗 Linear Algebra — Problems 3 &amp; 4</summary>

**Problem 3.** Let $A$ be a real $n \times n$ matrix (not necessarily symmetric).

(a) Prove that all eigenvalues of $A^T A$ are nonnegative.

(b) Prove that $A$ is invertible if and only if all singular values of $A$ are strictly positive.

(c) Show that $\|A\|_2 = \sigma_{\max}(A)$, the largest singular value.

---

**Problem 4.** Let $P$ be an $n \times n$ matrix satisfying $P^2 = P$ (idempotent).

(a) Prove that the eigenvalues of $P$ are 0 or 1.

(b) Prove that $\operatorname{rank}(P) = \operatorname{trace}(P)$.

(c) If additionally $P = P^T$, prove that $P$ is the orthogonal projection onto $\operatorname{Col}(P)$.

</details>

<details>
<summary>📙 Probability — Problems 5 &amp; 6</summary>

**Problem 5.** Let $(M_n, \mathcal{F}_n)_{n \geq 0}$ be a martingale with $M_0 = 0$.

(a) Prove that $E[M_n] = 0$ for all $n \geq 0$.

(b) Prove that if $E[M_n^2] < \infty$ for all $n$, then $E[M_n^2] = \sum_{k=1}^n E[(M_k - M_{k-1})^2]$.

(c) Let $X_i$ be i.i.d. with $P(X_i = 1) = P(X_i = -1) = 1/2$. Define $S_n = X_1 + \cdots + X_n$. Show that $S_n$ is a martingale and that $S_n^2 - n$ is a martingale.

---

**Problem 6.** Let $X$ and $Y$ be jointly distributed with $X \sim N(0, 1)$ and $Y | X \sim N(X, 1)$.

(a) Compute $E[Y]$, $\operatorname{Var}(Y)$, and $\operatorname{Cov}(X, Y)$.

(b) Compute $E[X | Y = y]$ and $\operatorname{Var}(X | Y = y)$.

(c) Is $(X, Y)$ jointly Gaussian? Prove your claim.

</details>

---

## Mock Exam 3

<details>
<summary>📘 Analysis — Problems 1 &amp; 2</summary>

**Problem 1.** Let $K \subset \mathbb{R}^n$ be compact and $\{U_\alpha\}_{\alpha \in A}$ an open cover.

(a) Prove that there exists a **Lebesgue number** $\delta > 0$ such that every subset of $K$ with diameter less than $\delta$ is contained in some $U_\alpha$.

(b) Use part (a) to prove that every continuous function on a compact metric space is uniformly continuous.

---

**Problem 2.** Let $f_n(x) = \frac{nx}{1 + n^2 x^2}$ for $x \in [0, 1]$.

(a) Find $f(x) = \lim_{n \to \infty} f_n(x)$ for each $x \in [0,1]$. Determine whether convergence is uniform, and justify your answer.

(b) Compute $\lim_{n \to \infty} \int_0^1 f_n(x)\,dx$ and $\int_0^1 f(x)\,dx$. Are they equal?

(c) Does your answer contradict the Uniform Limit Integration Theorem? Explain precisely.

</details>

<details>
<summary>📗 Linear Algebra — Problems 3 &amp; 4</summary>

**Problem 3.** (Positive Definite Matrices)

(a) Prove that $A \succ 0$ (positive definite) if and only if all eigenvalues of $A$ are strictly positive.

(b) Prove that if $A \succ 0$ and $B \succeq 0$, then $\lambda_i(A + B) \geq \lambda_i(A)$ for all $i$ (using Weyl's inequality).

(c) Prove that the set of $n \times n$ positive definite matrices is an open subset of the space of symmetric matrices.

---

**Problem 4.** Let $A$ be $m \times n$ with $m \geq n$ and $\operatorname{rank}(A) = n$.

(a) Prove that $A^T A$ is invertible and positive definite.

(b) Show that $P = A(A^T A)^{-1} A^T$ is the orthogonal projection onto $\operatorname{Col}(A)$.

(c) Prove that the least-squares solution to $Ax = b$ is $x^* = (A^T A)^{-1} A^T b$ and that $x^*$ is unique.

</details>

<details>
<summary>📙 Probability — Problems 5 &amp; 6</summary>

**Problem 5.** (Modes of Convergence)

(a) Prove: almost sure convergence implies convergence in probability.

(b) Prove: convergence in probability implies convergence in distribution.

(c) Construct an explicit example showing convergence in probability does **not** imply almost sure convergence.

(d) Prove: if $X_n \xrightarrow{d} c$ for some constant $c \in \mathbb{R}$, then $X_n \xrightarrow{P} c$.

---

**Problem 6.** Let $X_1, X_2, \ldots$ be i.i.d. Exponential($\lambda$) random variables.

(a) Derive the MLE $\hat{\lambda}_n$ of $\lambda$ and show it is consistent.

(b) Compute the Fisher Information $I(\lambda)$ and verify that $\hat{\lambda}_n$ is asymptotically efficient (achieves the CRLB asymptotically).

(c) Find the asymptotic distribution of $\sqrt{n}(\hat{\lambda}_n - \lambda)$.

(d) Construct an approximate 95% confidence interval for $\lambda$ based on part (c).

</details>

---

## Grading Rubric

| Score | Description |
|-------|-------------|
| 9–10 | Complete, rigorous proof with clear, well-organized exposition |
| 7–8 | Correct proof with minor gaps or imprecise but non-fatal steps |
| 5–6 | Correct overall approach; significant gaps in rigor or key steps missing |
| 3–4 | Partial understanding; major errors or critical omissions |
| 1–2 | Relevant definitions or ideas mentioned but no coherent proof |
| 0 | Blank, or approach is wholly incorrect |

---

## Preparation Tips

<div class="steps-grid">
  <div class="step-card">
    <div class="step-number">1</div>
    <div class="step-title">Start with Definitions</div>
    <div class="step-desc">Begin every answer by stating the relevant definitions precisely. This grounds your proof, demonstrates mastery, and earns partial credit even if the proof is incomplete.</div>
  </div>
  <div class="step-card">
    <div class="step-number">2</div>
    <div class="step-title">State Theorems Explicitly</div>
    <div class="step-desc">When invoking a named theorem — Bolzano-Weierstrass, Courant-Fischer, Dominated Convergence — state it fully before using it. Do not assume the reader knows what you mean.</div>
  </div>
  <div class="step-card">
    <div class="step-number">3</div>
    <div class="step-title">Time Management</div>
    <div class="step-desc">Allocate approximately 45 minutes per problem. If stuck after 20 minutes, move on and return. A partial proof on four problems beats an incomplete proof on two.</div>
  </div>
  <div class="step-card">
    <div class="step-number">4</div>
    <div class="step-title">Practice Proof Writing</div>
    <div class="step-desc">Work through Rudin Ch. 2, 3, 7, 9 and Horn &amp; Johnson Ch. 1, 4, 7 for exam-representative problems. Write complete proofs — do not just sketch arguments.</div>
  </div>
  <div class="step-card">
    <div class="step-number">5</div>
    <div class="step-title">Use Past Exams</div>
    <div class="step-desc">JHU departmental past qualifying exams are the single best preparation resource for calibrating difficulty, format, and the standard of rigor expected.</div>
  </div>
</div>
