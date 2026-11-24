---
layout: default
title: "0.3 — Proof-Based Linear Algebra"
parent: "Module 0 — Foundations"
nav_order: 3
permalink: /module_0/linear_algebra/
---

# 0.3 — Proof-Based Linear Algebra

> *A matrix is just one way of writing down a linear map, after choosing bases. This course studies the maps themselves: their kernels, ranks, eigenvalues, and geometry. Everything here holds in any basis, and that basis-free view is what Matrix Analysis, statistics, and optimization all build on.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Work abstractly with vector spaces**: subspaces, span, linear independence, bases, and dimension.
2. **Prove and apply the rank–nullity theorem**, and translate between linear maps and matrices under change of basis.
3. **Prove that eigenvalues exist** over $\mathbb{C}$ and characterize diagonalizability.
4. **Use inner products**: Cauchy–Schwarz, Gram–Schmidt, orthogonal projections, and adjoints.
5. **State and prove the spectral theorem** for self-adjoint operators.

---

## Core Theory

### Unit 1: Vector Spaces, Bases, and Dimension

A **vector space** over $\mathbb{F}$ ($= \mathbb{R}$ or $\mathbb{C}$) is a set closed under addition and scalar multiplication, satisfying the usual axioms. Examples beyond $\mathbb{F}^n$: polynomials of degree $\leq n$, continuous functions on $[0,1]$, $m \times n$ matrices, solutions of a linear ODE.

- A list $v_1, \ldots, v_k$ is **linearly independent** if $\sum a_i v_i = 0$ forces all $a_i = 0$.
- A **basis** is a linearly independent spanning list.

**Key Lemma (Exchange)**: In a finite-dimensional space, the length of every linearly independent list is at most the length of every spanning list.

**Consequence**: all bases have the same length, the **dimension**.

**Intuition**: independence says "no redundancy", and spanning says "nothing missing". The exchange lemma says you can never have more non-redundant vectors than it takes to reach everything. Dimension counts the true degrees of freedom.

---

### Unit 2: Linear Maps

A map $T: V \to W$ is **linear** if $T(au + bv) = aT(u) + bT(v)$. Its **null space** is $\operatorname{null} T = \{v : Tv = 0\}$ and its **range** is $\operatorname{range} T = \{Tv : v \in V\}$.

**Rank–Nullity Theorem**: If $V$ is finite-dimensional,

$$\dim V = \dim \operatorname{null} T + \dim \operatorname{range} T.$$

**Intuition**: each dimension of the input is either crushed to zero or survives into the output; none is created or lost. **Consequences**: for $T: V \to V$, injective $\iff$ surjective $\iff$ invertible. A system with more unknowns than equations has a nonzero solution.

**Matrices and change of basis**: once bases are fixed, $T$ is represented by a matrix $M(T)$, and composition corresponds to matrix multiplication. Changing basis replaces $M(T)$ by $S^{-1}M(T)S$. **Similar matrices represent the same map**, which is why rank, determinant, trace, and eigenvalues are similarity invariants: they describe the map, not the coordinates.

---

### Unit 3: Eigenvalues and Eigenvectors

$\lambda$ is an **eigenvalue** of $T: V \to V$ if $Tv = \lambda v$ for some $v \neq 0$; equivalently, $T - \lambda I$ is not injective.

**Theorem**: Every operator on a finite-dimensional **complex** vector space ($\dim V \geq 1$) has an eigenvalue.
*Proof idea*: The $n+1$ vectors $v, Tv, \ldots, T^n v$ are dependent, so $p(T)v = 0$ for some nonzero polynomial $p$. Factor $p$ over $\mathbb{C}$ into linear factors: some factor $T - \lambda I$ must fail to be injective.

**Over $\mathbb{R}$ this can fail**: rotation of $\mathbb{R}^2$ by $90°$ has no real eigenvalue.

**Results**:
- Eigenvectors for distinct eigenvalues are linearly independent. So $n$ distinct eigenvalues imply diagonalizability.
- $T$ is **diagonalizable** iff $V$ has a basis of eigenvectors.
- **(Schur)** Over $\mathbb{C}$, every operator has an upper-triangular matrix in some (even orthonormal) basis. Its diagonal entries are the eigenvalues.
- Not every operator is diagonalizable: $\begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}$ has only the eigenvalue $0$ and a one-dimensional eigenspace. The **Jordan form** describes the general case.

---

### Unit 4: Inner Product Spaces

An **inner product** $\langle \cdot, \cdot \rangle$ gives lengths ($\|v\| = \sqrt{\langle v,v \rangle}$) and angles.

**Cauchy–Schwarz**: $|\langle u, v \rangle| \leq \|u\| \|v\|$, with equality iff $u, v$ are dependent.
*Proof idea*: if $v \neq 0$, write $u = cv + w$ with $w \perp v$ (orthogonal decomposition); then $\|u\|^2 = |c|^2\|v\|^2 + \|w\|^2 \geq |c|^2 \|v\|^2$.

**Gram–Schmidt**: turns any basis into an orthonormal basis with the same nested spans. (In matrix form, this is the QR factorization.)

**Orthogonal Projection**: For a subspace $U$, every $v$ splits uniquely as $v = P_U v + w$ with $P_U v \in U$, $w \perp U$, and

$$\|v - P_U v\| \leq \|v - u\| \quad \text{for all } u \in U.$$

**Why this matters**: least squares, linear regression, conditional expectation (Module B), and PCA are all orthogonal projections.

**Adjoint**: $T^*$ is defined by $\langle Tv, w \rangle = \langle v, T^* w \rangle$. In an orthonormal basis, $M(T^*)$ is the conjugate transpose of $M(T)$.

### Unit 5: The Spectral Theorem

**Theorem**:
- **(Real)** $T$ on a real inner product space is **self-adjoint** ($T = T^*$) iff $V$ has an orthonormal basis of eigenvectors of $T$.
- **(Complex)** $T$ on a complex inner product space is **normal** ($TT^* = T^*T$) iff $V$ has an orthonormal basis of eigenvectors of $T$.

**Intuition**: a symmetric matrix acts by pure stretching along perpendicular axes, with no rotation or shear. Every quadratic form $x^T A x$ becomes a weighted sum of squares $\sum \lambda_i y_i^2$ in the right coordinates. This is the geometry behind covariance matrices, Hessians, and PCA.

**Determinant and trace**: $\det T = \prod \lambda_i$ and $\operatorname{tr} T = \sum \lambda_i$ (over $\mathbb{C}$, with multiplicity). $\det$ measures how volume scales; $\det T = 0$ iff $T$ is not invertible.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| [*Linear Algebra Done Right*](https://linear.axler.net/) (4th ed.) | Sheldon Axler | **Primary** — Free electronic edition; this course follows its approach |
| *Linear Algebra* (5th ed.) | Friedberg, Insel &amp; Spence | **Alternative** — More examples and matrix computations alongside proofs |
| [*Linear Algebra Done Wrong*](https://www.math.brown.edu/streil/papers/LADW/LADW.html) | Sergei Treil | **Free alternative** — Proof-based but more matrix-friendly |
| *Introduction to Linear Algebra* | Gilbert Strang | **Intuition** — Computational, but unmatched for geometric pictures |

---

## Problem Sets

### Problem Set 1: Spaces and Maps

1. **(Core)** Show that $\{p \in \mathcal{P}_3(\mathbb{R}) : p(1) = 0\}$ is a subspace, find a basis, and compute its dimension.
2. **(Core)** Prove that if $v_1, \ldots, v_n$ spans $V$, then so does $v_1 - v_2, v_2 - v_3, \ldots, v_{n-1} - v_n, v_n$.
3. **(Proof)** Prove the rank–nullity theorem.
4. **(Core)** Let $D: \mathcal{P}_n(\mathbb{R}) \to \mathcal{P}_n(\mathbb{R})$ be differentiation. Find its null space, range, and matrix in the basis $1, x, \ldots, x^n$, and verify rank–nullity.
5. **(Challenge)** Prove that for $T: V \to W$ and $S: W \to U$ (finite-dimensional), $\dim\operatorname{null}(ST) \leq \dim\operatorname{null} S + \dim\operatorname{null} T$.

### Problem Set 2: Eigenvalues

1. **(Core)** Find all eigenvalues and eigenvectors of $T(x, y) = (y, x)$ on $\mathbb{R}^2$ and of rotation by angle $\theta$ on $\mathbb{R}^2$ (as a real map, then as a map on $\mathbb{C}^2$).
2. **(Proof)** Prove that eigenvectors corresponding to distinct eigenvalues are linearly independent.
3. **(Core)** Prove that $\begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$ is not diagonalizable.
4. **(Proof)** Prove that every operator on a finite-dimensional complex vector space has an eigenvalue.
5. **(Challenge)** Suppose $T^2 = T$. Prove that $V = \operatorname{null} T \oplus \operatorname{range} T$ and that $T$ is diagonalizable with eigenvalues in $\{0, 1\}$.

### Problem Set 3: Inner Products and the Spectral Theorem

1. **(Core)** Apply Gram–Schmidt to $1, x, x^2$ on $[-1,1]$ with $\langle f, g \rangle = \int_{-1}^1 fg$. (You will get multiples of the first Legendre polynomials.)
2. **(Proof)** Prove the Cauchy–Schwarz inequality and the triangle inequality.
3. **(Core)** Find the orthogonal projection of $(1, 2, 3)$ onto the plane $x + y + z = 0$ in $\mathbb{R}^3$, and verify that it minimizes distance.
4. **(Proof)** Prove that a self-adjoint operator has real eigenvalues and that eigenvectors for distinct eigenvalues are orthogonal.
5. **(Challenge)** Prove the real spectral theorem. *(Hint: induct on dimension; show that the orthogonal complement of an eigenvector is invariant under $T$.)*

---

## Study Guide

{: .important }
> **Theorems to know at the full-proof level**
>
> - The exchange lemma, hence the invariance of dimension
> - Rank–nullity, and its corollary that injective $\iff$ surjective for operators
> - Existence of eigenvalues over $\mathbb{C}$; linear independence of eigenvectors for distinct eigenvalues
> - Cauchy–Schwarz, and orthogonal projection as the best approximation
> - The real spectral theorem

**Translate everything**: after each theorem, write its matrix version. Rank–nullity for an $m \times n$ matrix $A$ reads $n = \dim \ker A + \operatorname{rank} A$; the spectral theorem reads $A = Q\Lambda Q^T$ for symmetric $A$. Module A and the Linear Algebra exam paper use both languages interchangeably.
