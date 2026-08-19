---
layout: default
title: "EN.553.731 — Statistical Theory II"
parent: "Module C — Statistics & Statistical Learning"
nav_order: 2
permalink: /module_c/statistical_theory_2/
---

# EN.553.731 — Statistical Theory II

> *Hypothesis testing, the Neyman-Pearson framework, and the asymptotic theory of statistical inference. This course culminates in the fundamental result that the MLE achieves asymptotic efficiency: $\sqrt{n}(\hat{\theta}_n - \theta_0) \xrightarrow{d} N(0,\, I(\theta_0)^{-1})$.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Formulate and analyze hypothesis tests** within the Neyman-Pearson framework.
2. **Construct Uniformly Most Powerful (UMP) tests** for one-parameter families using the Karlin-Rubin theorem.
3. **Apply likelihood ratio tests** and derive their asymptotic distributions via Wilks' theorem.
4. **Prove consistency and asymptotic normality** of the MLE under regularity conditions.
5. **Construct confidence intervals** based on pivotal quantities and asymptotic distributions, including the delta method.

---

## Core Theory

### Unit 1: Hypothesis Testing Foundations

#### 1.1 The Neyman-Pearson Framework

A **hypothesis test** consists of:
- **Null hypothesis** $H_0: \theta \in \Theta_0$ vs. **alternative** $H_1: \theta \in \Theta_1 = \Theta \setminus \Theta_0$.
- A **test function** $\phi(x) = P(\text{reject } H_0 \mid X = x)$; for non-randomized tests, $\phi \in \{0, 1\}$.
- **Type I error**: $\alpha(\theta) = E_\theta[\phi(X)]$ for $\theta \in \Theta_0$. The **size** is $\sup_{\theta \in \Theta_0} \alpha(\theta)$.
- **Type II error**: $\beta(\theta) = 1 - E_\theta[\phi(X)]$ for $\theta \in \Theta_1$.
- **Power function**: $\pi(\theta) = E_\theta[\phi(X)]$.

#### 1.2 The Neyman-Pearson Lemma

**Theorem (Neyman-Pearson)**: For testing $H_0: \theta = \theta_0$ vs. $H_1: \theta = \theta_1$ (simple vs. simple), the **most powerful** test of size $\alpha$ is:

$$\phi(x) = \begin{cases} 1 & \text{if } \dfrac{f(x|\theta_1)}{f(x|\theta_0)} > k \\[6pt] \gamma & \text{if } \dfrac{f(x|\theta_1)}{f(x|\theta_0)} = k \\[6pt] 0 & \text{if } \dfrac{f(x|\theta_1)}{f(x|\theta_0)} < k \end{cases}$$

where $k \geq 0$ and $\gamma \in [0,1]$ are chosen so that $E_{\theta_0}[\phi(X)] = \alpha$.

*Proof*: Let $\phi^*$ be the NP test and $\phi$ any other test with $E_{\theta_0}[\phi] \leq \alpha$. Then:

$$E_{\theta_1}[\phi^*] - E_{\theta_1}[\phi] = \int (\phi^* - \phi)(f_1 - kf_0) \, d\mu \geq 0,$$

because on $\{\phi^* = 1\}$: $({\phi^* - \phi}) \geq 0$ and $(f_1 - kf_0) > 0$; on $\{\phi^* = 0\}$: $(\phi^* - \phi) \leq 0$ and $(f_1 - kf_0) < 0$. In both regions the integrand is nonnegative.

---

### Unit 2: UMP Tests and Monotone Likelihood Ratio

#### 2.1 Uniformly Most Powerful Tests

**Definition**: A test $\phi$ is **UMP** at level $\alpha$ for $H_0: \theta \leq \theta_0$ vs. $H_1: \theta > \theta_0$ if it is the most powerful test against every $\theta_1 > \theta_0$.

#### 2.2 Monotone Likelihood Ratio

**Definition**: A family $\{f(x|\theta)\}$ has **Monotone Likelihood Ratio (MLR)** in $T(x)$ if, for $\theta_1 > \theta_0$, the ratio $f(x|\theta_1)/f(x|\theta_0)$ is a nondecreasing function of $T(x)$.

**Theorem (Karlin-Rubin)**: If the family has MLR in $T(x)$, then the UMP level-$\alpha$ test for $H_0: \theta \leq \theta_0$ vs. $H_1: \theta > \theta_0$ is:

$$\phi(x) = \begin{cases} 1 & \text{if } T(x) > c \\ \gamma & \text{if } T(x) = c \\ 0 & \text{if } T(x) < c \end{cases}$$

where $c$ and $\gamma$ are chosen so the size equals $\alpha$.

**Key Fact**: Every one-parameter exponential family has MLR in the natural sufficient statistic.

#### 2.3 Limitations and Two-Sided Tests

For two-sided alternatives ($H_1: \theta \neq \theta_0$), UMP tests generally do not exist. Standard approaches include:
- **Unbiased tests**: Require $\pi(\theta) \geq \alpha$ for all $\theta \in \Theta_1$.
- **UMP unbiased (UMPU) tests**: Exist for exponential families via Neyman structure.
- **Likelihood ratio tests**: A general-purpose approach with known asymptotic behavior.

---

### Unit 3: Likelihood Ratio Tests

#### 3.1 The Generalized Likelihood Ratio Statistic

$$\Lambda(x) = \frac{\sup_{\theta \in \Theta_0} L(\theta|x)}{\sup_{\theta \in \Theta} L(\theta|x)}.$$

Reject $H_0$ when $\Lambda(x) \leq c$, equivalently when $-2\log\Lambda(x) \geq \chi^2_\alpha$.

#### 3.2 Wilks' Theorem

**Theorem (Wilks)**: Under $H_0$ and standard regularity conditions, if $\Theta_0$ is defined by $r$ smooth constraints on a $k$-dimensional parameter space:

$$-2 \log \Lambda(X) \xrightarrow{d} \chi^2_{k-r} \quad \text{as } n \to \infty.$$

This provides an asymptotic calibration for the LRT without requiring the exact null distribution.

#### 3.3 The Trinity of Asymptotically Equivalent Tests

Three tests that are asymptotically equivalent under $H_0$:

| Test | Statistic | Intuition |
|------|-----------|-----------|
| **Likelihood Ratio** | $-2\log\Lambda$ | Compare maximum likelihoods under $H_0$ vs. $\Theta$ |
| **Wald** | $(\hat{\theta} - \theta_0)^T I(\hat{\theta})(\hat{\theta} - \theta_0)$ | Is the MLE far from $\theta_0$? |
| **Score (Rao)** | $S(\theta_0)^T I(\theta_0)^{-1} S(\theta_0)$ | Is the score nonzero when evaluated at $\theta_0$? |

All three converge in distribution to $\chi^2_{k-r}$ under $H_0$.

---

### Unit 4: Asymptotic Theory of Estimation

#### 4.1 Consistency of the MLE

**Theorem**: Under regularity conditions, $\hat{\theta}_{\text{MLE}} \xrightarrow{P} \theta_0$.

*Proof Strategy*: The normalized log-likelihood $\frac{1}{n}\ell_n(\theta) - \frac{1}{n}\ell_n(\theta_0)$ converges uniformly (by the SLLN) to $E_{\theta_0}[\log f(X|\theta)/f(X|\theta_0)]$, which equals the negative Kullback-Leibler divergence $-D_{\text{KL}}(\theta_0 \| \theta) \leq 0$, with equality if and only if $\theta = \theta_0$.

#### 4.2 Asymptotic Normality of the MLE

**Theorem**: Under regularity conditions:

$$\sqrt{n}(\hat{\theta}_n - \theta_0) \xrightarrow{d} N(0, I(\theta_0)^{-1}),$$

where $I(\theta_0)$ is the Fisher Information at the true parameter.

*Proof Sketch (Score Expansion)*: Taylor-expand the score at $\hat{\theta}_n$:

$$0 = \frac{1}{\sqrt{n}} S_n(\hat{\theta}_n) = \frac{1}{\sqrt{n}} S_n(\theta_0) + \frac{1}{n} S_n'(\tilde{\theta}_n) \cdot \sqrt{n}(\hat{\theta}_n - \theta_0),$$

where $\tilde{\theta}_n$ lies between $\hat{\theta}_n$ and $\theta_0$. By the CLT, $\frac{1}{\sqrt{n}} S_n(\theta_0) \xrightarrow{d} N(0, I(\theta_0))$. By the SLLN, $\frac{1}{n} S_n'(\tilde{\theta}_n) \xrightarrow{P} -I(\theta_0)$. Solving:

$$\sqrt{n}(\hat{\theta}_n - \theta_0) \approx I(\theta_0)^{-1} \cdot \frac{1}{\sqrt{n}} S_n(\theta_0) \xrightarrow{d} N(0, I(\theta_0)^{-1}).$$

#### 4.3 Asymptotic Efficiency

**Definition**: An estimator $\tilde{\theta}_n$ is **asymptotically efficient** if $\sqrt{n}(\tilde{\theta}_n - \theta_0) \xrightarrow{d} N(0, I(\theta_0)^{-1})$, achieving the Cramér-Rao bound in the limit.

**Result**: The MLE is asymptotically efficient under regularity conditions — it is asymptotically optimal among all regular estimators.

#### 4.4 The Delta Method

**Theorem**: If $\sqrt{n}(\hat{\theta}_n - \theta) \xrightarrow{d} N(0, \sigma^2)$ and $g$ is differentiable at $\theta$ with $g'(\theta) \neq 0$, then:

$$\sqrt{n}(g(\hat{\theta}_n) - g(\theta)) \xrightarrow{d} N(0, [g'(\theta)]^2 \sigma^2).$$

---

### Unit 5: Confidence Intervals and Regions

#### 5.1 Pivotal Quantities

A **pivotal quantity** $Q(X, \theta)$ has a distribution that does not depend on $\theta$.

**Example**: For $X_i \overset{\text{iid}}{\sim} N(\mu, \sigma^2)$ with $\sigma^2$ unknown, $T = \frac{\bar{X} - \mu}{S/\sqrt{n}} \sim t_{n-1}$, yielding the exact $100(1-\alpha)\%$ confidence interval:

$$\bar{X} \pm t_{\alpha/2,\, n-1} \frac{S}{\sqrt{n}}.$$

#### 5.2 Asymptotic Confidence Intervals

Using MLE asymptotics, an approximate $100(1-\alpha)\%$ confidence interval for $\theta$ is:

$$\hat{\theta}_n \pm z_{\alpha/2} \sqrt{\frac{1}{n I(\hat{\theta}_n)}}.$$

By the delta method, an interval for $g(\theta)$ is:

$$g(\hat{\theta}_n) \pm z_{\alpha/2}\, |g'(\hat{\theta}_n)| \sqrt{\frac{1}{n I(\hat{\theta}_n)}}.$$

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Statistical Inference* (2nd ed.) | George Casella &amp; Roger L. Berger | **Primary** — Chapters 8–10 |
| *Testing Statistical Hypotheses* (3rd ed.) | E.L. Lehmann &amp; Joseph Romano | **Advanced** — The definitive reference on hypothesis testing |
| *Asymptotic Statistics* | A.W. van der Vaart | **Advanced** — Rigorous treatment of MLE asymptotics and efficiency |
| *Mathematical Statistics* | Jun Shao | **Supplementary** — Comprehensive reference |

---

## Problem Sets

### Problem Set 1: Neyman-Pearson and UMP Tests

1. **(Casella &amp; Berger 8.3)** Derive the most powerful test of $H_0: \mu = 0$ vs. $H_1: \mu = 1$ for $N(\mu, 1)$ data at level $\alpha = 0.05$.
2. **(Exam-style)** Prove the Neyman-Pearson Lemma.
3. **(Exam-style)** Show that the Poisson family has MLR in $\sum X_i$ and derive the UMP test for $H_0: \lambda \leq \lambda_0$ vs. $H_1: \lambda > \lambda_0$.
4. **(Proof)** Prove that for exponential families with natural parameter $\eta(\theta)$ increasing in $\theta$, the UMP test rejects for large values of the natural sufficient statistic.
5. **(Challenge)** Show that no UMP test exists for $H_0: \mu = 0$ vs. $H_1: \mu \neq 0$ in the $N(\mu, 1)$ family.

### Problem Set 2: Likelihood Ratio Tests

1. **(Casella &amp; Berger 8.2)** Derive the LRT for $H_0: \mu = \mu_0$ vs. $H_1: \mu \neq \mu_0$ when $X_i \overset{\text{iid}}{\sim} N(\mu, \sigma^2)$ with $\sigma^2$ known.
2. **(Exam-style)** Prove Wilks' theorem in the scalar ($k=1, r=1$) case.
3. **(Exam-style)** Construct the LRT for independence in a $2 \times 2$ contingency table.
4. **(Application)** Compare the Wald, Score, and LRT statistics for testing $p = 1/2$ vs. $p \neq 1/2$ in a $\operatorname{Binomial}(n, p)$ model.
5. **(Proof)** Show that the three test statistics (Wald, Score, LRT) are asymptotically equivalent under $H_0$.

### Problem Set 3: MLE Asymptotics

1. **(van der Vaart, Ch. 5)** Prove the consistency of the MLE using the Kullback-Leibler divergence argument.
2. **(Exam-style)** Derive the asymptotic distribution $\sqrt{n}(\hat{p} - p) \xrightarrow{d} N(0, p(1-p))$ for $\hat{p} = \bar{X}$ when $X_i \overset{\text{iid}}{\sim} \operatorname{Bernoulli}(p)$.
3. **(Exam-style)** Use the delta method to find the asymptotic distribution of $\log(\hat{p})$ and construct an approximate 95% confidence interval for $\log(p)$.
4. **(Proof)** Prove asymptotic normality of the MLE via the score function Taylor expansion.
5. **(Challenge)** Show that the MLE is not always consistent: consider $X_i \overset{\text{iid}}{\sim} \operatorname{Uniform}(0, \theta)$ and discuss why the standard regularity conditions fail.

---

## Study Guide &amp; Exam Preparation

> [!IMPORTANT]
> **Key Theorems for Statistical Theory II**
>
> - **Neyman-Pearson Lemma** — most powerful test for simple vs. simple hypotheses; full proof required
> - **Karlin-Rubin Theorem** — MLR $\Rightarrow$ UMP test; know what MLR means and verify it for exponential families
> - **Wilks' Theorem** — $-2\log\Lambda \xrightarrow{d} \chi^2_{k-r}$; know the degrees-of-freedom formula
> - **Consistency of MLE** — KL divergence argument; identify where $D_{\text{KL}}(\theta_0 \| \theta) = 0$
> - **Asymptotic Normality of MLE** — score expansion proof; know both CLT and LLN roles
> - **Delta Method** — linearization; apply to get asymptotic intervals for transformations of $\theta$

**Proof-Writing Strategy**:
- For NP problems, always verify the size condition explicitly.
- For Wilks, state the regularity conditions and the $\chi^2$ degrees of freedom.
- For MLE asymptotics, the two key ingredients are: (i) CLT applied to the score, (ii) LLN applied to the observed information.
