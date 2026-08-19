---
layout: default
title: "EN.553.721 — Probability Theory II"
parent: "Module B — Probability & Stochastic Processes"
nav_order: 2
permalink: /module_b/probability_theory_2/
---

# EN.553.721 — Probability Theory II

> *Advanced probability: conditional expectation, the Radon-Nikodym theorem, martingale theory, and an introduction to Brownian motion. This course provides the stochastic machinery essential for statistical theory, financial mathematics, and the modern theory of stochastic processes.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Compute and interpret conditional expectations** as $L^2$ projections onto sub-$\sigma$-algebras.
2. **State and apply the Radon-Nikodym theorem** for absolutely continuous measures, including its role in likelihood ratios.
3. **Define martingales** and prove the key convergence results: Doob's upcrossing inequality and the Martingale Convergence Theorem.
4. **Apply optional stopping** and Doob's maximal inequality to concrete problems.
5. **Characterize standard Brownian motion** and derive its fundamental properties.

---

## Core Theory

### Unit 1: Conditional Expectation

#### 1.1 Existence and Uniqueness

**Theorem**: Let $X$ be integrable on $(\Omega, \mathcal{F}, P)$ and $\mathcal{G} \subseteq \mathcal{F}$ a sub-$\sigma$-algebra. There exists a $\mathcal{G}$-measurable random variable $E[X|\mathcal{G}]$, unique $P$-a.s., satisfying:

$$\int_G E[X|\mathcal{G}] \, dP = \int_G X \, dP \quad \text{for all } G \in \mathcal{G}.$$

*Proof*: The set function $\nu(G) = \int_G X \, dP$ is a signed measure that is absolutely continuous with respect to $P|_\mathcal{G}$. By the Radon-Nikodym theorem, $E[X|\mathcal{G}] = d\nu / dP|_\mathcal{G}$.

#### 1.2 Properties of Conditional Expectation

For integrable random variables $X, Y$ and sub-$\sigma$-algebra $\mathcal{G}$:

1. **Linearity**: $E[aX + bY | \mathcal{G}] = aE[X|\mathcal{G}] + bE[Y|\mathcal{G}]$ a.s.
2. **Tower property**: If $\mathcal{H} \subseteq \mathcal{G}$, then $E[E[X|\mathcal{G}]|\mathcal{H}] = E[X|\mathcal{H}]$ a.s.
3. **Independence**: If $X$ is independent of $\mathcal{G}$, then $E[X|\mathcal{G}] = E[X]$ a.s.
4. **Taking out what is known**: If $Y$ is $\mathcal{G}$-measurable and $XY$ is integrable, then $E[XY|\mathcal{G}] = Y \cdot E[X|\mathcal{G}]$ a.s.
5. **Jensen**: If $\varphi$ is convex and $\varphi(X)$ is integrable, then $\varphi(E[X|\mathcal{G}]) \leq E[\varphi(X)|\mathcal{G}]$ a.s.

#### 1.3 $L^2$ Projection Interpretation

$E[X|\mathcal{G}]$ is the **orthogonal projection** of $X$ onto the closed subspace $L^2(\mathcal{G}) \subseteq L^2(\Omega, \mathcal{F}, P)$:

$$E[X|\mathcal{G}] = \underset{Y \in L^2(\mathcal{G})}{\arg\min}\; E[(X - Y)^2].$$

This geometric interpretation is fundamental: conditional expectation is the best $\mathcal{G}$-measurable predictor of $X$ in the mean-squared-error sense.

---

### Unit 2: The Radon-Nikodym Theorem

#### 2.1 Absolute Continuity

**Definition**: A measure $\nu$ is **absolutely continuous** with respect to $\mu$ (written $\nu \ll \mu$) if $\mu(A) = 0 \Rightarrow \nu(A) = 0$.

**Lebesgue Decomposition Theorem**: Any $\sigma$-finite measure $\nu$ decomposes uniquely as $\nu = \nu_{ac} + \nu_s$, where $\nu_{ac} \ll \mu$ and $\nu_s \perp \mu$ (mutually singular).

#### 2.2 The Radon-Nikodym Theorem

**Theorem**: Let $\nu$ and $\mu$ be $\sigma$-finite measures on $(\Omega, \mathcal{F})$ with $\nu \ll \mu$. Then there exists a nonneg­ative measurable function $f$ — the **Radon-Nikodym derivative** $\frac{d\nu}{d\mu}$ — unique $\mu$-a.e., such that:

$$\nu(A) = \int_A f \, d\mu \quad \text{for all } A \in \mathcal{F}.$$

**Applications in Probability**:
- **Likelihood ratios**: If $Q \ll P$, then $L = \frac{dQ}{dP}$ satisfies $E_P[L] = 1$ and $E_Q[X] = E_P[XL]$.
- **Change of measure**: $E_Q[X] = E_P\!\left[X \frac{dQ}{dP}\right]$ — the foundation of importance sampling and risk-neutral pricing.
- **Density functions**: If $\mu_X \ll \lambda$ (Lebesgue), then $f_X = \frac{d\mu_X}{d\lambda}$ is the probability density function.

---

### Unit 3: Martingale Theory

#### 3.1 Definitions

A sequence $(M_n, \mathcal{F}_n)_{n \geq 0}$ is a **martingale** if:

1. $\mathcal{F}_0 \subseteq \mathcal{F}_1 \subseteq \cdots$ is a **filtration**.
2. $M_n$ is $\mathcal{F}_n$-measurable and integrable for each $n$.
3. $E[M_{n+1} | \mathcal{F}_n] = M_n$ a.s. (the "fair game" condition).

If condition 3 is replaced by $\geq$ ($\leq$), $(M_n)$ is a **submartingale** (**supermartingale**).

**Canonical Examples**:
- **Zero-mean random walk**: $S_n = X_1 + \cdots + X_n$ with $E[X_i] = 0$ is a martingale w.r.t. $\mathcal{F}_n = \sigma(X_1, \ldots, X_n)$.
- **Likelihood ratio process**: $L_n = \prod_{i=1}^n \frac{q(X_i)}{p(X_i)}$ under $P$.
- **Doob martingale**: $M_n = E[X | \mathcal{F}_n]$ for any integrable $X$ — the prototypical example.

#### 3.2 The Upcrossing Inequality and Martingale Convergence

**Doob's Upcrossing Inequality**: Let $(M_n)$ be a submartingale and $U_n(a, b)$ the number of upcrossings of $[a, b]$ by $M_0, \ldots, M_n$. Then:

$$E[U_n(a, b)] \leq \frac{E[(M_n - a)^+]}{b - a}.$$

**Theorem (Martingale Convergence Theorem)**: If $(M_n)$ is a submartingale with $\sup_n E[M_n^+] < \infty$, then $M_n \to M_\infty$ a.s. for some integrable $M_\infty$.

*Proof*: If $M_n$ fails to converge, it must oscillate, producing infinitely many upcrossings of some rational interval $[a, b]$. The upcrossing inequality gives $E[U_\infty(a,b)] < \infty$, so $U_\infty(a,b) < \infty$ a.s. — a contradiction.

> [!NOTE]
> Almost-sure convergence does **not** imply $L^1$ convergence. The additional condition needed is **uniform integrability**.

#### 3.3 Uniform Integrability and $L^1$ Convergence

**Definition**: A collection $\{X_\alpha\}$ is **uniformly integrable (UI)** if:

$$\lim_{c \to \infty} \sup_\alpha E[|X_\alpha| \mathbf{1}_{|X_\alpha| > c}] = 0.$$

**Theorem**: For a martingale $(M_n)$, the following are equivalent:
1. $(M_n)$ is uniformly integrable.
2. $M_n \to M_\infty$ in $L^1$.
3. $M_n = E[M_\infty | \mathcal{F}_n]$ for all $n$ (the martingale is *closed*).

#### 3.4 Optional Stopping

**Theorem (Optional Stopping Theorem)**: Let $(M_n)$ be a uniformly integrable martingale and $\tau$ a stopping time. Then:

$$E[M_\tau] = E[M_0].$$

More generally, if $\sigma \leq \tau$ are bounded stopping times, then $E[M_\tau | \mathcal{F}_\sigma] = M_\sigma$.

**Theorem (Doob's Maximal Inequality)**: If $(M_n)$ is a nonnegative submartingale:

$$P\!\left(\max_{0 \leq k \leq n} M_k \geq \lambda\right) \leq \frac{E[M_n]}{\lambda}.$$

---

### Unit 4: Introduction to Brownian Motion

#### 4.1 Definition

A stochastic process $(B_t)_{t \geq 0}$ is a **standard Brownian motion** (Wiener process) if:

1. $B_0 = 0$.
2. **Independent increments**: $B_{t_2} - B_{t_1}, \ldots, B_{t_n} - B_{t_{n-1}}$ are independent for $t_1 < \cdots < t_n$.
3. **Gaussian increments**: $B_t - B_s \sim N(0, t - s)$ for $s < t$.
4. $t \mapsto B_t$ is continuous a.s.

#### 4.2 Key Properties

- **Martingale**: $(B_t)$ is a martingale w.r.t. its natural filtration $\mathcal{F}_t = \sigma(B_s : s \leq t)$.
- **Quadratic variation**: $[B]_t = t$ (the "clock" of Brownian motion; fundamental to stochastic calculus).
- **Self-similarity**: $\{c^{-1/2}B_{ct}\}_{t \geq 0} \overset{d}{=} \{B_t\}_{t \geq 0}$ for any $c > 0$.
- **Nowhere differentiable**: $B_t$ is a.s. continuous on $[0,\infty)$ but nowhere differentiable.
- **Recurrence**: In $\mathbb{R}^1$ and $\mathbb{R}^2$, Brownian motion is recurrent; in $\mathbb{R}^d$ for $d \geq 3$, it is transient.

#### 4.3 Donsker's Invariance Principle (Functional CLT)

Let $X_i$ be i.i.d. with $E[X_i] = 0$, $\operatorname{Var}(X_i) = 1$, and $S_n = X_1 + \cdots + X_n$. Define the linearly interpolated process:

$$W_n(t) = \frac{1}{\sqrt{n}} S_{\lfloor nt \rfloor} + (nt - \lfloor nt \rfloor) \frac{X_{\lfloor nt \rfloor + 1}}{\sqrt{n}}.$$

Then $W_n \xrightarrow{d} B$ in $(C[0,1], \|\cdot\|_\infty)$. This is the **Functional CLT** (or Donsker's Theorem) — the random walk converges to Brownian motion as a process.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Probability: Theory and Examples* (5th ed.) | Rick Durrett | **Primary** — Chapters 4–8 |
| *Probability with Martingales* | David Williams | **Supplementary** — Elegant, concise martingale-focused treatment |
| *Brownian Motion and Stochastic Calculus* | Ioannis Karatzas &amp; Steven Shreve | **Advanced** — The definitive reference for further study |
| *Continuous Martingales and Brownian Motion* | Daniel Revuz &amp; Marc Yor | **Reference** — Encyclopedic treatment of Brownian motion |

---

## Problem Sets

### Problem Set 1: Conditional Expectation &amp; Radon-Nikodym

1. **(Durrett 4.1)** Prove the tower property of conditional expectation.
2. **(Exam-style)** Let $X \sim N(\mu, \sigma^2)$ and $Y = X + Z$ where $Z \sim N(0, \tau^2)$ is independent of $X$. Compute $E[X|Y]$ and $\operatorname{Var}(X|Y)$.
3. **(Exam-style)** Let $P$ and $Q$ be probability measures with $\frac{dQ}{dP} = L$. Show $E_Q[X] = E_P[XL]$ and compute the Radon-Nikodym derivative for two Gaussian measures with different means.
4. **(Proof)** Prove that conditional expectation is a contraction in $L^2$: $E[(E[X|\mathcal{G}])^2] \leq E[X^2]$.
5. **(Application — Bayesian Inference)** With prior $\theta \sim N(0,1)$ and likelihood $X|\theta \sim N(\theta, 1)$, compute the posterior mean $E[\theta|X]$ and posterior variance $\operatorname{Var}(\theta|X)$.

### Problem Set 2: Martingales

1. **(Durrett 5.2)** Prove: if $(M_n)$ is a martingale with $M_0 = 0$ and $\sup_n E[M_n^2] < \infty$, then $M_n$ converges a.s. and in $L^2$.
2. **(Exam-style)** Let $S_n = X_1 + \cdots + X_n$ with $P(X_i = 1) = P(X_i = -1) = 1/2$. Show $S_n^2 - n$ is a martingale.
3. **(Exam-style)** State and prove Doob's upcrossing inequality.
4. **(Application — Gambler's Ruin)** A gambler begins with $\$k$ and at each step wins $\$1$ with probability $p$ or loses $\$1$ with probability $q = 1-p$. Use optional stopping to find the probability of reaching $\$N$ before ruin.
5. **(Challenge)** Construct a martingale that converges a.s. to $0$ but does not converge in $L^1$.

### Problem Set 3: Brownian Motion

1. **(Durrett 8.1)** Verify that the covariance function of standard Brownian motion is $\operatorname{Cov}(B_s, B_t) = \min(s, t)$.
2. **(Exam-style)** Show that $B_t^2 - t$ is a martingale with respect to the natural filtration of $(B_t)$.
3. **(Proof)** Prove that $e^{\theta B_t - \theta^2 t / 2}$ is a martingale for every $\theta \in \mathbb{R}$ (the Doléans-Dade exponential).
4. **(Application)** Use the reflection principle to compute $P\!\left(\max_{0 \leq s \leq t} B_s \geq a\right)$ for $a > 0$.
5. **(Challenge)** Prove that Brownian motion paths are a.s. nowhere differentiable.

---

## Study Guide &amp; Exam Preparation

> [!IMPORTANT]
> **Key Theorems for the Qualifying Exam (Advanced Probability)**
>
> - **Tower property** of conditional expectation — know the proof using the defining integral equation
> - **Radon-Nikodym theorem** — statement, uniqueness, and the likelihood ratio application
> - **Martingale Convergence Theorem** — proof via upcrossing inequality; UI condition for $L^1$ convergence
> - **Optional Stopping Theorem** — state precisely (UI or bounded $\tau$), then apply to gambler's ruin
> - **Doob's Maximal Inequality** — proof and connection to the upcrossing inequality
> - **Brownian motion** — know the four defining properties; be able to show $B_t^2 - t$ is a martingale

**Proof-Writing Tips**:
- When applying optional stopping, always verify the integrability/UI condition explicitly.
- For martingale convergence, the key step is showing $E[U_\infty] < \infty$ via the upcrossing inequality.
- Conditional expectation proofs typically reduce to verifying the defining integral equation on every $G \in \mathcal{G}$.
