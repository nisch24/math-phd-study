---
layout: default
title: "EN.553.721 — Probability Theory II"
parent: "Module B — Probability & Stochastic Processes"
nav_order: 2
---

# EN.553.721 — Probability Theory II

> *Advanced probability: conditional expectation, the Radon-Nikodym theorem, martingale theory, and an introduction to Brownian motion. This course provides the stochastic machinery essential for statistical theory, financial mathematics, and stochastic processes.*

---

## Learning Objectives

1. **Compute and interpret conditional expectations** as projections in $L^2$.
2. **State and apply the Radon-Nikodym theorem** for absolutely continuous measures.
3. **Define martingales** and prove key convergence results (upcrossing inequality, martingale convergence theorem).
4. **Apply optional stopping** and martingale transforms in applications.
5. **Characterize Brownian motion** and derive its basic properties.

---

## Core Theory

### Unit 1: Conditional Expectation

#### 1.1 Definition and Existence

**Theorem (Existence & Uniqueness)**: Let $X$ be integrable on $(\Omega, \mathcal{F}, P)$ and $\mathcal{G} \subseteq \mathcal{F}$ a sub-$\sigma$-algebra. There exists a $\mathcal{G}$-measurable random variable $E[X|\mathcal{G}]$, unique a.s., satisfying:

$$\int_G E[X|\mathcal{G}] \, dP = \int_G X \, dP \quad \text{for all } G \in \mathcal{G}$$

*Proof*: The measure $\nu(G) = \int_G X \, dP$ is absolutely continuous w.r.t. $P|_\mathcal{G}$. By the Radon-Nikodym theorem, $E[X|\mathcal{G}] = d\nu/dP|_\mathcal{G}$.

#### 1.2 Properties

For integrable random variables $X, Y$ and sub-$\sigma$-algebra $\mathcal{G}$:

1. **Linearity**: $E[aX + bY | \mathcal{G}] = aE[X|\mathcal{G}] + bE[Y|\mathcal{G}]$ a.s.
2. **Tower property**: If $\mathcal{H} \subseteq \mathcal{G}$, then $E[E[X|\mathcal{G}]|\mathcal{H}] = E[X|\mathcal{H}]$ a.s.
3. **Independence**: If $X$ is independent of $\mathcal{G}$, then $E[X|\mathcal{G}] = E[X]$ a.s.
4. **Taking out what is known**: If $Y$ is $\mathcal{G}$-measurable and $XY$ is integrable, then $E[XY|\mathcal{G}] = Y \cdot E[X|\mathcal{G}]$ a.s.
5. **Jensen**: If $\varphi$ is convex, $\varphi(E[X|\mathcal{G}]) \leq E[\varphi(X)|\mathcal{G}]$ a.s.

#### 1.3 $L^2$ Projection Interpretation

$E[X|\mathcal{G}]$ is the **orthogonal projection** of $X$ onto $L^2(\mathcal{G})$ — the closest $\mathcal{G}$-measurable random variable to $X$ in the $L^2$ norm:

$$E[X|\mathcal{G}] = \arg\min_{Y \in L^2(\mathcal{G})} E[(X - Y)^2]$$

---

### Unit 2: The Radon-Nikodym Theorem

#### 2.1 Absolute Continuity

**Definition**: Measure $\nu$ is **absolutely continuous** w.r.t. $\mu$ (written $\nu \ll \mu$) if $\mu(A) = 0 \Rightarrow \nu(A) = 0$.

**Lebesgue Decomposition**: Any $\sigma$-finite measure $\nu$ can be uniquely decomposed as $\nu = \nu_{ac} + \nu_s$ where $\nu_{ac} \ll \mu$ and $\nu_s \perp \mu$.

#### 2.2 The Radon-Nikodym Theorem

**Theorem**: Let $\nu$ and $\mu$ be $\sigma$-finite measures on $(\Omega, \mathcal{F})$ with $\nu \ll \mu$. Then there exists a nonnegative measurable function $f$ (the **Radon-Nikodym derivative** $\frac{d\nu}{d\mu}$) such that:

$$\nu(A) = \int_A f \, d\mu \quad \text{for all } A \in \mathcal{F}$$

$f$ is unique $\mu$-a.e.

**Applications in Probability**:
- **Likelihood ratios**: If $P$ and $Q$ are probability measures with $Q \ll P$, then $L = \frac{dQ}{dP}$ satisfies $E_P[L] = 1$ and $E_Q[X] = E_P[XL]$.
- **Change of measure**: $E_Q[X] = E_P\left[X \frac{dQ}{dP}\right]$ — the foundation of importance sampling.
- **Density functions**: If $\mu_X \ll \lambda$ (Lebesgue measure), then $f_X = \frac{d\mu_X}{d\lambda}$ is the pdf.

---

### Unit 3: Martingale Theory

#### 3.1 Definitions

A sequence $(M_n, \mathcal{F}_n)_{n \geq 0}$ is a **martingale** if:

1. $\mathcal{F}_0 \subseteq \mathcal{F}_1 \subseteq \cdots$ is a **filtration**.
2. $M_n$ is $\mathcal{F}_n$-measurable and integrable for each $n$.
3. $E[M_{n+1} | \mathcal{F}_n] = M_n$ a.s.

If condition 3 is replaced by $\geq$ ($\leq$), $(M_n)$ is a **submartingale** (**supermartingale**).

**Key Examples**:
- **Random walk**: $S_n = X_1 + \cdots + X_n$ with $E[X_i] = 0$ is a martingale w.r.t. $\mathcal{F}_n = \sigma(X_1, \ldots, X_n)$.
- **Likelihood ratios**: $L_n = \prod_{i=1}^n \frac{q(X_i)}{p(X_i)}$ under $P$.
- **Doob martingale**: $M_n = E[X | \mathcal{F}_n]$ for any integrable $X$.

#### 3.2 The Upcrossing Inequality and Martingale Convergence

**Doob's Upcrossing Inequality**: Let $(M_n)$ be a submartingale and $U_n(a, b)$ the number of upcrossings of $[a, b]$ by $M_0, \ldots, M_n$. Then:

$$E[U_n(a, b)] \leq \frac{E[(M_n - a)^+]}{b - a}$$

**Theorem (Martingale Convergence Theorem)**: If $(M_n)$ is a submartingale with $\sup_n E[M_n^+] < \infty$, then $M_n \to M_\infty$ a.s. for some integrable $M_\infty$.

*Proof*: If $M_n$ does not converge, it must oscillate, creating infinitely many upcrossings of some interval $[a, b]$ with $a < b$. But the upcrossing inequality implies $E[U_\infty(a,b)] < \infty$ for all $a < b$, so $U_\infty(a,b) < \infty$ a.s. This is a contradiction. Hence $M_n$ converges a.s.

**Important Note**: Convergence a.s. does NOT imply convergence in $L^1$. The additional condition for $L^1$ convergence is **uniform integrability**.

#### 3.3 Uniform Integrability and $L^1$ Convergence

**Definition**: A collection $\{X_\alpha\}$ is **uniformly integrable** if:

$$\lim_{c \to \infty} \sup_\alpha E[|X_\alpha| \mathbf{1}_{|X_\alpha| > c}] = 0$$

**Theorem**: If $(M_n)$ is a martingale, the following are equivalent:
1. $(M_n)$ is uniformly integrable.
2. $M_n \to M_\infty$ in $L^1$.
3. $M_n = E[M_\infty | \mathcal{F}_n]$ for all $n$ (the martingale is "closed").

#### 3.4 Optional Stopping

**Theorem (Optional Stopping)**: Let $(M_n)$ be a uniformly integrable martingale and $\tau$ a stopping time. Then:

$$E[M_\tau] = E[M_0]$$

More generally, if $\sigma \leq \tau$ are bounded stopping times, then $E[M_\tau | \mathcal{F}_\sigma] = M_\sigma$.

**Theorem (Doob's Maximal Inequality)**: If $(M_n)$ is a nonnegative submartingale:

$$P\left(\max_{0 \leq k \leq n} M_k \geq \lambda\right) \leq \frac{E[M_n]}{\lambda}$$

---

### Unit 4: Brownian Motion (Introduction)

#### 4.1 Definition

A stochastic process $(B_t)_{t \geq 0}$ is a **standard Brownian motion** (Wiener process) if:

1. $B_0 = 0$.
2. **Independent increments**: $B_{t_1}, B_{t_2} - B_{t_1}, \ldots, B_{t_n} - B_{t_{n-1}}$ are independent for $t_1 < \cdots < t_n$.
3. **Gaussian increments**: $B_t - B_s \sim N(0, t - s)$ for $s < t$.
4. $t \mapsto B_t$ is continuous a.s.

#### 4.2 Key Properties

- **Martingale**: $(B_t)$ is a martingale w.r.t. its natural filtration.
- **Quadratic variation**: $[B]_t = t$ (the "clock" of Brownian motion).
- **Self-similarity**: $\{c^{-1/2}B_{ct}\}$ has the same distribution as $\{B_t\}$.
- **Nowhere differentiable**: $B_t$ is a.s. continuous but nowhere differentiable.
- **Recurrence**: In $\mathbb{R}^1$ and $\mathbb{R}^2$, Brownian motion is recurrent; in $\mathbb{R}^d$ ($d \geq 3$), it is transient.

#### 4.3 Donsker's Invariance Principle

Let $X_i$ be i.i.d. with $E[X_i] = 0$, $\text{Var}(X_i) = 1$, and $S_n = X_1 + \cdots + X_n$. Define:

$$W_n(t) = \frac{1}{\sqrt{n}} S_{\lfloor nt \rfloor} + (nt - \lfloor nt \rfloor) \frac{X_{\lfloor nt \rfloor + 1}}{\sqrt{n}}$$

Then $W_n \xrightarrow{d} B$ in $C[0,1]$ with the sup norm topology. This is the **functional CLT**.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Probability: Theory and Examples* (5th ed.) | Rick Durrett | **Primary** — Chapters 4–8 |
| *Probability with Martingales* | David Williams | **Supplementary** — Elegant martingale-focused treatment |
| *Brownian Motion and Stochastic Calculus* | Ioannis Karatzas & Steven Shreve | **Advanced** — For further study of Brownian motion |
| *Continuous Martingales and Brownian Motion* | Daniel Revuz & Marc Yor | **Reference** — Encyclopedia of Brownian motion |

---

## Problem Sets

### Problem Set 1: Conditional Expectation & Radon-Nikodym

1. **(Durrett 4.1)** Prove the tower property of conditional expectation.
2. **(Exam-style)** Let $X \sim N(\mu, \sigma^2)$ and $Y = X + Z$ where $Z \sim N(0, \tau^2)$ is independent of $X$. Compute $E[X|Y]$.
3. **(Exam-style)** Let $P$ and $Q$ be probability measures with $\frac{dQ}{dP} = L$. Show $E_Q[X] = E_P[XL]$ and compute the Radon-Nikodym derivative for two Gaussian measures with different means.
4. **(Proof)** Prove that conditional expectation is a contraction in $L^2$: $E[(E[X|\mathcal{G}])^2] \leq E[X^2]$.
5. **(Application)** In a Bayesian setting with prior $\theta \sim N(0,1)$ and data $X|\theta \sim N(\theta, 1)$, compute $E[\theta|X]$ and $\text{Var}(\theta|X)$.

### Problem Set 2: Martingales

1. **(Durrett 5.2)** Prove that if $(M_n)$ is a martingale with $M_0 = 0$ and $\sup_n E[M_n^2] < \infty$, then $M_n$ converges a.s. and in $L^2$.
2. **(Exam-style)** Let $X_n$ be a simple random walk ($P(X_i = 1) = P(X_i = -1) = 1/2$), $S_n = \sum X_i$. Show $S_n^2 - n$ is a martingale.
3. **(Exam-style)** State and prove Doob's upcrossing inequality.
4. **(Application — Gambler's Ruin)** A gambler starts with $\$k$ and at each step wins $\$1$ with probability $p$ or loses $\$1$ with probability $q = 1-p$. Use optional stopping to find the probability of reaching $\$N$ before $\$0$.
5. **(Challenge)** Construct a martingale that converges a.s. to 0 but not in $L^1$.

### Problem Set 3: Brownian Motion

1. **(Durrett 8.1)** Verify that the covariance function of standard Brownian motion is $\text{Cov}(B_s, B_t) = \min(s, t)$.
2. **(Exam-style)** Show that $B_t^2 - t$ is a martingale.
3. **(Proof)** Prove that $e^{\theta B_t - \theta^2 t / 2}$ is a martingale for any $\theta \in \mathbb{R}$.
4. **(Application)** Use the reflection principle to compute $P(\max_{0 \leq s \leq t} B_s \geq a)$ for $a > 0$.
5. **(Challenge)** Prove that Brownian motion paths are a.s. nowhere differentiable.
