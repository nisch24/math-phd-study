---
layout: default
title: "Qualifying Exam Simulation"
nav_order: 11
permalink: /qualifying_exam/
---

# Qualifying Exam Simulation

> *The JHU AMS Introductory Exam is given as **three separate papers**: Real Analysis, Linear Algebra, and Probability. The practice papers below follow that structure, with one six-problem paper per subject. Each problem requires a complete, rigorous proof.*

{: .warning }
> The format below is taken from recent past papers posted by the JHU AMS department (2023–2025), whose instruction sheets read roughly: *closed book, 6 problems worth 5 points each, best five scores count, passing grade 2/3*. Deadlines and rules change; confirm the current format and the semester by which you must pass in the official AMS PhD handbook before relying on it. These practice papers are original problems written in the same style, **not** past exam questions.

<div class="info-card">
  <div class="info-row"><span class="info-label">📂 Papers</span> Real Analysis · Linear Algebra · Probability (taken separately)</div>
  <div class="info-row"><span class="info-label">⏱ Duration</span> 3 hours per paper (recent sessions ran 8:30–11:30)</div>
  <div class="info-row"><span class="info-label">📝 Problems</span> 6 per paper, 5 points each; your best 5 count (25 points)</div>
  <div class="info-row"><span class="info-label">📊 Passing</span> 2/3 of the available points, i.e. at least 17 of 25</div>
  <div class="info-row"><span class="info-label">✍️ Style</span> Closed book. Formal proofs required; state every theorem you invoke.</div>
</div>

**How to use these papers.** Sit each paper in one 3-hour block, with no notes and no internet. Then grade yourself against the rubric below, ideally by trading papers with a study partner. Once you have done these three, move on to the **real past papers**, which the JHU AMS department posts publicly. Search for "JHU AMS Introductory Exam" to find the department's PDF archive, which includes solutions for some sessions.

---

## Paper A — Real Analysis

<details open markdown="1">
<summary>📘 Real Analysis — 6 problems (3 hours)</summary>

**Problem 1.** Let $f: [0,1] \to \mathbb{R}$ be continuous with $f(0) = f(1)$.

(a) Prove that for each $n \in \mathbb{N}$, there exists $x_n \in [0, 1 - 1/n]$ such that $f(x_n + 1/n) = f(x_n)$.

(b) Show that (a) fails for chord lengths not of the form $1/n$: if $h \in (0,1)$ and $1/h \notin \mathbb{N}$, then $f(x) = \sin^2(\pi x / h) - x \sin^2(\pi / h)$ satisfies $f(0) = f(1)$ but $f(x + h) \neq f(x)$ for every $x \in [0, 1-h]$.

---

**Problem 2.** Let $\{f_n\}$ be a sequence of continuous functions on $[0,1]$ converging uniformly to $f$.

(a) Prove that $f$ is continuous.

(b) Prove that $\displaystyle\int_0^1 f_n(x)\,dx \to \int_0^1 f(x)\,dx$.

(c) Give an explicit example where $f_n \to f$ pointwise, each $f_n$ is continuous, but $f$ is discontinuous.

---

**Problem 3.** Let $(X, d)$ be a compact metric space and $f: X \to X$ a continuous function satisfying $d(f(x), f(y)) < d(x, y)$ for all $x \neq y$.

(a) Prove that $f$ has a unique fixed point. *(Hint: minimize $x \mapsto d(x, f(x))$.)*

(b) Show that compactness is necessary by giving an explicit counterexample on a non-compact metric space.

---

**Problem 4.** Consider $g: \mathbb{R}^2 \to \mathbb{R}^2$ defined by $g(x, y) = (e^x \cos y - 1,\; e^x \sin y)$.

(a) Show that $g(0, 0) = (0, 0)$ and compute the Jacobian $Dg(0, 0)$.

(b) Apply the Inverse Function Theorem to show $g$ is locally invertible near $(0, 0)$.

(c) Compute $D(g^{-1})(0, 0)$ explicitly.

---

**Problem 5.** Let $(K, d)$ be a compact metric space and $\{U_\alpha\}_{\alpha \in A}$ an open cover of $K$.

(a) Prove that there exists a **Lebesgue number** $\delta > 0$ such that every subset of $K$ with diameter less than $\delta$ is contained in some $U_\alpha$.

(b) Use part (a) to prove that every continuous function from a compact metric space to $\mathbb{R}$ is uniformly continuous.

---

**Problem 6.** Let $f_n(x) = \dfrac{nx}{1 + n^2 x^2}$ for $x \in [0, 1]$.

(a) Find $f(x) = \lim_{n \to \infty} f_n(x)$ for each $x \in [0,1]$. Determine whether convergence is uniform, and justify your answer.

(b) Compute $\lim_{n \to \infty} \int_0^1 f_n(x)\,dx$ and $\int_0^1 f(x)\,dx$. Are they equal?

(c) Explain why your answers to (a) and (b) are consistent with the theorem that uniform convergence allows limits and integrals to be interchanged. What does this example show about whether uniform convergence is *necessary* for the interchange?

</details>

---

## Paper B — Linear Algebra

<details markdown="1">
<summary>📗 Linear Algebra — 6 problems (3 hours)</summary>

**Problem 1.** Let $A \in \mathbb{R}^{n \times n}$ be symmetric with eigenvalues $\lambda_1 \leq \lambda_2 \leq \cdots \leq \lambda_n$.

(a) Prove that $\lambda_1 = \min_{\|x\|=1} x^T A x$ and $\lambda_n = \max_{\|x\|=1} x^T A x$.

(b) Let $B$ be obtained from $A$ by deleting the $n$-th row and corresponding column. Prove that the eigenvalues of $B$ interlace those of $A$.

---

**Problem 2.** Let $A \in \mathbb{R}^{m \times n}$.

(a) Prove that $\operatorname{rank}(A) = \operatorname{rank}(A^T A) = \operatorname{rank}(AA^T)$.

(b) Show that the nonzero eigenvalues of $A^T A$ and $AA^T$ coincide, with the same multiplicities.

(c) State the Singular Value Decomposition of $A$ and prove its existence using (a) and (b) together with the spectral theorem.

---

**Problem 3.** Let $A$ be a real $n \times n$ matrix (not necessarily symmetric).

(a) Prove that all eigenvalues of $A^T A$ are nonnegative.

(b) Prove that $A$ is invertible if and only if all singular values of $A$ are strictly positive.

(c) Show that $\|A\|_2 = \sigma_{\max}(A)$, the largest singular value.

---

**Problem 4.** Let $P$ be an $n \times n$ matrix satisfying $P^2 = P$ (idempotent).

(a) Prove that the eigenvalues of $P$ are 0 or 1.

(b) Prove that $\operatorname{rank}(P) = \operatorname{trace}(P)$.

(c) If additionally $P = P^T$, prove that $P$ is the orthogonal projection onto $\operatorname{Col}(P)$.

---

**Problem 5.** (Positive Definite Matrices)

(a) Prove that a symmetric matrix $A$ is positive definite if and only if all eigenvalues of $A$ are strictly positive.

(b) Prove that if $A$ is symmetric and $B \succeq 0$, then $\lambda_i(A + B) \geq \lambda_i(A)$ for all $i$ (eigenvalues in increasing order).

(c) Prove that the set of $n \times n$ positive definite matrices is an open subset of the space of symmetric matrices.

---

**Problem 6.** Let $A$ be $m \times n$ with $m \geq n$ and $\operatorname{rank}(A) = n$.

(a) Prove that $A^T A$ is invertible and positive definite.

(b) Show that $P = A(A^T A)^{-1} A^T$ is the orthogonal projection onto $\operatorname{Col}(A)$.

(c) Prove that the least-squares problem $\min_x \|Ax - b\|_2$ has the unique solution $x^* = (A^T A)^{-1} A^T b$.

</details>

---

## Paper C — Probability

<details markdown="1">
<summary>📙 Probability — 6 problems (3 hours)</summary>

**Problem 1.** Let $X_1, X_2, \ldots$ be i.i.d. with $E[X_1] = \mu$ and $\operatorname{Var}(X_1) = \sigma^2 < \infty$.

(a) State and prove the Weak Law of Large Numbers.

(b) State the Strong Law of Large Numbers. (Proof not required.)

(c) State and prove the Central Limit Theorem using characteristic functions (Lévy's Continuity Theorem may be cited without proof).

---

**Problem 2.** Let $(\Omega, \mathcal{F}, P)$ be a probability space.

(a) State the Monotone Convergence Theorem and the Dominated Convergence Theorem.

(b) Compute $\displaystyle\lim_{n \to \infty} \int_0^\infty \frac{n \sin(x/n)}{x(1 + x^2)}\,dx$, justifying every step.

(c) Prove Borel–Cantelli Lemma I: if $\sum_{n=1}^\infty P(A_n) < \infty$, then $P(\limsup A_n) = 0$.

---

**Problem 3.** Let $(M_n, \mathcal{F}_n)_{n \geq 0}$ be a martingale with $M_0 = 0$.

(a) Prove that $E[M_n] = 0$ for all $n \geq 0$.

(b) Prove that if $E[M_n^2] < \infty$ for all $n$, then $E[M_n^2] = \sum_{k=1}^n E[(M_k - M_{k-1})^2]$.

(c) Let $X_i$ be i.i.d. with $P(X_i = 1) = P(X_i = -1) = 1/2$ and $S_n = X_1 + \cdots + X_n$. Show that $S_n$ and $S_n^2 - n$ are martingales with respect to $\mathcal{F}_n = \sigma(X_1, \ldots, X_n)$.

---

**Problem 4.** Let $X \sim N(0, 1)$ and suppose that, conditionally on $X$, $Y \sim N(X, 1)$.

(a) Compute $E[Y]$, $\operatorname{Var}(Y)$, and $\operatorname{Cov}(X, Y)$.

(b) Compute $E[X \mid Y]$ and $\operatorname{Var}(X \mid Y)$.

(c) Is $(X, Y)$ jointly Gaussian? Prove your claim.

---

**Problem 5.** (Modes of Convergence)

(a) Prove that almost sure convergence implies convergence in probability.

(b) Prove that convergence in probability implies convergence in distribution.

(c) Construct an explicit example showing that convergence in probability does **not** imply almost sure convergence.

(d) Prove that if $X_n \xrightarrow{d} c$ for a constant $c \in \mathbb{R}$, then $X_n \xrightarrow{P} c$.

---

**Problem 6.** Let $X_1, X_2, \ldots$ be i.i.d. Exponential(1) random variables.

(a) Show that for every $c > 1$, $P(X_n > c \log n \text{ i.o.}) = 0$.

(b) Show that $P(X_n > \log n \text{ i.o.}) = 1$.

(c) Conclude that $\displaystyle\limsup_{n \to \infty} \frac{X_n}{\log n} = 1$ almost surely.

(d) Let $M_n = \max_{1 \leq i \leq n} X_i$. Show that $M_n - \log n$ converges in distribution, and identify the limit (the Gumbel distribution).

</details>

---

## Grading Rubric (per problem, 5 points)

| Score | Description |
|-------|-------------|
| 5 | Complete, rigorous proof with clear, well-organized exposition |
| 4 | Correct proof with a minor gap or an imprecise but non-fatal step |
| 3 | Correct overall approach; a significant gap or a key step missing |
| 2 | Partial progress: correct setup and relevant ideas, but no complete argument |
| 1 | Relevant definitions or theorems stated, with no real progress |
| 0 | Blank, or the approach is wholly incorrect |

**Passing a paper** means 17 or more points from your best five problems. Grade honestly. Any score of 4 should come with a written note on exactly what the gap was.

---

## Preparation Tips

<div class="steps-grid">
  <div class="step-card">
    <div class="step-number">1</div>
    <div class="step-title">Start with Definitions</div>
    <div class="step-desc">Begin every answer by stating the relevant definitions precisely. This grounds your proof, shows you know the material, and earns partial credit even if the proof is incomplete.</div>
  </div>
  <div class="step-card">
    <div class="step-number">2</div>
    <div class="step-title">State Theorems Explicitly</div>
    <div class="step-desc">When invoking a named theorem (Bolzano–Weierstrass, Courant–Fischer, Dominated Convergence), state it and check its hypotheses before using it.</div>
  </div>
  <div class="step-card">
    <div class="step-number">3</div>
    <div class="step-title">Time Management</div>
    <div class="step-desc">With 3 hours for 6 problems and only 5 counting, plan about 30 minutes per problem. Read all six first, and skip the one you like least. If you're stuck after 15 minutes, move on and come back.</div>
  </div>
  <div class="step-card">
    <div class="step-number">4</div>
    <div class="step-title">Practice Proof Writing</div>
    <div class="step-desc">Work Rudin Ch. 2, 3, 7, 9; Horn &amp; Johnson Ch. 1, 2, 4, 7; and Durrett Ch. 1–3 (or an undergraduate probability text, depending on the level of recent probability papers). Write complete proofs, not sketches.</div>
  </div>
  <div class="step-card">
    <div class="step-number">5</div>
    <div class="step-title">Use Past Exams</div>
    <div class="step-desc">Past papers from the department are the single best resource for calibrating difficulty and the expected standard of rigor. Do at least three per subject under timed conditions.</div>
  </div>
</div>
