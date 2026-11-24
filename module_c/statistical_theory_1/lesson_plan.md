---
layout: default
title: "EN.553.730 — Statistical Theory I"
parent: "Module C — Statistics & Statistical Learning"
nav_order: 1
permalink: /module_c/statistical_theory_1/
---

# EN.553.730 — Statistical Theory I

> *The mathematical theory of statistical inference. This course develops the Sufficiency Principle, exponential families, Fisher Information, the Cramér-Rao lower bound, and the theory of optimal estimation — establishing the principled foundation for how to extract information from data.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Define and identify sufficient statistics** using the Fisher-Neyman factorization criterion.
2. **Work with exponential families**: identify natural parameters, derive moment formulas from the log-partition function, and establish completeness.
3. **Compute Fisher Information** and apply the Cramér-Rao lower bound to assess estimator optimality.
4. **Construct and evaluate unbiased estimators** using the Rao-Blackwell theorem and the Lehmann-Scheffé theorem.
5. **Derive maximum likelihood estimators** and characterize their large-sample properties.

---

## Core Theory

### Unit 1: Sufficiency and Minimal Sufficiency

#### 1.1 The Sufficiency Principle

**Definition**: A statistic $T(X)$ is **sufficient** for a parameter $\theta$ if the conditional distribution of $X$ given $T(X) = t$ does not depend on $\theta$.

**Intuition**: $T$ captures all information in the data $X$ that is relevant to $\theta$. Once $T$ is known, the remaining variation in the data carries no further information about the parameter.

**Theorem (Fisher-Neyman Factorization)**: $T(X)$ is sufficient for $\theta$ if and only if the density (or pmf) factorizes as:

$$f(x|\theta) = g(T(x), \theta) \cdot h(x),$$

where $g$ depends on $x$ only through $T(x)$, and $h$ does not depend on $\theta$.

*Proof sketch (discrete case)*: By definition, $f(x|\theta) = P(X = x | T = T(x), \theta) \cdot P(T = T(x) | \theta)$. Sufficiency means the first factor $P(X=x|T=T(x),\theta) = h(x)$ is free of $\theta$, and we set $g(T(x),\theta) = P(T=T(x)|\theta)$.

**Example**: For $X_1, \ldots, X_n \overset{\text{iid}}{\sim} N(\mu, \sigma^2)$ with $\sigma^2$ known, $T = \bar{X}$ is sufficient for $\mu$:

$$\prod_{i=1}^n f(x_i|\mu) \propto \exp\!\left(-\frac{n}{2\sigma^2}(\bar{x} - \mu)^2\right) \cdot \exp\!\left(-\frac{1}{2\sigma^2}\sum(x_i - \bar{x})^2\right).$$

The second factor depends only on the data (not on $\mu$), confirming sufficiency by factorization.

#### 1.2 Minimal Sufficiency

**Definition**: A sufficient statistic $T$ is **minimal sufficient** if it is a function of every other sufficient statistic — it achieves the maximum possible data reduction while retaining all information about $\theta$.

**Theorem (Lehmann-Scheffé Criterion)**: Suppose that for every pair of sample points $x, y$,

$$\frac{f(x|\theta)}{f(y|\theta)} \text{ is constant as a function of } \theta \quad\Longleftrightarrow\quad T(x) = T(y).$$

Then $T(X)$ is minimal sufficient. Both directions matter: "$\Leftarrow$" gives sufficiency (via factorization), and "$\Rightarrow$" gives minimality.

#### 1.3 Completeness

**Definition**: A statistic $T$ is **complete** if $E_\theta[g(T)] = 0$ for all $\theta$ implies $g(T) = 0$ a.s. under all $\theta$.

**Theorem (Bahadur)**: If a minimal sufficient statistic exists, then any complete sufficient statistic is minimal sufficient. (The existence hypothesis holds in every standard model, e.g. whenever the family is dominated by a $\sigma$-finite measure on $\mathbb{R}^n$.)

**Theorem (Basu)**: If $T$ is complete sufficient and $V$ is ancillary (its distribution does not depend on $\theta$), then $T$ and $V$ are independent. This is the cleanest proof that $\bar{X}$ and $S^2$ are independent for normal samples.

---

### Unit 2: Exponential Families

#### 2.1 Definition

A family of distributions is a **$k$-parameter exponential family** if the density takes the form:

$$f(x|\boldsymbol{\eta}) = h(x) \exp\!\left(\sum_{j=1}^k \eta_j T_j(x) - A(\boldsymbol{\eta})\right),$$

where $\boldsymbol{\eta} = (\eta_1, \ldots, \eta_k)$ are the **natural parameters**, $T_j(x)$ are the **natural sufficient statistics**, and $A(\boldsymbol{\eta})$ is the **log-partition function** (or cumulant generating function).

#### 2.2 Key Properties

1. **Sufficiency**: $(T_1(X), \ldots, T_k(X))$ is sufficient by the Factorization Theorem.
2. **Moment generation from $A$**: $E[T_j] = \frac{\partial A}{\partial \eta_j}$ and $\operatorname{Cov}(T_i, T_j) = \frac{\partial^2 A}{\partial \eta_i \partial \eta_j}$.
3. **Completeness**: If the natural parameter space contains an open set in $\mathbb{R}^k$ (a *full-rank* family), then $T = (T_1, \ldots, T_k)$ is a complete sufficient statistic. Curved families (e.g. $N(\theta, \theta^2)$) fail this condition, and their natural statistic is typically not complete.
4. **Convexity**: $A(\boldsymbol{\eta})$ is convex, and the natural parameter space is convex.
5. **MLE existence**: For a full-rank family with open natural parameter space, if the observed average $\bar{T} = \frac{1}{n}\sum_i T(X_i)$ lies in the interior of the convex hull of the support of $T$, the MLE exists, is unique, and solves the moment equations $\nabla A(\hat{\boldsymbol{\eta}}) = E_{\hat{\boldsymbol{\eta}}}[T] = \bar{T}$.

**Examples**: The Normal, Poisson, Binomial, Gamma, Beta, and Multinomial families are all exponential families. The Cauchy distribution is not.

---

### Unit 3: Fisher Information and the Cramér-Rao Lower Bound

#### 3.1 The Score Function and Fisher Information

The **score function** is $S(\theta) = \frac{\partial}{\partial \theta} \log f(X|\theta)$.

Under regularity conditions: $E_\theta[S(\theta)] = 0$ and the **Fisher Information** satisfies three equivalent expressions:

$$I(\theta) = E_\theta[S(\theta)^2] = \operatorname{Var}_\theta(S(\theta)) = -E_\theta\!\left[\frac{\partial^2}{\partial \theta^2} \log f(X|\theta)\right].$$

For $n$ i.i.d. observations: $I_n(\theta) = n I_1(\theta)$.

#### 3.2 The Cramér-Rao Lower Bound

**Theorem**: Let $T(X)$ be an unbiased estimator of $g(\theta)$ with finite variance. Under standard regularity conditions:

$$\operatorname{Var}_\theta(T) \geq \frac{[g'(\theta)]^2}{I_n(\theta)}.$$

For the special case $g(\theta) = \theta$ (estimating $\theta$ itself):

$$\operatorname{Var}_\theta(T) \geq \frac{1}{n I_1(\theta)}.$$

*Proof*: The Cauchy-Schwarz inequality applied to $\operatorname{Cov}(T, S)$:

$$[g'(\theta)]^2 = [\operatorname{Cov}(T, S)]^2 \leq \operatorname{Var}(T) \cdot \operatorname{Var}(S) = \operatorname{Var}(T) \cdot I_n(\theta).$$

An estimator that achieves the CRLB at every $\theta$ is called **efficient**.

#### 3.3 Multivariate Fisher Information

For $\boldsymbol{\theta} \in \mathbb{R}^k$, the Fisher Information is the $k \times k$ matrix:

$$[I(\boldsymbol{\theta})]_{ij} = E\!\left[\frac{\partial \log f}{\partial \theta_i} \cdot \frac{\partial \log f}{\partial \theta_j}\right] = -E\!\left[\frac{\partial^2 \log f}{\partial \theta_i \partial \theta_j}\right].$$

The multivariate CRLB states $\operatorname{Var}(\hat{\boldsymbol{\theta}}) \succeq I(\boldsymbol{\theta})^{-1}$ (the difference is positive semidefinite).

---

### Unit 4: Optimal Estimation

#### 4.1 The Rao-Blackwell Theorem

**Theorem**: Let $\hat{\theta}$ be an unbiased estimator of $\theta$ and $T$ a sufficient statistic. Define the Rao-Blackwell estimator $\tilde{\theta} = E[\hat{\theta}|T]$. Then:

1. $\tilde{\theta}$ is unbiased: $E[\tilde{\theta}] = \theta$.
2. $\operatorname{Var}(\tilde{\theta}) \leq \operatorname{Var}(\hat{\theta})$, with equality if and only if $\hat{\theta}$ is already a function of $T$.

*Proof*: Unbiasedness follows from the tower property. Variance reduction follows from the law of total variance:

$$\operatorname{Var}(\hat{\theta}) = \operatorname{Var}(\tilde{\theta}) + E[\operatorname{Var}(\hat{\theta}|T)] \geq \operatorname{Var}(\tilde{\theta}).$$

#### 4.2 The Lehmann-Scheffé Theorem

**Theorem**: If $T$ is a complete sufficient statistic and $\tilde{\theta} = g(T)$ is unbiased for $\theta$, then $\tilde{\theta}$ is the **unique** unbiased estimator that is a function of $T$, and it is the **Uniformly Minimum Variance Unbiased Estimator (UMVUE)**.

*Proof*: If $\tilde{\theta}_1$ and $\tilde{\theta}_2$ are both unbiased functions of $T$, then $E[\tilde{\theta}_1 - \tilde{\theta}_2] = 0$ for all $\theta$. Completeness gives $\tilde{\theta}_1 = \tilde{\theta}_2$ a.s. By Rao-Blackwell, the UMVUE has the smallest variance among all unbiased estimators.

#### 4.3 Maximum Likelihood Estimation

**Definition**: The **MLE** is $\hat{\theta}_{\text{MLE}} = \arg\max_\theta L(\theta|x) = \arg\max_\theta \prod_{i=1}^n f(x_i|\theta)$.

**Invariance**: If $\hat{\theta}$ is the MLE of $\theta$, then $g(\hat{\theta})$ is the MLE of $g(\theta)$ for any function $g$.

**Asymptotic Properties** (under regularity conditions):
1. **Consistency**: $\hat{\theta}_n \xrightarrow{P} \theta_0$.
2. **Asymptotic normality**: $\sqrt{n}(\hat{\theta}_n - \theta_0) \xrightarrow{d} N(0, I(\theta_0)^{-1})$.
3. **Asymptotic efficiency**: The MLE achieves the CRLB asymptotically.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Statistical Inference* (2nd ed.) | George Casella &amp; Roger L. Berger | **Primary** — Chapters 5–7 |
| *Theory of Point Estimation* (2nd ed.) | E.L. Lehmann &amp; George Casella | **Advanced** — The definitive reference on estimation theory |
| *Mathematical Statistics: Basic Ideas and Selected Topics* Vol. I | Peter Bickel &amp; Kjell Doksum | **Supplementary** — Clear, modern treatment of estimation |
| *All of Statistics* | Larry Wasserman | **Review** — Concise overview suitable for rapid revision |

---

## Problem Sets

### Problem Set 1: Sufficiency and Exponential Families

1. **(cf. Casella &amp; Berger §6.2)** Find a sufficient statistic for $\theta$ when $X_1, \ldots, X_n \overset{\text{iid}}{\sim} \operatorname{Uniform}(0, \theta)$. Is it minimal sufficient?
2. **(Exam-style)** Show that the $\operatorname{Poisson}(\lambda)$ family is a one-parameter exponential family. Identify the natural parameter, natural sufficient statistic, and log-partition function.
3. **(Exam-style)** Prove that a complete sufficient statistic is minimal sufficient.
4. **(Proof)** Let $X_1, \ldots, X_n \overset{\text{iid}}{\sim} N(\mu, \sigma^2)$. Show that $(\bar{X}, S^2)$ is jointly sufficient for $(\mu, \sigma^2)$.
5. **(Challenge)** Prove that the Cauchy location family is not an exponential family.

### Problem Set 2: Fisher Information and Cramér-Rao

1. **(cf. Casella &amp; Berger §7.3)** Compute the Fisher Information $I(\theta)$ when $X \sim \operatorname{Binomial}(n, \theta)$.
2. **(Exam-style)** Prove the Cramér-Rao lower bound using the Cauchy-Schwarz inequality.
3. **(Exam-style)** Find the CRLB for unbiased estimators of $\lambda$ when $X_1, \ldots, X_n \overset{\text{iid}}{\sim} \operatorname{Poisson}(\lambda)$. Show that $\bar{X}$ achieves this bound.
4. **(Proof)** Show that the two forms of Fisher Information are equal — $E[S^2]$ and $-E[\partial^2 \ell / \partial\theta^2]$ — under appropriate regularity conditions (interchange of derivative and integral).
5. **(Application)** Compute the multivariate Fisher Information matrix for $(\mu, \sigma^2)$ in the $N(\mu, \sigma^2)$ family.

### Problem Set 3: Optimal Estimation

1. **(cf. Casella &amp; Berger §7.3)** Use Rao-Blackwell to improve the estimator $\hat{\lambda} = X_1$ for $\lambda$ when $X_i \overset{\text{iid}}{\sim} \operatorname{Poisson}(\lambda)$.
2. **(Exam-style)** Find the UMVUE of $\theta^2$ when $X_1, \ldots, X_n \overset{\text{iid}}{\sim} N(\theta, 1)$ using the Lehmann-Scheffé theorem.
3. **(Exam-style)** Compute the MLE of $(\mu, \sigma^2)$ for a $N(\mu, \sigma^2)$ sample. Show that the MLE of $\sigma^2$ is biased.
4. **(Proof)** Prove the invariance property of MLEs.
5. **(Challenge)** Let $X = (X_1, \ldots, X_p) \sim N_p(\theta, I_p)$ under squared-error loss $\|\hat{\theta} - \theta\|^2$. (a) For $p = 1$, show that $\hat{\theta} = X$ is admissible (e.g. via a limiting-Bayes argument). (b) For $p \geq 3$, use Stein's lemma $E[(X_i - \theta_i) g(X)] = E[\partial_i g(X)]$ to show that the James-Stein estimator $\hat{\theta}_{JS} = \left(1 - \frac{p-2}{\|X\|^2}\right)X$ has strictly smaller risk than $X$ for every $\theta$, so the MLE is inadmissible. ($X$ is also admissible when $p = 2$.)

---

## Study Guide &amp; Exam Preparation

{: .important }
> **Key Theorems for Statistical Theory I**
>
> - **Fisher-Neyman Factorization** — the primary tool for identifying sufficient statistics
> - **Lehmann-Scheffé Criterion** — characterizing minimal sufficiency via likelihood ratios
> - **Completeness** — $E_\theta[g(T)] = 0 \;\forall\theta \Rightarrow g(T) = 0$ a.s.; key to UMVUE uniqueness
> - **Cramér-Rao Lower Bound** — Cauchy-Schwarz proof; recognize when equality holds
> - **Rao-Blackwell** — conditioning on a sufficient statistic never increases variance
> - **Lehmann-Scheffé** — unique unbiased function of a complete sufficient statistic is the UMVUE

**Common Exam Tasks**:
- *"Find the UMVUE of $g(\theta)$"*: First find a complete sufficient statistic, then find an unbiased function of it.
- *"Show $T$ is sufficient"*: Use the Factorization Theorem; write the joint density as $g(T(x), \theta) \cdot h(x)$.
- *"Compute the CRLB"*: Calculate $I(\theta)$ via either formula; apply the bound $[g'(\theta)]^2 / I_n(\theta)$.
