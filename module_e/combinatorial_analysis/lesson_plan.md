---
layout: default
title: "EN.553.671 — Combinatorial Analysis"
parent: "Module E — Discrete Mathematics"
nav_order: 1
---

# EN.553.671 — Combinatorial Analysis

> *The art and science of counting. This course develops generating functions, recurrence relations, Pólya's theory of counting under group actions, and advanced principles of enumeration — tools used throughout probability, algorithms, and discrete optimization.*

---

## Learning Objectives

1. **Construct and manipulate generating functions** (ordinary and exponential) to solve counting problems.
2. **Solve recurrence relations** using generating function techniques and the transfer matrix method.
3. **Apply Pólya's Enumeration Theorem** to count distinct objects under symmetry.
4. **Use the Principle of Inclusion-Exclusion** and derive combinatorial identities.
5. **Apply Ramsey-theoretic arguments** in extremal combinatorics.

---

## Core Theory

### Unit 1: Generating Functions

#### 1.1 Ordinary Generating Functions (OGFs)

**Definition**: The OGF of a sequence $(a_n)_{n \geq 0}$ is:

$$A(x) = \sum_{n=0}^\infty a_n x^n$$

**Key operations**:

| Operation | Sequence | OGF |
|-----------|----------|-----|
| Scaling | $c \cdot a_n$ | $c \cdot A(x)$ |
| Addition | $a_n + b_n$ | $A(x) + B(x)$ |
| Right shift | $a_{n-1}$ (with $a_{-1} = 0$) | $x A(x)$ |
| Convolution | $\sum_{k=0}^n a_k b_{n-k}$ | $A(x) B(x)$ |
| Differentiation | $(n+1) a_{n+1}$ | $A'(x)$ |

**Example**: The number of ways to make change for $n$ cents using pennies, nickels, and dimes:

$$C(x) = \frac{1}{(1-x)(1-x^5)(1-x^{10})}$$

#### 1.2 Exponential Generating Functions (EGFs)

**Definition**: The EGF of $(a_n)$ is:

$$\hat{A}(x) = \sum_{n=0}^\infty a_n \frac{x^n}{n!}$$

**Key property**: Product of EGFs corresponds to labeled structures. If $\hat{A}(x)$ counts labeled $\mathcal{A}$-structures and $\hat{B}(x)$ counts labeled $\mathcal{B}$-structures:

$$\hat{A}(x) \hat{B}(x) = \sum_{n=0}^\infty \left(\sum_{k=0}^n \binom{n}{k} a_k b_{n-k}\right) \frac{x^n}{n!}$$

**Example**: The EGF for the number of permutations of $[n]$ is $\frac{1}{1-x}$ since $a_n = n!$, so $\hat{A}(x) = \sum x^n / 1 = 1/(1-x)$.

**Derangements**: The number of derangements $D_n$ satisfies $\hat{D}(x) = \frac{e^{-x}}{1-x}$, giving:

$$D_n = n! \sum_{k=0}^n \frac{(-1)^k}{k!}$$

#### 1.3 Solving Recurrences with GFs

**Example — Fibonacci numbers**: $F_n = F_{n-1} + F_{n-2}$, $F_0 = 0, F_1 = 1$.

Multiply by $x^n$ and sum: $F(x) = xF(x) + x^2F(x) + x$, so:

$$F(x) = \frac{x}{1 - x - x^2} = \frac{x}{(1 - \phi x)(1 - \hat{\phi}x)}$$

Partial fractions yield the **Binet formula**: $F_n = \frac{\phi^n - \hat{\phi}^n}{\sqrt{5}}$ where $\phi = \frac{1+\sqrt{5}}{2}$.

---

### Unit 2: Advanced Enumeration

#### 2.1 The Principle of Inclusion-Exclusion (PIE)

$$\left|\bigcup_{i=1}^n A_i\right| = \sum_{i} |A_i| - \sum_{i<j} |A_i \cap A_j| + \cdots + (-1)^{n+1} |A_1 \cap \cdots \cap A_n|$$

**Applications**:
- **Euler's totient**: $\varphi(n) = n \prod_{p | n} (1 - 1/p)$.
- **Surjections**: The number of surjections from $[n]$ to $[k]$ is $\sum_{j=0}^k (-1)^j \binom{k}{j}(k-j)^n$.
- **Chromatic polynomial**: Counts proper colorings of a graph.

#### 2.2 Catalan Numbers

The $n$-th Catalan number $C_n = \frac{1}{n+1}\binom{2n}{n}$ counts:
- Valid parenthesizations of $n+1$ factors
- Paths from $(0,0)$ to $(2n,0)$ using up/down steps that never go below the $x$-axis
- Binary trees with $n$ internal nodes

**OGF**: $C(x) = \frac{1 - \sqrt{1-4x}}{2x}$ satisfying $C(x) = 1 + xC(x)^2$.

#### 2.3 Partition Function

The number of partitions $p(n)$ of an integer $n$ has generating function:

$$\sum_{n=0}^\infty p(n) x^n = \prod_{k=1}^\infty \frac{1}{1-x^k}$$

---

### Unit 3: Pólya's Theory of Counting

#### 3.1 Group Actions and Burnside's Lemma

**Burnside's Lemma (Cauchy-Frobenius)**: The number of distinct objects under group $G$ acting on a set $X$ is:

$$|X/G| = \frac{1}{|G|} \sum_{g \in G} |X^g|$$

where $X^g = \{x \in X : g \cdot x = x\}$ is the set of elements fixed by $g$.

**Example**: Count the number of distinct necklaces with $n$ beads of $k$ colors. The group is $\mathbb{Z}_n$ (rotations), and $|X^{r^j}| = k^{\gcd(n,j)}$.

#### 3.2 The Cycle Index

For a permutation group $G$ acting on $[n]$, the **cycle index** is:

$$Z_G(x_1, x_2, \ldots, x_n) = \frac{1}{|G|} \sum_{g \in G} x_1^{c_1(g)} x_2^{c_2(g)} \cdots x_n^{c_n(g)}$$

where $c_k(g)$ is the number of $k$-cycles in the permutation $g$.

#### 3.3 Pólya's Enumeration Theorem (PET)

**Theorem**: The number of distinct ways to color $n$ objects with $k$ colors under the action of group $G$ is:

$$Z_G(k, k, \ldots, k)$$

More generally, if colors have weights, the **pattern inventory** is:

$$Z_G(f_1 + f_2 + \cdots + f_k, f_1^2 + f_2^2 + \cdots + f_k^2, \ldots)$$

where $f_i$ is the weight of color $i$.

**Example**: Distinct colorings of the faces of a cube with $k$ colors: $Z_{S_{\text{cube}}}(k, k, \ldots, k)$ where the rotation group of the cube has 24 elements.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Introductory Combinatorics* (5th ed.) | Richard A. Brualdi | **Primary** |
| *Enumerative Combinatorics* Vol. I & II | Richard P. Stanley | **Advanced** — Definitive reference |
| *Generatingfunctionology* (3rd ed.) | Herbert S. Wilf | **Supplementary** — GF-focused, freely available online |
| *Analytic Combinatorics* | Philippe Flajolet & Robert Sedgewick | **Advanced** — Asymptotic counting |

---

## Problem Sets

### Problem Set 1: Generating Functions

1. **(Brualdi 7.2)** Find the OGF for the number of ways to distribute $n$ identical balls into 4 distinct boxes with at most 5 balls per box.
2. **(Exam-style)** Use generating functions to solve $a_n = 3a_{n-1} - 2a_{n-2}$ with $a_0 = 1, a_1 = 3$.
3. **(Exam-style)** Derive the EGF for the Bell numbers $B_n$ (number of set partitions of $[n]$).
4. **(Proof)** Prove the Binet formula for Fibonacci numbers using partial fractions.
5. **(Challenge)** Use generating functions to show $\sum_{k=0}^n \binom{n}{k}^2 = \binom{2n}{n}$ (Vandermonde's identity).

### Problem Set 2: Inclusion-Exclusion and Catalan Numbers

1. **(Brualdi 6.1)** Use PIE to count derangements $D_n$ and verify $D_n/n! \to 1/e$.
2. **(Exam-style)** Compute the number of surjections from a set of 5 elements onto a set of 3 elements.
3. **(Exam-style)** Derive the recurrence $C_n = \sum_{k=0}^{n-1} C_k C_{n-1-k}$ for Catalan numbers and use it to find $C(x)$.
4. **(Proof)** Give a bijective proof that Catalan numbers count both Dyck paths and full binary trees.
5. **(Challenge)** Prove that $C_n = \frac{1}{n+1}\binom{2n}{n}$ using the cycle lemma or reflection principle.

### Problem Set 3: Pólya Counting

1. **(Brualdi 14.3)** Use Burnside's lemma to count the number of distinct necklaces with 6 beads of 3 colors.
2. **(Exam-style)** Compute the cycle index of $\mathbb{Z}_4$ acting on 4 objects and use PET to count distinct 2-colorings.
3. **(Exam-style)** How many distinct ways can you color the faces of a regular tetrahedron with $k$ colors?
4. **(Proof)** Prove Burnside's Lemma using the orbit-stabilizer theorem.
5. **(Challenge)** Use Pólya's theorem to compute the number of distinct simple graphs on 4 labeled vertices.
