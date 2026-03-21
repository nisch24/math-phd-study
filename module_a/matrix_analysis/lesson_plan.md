---
layout: default
title: "EN.553.792 — Matrix Analysis"
parent: "Module A — Analysis & Linear Algebra"
nav_order: 2
permalink: /module_a/matrix_analysis/
---

# EN.553.792 — Matrix Analysis

> *A rigorous study of matrices as linear operators, with emphasis on spectral theory, decompositions, and their applications across statistics, optimization, and applied mathematics.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Characterize eigenvalues and eigenvectors** using spectral theory and canonical forms.
2. **Decompose matrices** via spectral decomposition, Singular Value Decomposition (SVD), and other factorizations.
3. **Apply variational characterizations** (Courant-Fischer, Weyl) to bound and estimate eigenvalues.
4. **Analyze matrix norms** and their relationships to spectral properties.
5. **Use perturbation theory** to study the sensitivity of eigenvalues and singular values.

---

## Core Theory

### Unit 1: Eigenvalues and the Spectral Theorem

#### 1.1 Eigenvalues, Eigenvectors, and Characteristic Polynomial

Let $A \in \mathbb{C}^{n \times n}$. A scalar $\lambda \in \mathbb{C}$ is an **eigenvalue** of $A$ if there exists a nonzero $x$ such that $Ax = \lambda x$. The eigenvalues are the roots of the **characteristic polynomial**:

$$p(\lambda) = \det(A - \lambda I)$$

**Algebraic multiplicity**: the multiplicity of $\lambda$ as a root of $p(\lambda)$.

**Geometric multiplicity**: $\dim \ker(A - \lambda I)$. Always satisfies: geometric $\leq$ algebraic multiplicity.

#### 1.2 The Spectral Theorem for Hermitian Matrices

**Theorem**: Let $A \in \mathbb{C}^{n \times n}$ be Hermitian ($A = A^*$). Then:

1. All eigenvalues of $A$ are real.
2. Eigenvectors corresponding to distinct eigenvalues are orthogonal.
3. $A$ has an orthonormal basis of eigenvectors. That is, there exists a unitary matrix $U$ and a real diagonal matrix $\Lambda$ such that:

$$A = U \Lambda U^*$$

*Proof Sketch*:
- **Real eigenvalues**: If $Ax = \lambda x$ with $x \neq 0$, then $\lambda \|x\|^2 = x^*Ax = (x^*Ax)^* = \bar{\lambda}\|x\|^2$, so $\lambda = \bar{\lambda}$.
- **Orthogonality**: If $Ax = \lambda x$ and $Ay = \mu y$ with $\lambda \neq \mu$, then $\lambda \langle x, y \rangle = \langle Ax, y \rangle = \langle x, Ay \rangle = \mu \langle x, y \rangle$, so $\langle x, y \rangle = 0$.
- **Full diagonalization**: Proceed by induction on $n$, using the fact that the orthogonal complement of an eigenspace is $A$-invariant.

#### 1.3 Normal Matrices

**Definition**: $A$ is **normal** if $AA^* = A^*A$.

**Theorem (Spectral Theorem for Normal Matrices)**: $A$ is unitarily diagonalizable ($A = U\Lambda U^*$ with $U$ unitary) if and only if $A$ is normal.

**Examples**: Hermitian, skew-Hermitian, unitary, and real symmetric matrices are all normal.

---

### Unit 2: Singular Value Decomposition (SVD)

#### 2.1 Statement of the SVD

**Theorem**: For any $A \in \mathbb{C}^{m \times n}$, there exist unitary matrices $U \in \mathbb{C}^{m \times m}$, $V \in \mathbb{C}^{n \times n}$, and a diagonal matrix $\Sigma \in \mathbb{R}^{m \times n}$ with nonnegative entries $\sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_{\min(m,n)} \geq 0$ such that:

$$A = U \Sigma V^*$$

The $\sigma_i$ are the **singular values** of $A$. They are the square roots of the eigenvalues of $A^*A$ (or equivalently $AA^*$).

#### 2.2 Geometric Interpretation

The SVD reveals that any linear map $A: \mathbb{C}^n \to \mathbb{C}^m$ can be decomposed into three steps:
1. **Rotation/reflection** by $V^*$ in the domain.
2. **Scaling** by the singular values along coordinate axes.
3. **Rotation/reflection** by $U$ in the codomain.

#### 2.3 Fundamental Subspaces

From $A = U\Sigma V^*$ with $r = \text{rank}(A)$:

| Subspace | Description | Basis |
|----------|-------------|-------|
| $\text{Col}(A)$ | Column space | First $r$ columns of $U$ |
| $\text{Null}(A^*)$ | Left null space | Last $m - r$ columns of $U$ |
| $\text{Row}(A)$ | Row space | First $r$ columns of $V$ |
| $\text{Null}(A)$ | Null space | Last $n - r$ columns of $V$ |

#### 2.4 Low-Rank Approximation

**Theorem (Eckart-Young-Mirsky)**: The best rank-$k$ approximation to $A$ (in both the spectral norm and Frobenius norm) is:

$$A_k = \sum_{i=1}^k \sigma_i u_i v_i^*$$

The approximation error is $\|A - A_k\|_2 = \sigma_{k+1}$ and $\|A - A_k\|_F = \sqrt{\sigma_{k+1}^2 + \cdots + \sigma_r^2}$.

This is the theoretical basis for **Principal Component Analysis (PCA)** in statistics.

#### 2.5 Pseudoinverse

The **Moore-Penrose pseudoinverse** $A^+$ is defined via the SVD as:

$$A^+ = V \Sigma^+ U^*$$

where $\Sigma^+$ replaces each nonzero $\sigma_i$ with $\sigma_i^{-1}$. This gives the minimum-norm least squares solution: $x^+ = A^+ b$ minimizes $\|Ax - b\|_2$ and among all minimizers, has the smallest $\|x\|_2$.

---

### Unit 3: Variational Characterizations of Eigenvalues

#### 3.1 The Rayleigh Quotient

For a Hermitian matrix $A$ and nonzero vector $x$:

$$R(x) = \frac{x^* A x}{x^* x}$$

**Key property**: If $\lambda_1 \leq \lambda_2 \leq \cdots \leq \lambda_n$ are the eigenvalues of $A$, then $\lambda_1 \leq R(x) \leq \lambda_n$ for all nonzero $x$.

#### 3.2 Courant-Fischer Theorem

**Theorem (Min-Max)**: Let $A$ be Hermitian with eigenvalues $\lambda_1 \leq \lambda_2 \leq \cdots \leq \lambda_n$. Then:

$$\lambda_k = \min_{\dim S = k} \max_{x \in S, x \neq 0} \frac{x^* A x}{x^* x} = \max_{\dim S = n-k+1} \min_{x \in S, x \neq 0} \frac{x^* A x}{x^* x}$$

where $S$ ranges over subspaces of $\mathbb{C}^n$.

*Proof Sketch*: Express $x$ in the eigenbasis. For a $k$-dimensional subspace $S$, the maximum Rayleigh quotient is at least $\lambda_k$ because any $k$-dimensional subspace must intersect $\text{span}\{v_k, \ldots, v_n\}$ nontrivially (dimension counting). The eigenspace $\text{span}\{v_1, \ldots, v_k\}$ achieves the minimum over such maxima.

#### 3.3 Weyl's Inequalities

**Theorem (Weyl)**: Let $A, B$ be Hermitian $n \times n$ matrices with eigenvalues $\alpha_1 \leq \cdots \leq \alpha_n$ and $\beta_1 \leq \cdots \leq \beta_n$. If $C = A + B$ has eigenvalues $\gamma_1 \leq \cdots \leq \gamma_n$, then:

$$\alpha_i + \beta_1 \leq \gamma_i \leq \alpha_i + \beta_n$$

More generally: $\gamma_{i+j-1} \leq \alpha_i + \beta_j$ when $i + j - 1 \leq n$ and $\gamma_{i+j-n} \geq \alpha_i + \beta_j$ when $i + j \geq n + 1$.

**Application**: If $B$ is a small perturbation, Weyl's inequality bounds the change in eigenvalues: $|\gamma_i - \alpha_i| \leq \|B\|_2$.

#### 3.4 Interlacing Theorems

**Cauchy Interlacing Theorem**: Let $A$ be an $n \times n$ Hermitian matrix and $B$ be a principal $(n-1) \times (n-1)$ submatrix (obtained by deleting one row and the corresponding column). If $\lambda_1 \leq \cdots \leq \lambda_n$ are eigenvalues of $A$ and $\mu_1 \leq \cdots \leq \mu_{n-1}$ are eigenvalues of $B$, then:

$$\lambda_1 \leq \mu_1 \leq \lambda_2 \leq \mu_2 \leq \cdots \leq \mu_{n-1} \leq \lambda_n$$

---

### Unit 4: Matrix Norms and Perturbation Theory

#### 4.1 Matrix Norms

**Induced (operator) norms**: For a matrix $A \in \mathbb{C}^{m \times n}$:

$$\|A\|_p = \sup_{x \neq 0} \frac{\|Ax\|_p}{\|x\|_p}$$

Key cases:
- $\|A\|_2 = \sigma_1(A)$ (largest singular value)
- $\|A\|_1 = \max_j \sum_i |a_{ij}|$ (maximum column sum)
- $\|A\|_\infty = \max_i \sum_j |a_{ij}|$ (maximum row sum)

**Frobenius norm**: $\|A\|_F = \sqrt{\sum_{i,j} |a_{ij}|^2} = \sqrt{\text{tr}(A^*A)} = \sqrt{\sigma_1^2 + \cdots + \sigma_r^2}$

#### 4.2 Condition Number

The **condition number** of an invertible matrix $A$: $\kappa(A) = \|A\| \cdot \|A^{-1}\| = \frac{\sigma_1}{\sigma_n}$ (for the 2-norm).

**Significance**: When solving $Ax = b$, the relative error satisfies:

$$\frac{\|\delta x\|}{\|x\|} \leq \kappa(A) \frac{\|\delta b\|}{\|b\|}$$

A large condition number indicates an ill-conditioned system.

#### 4.3 Perturbation of Singular Values

**Weyl's Perturbation Theorem for Singular Values**: For $A, E \in \mathbb{C}^{m \times n}$:

$$|\sigma_i(A + E) - \sigma_i(A)| \leq \|E\|_2$$

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Matrix Analysis* (2nd ed.) | Roger A. Horn & Charles R. Johnson | **Primary** — Comprehensive reference for all topics |
| *Topics in Matrix Analysis* | Roger A. Horn & Charles R. Johnson | **Supplementary** — Advanced topics, norm theory |
| *Matrix Analysis and Applied Linear Algebra* | Carl D. Meyer | **Alternative** — Applications-focused |
| *Matrix Computations* (4th ed.) | Gene H. Golub & Charles F. Van Loan | **Computational** — Algorithms for SVD, eigenvalue problems |

---

## Problem Sets

### Problem Set 1: Spectral Theory

1. **(Horn & Johnson, 1.3.P4)** Prove that every Hermitian matrix is unitarily diagonalizable.
2. **(Exam-style)** Let $A$ be a real symmetric matrix. Show that $\|A\|_2 = \max_i |\lambda_i(A)|$.
3. **(Exam-style)** Prove that if $A$ and $B$ are Hermitian and $AB = BA$, then $A$ and $B$ are simultaneously diagonalizable.
4. **(Proof)** Show that $A$ is normal if and only if $\|Ax\| = \|A^*x\|$ for all $x$.
5. **(Challenge)** Prove that every matrix is the product of two Hermitian matrices.

### Problem Set 2: Singular Value Decomposition

1. **(Horn & Johnson, 7.3.P1)** Compute the SVD of $A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \\ 1 & 0 \end{pmatrix}$.
2. **(Exam-style)** Prove that $\text{rank}(A) = $ number of nonzero singular values of $A$.
3. **(Exam-style)** Show that for any $A$: $\|A\|_F^2 = \sum \sigma_i^2$ and $\|A\|_2 = \sigma_1$.
4. **(Application)** Given a data matrix $X \in \mathbb{R}^{n \times p}$, explain how the SVD of $X$ relates to Principal Component Analysis. What are the principal components and principal directions in terms of $U$, $\Sigma$, $V$?
5. **(Proof)** Prove the Eckart-Young-Mirsky theorem for the Frobenius norm.

### Problem Set 3: Variational Characterizations

1. **(Horn & Johnson, 4.2.P1)** Use the Courant-Fischer theorem to prove Weyl's inequality.
2. **(Exam-style)** Let $A$ be $n \times n$ positive semidefinite. Prove that $\lambda_{\max}(A) = \max_{\|x\|=1} x^T A x$.
3. **(Exam-style)** Prove the Cauchy interlacing theorem using the Courant-Fischer theorem.
4. **(Application)** Let $A = \begin{pmatrix} 4 & 1 \\ 1 & 3 \end{pmatrix}$ and $B = \begin{pmatrix} 0.01 & 0 \\ 0 & -0.02 \end{pmatrix}$. Use Weyl's inequality to bound the eigenvalues of $A + B$.
5. **(Challenge)** Prove that if $A$ is positive definite and $B$ is Hermitian, then the eigenvalues of $AB$ are real.

---

## Study Guide & Exam Preparation

**For the Introductory Exam (Linear Algebra portion)**:
- Be able to state and prove the Spectral Theorem for Hermitian matrices.
- Know the SVD statement and its implications (rank, pseudoinverse, low-rank approximation).
- Master Courant-Fischer: be able to use it to derive eigenvalue bounds and prove interlacing.
- Understand the connection between eigenvalues of $A^*A$ and singular values of $A$.
- Practice computational problems: diagonalize small matrices, compute SVDs by hand.
