---
layout: default
title: "EN.553.671 — Combinatorial Analysis"
parent: "Module E — Discrete Mathematics"
nav_order: 1
permalink: /module_e/combinatorial_analysis/
---

# EN.553.671 — Combinatorial Analysis

> *The art and science of counting. This course develops generating functions, recurrence relations, Pólya's theory of counting under group actions, and the Principle of Inclusion-Exclusion — tools used throughout probability, algorithm analysis, and discrete optimization.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Construct and manipulate generating functions** — both ordinary (OGF) and exponential (EGF) — to solve counting problems and extract asymptotic information.
2. **Solve linear recurrence relations** using generating function techniques and the transfer matrix method.
3. **Apply Pólya's Enumeration Theorem** to count distinct objects under symmetry group actions.
4. **Apply the Principle of Inclusion-Exclusion** and derive classical combinatorial identities.
5. **Use Ramsey-theoretic arguments** in extremal combinatorics.

---

## Core Theory

### Unit 1: Generating Functions

#### 1.1 Ordinary Generating Functions (OGFs)

**Definition**: The **ordinary generating function** of a sequence $(a_n)_{n \geq 0}$ is the formal power series:

$$A(x) = \sum_{n=0}^\infty a_n x^n.$$

**Key Operations**:

| Operation | Sequence | OGF |
|-----------|----------|-----|
| Scaling | $c \cdot a_n$ | $c \cdot A(x)$ |
| Addition | $a_n + b_n$ | $A(x) + B(x)$ |
| Right shift | $a_{n-1}$ (with $a_{-1} = 0$) | $x A(x)$ |
| Convolution | $\sum_{k=0}^n a_k b_{n-k}$ | $A(x) B(x)$ |
| Differentiation | $(n+1) a_{n+1}$ | $A'(x)$ |

**Example**: The number of ways to make change for $n$ cents using pennies (1¢), nickels (5¢), and dimes (10¢) has generating function:

$$C(x) = \frac{1}{(1-x)(1-x^5)(1-x^{10})}.$$

#### 1.2 Exponential Generating Functions (EGFs)

**Definition**: The **exponential generating function** of $(a_n)$ is:

$$\hat{A}(x) = \sum_{n=0}^\infty a_n \frac{x^n}{n!}.$$

**Key Property**: Products of EGFs correspond to the "labeled" composition of combinatorial structures. If $\hat{A}(x)$ counts labeled $\mathcal{A}$-structures and $\hat{B}(x)$ counts labeled $\mathcal{B}$-structures:

$$\hat{A}(x) \hat{B}(x) = \sum_{n=0}^\infty \left(\sum_{k=0}^n \binom{n}{k} a_k b_{n-k}\right) \frac{x^n}{n!}.$$

**Derangements**: The number of derangements $D_n$ (permutations of $[n]$ with no fixed point) satisfies $\hat{D}(x) = e^{-x}/(1-x)$, yielding the closed form:

$$D_n = n! \sum_{k=0}^n \frac{(-1)^k}{k!} \;\xrightarrow{n\to\infty}\; n!/e.$$

#### 1.3 Solving Recurrences with Generating Functions

**Example — Fibonacci Numbers**: $F_n = F_{n-1} + F_{n-2}$, with $F_0 = 0$, $F_1 = 1$.

Multiply by $x^n$ and sum over $n \geq 2$ to obtain $F(x) = xF(x) + x^2F(x) + x$, so:

$$F(x) = \frac{x}{1 - x - x^2} = \frac{x}{(1 - \varphi x)(1 - \hat{\varphi} x)},$$

where $\varphi = \frac{1+\sqrt{5}}{2}$ (the golden ratio) and $\hat{\varphi} = \frac{1-\sqrt{5}}{2}$ (its conjugate). Partial fractions yield the **Binet formula**:

$$F_n = \frac{\varphi^n - \hat{\varphi}^n}{\sqrt{5}}.$$

---

### Unit 2: Advanced Enumeration

#### 2.1 The Principle of Inclusion-Exclusion (PIE)

$$\left|\bigcup_{i=1}^n A_i\right| = \sum_{i} |A_i| - \sum_{i<j} |A_i \cap A_j| + \cdots + (-1)^{n+1} |A_1 \cap \cdots \cap A_n|.$$

**Applications**:
- **Euler's totient function**: $\varphi(n) = n \prod_{p \mid n} (1 - 1/p)$.
- **Surjections**: The number of surjections from $[n]$ to $[k]$ is $\sum_{j=0}^k (-1)^j \binom{k}{j}(k-j)^n$.
- **Chromatic polynomial**: Counts proper $k$-colorings of a graph via deletion-contraction.

#### 2.2 Catalan Numbers

The $n$-th Catalan number is $C_n = \frac{1}{n+1}\binom{2n}{n}$, which counts:
- Valid parenthesizations of $n+1$ factors
- Dyck paths from $(0,0)$ to $(2n,0)$ using unit up/down steps that never dip below the $x$-axis
- Full binary trees with $n$ internal nodes
- Triangulations of a convex $(n+2)$-gon

**Generating Function**: $C(x) = \frac{1 - \sqrt{1-4x}}{2x}$, satisfying the functional equation $C(x) = 1 + x C(x)^2$.

#### 2.3 Integer Partitions

The number of partitions $p(n)$ of $n$ (ways to write $n$ as an unordered sum of positive integers) has generating function:

$$\sum_{n=0}^\infty p(n) x^n = \prod_{k=1}^\infty \frac{1}{1-x^k}.$$

---

### Unit 3: Pólya's Theory of Counting

#### 3.1 Group Actions and Burnside's Lemma

**Burnside's Lemma (Cauchy-Frobenius)**: The number of distinct objects under the action of a group $G$ on a set $X$ is:

$$|X/G| = \frac{1}{|G|} \sum_{g \in G} |X^g|,$$

where $X^g = \{x \in X : g \cdot x = x\}$ is the **fixed-point set** of $g$.

**Example**: Count distinct necklaces with $n$ beads in $k$ colors. The symmetry group is $\mathbb{Z}_n$ (rotations). The rotation $r^j$ fixes exactly $k^{\gcd(n,j)}$ colorings, so the number of distinct necklaces is:

$$\frac{1}{n}\sum_{j=0}^{n-1} k^{\gcd(n,j)}.$$

#### 3.2 The Cycle Index

For a permutation group $G$ acting on $[n]$, the **cycle index** is the polynomial:

$$Z_G(x_1, x_2, \ldots, x_n) = \frac{1}{|G|} \sum_{g \in G} x_1^{c_1(g)} x_2^{c_2(g)} \cdots x_n^{c_n(g)},$$

where $c_k(g)$ denotes the number of $k$-cycles in the disjoint cycle decomposition of $g$.

#### 3.3 Pólya's Enumeration Theorem

**Theorem**: The number of distinct ways to color $n$ objects with $k$ colors under the action of group $G$ is:

$$Z_G(\underbrace{k, k, \ldots, k}_{n}).$$

More generally, if colors have formal weights $f_1, \ldots, f_k$, the **pattern inventory** (weighted count) is:

$$Z_G\!\left(\sum_i f_i,\; \sum_i f_i^2,\; \ldots,\; \sum_i f_i^n\right).$$

**Example**: The number of distinct colorings of the faces of a cube with $k$ colors is obtained by computing $Z_G(k,k,\ldots,k)$ where $G$ is the rotation group of the cube (24 elements).

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Introductory Combinatorics* (5th ed.) | Richard A. Brualdi | **Primary** — Comprehensive undergraduate-to-graduate coverage |
| *Enumerative Combinatorics* Vol. I &amp; II | Richard P. Stanley | **Advanced** — The definitive graduate-level reference |
| *Generatingfunctionology* (3rd ed.) | Herbert S. Wilf | **Supplementary** — GF-focused; freely available online |
| *Analytic Combinatorics* | Philippe Flajolet &amp; Robert Sedgewick | **Advanced** — Asymptotic enumeration via singularity analysis |

---

## Problem Sets

### Problem Set 1: Generating Functions

1. **(Brualdi 7.2)** Find the OGF for the number of ways to distribute $n$ identical balls into 4 distinct boxes with at most 5 balls per box.
2. **(Exam-style)** Use generating functions to solve $a_n = 3a_{n-1} - 2a_{n-2}$ with $a_0 = 1$, $a_1 = 3$.
3. **(Exam-style)** Derive the EGF for the Bell numbers $B_n$ (the number of set partitions of $[n]$).
4. **(Proof)** Prove the Binet formula $F_n = (\varphi^n - \hat{\varphi}^n)/\sqrt{5}$ using partial fraction decomposition of $F(x)$.
5. **(Challenge)** Use generating functions to prove the Vandermonde identity: $\sum_{k=0}^n \binom{n}{k}^2 = \binom{2n}{n}$.

### Problem Set 2: Inclusion-Exclusion and Catalan Numbers

1. **(Brualdi 6.1)** Use PIE to derive the formula for $D_n$ and verify that $D_n/n! \to 1/e$ as $n \to \infty$.
2. **(Exam-style)** Compute the number of surjections from a 5-element set onto a 3-element set.
3. **(Exam-style)** Derive the recurrence $C_n = \sum_{k=0}^{n-1} C_k C_{n-1-k}$ for Catalan numbers and use it to find the generating function $C(x)$.
4. **(Proof)** Give a bijective proof that Catalan numbers simultaneously count Dyck paths and full binary trees.
5. **(Challenge)** Prove $C_n = \frac{1}{n+1}\binom{2n}{n}$ using the cycle lemma or reflection principle.

### Problem Set 3: Pólya Counting

1. **(Brualdi 14.3)** Use Burnside's lemma to count the number of distinct necklaces with 6 beads in 3 colors.
2. **(Exam-style)** Compute the cycle index of $\mathbb{Z}_4$ acting on 4 positions and use PET to count distinct binary colorings.
3. **(Exam-style)** How many distinct ways can the faces of a regular tetrahedron be colored with $k$ colors?
4. **(Proof)** Prove Burnside's Lemma using the orbit-stabilizer theorem.
5. **(Challenge)** Use Pólya's theorem to enumerate the number of non-isomorphic simple graphs on 4 labeled vertices.

---

## Study Guide &amp; Exam Preparation

> [!IMPORTANT]
> **Key Theorems for Combinatorial Analysis**
>
> - **OGF Convolution Rule** — $[A(x)B(x)]$ corresponds to the convolution $\sum_k a_k b_{n-k}$; fundamental to all GF manipulations
> - **EGF Product Rule** — products of EGFs correspond to labeled compositions (binomial coefficient appears)
> - **Binet Formula** — derived via partial fractions of $F(x) = x/(1-x-x^2)$; uses $\varphi = (1+\sqrt5)/2$ and $\hat\varphi = (1-\sqrt5)/2$
> - **Principle of Inclusion-Exclusion** — alternating sum formula; know the surjection and derangement applications
> - **Burnside's Lemma** — average number of fixed points over the group; the foundation of Pólya's theorem
> - **Pólya's Enumeration Theorem** — cycle index evaluated at $(k,k,\ldots,k)$ for uniform coloring counts

**Exam Preparation Tips**:
- OGF and EGF problems typically reduce to: write a functional equation, solve for the GF, extract coefficients via partial fractions or known series.
- For PIE problems: carefully define the events $A_i$ (usually "$\sigma$ maps element $i$ to itself") and compute $|A_I|$ for each intersection.
- For Burnside/Pólya: list all group elements, compute their cycle types, and apply the formula directly.
