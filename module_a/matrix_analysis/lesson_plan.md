---
layout: default
title: "EN.553.792 — Matrix Analysis"
parent: "Module A — Analysis & Linear Algebra"
nav_order: 2
permalink: /module_a/matrix_analysis/
---

# EN.553.792 — Matrix Analysis

> *A rigorous study of matrices as linear operators, with emphasis on spectral theory, canonical decompositions, and their applications across statistics, optimization, and applied mathematics. This course provides the algebraic toolkit used throughout the PhD program.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Characterize eigenvalues and eigenvectors** using spectral theory and the characteristic polynomial.
2. **Decompose matrices** via the Spectral Theorem, Singular Value Decomposition (SVD), and related factorizations.
3. **Apply variational characterizations** — Courant-Fischer and Weyl's inequalities — to bound and estimate eigenvalues.
4. **Analyze matrix norms** and their relationships to singular values and spectral properties.
5. **Use perturbation theory** to study the sensitivity of eigenvalues and singular values to small changes in the matrix.

---

## Core Theory

### Unit 1: Eigenvalues and the Spectral Theorem

#### 1.1 Eigenvalues, Eigenvectors, and the Characteristic Polynomial

Let $A \in \mathbb{C}^{n \times n}$. A scalar $\lambda \in \mathbb{C}$ is an **eigenvalue** of $A$ if there exists a nonzero vector $x$ such that $Ax = \lambda x$. The eigenvalues are the roots of the **characteristic polynomial**:

$$p(\lambda) = \det(A - \lambda I).$$

- **Algebraic multiplicity**: the multiplicity of $\lambda$ as a root of $p(\lambda)$.
- **Geometric multiplicity**: $\dim \ker(A - \lambda I)$. One always has: geometric $\leq$ algebraic multiplicity.

#### 1.2 The Spectral Theorem for Hermitian Matrices

**Theorem**: Let $A \in \mathbb{C}^{n \times n}$ be Hermitian ($A = A^*$). Then:

1. All eigenvalues of $A$ are real.
2. Eigenvectors corresponding to distinct eigenvalues are orthogonal.
3. $A$ has an orthonormal basis of eigenvectors; i.e., there exists a unitary $U$ and real diagonal $\Lambda$ such that:

$$A = U \Lambda U^*.$$

*Proof Sketch*:
- **Real eigenvalues**: If $Ax = \lambda x$ with $x \neq 0$, then $\lambda \|x\|^2 = x^*Ax = \overline{x^*Ax} = \bar{\lambda}\|x\|^2$, so $\lambda = \bar{\lambda}$.
- **Orthogonality**: If $Ax = \lambda x$ and $Ay = \mu y$ with $\lambda \neq \mu$, then $\lambda \langle x, y \rangle = \langle Ax, y \rangle = \langle x, Ay \rangle = \mu \langle x, y \rangle$, so $\langle x, y \rangle = 0$.
- **Full diagonalization**: By induction on $n$, using the $A$-invariance of the orthogonal complement of each eigenspace.

#### 1.3 Normal Matrices

**Definition**: $A$ is **normal** if $AA^* = A^*A$.

**Theorem (Spectral Theorem for Normal Matrices)**: $A$ is unitarily diagonalizable ($A = U\Lambda U^*$ with $U$ unitary) if and only if $A$ is normal.

**Examples**: Hermitian, skew-Hermitian, unitary, and real symmetric matrices are all normal.

---

### Unit 2: Singular Value Decomposition (SVD)

#### 2.1 Statement of the SVD

**Theorem**: For any $A \in \mathbb{C}^{m \times n}$, there exist unitary matrices $U \in \mathbb{C}^{m \times m}$ and $V \in \mathbb{C}^{n \times n}$, and a rectangular diagonal matrix $\Sigma \in \mathbb{R}^{m \times n}$ with nonnegative diagonal entries $\sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_{\min(m,n)} \geq 0$ such that:

$$A = U \Sigma V^*.$$

The values $\sigma_i$ are the **singular values** of $A$, equal to the square roots of the eigenvalues of $A^*A$ (equivalently, of $AA^*$).

#### 2.2 Geometric Interpretation

The SVD reveals that any linear map $A: \mathbb{C}^n \to \mathbb{C}^m$ decomposes into three steps:
1. **Rotation/reflection** in the domain by $V^*$.
2. **Scaling** along coordinate axes by the singular values.
3. **Rotation/reflection** in the codomain by $U$.

#### 2.3 Fundamental Subspaces

From $A = U\Sigma V^*$ with $r = \operatorname{rank}(A)$:

| Subspace | Description | Basis |
|----------|-------------|-------|
| $\operatorname{Col}(A)$ | Column space | First $r$ columns of $U$ |
| $\operatorname{Null}(A^*)$ | Left null space | Last $m - r$ columns of $U$ |
| $\operatorname{Row}(A)$ | Row space | First $r$ columns of $V$ |
| $\operatorname{Null}(A)$ | Null space | Last $n - r$ columns of $V$ |

#### 2.4 Low-Rank Approximation (Eckart-Young-Mirsky)

**Theorem**: The best rank-$k$ approximation to $A$ in both the spectral norm and Frobenius norm is:

$$A_k = \sum_{i=1}^k \sigma_i u_i v_i^*.$$

The errors are $\|A - A_k\|_2 = \sigma_{k+1}$ and $\|A - A_k\|_F = \sqrt{\sigma_{k+1}^2 + \cdots + \sigma_r^2}$.

This result is the theoretical foundation of **Principal Component Analysis (PCA)**.

#### 2.5 The Moore-Penrose Pseudoinverse

The **Moore-Penrose pseudoinverse** $A^+$ is defined via the SVD as:

$$A^+ = V \Sigma^+ U^*,$$

where $\Sigma^+$ replaces each nonzero $\sigma_i$ with $\sigma_i^{-1}$. The vector $x^+ = A^+ b$ is the minimum-norm least-squares solution: it minimizes $\|Ax - b\|_2$, and among all minimizers has the smallest $\|x\|_2$.

---

### Unit 3: Variational Characterizations of Eigenvalues

#### 3.1 The Rayleigh Quotient

For a Hermitian matrix $A$ and nonzero vector $x$, the **Rayleigh quotient** is:

$$R(x) = \frac{x^* A x}{x^* x}.$$

If $\lambda_1 \leq \lambda_2 \leq \cdots \leq \lambda_n$ are the eigenvalues of $A$, then $\lambda_1 \leq R(x) \leq \lambda_n$ for all nonzero $x$, with equality achieved at the corresponding eigenvectors.

#### 3.2 The Courant-Fischer Min-Max Theorem

**Theorem**: Let $A$ be Hermitian with eigenvalues $\lambda_1 \leq \cdots \leq \lambda_n$. Then:

$$\lambda_k = \min_{\dim S = k} \max_{x \in S,\, x \neq 0} \frac{x^* A x}{x^* x} = \max_{\dim S = n-k+1} \min_{x \in S,\, x \neq 0} \frac{x^* A x}{x^* x},$$

where $S$ ranges over all subspaces of $\mathbb{C}^n$.

*Proof Sketch*: Express $x$ in the eigenbasis. Any $k$-dimensional subspace $S$ must intersect $\operatorname{span}\{v_k, \ldots, v_n\}$ nontrivially by dimension counting, so the maximum Rayleigh quotient over $S$ is at least $\lambda_k$. The eigenspace $\operatorname{span}\{v_1, \ldots, v_k\}$ achieves the minimum over all such subspaces.

#### 3.3 Weyl's Perturbation Inequalities

**Theorem (Weyl)**: Let $A, B$ be Hermitian $n \times n$ matrices with eigenvalues $\alpha_1 \leq \cdots \leq \alpha_n$ and $\beta_1 \leq \cdots \leq \beta_n$. If $C = A + B$ has eigenvalues $\gamma_1 \leq \cdots \leq \gamma_n$, then:

$$\alpha_i + \beta_1 \leq \gamma_i \leq \alpha_i + \beta_n.$$

**Application**: If $B$ is a small perturbation, then $|\gamma_i - \alpha_i| \leq \|B\|_2$ for all $i$ — eigenvalues are Lipschitz continuous functions of the matrix entries.

#### 3.4 Cauchy Interlacing Theorem

**Theorem**: Let $A$ be $n \times n$ Hermitian and $B$ a principal $(n-1) \times (n-1)$ submatrix (deleting one row and the corresponding column). If $\lambda_1 \leq \cdots \leq \lambda_n$ and $\mu_1 \leq \cdots \leq \mu_{n-1}$ are their respective eigenvalues, then:

$$\lambda_1 \leq \mu_1 \leq \lambda_2 \leq \mu_2 \leq \cdots \leq \mu_{n-1} \leq \lambda_n.$$

---

### Unit 4: Matrix Norms and Perturbation Theory

#### 4.1 Induced and Frobenius Norms

**Induced (operator) norms**: For $A \in \mathbb{C}^{m \times n}$:

$$\|A\|_p = \sup_{x \neq 0} \frac{\|Ax\|_p}{\|x\|_p}.$$

Key cases:
- $\|A\|_2 = \sigma_1(A)$ — largest singular value (spectral norm).
- $\|A\|_1 = \max_j \sum_i |a_{ij}|$ — maximum column sum.
- $\|A\|_\infty = \max_i \sum_j |a_{ij}|$ — maximum row sum.

**Frobenius norm**: $\|A\|_F = \sqrt{\sum_{i,j} |a_{ij}|^2} = \sqrt{\operatorname{tr}(A^*A)} = \sqrt{\sigma_1^2 + \cdots + \sigma_r^2}$.

#### 4.2 Condition Number

The **condition number** of an invertible matrix $A$: $\kappa(A) = \|A\|_2 \cdot \|A^{-1}\|_2 = \sigma_1 / \sigma_n$.

**Significance**: When solving $Ax = b$, the relative perturbation in the solution satisfies:

$$\frac{\|\delta x\|}{\|x\|} \leq \kappa(A) \frac{\|\delta b\|}{\|b\|}.$$

A large condition number signals an ill-conditioned system sensitive to numerical errors or data perturbations.

#### 4.3 Weyl's Perturbation Theorem for Singular Values

**Theorem**: For $A, E \in \mathbb{C}^{m \times n}$:

$$|\sigma_i(A + E) - \sigma_i(A)| \leq \|E\|_2.$$

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Matrix Analysis* (2nd ed.) | Roger A. Horn &amp; Charles R. Johnson | **Primary** — The comprehensive reference for all topics in this course |
| *Topics in Matrix Analysis* | Roger A. Horn &amp; Charles R. Johnson | **Supplementary** — Advanced topics including norm theory and inertia |
| *Matrix Analysis and Applied Linear Algebra* | Carl D. Meyer | **Alternative** — Applications-focused with detailed examples |
| *Matrix Computations* (4th ed.) | Gene H. Golub &amp; Charles F. Van Loan | **Computational** — Algorithms for SVD, eigenvalue, and linear system problems |

---

## Problem Sets

### Problem Set 1: Spectral Theory

1. **(cf. Horn &amp; Johnson §2.5)** Prove that every Hermitian matrix is unitarily diagonalizable.
2. **(Exam-style)** Let $A$ be a real symmetric matrix. Show that $\|A\|_2 = \max_i |\lambda_i(A)|$.
3. **(Exam-style)** Prove that if $A$ and $B$ are Hermitian and $AB = BA$, then $A$ and $B$ are simultaneously diagonalizable.
4. **(Proof)** Show that $A$ is normal if and only if $\|Ax\| = \|A^*x\|$ for all $x \in \mathbb{C}^n$.
5. **(Challenge)** Prove or disprove: every $A \in \mathbb{C}^{n \times n}$ is a product of two Hermitian matrices. Hint: if $A = HK$ with $H, K$ Hermitian and $H$ invertible, show $A$ is similar to $A^*$, then test $A = \operatorname{diag}(i, 1)$. (The full characterization, due to Taussky: $A$ is a product of two Hermitian matrices iff $A$ is similar to $A^*$. Contrast this with the true statement that every complex square matrix is a product of two complex *symmetric* matrices.)

### Problem Set 2: Singular Value Decomposition

1. **(cf. Horn &amp; Johnson §2.6)** Compute the SVD of $A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \\ 1 & 0 \end{pmatrix}$.
2. **(Exam-style)** Prove that $\operatorname{rank}(A)$ equals the number of nonzero singular values of $A$.
3. **(Exam-style)** Show that $\|A\|_F^2 = \sum_i \sigma_i^2$ and $\|A\|_2 = \sigma_1$.
4. **(Application)** Given a data matrix $X \in \mathbb{R}^{n \times p}$, explain how the SVD of $X$ relates to Principal Component Analysis. Identify the principal components and principal directions in terms of $U$, $\Sigma$, and $V$.
5. **(Proof)** Prove the Eckart-Young-Mirsky theorem for the Frobenius norm.

### Problem Set 3: Variational Characterizations

1. **(cf. Horn &amp; Johnson §4.3)** Use the Courant-Fischer theorem to prove Weyl's inequality.
2. **(Exam-style)** Let $A$ be $n \times n$ positive semidefinite. Prove $\lambda_{\max}(A) = \max_{\|x\|=1} x^T A x$.
3. **(Exam-style)** Prove the Cauchy Interlacing Theorem using the Courant-Fischer min-max characterization.
4. **(Application)** Let $A = \begin{pmatrix} 4 & 1 \\ 1 & 3 \end{pmatrix}$ and $B = \begin{pmatrix} 0.01 & 0 \\ 0 & -0.02 \end{pmatrix}$. Apply Weyl's inequalities to bound the eigenvalues of $A + B$.
5. **(Challenge)** Prove that if $A$ is positive definite and $B$ is Hermitian, then the eigenvalues of $AB$ are real.

---

## Study Guide &amp; Exam Preparation

{: .important }
> **Key Theorems for the Introductory Exam (Linear Algebra Portion)**
>
> The following results must be mastered at the full-proof level:
> - **Spectral Theorem** — every Hermitian matrix is unitarily diagonalizable; real eigenvalues, orthogonal eigenvectors
> - **SVD** — existence, fundamental subspace interpretation, and the Eckart-Young low-rank approximation
> - **Courant-Fischer** — min-max characterization; use it to prove interlacing and Weyl's inequalities
> - **Cauchy Interlacing** — deletion of one row/column interlaces eigenvalues
> - **Perturbation bounds** — $|\sigma_i(A+E) - \sigma_i(A)| \leq \|E\|_2$

**Exam Preparation Tips**:
- Be able to state and prove the Spectral Theorem from scratch within 20 minutes.
- Practice computing SVDs of small ($2 \times 3$) matrices by hand.
- Know the relationship between eigenvalues of $A^*A$ and singular values of $A$.
- For Courant-Fischer problems: always use dimension counting to show that the relevant subspaces intersect nontrivially.
