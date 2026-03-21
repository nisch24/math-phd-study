---
layout: default
title: "EN.553.730 — Statistical Theory I"
parent: "Module C — Statistics & Statistical Learning"
nav_order: 1
permalink: /module_c/statistical_theory_1/
---

# EN.553.730 — Statistical Theory I

> *The mathematical theory of statistical inference. This course covers the Sufficiency Principle, exponential families, Fisher Information, the Cramér-Rao bound, and the theory of optimal estimation — establishing the principled foundation for how to extract information from data.*

---

## Learning Objectives

1. **Define and identify sufficient statistics** using the factorization criterion.
2. **Work with exponential families** and derive their canonical properties.
3. **Compute Fisher Information** and apply the Cramér-Rao lower bound.
4. **Construct and evaluate unbiased estimators** using Rao-Blackwell and Lehmann-Scheffé.
5. **Derive maximum likelihood estimators** and analyze their properties.

---

## Core Theory

### Unit 1: Sufficiency and Minimal Sufficiency

#### 1.1 The Sufficiency Principle

**Definition**: A statistic $T(X)$ is **sufficient** for a parameter $\theta$ if the conditional distribution of $X$ given $T(X) = t$ does not depend on $\theta$.

**Intuition**: $T$ captures all the information in the data $X$ relevant to $\theta$. Once you know $T$, the remaining data is just noise unrelated to the parameter.

**Theorem (Fisher-Neyman Factorization)**: $T(X)$ is sufficient for $\theta$ if and only if the density/pmf can be written as:

$$f(x|\theta) = g(T(x), \theta) \cdot h(x)$$

where $g$ depends on $x$ only through $T(x)$, and $h$ does not depend on $\theta$.

*Proof sketch (discrete case)*: By definition, $f(x|\theta) = P(X = x | T = T(x), \theta) \cdot P(T = T(x) | \theta)$. Sufficiency means $P(X=x|T=T(x),\theta) = h(x)$ does not depend on $\theta$, so set $g(T(x),\theta) = P(T=T(x)|\theta)$.

**Example**: For $X_1, \ldots, X_n \overset{\text{iid}}{\sim} N(\mu, \sigma^2)$ with $\sigma^2$ known, $T = \bar{X}$ is sufficient for $\mu$ since:

$$\prod_{i=1}^n f(x_i|\mu) \propto \exp\left(-\frac{n}{2\sigma^2}(\bar{x} - \mu)^2\right) \cdot \exp\left(-\frac{1}{2\sigma^2}\sum(x_i - \bar{x})^2\right)$$

#### 1.2 Minimal Sufficiency

**Definition**: A sufficient statistic $T$ is **minimal sufficient** if for every other sufficient statistic $T'$, $T$ is a function of $T'$. Minimal sufficient statistics achieve the greatest possible data reduction.

**Theorem (Lehmann-Scheffé criterion)**: $T(X)$ is minimal sufficient if $T(x) = T(y)$ whenever $\frac{f(x|\theta)}{f(y|\theta)}$ is constant as a function of $\theta$.

#### 1.3 Completeness

**Definition**: A statistic $T$ is **complete** if $E_\theta[g(T)] = 0$ for all $\theta$ implies $g(T) = 0$ a.s. for all $\theta$.

**Theorem (Bahadur)**: A complete sufficient statistic is minimal sufficient.

---

### Unit 2: Exponential Families

#### 2.1 Definition

A family of distributions is a **$k$-parameter exponential family** if the density can be written:

$$f(x|\boldsymbol{\eta}) = h(x) \exp\left(\sum_{j=1}^k \eta_j T_j(x) - A(\boldsymbol{\eta})\right)$$

where $\boldsymbol{\eta} = (\eta_1, \ldots, \eta_k)$ are the **natural parameters**, $T_j(x)$ are the **natural sufficient statistics**, and $A(\boldsymbol{\eta})$ is the **log-partition function** (cumulant generating function).

#### 2.2 Key Properties

1. **Sufficient statistic**: $(T_1(X), \ldots, T_k(X))$ is sufficient (by factorization).
2. **Moments from $A$**: $E[T_j] = \frac{\partial A}{\partial \eta_j}$ and $\text{Cov}(T_i, T_j) = \frac{\partial^2 A}{\partial \eta_i \partial \eta_j}$.
3. **Completeness**: If the natural parameter space contains an open set in $\mathbb{R}^k$, the family is **complete**.
4. **Convexity**: $A(\boldsymbol{\eta})$ is convex, and the natural parameter space is convex.
5. **MLE existence**: If the observed $T$ is in the interior of the convex hull of the support of $T$, the MLE exists and satisfies the moment equations $E_{\hat{\theta}}[T] = T_{\text{obs}}$.

**Examples**: Normal, Poisson, Binomial, Gamma, Beta, Multinomial are all exponential families. The Cauchy distribution is not.

---

### Unit 3: Fisher Information and the Cramér-Rao Bound

#### 3.1 The Score Function and Fisher Information

The **score function**: $S(\theta) = \frac{\partial}{\partial \theta} \log f(X|\theta)$

Under regularity conditions: $E_\theta[S(\theta)] = 0$ and the **Fisher Information** is:

$$I(\theta) = E_\theta[S(\theta)^2] = \text{Var}_\theta(S(\theta)) = -E_\theta\left[\frac{\partial^2}{\partial \theta^2} \log f(X|\theta)\right]$$

For $n$ i.i.d. observations: $I_n(\theta) = n I_1(\theta)$.

**For exponential families**: $I(\theta) = \frac{\partial^2 A}{\partial \theta^2} = \text{Var}_\theta(T)$ (related via the natural parameterization).

#### 3.2 The Cramér-Rao Lower Bound

**Theorem**: Let $T(X)$ be an unbiased estimator of $g(\theta)$ with finite variance. Under regularity conditions:

$$\text{Var}_\theta(T) \geq \frac{[g'(\theta)]^2}{I_n(\theta)}$$

If $g(\theta) = \theta$ (unbiased for $\theta$ itself):

$$\text{Var}_\theta(T) \geq \frac{1}{nI_1(\theta)}$$

*Proof*: Apply Cauchy-Schwarz: $[g'(\theta)]^2 = [\text{Cov}(T, S)]^2 \leq \text{Var}(T) \cdot \text{Var}(S) = \text{Var}(T) \cdot I_n(\theta)$.

An estimator achieving the CRLB is called **efficient**.

#### 3.3 Multivariate Fisher Information

For $\boldsymbol{\theta} \in \mathbb{R}^k$, the Fisher Information is the $k \times k$ matrix:

$$[I(\boldsymbol{\theta})]_{ij} = E\left[\frac{\partial \log f}{\partial \theta_i} \cdot \frac{\partial \log f}{\partial \theta_j}\right] = -E\left[\frac{\partial^2 \log f}{\partial \theta_i \partial \theta_j}\right]$$

The multivariate CRLB: $\text{Var}(\hat{\theta}) \succeq I(\boldsymbol{\theta})^{-1}$ (matrix inequality: the difference is positive semidefinite).

---

### Unit 4: Optimal Estimation

#### 4.1 The Rao-Blackwell Theorem

**Theorem**: Let $\hat{\theta}$ be an unbiased estimator of $\theta$ and $T$ a sufficient statistic. Define $\tilde{\theta} = E[\hat{\theta}|T]$. Then:

1. $\tilde{\theta}$ is unbiased for $\theta$.
2. $\text{Var}(\tilde{\theta}) \leq \text{Var}(\hat{\theta})$ (with equality iff $\hat{\theta}$ is already a function of $T$).

*Proof*: Unbiasedness: $E[\tilde{\theta}] = E[E[\hat{\theta}|T]] = E[\hat{\theta}] = \theta$. Variance reduction: $\text{Var}(\hat{\theta}) = \text{Var}(\tilde{\theta}) + E[\text{Var}(\hat{\theta}|T)] \geq \text{Var}(\tilde{\theta})$ by the law of total variance.

#### 4.2 The Lehmann-Scheffé Theorem

**Theorem**: If $T$ is a complete sufficient statistic and $\tilde{\theta} = g(T)$ is unbiased for $\theta$, then $\tilde{\theta}$ is the **unique** unbiased estimator that is a function of $T$, and it is the **Uniformly Minimum Variance Unbiased Estimator (UMVUE)**.

*Proof*: If $\tilde{\theta}_1$ and $\tilde{\theta}_2$ are both unbiased functions of $T$, then $E[\tilde{\theta}_1 - \tilde{\theta}_2] = 0$ for all $\theta$. By completeness, $\tilde{\theta}_1 = \tilde{\theta}_2$ a.s. By Rao-Blackwell, any function of a complete sufficient statistic has variance $\leq$ any other unbiased estimator.

#### 4.3 Maximum Likelihood Estimation

**Definition**: The **MLE** is $\hat{\theta}_{\text{MLE}} = \arg\max_\theta L(\theta|x) = \arg\max_\theta \prod_{i=1}^n f(x_i|\theta)$.

**Invariance**: If $\hat{\theta}$ is the MLE of $\theta$, then $g(\hat{\theta})$ is the MLE of $g(\theta)$.

**Properties** (under regularity conditions):
1. **Consistency**: $\hat{\theta}_n \xrightarrow{P} \theta_0$.
2. **Asymptotic normality**: $\sqrt{n}(\hat{\theta}_n - \theta_0) \xrightarrow{d} N(0, I(\theta_0)^{-1})$.
3. **Asymptotic efficiency**: The MLE achieves the CRLB asymptotically.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Statistical Inference* (2nd ed.) | George Casella & Roger L. Berger | **Primary** — Chapters 5–7 |
| *Theory of Point Estimation* (2nd ed.) | E.L. Lehmann & George Casella | **Advanced** — Comprehensive estimation theory |
| *Mathematical Statistics: Basic Ideas and Selected Topics* Vol. I | Peter Bickel & Kjell Doksum | **Supplementary** — Clear treatment of estimation |
| *All of Statistics* | Larry Wasserman | **Review** — Concise overview |

---

## Problem Sets

### Problem Set 1: Sufficiency and Exponential Families

1. **(Casella & Berger 6.2)** Find a sufficient statistic for $\theta$ when $X_1, \ldots, X_n \sim \text{Uniform}(0, \theta)$. Is it minimal sufficient?
2. **(Exam-style)** Show that the family $\text{Poisson}(\lambda)$ is a one-parameter exponential family. Identify the natural parameter, natural sufficient statistic, and log-partition function.
3. **(Exam-style)** Prove that a complete sufficient statistic is minimal sufficient.
4. **(Proof)** Let $X_1, \ldots, X_n \sim N(\mu, \sigma^2)$. Show that $(\bar{X}, S^2)$ is jointly sufficient for $(\mu, \sigma^2)$.
5. **(Challenge)** Prove that the Cauchy location family is not an exponential family.

### Problem Set 2: Fisher Information and Cramér-Rao

1. **(Casella & Berger 7.7)** Compute the Fisher Information for $\theta$ when $X \sim \text{Binomial}(n, \theta)$.
2. **(Exam-style)** Prove the Cramér-Rao lower bound using Cauchy-Schwarz.
3. **(Exam-style)** Find the CRLB for unbiased estimators of $\lambda$ when $X_1, \ldots, X_n \sim \text{Poisson}(\lambda)$. Show that $\bar{X}$ achieves this bound.
4. **(Proof)** Show that the second form of Fisher Information ($-E[\partial^2 \ell / \partial \theta^2]$) equals the first form ($E[S^2]$) under appropriate regularity conditions.
5. **(Application)** Compute the multivariate Fisher Information matrix for $(\mu, \sigma^2)$ in the $N(\mu, \sigma^2)$ family.

### Problem Set 3: Optimal Estimation

1. **(Casella & Berger 7.9)** Use Rao-Blackwell to improve the estimator $\hat{\theta} = X_1$ for $\lambda$ when $X_i \sim \text{Poisson}(\lambda)$.
2. **(Exam-style)** Find the UMVUE of $\theta^2$ when $X_1, \ldots, X_n \sim N(\theta, 1)$ using Lehmann-Scheffé.
3. **(Exam-style)** Compute the MLE of $(\mu, \sigma^2)$ for a $N(\mu, \sigma^2)$ sample. Show the MLE of $\sigma^2$ is biased.
4. **(Proof)** Prove the invariance property of MLEs.
5. **(Challenge)** Consider $X \sim N(\theta, 1)$ and estimating $\theta$ under squared error loss. Show that the MLE $\hat{\theta} = X$ is admissible but the James-Stein estimator dominates $\hat{\theta} = (X_1, \ldots, X_p)$ when $p \geq 3$.
