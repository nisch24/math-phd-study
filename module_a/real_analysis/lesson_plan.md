---
layout: default
title: "EN.553.701 — Real Analysis"
parent: "Module A — Analysis & Linear Algebra"
nav_order: 1
permalink: /module_a/real_analysis/
---

# EN.553.701 — Real Analysis

> *The rigorous foundation for all of modern mathematics. This course develops the theory of analysis in metric spaces, the convergence of sequences and series of functions, and the powerful machinery of the Inverse and Implicit Function Theorems.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Define and work with metric spaces**: open/closed sets, compactness, connectedness, completeness.
2. **Prove convergence results** for sequences and series of functions, distinguishing pointwise from uniform convergence.
3. **Apply the Contraction Mapping Principle** to existence and uniqueness problems.
4. **State and prove the Inverse and Implicit Function Theorems** in $\mathbb{R}^n$.
5. **Construct rigorous proofs** using $\varepsilon$-$\delta$ arguments, subsequences, and covering arguments.

---

## Core Theory

### Unit 1: Topology of Metric Spaces

#### 1.1 Metric Spaces — Definitions and Examples

A **metric space** is a pair $(X, d)$ where $X$ is a set and $d: X \times X \to [0, \infty)$ satisfies:

1. **Positivity**: $d(x, y) \geq 0$ with equality iff $x = y$.
2. **Symmetry**: $d(x, y) = d(y, x)$.
3. **Triangle inequality**: $d(x, z) \leq d(x, y) + d(y, z)$.

**Key Examples**:
- $(\mathbb{R}^n, \|\cdot\|_2)$: Euclidean space with the standard norm.
- $(C[a,b], \|\cdot\|_\infty)$: Continuous functions on $[a,b]$ with the supremum norm $\|f\|_\infty = \sup_{x \in [a,b]} |f(x)|$.
- $(\ell^p, \|\cdot\|_p)$: Sequence spaces with $\|x\|_p = \left(\sum_{n=1}^\infty |x_n|^p\right)^{1/p}$.

#### 1.2 Open and Closed Sets

Let $(X, d)$ be a metric space.

- The **open ball** of radius $r > 0$ centered at $x$: $B(x, r) = \{y \in X : d(x, y) < r\}$.
- A set $U \subseteq X$ is **open** if for every $x \in U$, there exists $r > 0$ such that $B(x, r) \subseteq U$.
- A set $F \subseteq X$ is **closed** if $X \setminus F$ is open, equivalently if $F$ contains all its limit points.

**Theorem** (Properties of open sets):
1. $\emptyset$ and $X$ are open.
2. Arbitrary unions of open sets are open.
3. Finite intersections of open sets are open.

#### 1.3 Compactness

**Definition**: A subset $K$ of a metric space is **compact** if every open cover of $K$ has a finite subcover.

**Theorem (Heine-Borel)**: A subset of $\mathbb{R}^n$ is compact if and only if it is closed and bounded.

**Theorem (Sequential Compactness)**: In a metric space, $K$ is compact if and only if every sequence in $K$ has a subsequence converging to a point in $K$.

**Theorem (Bolzano-Weierstrass)**: Every bounded sequence in $\mathbb{R}^n$ has a convergent subsequence.

#### 1.4 Completeness

**Definition**: A metric space $(X, d)$ is **complete** if every Cauchy sequence converges. A sequence $(x_n)$ is **Cauchy** if for every $\varepsilon > 0$, there exists $N$ such that $d(x_m, x_n) < \varepsilon$ for all $m, n \geq N$.

**Key Result**: $\mathbb{R}^n$ is complete. $C[a,b]$ with the sup norm is complete. The rationals $\mathbb{Q}$ are not complete.

**Theorem (Baire Category Theorem)**: A complete metric space cannot be written as a countable union of nowhere dense sets.

#### 1.5 Connectedness

**Definition**: A metric space $X$ is **connected** if it cannot be partitioned into two nonempty open sets. Equivalently, the only subsets that are both open and closed are $\emptyset$ and $X$.

**Theorem**: The continuous image of a connected set is connected. An interval $[a,b] \subseteq \mathbb{R}$ is connected.

---

### Unit 2: Sequences and Series of Functions

#### 2.1 Pointwise vs. Uniform Convergence

Let $f_n : D \to \mathbb{R}$ be a sequence of functions.

- **Pointwise convergence**: $f_n \to f$ pointwise if for each $x \in D$, $\lim_{n \to \infty} f_n(x) = f(x)$.
- **Uniform convergence**: $f_n \to f$ uniformly if

$$\lim_{n \to \infty} \sup_{x \in D} |f_n(x) - f(x)| = 0$$

Equivalently, for every $\varepsilon > 0$, there exists $N$ (independent of $x$) such that $|f_n(x) - f(x)| < \varepsilon$ for all $n \geq N$ and all $x \in D$.

**Critical Distinction**: Pointwise convergence allows $N$ to depend on $x$; uniform convergence requires a single $N$ that works for all $x$ simultaneously.

#### 2.2 Consequences of Uniform Convergence

**Theorem (Uniform Limit of Continuous Functions)**: If $f_n \to f$ uniformly on $D$ and each $f_n$ is continuous, then $f$ is continuous.

*Proof Sketch*: Fix $x_0 \in D$ and $\varepsilon > 0$. Choose $N$ such that $\|f_n - f\|_\infty < \varepsilon/3$. Since $f_N$ is continuous, choose $\delta > 0$ such that $|f_N(x) - f_N(x_0)| < \varepsilon/3$ when $|x - x_0| < \delta$. Then:

$$|f(x) - f(x_0)| \leq |f(x) - f_N(x)| + |f_N(x) - f_N(x_0)| + |f_N(x_0) - f(x_0)| < \varepsilon$$

**Theorem (Term-by-term Integration)**: If $f_n \to f$ uniformly on $[a,b]$, then:

$$\lim_{n \to \infty} \int_a^b f_n(x)\,dx = \int_a^b f(x)\,dx$$

**Theorem (Weierstrass M-test)**: If $|g_n(x)| \leq M_n$ for all $x \in D$ and $\sum M_n < \infty$, then $\sum g_n$ converges uniformly and absolutely on $D$.

#### 2.3 Equicontinuity and Arzelà-Ascoli

**Definition**: A family $\mathcal{F} \subseteq C[a,b]$ is **equicontinuous** if for every $\varepsilon > 0$, there exists $\delta > 0$ such that $|f(x) - f(y)| < \varepsilon$ for all $f \in \mathcal{F}$ whenever $|x - y| < \delta$.

**Theorem (Arzelà-Ascoli)**: A subset $\mathcal{F} \subseteq C[a,b]$ is relatively compact (every sequence has a uniformly convergent subsequence) if and only if $\mathcal{F}$ is uniformly bounded and equicontinuous.

---

### Unit 3: Differentiation in $\mathbb{R}^n$

#### 3.1 The Total Derivative

**Definition**: A function $f: \mathbb{R}^n \to \mathbb{R}^m$ is **differentiable** at $x_0$ if there exists a linear map $Df(x_0): \mathbb{R}^n \to \mathbb{R}^m$ such that:

$$\lim_{h \to 0} \frac{\|f(x_0 + h) - f(x_0) - Df(x_0)h\|}{\|h\|} = 0$$

The matrix representation of $Df(x_0)$ is the **Jacobian matrix** $J_f(x_0)$ with entries $\frac{\partial f_i}{\partial x_j}(x_0)$.

#### 3.2 The Contraction Mapping Principle

**Theorem (Banach Fixed-Point Theorem)**: Let $(X, d)$ be a complete metric space and $T: X \to X$ a contraction, i.e., there exists $0 \leq c < 1$ such that $d(T(x), T(y)) \leq c \cdot d(x, y)$ for all $x, y \in X$. Then $T$ has a unique fixed point $x^* \in X$, and for any $x_0 \in X$, the iterates $x_{n+1} = T(x_n)$ converge to $x^*$.

*Proof*: The sequence $(x_n)$ is Cauchy since $d(x_{n+1}, x_n) \leq c^n d(x_1, x_0)$. By completeness, $x_n \to x^*$. Continuity of $T$ gives $T(x^*) = x^*$. Uniqueness follows from the contraction condition.

#### 3.3 The Inverse Function Theorem

**Theorem**: Let $f: \mathbb{R}^n \to \mathbb{R}^n$ be $C^1$ in a neighborhood of $a$, and suppose $Df(a)$ is invertible. Then there exist open sets $U \ni a$ and $V \ni f(a)$ such that $f: U \to V$ is a bijection with $C^1$ inverse $f^{-1}: V \to U$, and:

$$D(f^{-1})(y) = [Df(f^{-1}(y))]^{-1}$$

*Proof Strategy*:
1. Reduce to the case $a = 0$, $f(0) = 0$, $Df(0) = I$ by composing with $[Df(a)]^{-1}$.
2. Define $g(x) = x - f(x)$, so $Dg(0) = 0$. By continuity of $Dg$, $g$ is a contraction on a small ball.
3. For each $y$ near $0$, show $x \mapsto y + g(x) = y + x - f(x)$ is a contraction, so the Banach Fixed-Point Theorem yields a unique $x$ with $f(x) = y$.
4. Verify $C^1$ smoothness of the inverse using the chain rule.

#### 3.4 The Implicit Function Theorem

**Theorem**: Let $F: \mathbb{R}^n \times \mathbb{R}^m \to \mathbb{R}^m$ be $C^1$ near $(a, b)$ with $F(a, b) = 0$. If the partial derivative $D_y F(a, b)$ (the $m \times m$ matrix of partials with respect to $y$) is invertible, then there exist neighborhoods $U \ni a$ and $W \ni b$ and a $C^1$ function $g: U \to W$ such that:

$$F(x, g(x)) = 0 \quad \text{for all } x \in U$$

Moreover, $Dg(a) = -[D_y F(a,b)]^{-1} D_x F(a,b)$.

*Proof*: Apply the Inverse Function Theorem to the map $(x, y) \mapsto (x, F(x, y))$.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Principles of Mathematical Analysis* (3rd ed.) | Walter Rudin | **Primary** — Chapters 1–9 cover the core material |
| *Real Analysis: Modern Techniques and Their Applications* (2nd ed.) | Gerald B. Folland | **Supplementary** — Deeper measure theory, functional analysis connections |
| *Analysis I & II* | Terence Tao | **Alternative** — Detailed, proof-focused exposition |
| *Real and Complex Analysis* (3rd ed.) | Walter Rudin | **Advanced** — For students continuing to measure theory |

---

## Problem Sets

### Problem Set 1: Metric Space Topology

1. **(Rudin Ch. 2, #6)** Prove that every compact subset of a metric space is closed and bounded.
2. **(Rudin Ch. 2, #9)** Let $E$ be a connected subset of a metric space. Prove that $\overline{E}$ is connected.
3. **(Rudin Ch. 2, #22)** Prove that $\mathbb{R}^n$ is separable (has a countable dense subset).
4. **(Exam-style)** Let $(X, d)$ be a compact metric space and $f: X \to X$ be an isometry. Prove that $f$ is surjective.
5. **(Exam-style)** Prove or disprove: If $f: (0,1) \to \mathbb{R}$ is uniformly continuous, then $f$ extends to a continuous function on $[0,1]$.

### Problem Set 2: Sequences & Series of Functions

1. **(Rudin Ch. 7, #1)** Show that the sequence $f_n(x) = \frac{x}{1 + nx^2}$ converges uniformly on $\mathbb{R}$.
2. **(Rudin Ch. 7, #6)** Prove that if $f_n \to f$ uniformly on $[a,b]$ and each $f_n$ is Riemann integrable, then $f$ is Riemann integrable.
3. **(Exam-style)** Let $f_n(x) = x^n$ on $[0,1]$. Show that $f_n \to f$ pointwise but not uniformly, where $f(x) = 0$ for $x \in [0,1)$ and $f(1) = 1$.
4. **(Exam-style)** Use the Weierstrass M-test to show that $\sum_{n=0}^\infty \frac{x^n}{n!}$ converges uniformly on $[-R, R]$ for every $R > 0$.
5. **(Arzelà-Ascoli Application)** Let $f_n: [0,1] \to \mathbb{R}$ satisfy $|f_n(x)| \leq 1$ and $|f_n(x) - f_n(y)| \leq |x - y|$ for all $n, x, y$. Prove that $(f_n)$ has a uniformly convergent subsequence.

### Problem Set 3: Inverse and Implicit Function Theorems

1. **(Rudin Ch. 9, #17)** State and prove the Inverse Function Theorem.
2. **(Exam-style)** Let $F(x, y) = x^2 + y^2 - 1$. Use the Implicit Function Theorem to show that near $(1, 0)$, the unit circle can be written as $y = g(x)$ for a differentiable function $g$. Compute $g'(1)$.
3. **(Exam-style)** Let $f: \mathbb{R}^2 \to \mathbb{R}^2$ be defined by $f(x,y) = (e^x \cos y, e^x \sin y)$. Show that $f$ is locally invertible near every point. Find the derivative of the local inverse near $(1, 0)$.
4. **(Proof)** Use the Contraction Mapping Principle to prove that the equation $x = \frac{1}{3}\cos(x)$ has a unique solution in $\mathbb{R}$.
5. **(Challenge)** Prove that if $f: \mathbb{R}^n \to \mathbb{R}^n$ is $C^1$ and $Df(x)$ is invertible for all $x$, $f$ need not be globally injective. Construct a counterexample for $n = 2$.

---

## Study Guide & Exam Preparation

**For the Introductory Exam (Analysis portion)**:
- Master $\varepsilon$-$\delta$ proofs and sequential characterizations of continuity and compactness.
- Be prepared to prove that uniform limits of continuous functions are continuous (the standard "triple $\varepsilon$" argument).
- Know the Inverse Function Theorem statement cold; be able to state the key role of the Contraction Mapping Principle in its proof.
- Practice writing complete, rigorous proofs within time constraints (aim for 30–45 minutes per problem).
