---
layout: default
title: "0.2 — Analysis on the Real Line"
parent: "Module 0 — Foundations"
nav_order: 2
permalink: /module_0/undergraduate_analysis/
---

# 0.2 — Analysis on the Real Line

> *Calculus explains how to compute limits, derivatives, and integrals. Analysis explains why they exist. Everything here rests on one axiom, the completeness of $\mathbb{R}$, and a single technique: controlling errors with $\varepsilon$.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Use the completeness axiom** (least upper bounds) to prove existence results.
2. **Prove limits** of sequences and series from the $\varepsilon$–$N$ definition, and use the standard convergence tests correctly.
3. **Prove the core theorems on continuous functions**: Extreme Value, Intermediate Value, and uniform continuity on $[a,b]$.
4. **Use the Mean Value Theorem and Taylor's theorem with remainder** to bound errors.
5. **Define the Riemann integral** and prove the Fundamental Theorem of Calculus.

---

## Core Theory

### Unit 1: The Real Numbers and Sequences

#### 1.1 Completeness

**Axiom of Completeness**: Every nonempty subset of $\mathbb{R}$ that is bounded above has a **least upper bound** (supremum).

**Intuition**: $\mathbb{Q}$ has "holes". The set $\{q \in \mathbb{Q} : q^2 < 2\}$ is bounded above in $\mathbb{Q}$ but has no least upper bound there, because $\sqrt{2}$ is missing. Completeness says $\mathbb{R}$ has no holes. Every existence theorem in this course (limits of monotone sequences, the Intermediate Value Theorem, maxima of continuous functions) is ultimately this axiom at work.

**Useful characterization**: $s = \sup A$ iff $s$ is an upper bound and for every $\varepsilon > 0$ there is $a \in A$ with $a > s - \varepsilon$.

**Archimedean Property**: For every $x \in \mathbb{R}$ there is $n \in \mathbb{N}$ with $n > x$; hence $1/n \to 0$, and $\mathbb{Q}$ is dense in $\mathbb{R}$.

#### 1.2 Limits of Sequences

$a_n \to L$ means: $\forall \varepsilon > 0\; \exists N\; \forall n \geq N: |a_n - L| < \varepsilon$.

**Intuition**: $\varepsilon$ is a tolerance someone else gets to choose. Convergence means that no matter how strict the tolerance, the sequence eventually stays inside it for good.

**Standard technique**: work backward from $|a_n - L| < \varepsilon$ to find how large $n$ must be, then write the proof forward. *Example*: for $a_n = \frac{2n+1}{n+3} \to 2$, $|a_n - 2| = \frac{5}{n+3} < \frac{5}{n}$, so $N > 5/\varepsilon$ works.

#### 1.3 The Big Three Existence Theorems

| Theorem | Statement | Intuition |
|---------|-----------|-----------|
| **Monotone Convergence** | A bounded monotone sequence converges. | Increasing and bounded, so it must pile up at its supremum. |
| **Bolzano–Weierstrass** | Every bounded sequence has a convergent subsequence. | Halve the interval repeatedly, always keeping a half that contains infinitely many terms. |
| **Cauchy Criterion** | A sequence converges iff it is Cauchy: $\forall\varepsilon\, \exists N\, \forall m,n \geq N: \lvert a_m - a_n \rvert < \varepsilon$. | You can certify convergence without knowing the limit. |

**limsup and liminf**: $\limsup a_n = \lim_{n\to\infty} \sup_{k \geq n} a_k$. A bounded sequence converges iff $\limsup = \liminf$.

---

### Unit 2: Series

$\sum a_n$ converges if its partial sums $s_N = \sum_{n=1}^N a_n$ converge.

- **Divergence test**: if $\sum a_n$ converges, then $a_n \to 0$. The converse fails: $\sum 1/n = \infty$.
- **Comparison**: if $0 \leq a_n \leq b_n$ and $\sum b_n < \infty$, then $\sum a_n < \infty$.
- **Ratio / root tests**: if $\limsup |a_{n+1}/a_n| < 1$ (or $\limsup |a_n|^{1/n} < 1$), the series converges absolutely.
- **$p$-series**: $\sum 1/n^p$ converges iff $p > 1$ (by comparison with $\int_1^\infty x^{-p}\,dx$).
- **Alternating series**: if $a_n \downarrow 0$, then $\sum (-1)^n a_n$ converges.

**Absolute vs. conditional convergence**: absolute convergence ($\sum |a_n| < \infty$) implies convergence, and the sum is unchanged by any rearrangement. **Riemann's Rearrangement Theorem**: a conditionally convergent series can be rearranged to sum to *any* real number. **Lesson**: infinite sums are only "order-independent" when they converge absolutely. This is why expectations in probability require $E|X| < \infty$.

---

### Unit 3: Continuity

$f$ is **continuous at $c$** if $\forall \varepsilon > 0\, \exists \delta > 0: |x - c| < \delta \Rightarrow |f(x) - f(c)| < \varepsilon$.

**Sequential criterion**: $f$ is continuous at $c$ iff $x_n \to c$ implies $f(x_n) \to f(c)$. This is often the easiest way to prove *dis*continuity.

**Theorems on $[a,b]$** (each fails on $(a,b)$; find the counterexamples):
1. **Extreme Value Theorem**: a continuous $f$ on $[a,b]$ attains a max and a min. *(Bolzano–Weierstrass + continuity)*
2. **Intermediate Value Theorem**: $f$ takes every value between $f(a)$ and $f(b)$. *(Completeness: take $\sup\{x : f(x) < y\}$)*
3. **Uniform continuity**: a continuous $f$ on $[a,b]$ is **uniformly continuous**: one $\delta$ works for every $c$ simultaneously.

**Intuition for uniform continuity**: $f(x) = 1/x$ on $(0,1)$ is continuous, but near $0$ it is so steep that the required $\delta$ shrinks to $0$. Closed, bounded intervals rule this behavior out.

---

### Unit 4: Differentiation

$f'(c) = \lim_{h \to 0} \frac{f(c+h) - f(c)}{h}$. Differentiable implies continuous, but not conversely: $|x|$ is continuous at $0$ but not differentiable there.

**Mean Value Theorem**: If $f$ is continuous on $[a,b]$ and differentiable on $(a,b)$, then $f'(\xi) = \frac{f(b) - f(a)}{b - a}$ for some $\xi \in (a,b)$.

**Intuition**: on any trip, at some instant your speedometer showed your average speed. **Uses**: $f' = 0 \Rightarrow f$ constant; $f' > 0 \Rightarrow f$ increasing; $|f'| \leq M \Rightarrow |f(x) - f(y)| \leq M|x - y|$ (Lipschitz).

**Taylor's Theorem (Lagrange remainder)**: If $f$ is $n+1$ times differentiable, then

$$f(x) = \sum_{k=0}^{n} \frac{f^{(k)}(a)}{k!}(x-a)^k + \frac{f^{(n+1)}(\xi)}{(n+1)!}(x-a)^{n+1} \quad \text{for some } \xi \text{ between } a \text{ and } x.$$

**Why this matters later**: every asymptotic argument in statistics (the delta method, MLE asymptotics) and every convergence proof in optimization (Newton's method) is a Taylor expansion with a controlled remainder.

---

### Unit 5: The Riemann Integral

For a partition $P$ of $[a,b]$, the upper and lower sums $U(f,P)$ and $L(f,P)$ use the sup and inf of $f$ on each subinterval. $f$ is **Riemann integrable** if $\inf_P U(f,P) = \sup_P L(f,P)$.

**Criterion**: $f$ is integrable iff for every $\varepsilon > 0$ there is a partition with $U(f,P) - L(f,P) < \varepsilon$.

**Theorems**: continuous functions on $[a,b]$ are integrable (via uniform continuity), and so are monotone functions. The Dirichlet function $\mathbf{1}_{\mathbb{Q}}$ is **not** Riemann integrable, because every upper sum is $1$ and every lower sum is $0$. Fixing this defect is one motivation for the Lebesgue integral in Module B.

**Fundamental Theorem of Calculus**:
1. If $f$ is integrable on $[a,b]$ and $F' = f$, then $\int_a^b f = F(b) - F(a)$.
2. If $f$ is continuous, then $G(x) = \int_a^x f(t)\,dt$ is differentiable with $G' = f$.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Understanding Analysis* (2nd ed.) | Stephen Abbott | **Primary** — The clearest first course; motivates every definition |
| *Elementary Analysis* (2nd ed.) | Kenneth A. Ross | **Alternative** — Gentler pace, many worked examples |
| *Analysis I* | Terence Tao | **Alternative** — Builds $\mathbb{R}$ from scratch; maximally careful |
| *Principles of Mathematical Analysis*, Ch. 1–6 | Walter Rudin | **Bridge** — Terse; read after Abbott as preparation for Module A |

---

## Problem Sets

### Problem Set 1: Completeness and Sequences

1. **(Core)** Let $A = \{1 - 1/n : n \in \mathbb{N}\}$. Prove $\sup A = 1$ using the $\varepsilon$-characterization of the supremum.
2. **(Core)** Prove from the definition that $\frac{3n^2 + 1}{n^2 - 5} \to 3$.
3. **(Core)** Prove that a convergent sequence is bounded, and that limits are unique.
4. **(Proof)** Prove the Monotone Convergence Theorem using the Axiom of Completeness.
5. **(Challenge)** Define $a_1 = 1$, $a_{n+1} = \sqrt{2 + a_n}$. Prove that $(a_n)$ converges and find its limit.

### Problem Set 2: Series and Continuity

1. **(Core)** Determine convergence or divergence: (a) $\sum \frac{n}{2^n}$; (b) $\sum \frac{1}{n \log n}$ (for $n \geq 2$); (c) $\sum \frac{(-1)^n}{\sqrt{n}}$, and whether it converges absolutely.
2. **(Core)** Prove from the definition that $f(x) = x^2$ is continuous at every $c$, and that it is **not** uniformly continuous on $\mathbb{R}$.
3. **(Proof)** Prove the Intermediate Value Theorem.
4. **(Proof)** Prove that a continuous function on $[a,b]$ is uniformly continuous. *(Hint: argue by contradiction with Bolzano–Weierstrass.)*
5. **(Challenge)** Prove that $f(x) = x \sin(1/x)$ (with $f(0) = 0$) is continuous on $\mathbb{R}$ but not differentiable at $0$, while $g(x) = x^2 \sin(1/x)$ (with $g(0)=0$) is differentiable everywhere, yet $g'$ is not continuous at $0$.

### Problem Set 3: Differentiation and Integration

1. **(Core)** Use the Mean Value Theorem to prove $|\sin x - \sin y| \leq |x - y|$ for all $x, y$.
2. **(Core)** Use Taylor's theorem to show $\left|e^x - (1 + x + x^2/2)\right| \leq \frac{e}{6}|x|^3$ for $|x| \leq 1$.
3. **(Proof)** Prove that every continuous function on $[a,b]$ is Riemann integrable.
4. **(Core)** Prove that the Dirichlet function $\mathbf{1}_{\mathbb{Q}}$ is not Riemann integrable on $[0,1]$.
5. **(Challenge)** Prove both parts of the Fundamental Theorem of Calculus.

---

## Study Guide

{: .important }
> **Theorems to know at the full-proof level**
>
> - Monotone Convergence and Bolzano–Weierstrass, both from completeness
> - Extreme Value and Intermediate Value Theorems
> - Continuous on $[a,b]$ $\Rightarrow$ uniformly continuous
> - Mean Value Theorem (via Rolle) and Taylor with remainder
> - Continuous $\Rightarrow$ Riemann integrable; the Fundamental Theorem of Calculus

**Common mistakes**:
- Choosing $N$ or $\delta$ that depends on the wrong variable (for uniform continuity, $\delta$ may not depend on the point).
- Assuming a limit exists before proving it. Write "if the limit exists, it must equal $L$" and then prove existence separately.
- Dividing by something that could be zero, or using $f'$ where only continuity is assumed.

**Ready for Module A when** you can prove Problem Set 2 #4 and Problem Set 3 #3 from scratch without notes.
