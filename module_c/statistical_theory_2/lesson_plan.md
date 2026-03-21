---
layout: default
title: "EN.553.731 — Statistical Theory II"
parent: "Module C — Statistics & Statistical Learning"
nav_order: 2
---

# EN.553.731 — Statistical Theory II

> *Hypothesis testing, the Neyman-Pearson framework, and the asymptotic theory of statistical inference. This course culminates in the fundamental result that the MLE achieves asymptotic efficiency: $\sqrt{n}(\hat{\theta} - \theta) \xrightarrow{d} N(0, I(\theta)^{-1})$.*

---

## Learning Objectives

1. **Formulate and test hypotheses** using the Neyman-Pearson framework.
2. **Construct Uniformly Most Powerful (UMP) tests** for one-parameter families.
3. **Apply likelihood ratio tests** and derive their asymptotic distributions.
4. **Prove consistency and asymptotic normality** of the MLE.
5. **Construct confidence intervals** based on pivotal quantities and asymptotic distributions.

---

## Core Theory

### Unit 1: Hypothesis Testing Foundations

#### 1.1 Framework

A **hypothesis test** involves:
- **Null hypothesis** $H_0: \theta \in \Theta_0$ vs. **alternative** $H_1: \theta \in \Theta_1 = \Theta \setminus \Theta_0$.
- A **test function** $\phi(x) = P(\text{reject } H_0 | X = x)$. For non-randomized tests, $\phi \in \{0, 1\}$.
- **Type I error**: $\alpha(\theta) = E_\theta[\phi(X)]$ for $\theta \in \Theta_0$. Size $= \sup_{\theta \in \Theta_0} \alpha(\theta)$.
- **Type II error**: $\beta(\theta) = 1 - E_\theta[\phi(X)]$ for $\theta \in \Theta_1$.
- **Power function**: $\pi(\theta) = E_\theta[\phi(X)]$.

#### 1.2 The Neyman-Pearson Lemma

**Theorem (Neyman-Pearson)**: Consider testing $H_0: \theta = \theta_0$ vs. $H_1: \theta = \theta_1$ (simple vs. simple). The **most powerful** test of size $\alpha$ is:

$$\phi(x) = \begin{cases} 1 & \text{if } \frac{f(x|\theta_1)}{f(x|\theta_0)} > k \\ \gamma & \text{if } \frac{f(x|\theta_1)}{f(x|\theta_0)} = k \\ 0 & \text{if } \frac{f(x|\theta_1)}{f(x|\theta_0)} < k \end{cases}$$

where $k$ and $\gamma$ are chosen so that $E_{\theta_0}[\phi(X)] = \alpha$.

*Proof*: Let $\phi^*$ be the NP test and $\phi$ any other test with $E_{\theta_0}[\phi] \leq \alpha$. Then:

$$E_{\theta_1}[\phi^*] - E_{\theta_1}[\phi] = \int (\phi^* - \phi)(f_1 - kf_0) \, d\mu \geq 0$$

because on $\{\phi^* = 1\}$, $f_1 > kf_0$ so $(\phi^* - \phi) \geq 0$ and $(f_1 - kf_0) > 0$; on $\{\phi^* = 0\}$, $f_1 < kf_0$ so $(\phi^* - \phi) \leq 0$ and $(f_1 - kf_0) < 0$.

---

### Unit 2: UMP Tests and Monotone Likelihood Ratio

#### 2.1 Uniformly Most Powerful Tests

**Definition**: A test $\phi$ is **UMP** at level $\alpha$ for $H_0: \theta \leq \theta_0$ vs. $H_1: \theta > \theta_0$ if it is the most powerful test against every $\theta_1 > \theta_0$.

#### 2.2 Monotone Likelihood Ratio

**Definition**: A family $\{f(x|\theta)\}$ has **monotone likelihood ratio (MLR)** in $T(x)$ if for $\theta_1 > \theta_0$, $\frac{f(x|\theta_1)}{f(x|\theta_0)}$ is a nondecreasing function of $T(x)$.

**Theorem (Karlin-Rubin)**: If the family has MLR in $T(x)$, then the UMP level-$\alpha$ test for $H_0: \theta \leq \theta_0$ vs. $H_1: \theta > \theta_0$ is:

$$\phi(x) = \begin{cases} 1 & \text{if } T(x) > c \\ \gamma & \text{if } T(x) = c \\ 0 & \text{if } T(x) < c \end{cases}$$

where $c$ and $\gamma$ are chosen so the size is $\alpha$.

**Key Fact**: All one-parameter exponential families have MLR in the natural sufficient statistic.

#### 2.3 Limitations and Two-Sided Tests

For two-sided alternatives ($H_1: \theta \neq \theta_0$), UMP tests generally do not exist. Approaches:
- **Unbiased tests**: Require $\pi(\theta) \geq \alpha$ for all $\theta \in \Theta_1$.
- **UMP unbiased tests**: Exist for exponential families.
- **Likelihood ratio tests**: A general-purpose approach.

---

### Unit 3: Likelihood Ratio Tests

#### 3.1 Generalized Likelihood Ratio

The **generalized likelihood ratio statistic**:

$$\Lambda(x) = \frac{\sup_{\theta \in \Theta_0} L(\theta|x)}{\sup_{\theta \in \Theta} L(\theta|x)}$$

Reject $H_0$ when $\Lambda(x) \leq c$ (or equivalently, $-2\log\Lambda(x)$ is large).

#### 3.2 Wilks' Theorem

**Theorem (Wilks)**: Under $H_0$ and regularity conditions, if $\Theta_0$ is specified by $r$ constraints on a $k$-dimensional parameter:

$$-2 \log \Lambda(X) \xrightarrow{d} \chi^2_{k-r} \quad \text{as } n \to \infty$$

This provides an asymptotic calibration for the LRT without needing the exact null distribution.

#### 3.3 Score and Wald Tests

Three asymptotically equivalent test statistics:

| Test | Statistic | Intuition |
|------|-----------|-----------|
| **Likelihood Ratio** | $-2\log\Lambda$ | Compare max likelihoods |
| **Wald** | $(\hat{\theta} - \theta_0)^T I(\hat{\theta})(\hat{\theta} - \theta_0)$ | How far is MLE from $\theta_0$? |
| **Score (Rao)** | $S(\theta_0)^T I(\theta_0)^{-1} S(\theta_0)$ | Is the score nonzero at $\theta_0$? |

All three converge to $\chi^2_{k-r}$ under $H_0$.

---

### Unit 4: Asymptotic Theory of Estimation

#### 4.1 Consistency of the MLE

**Theorem**: Under regularity conditions, $\hat{\theta}_{\text{MLE}} \xrightarrow{P} \theta_0$ (the true parameter value).

*Proof Strategy*: The log-likelihood ratio $\frac{1}{n}\ell_n(\theta) - \frac{1}{n}\ell_n(\theta_0)$ converges uniformly to $E_{\theta_0}[\log f(X|\theta)/f(X|\theta_0)]$, which is maximized uniquely at $\theta = \theta_0$ by the information inequality (Kullback-Leibler divergence $\geq 0$ with equality iff the distributions are the same).

#### 4.2 Asymptotic Normality of the MLE

**Theorem**: Under regularity conditions:

$$\sqrt{n}(\hat{\theta}_n - \theta_0) \xrightarrow{d} N(0, I(\theta_0)^{-1})$$

where $I(\theta_0)$ is the Fisher Information.

*Proof Sketch*: Taylor-expand the score:

$$0 = \frac{1}{\sqrt{n}} S_n(\hat{\theta}_n) = \frac{1}{\sqrt{n}} S_n(\theta_0) + \frac{1}{n} S_n'(\tilde{\theta}_n) \cdot \sqrt{n}(\hat{\theta}_n - \theta_0)$$

By the CLT, $\frac{1}{\sqrt{n}} S_n(\theta_0) \xrightarrow{d} N(0, I(\theta_0))$. By the LLN, $\frac{1}{n} S_n'(\tilde{\theta}_n) \xrightarrow{P} -I(\theta_0)$. Solving:

$$\sqrt{n}(\hat{\theta}_n - \theta_0) = \left(-\frac{1}{n}S_n'(\tilde{\theta}_n)\right)^{-1} \frac{1}{\sqrt{n}} S_n(\theta_0) \xrightarrow{d} I(\theta_0)^{-1} N(0, I(\theta_0)) = N(0, I(\theta_0)^{-1})$$

#### 4.3 Asymptotic Efficiency

**Definition**: An estimator $\tilde{\theta}_n$ is **asymptotically efficient** if $\sqrt{n}(\tilde{\theta}_n - \theta_0) \xrightarrow{d} N(0, I(\theta_0)^{-1})$, achieving the Cramér-Rao bound asymptotically.

**Result**: The MLE is asymptotically efficient under regularity conditions.

#### 4.4 The Delta Method

**Theorem**: If $\sqrt{n}(\hat{\theta}_n - \theta) \xrightarrow{d} N(0, \sigma^2)$ and $g$ is differentiable with $g'(\theta) \neq 0$, then:

$$\sqrt{n}(g(\hat{\theta}_n) - g(\theta)) \xrightarrow{d} N(0, [g'(\theta)]^2 \sigma^2)$$

---

### Unit 5: Confidence Intervals and Regions

#### 5.1 Pivotal Quantities

A **pivotal quantity** $Q(X, \theta)$ has a distribution that does not depend on $\theta$.

**Example**: If $X_i \sim N(\mu, \sigma^2)$, then $T = \frac{\bar{X} - \mu}{S/\sqrt{n}} \sim t_{n-1}$, yielding:

$$P\left(\bar{X} - t_{\alpha/2, n-1}\frac{S}{\sqrt{n}} \leq \mu \leq \bar{X} + t_{\alpha/2, n-1}\frac{S}{\sqrt{n}}\right) = 1 - \alpha$$

#### 5.2 Asymptotic Confidence Intervals

Using the MLE asymptotics: an approximate $100(1-\alpha)\%$ confidence interval for $\theta$ is:

$$\hat{\theta}_n \pm z_{\alpha/2} \sqrt{\frac{1}{nI(\hat{\theta}_n)}}$$

By the delta method, for $g(\theta)$:

$$g(\hat{\theta}_n) \pm z_{\alpha/2} |g'(\hat{\theta}_n)| \sqrt{\frac{1}{nI(\hat{\theta}_n)}}$$

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Statistical Inference* (2nd ed.) | George Casella & Roger L. Berger | **Primary** — Chapters 8–10 |
| *Testing Statistical Hypotheses* (3rd ed.) | E.L. Lehmann & Joseph Romano | **Advanced** — Definitive hypothesis testing reference |
| *Asymptotic Statistics* | A.W. van der Vaart | **Advanced** — Rigorous asymptotic theory |
| *Mathematical Statistics* | Jun Shao | **Supplementary** |

---

## Problem Sets

### Problem Set 1: Neyman-Pearson and UMP Tests

1. **(Casella & Berger 8.3)** Derive the most powerful test of $H_0: \mu = 0$ vs. $H_1: \mu = 1$ for $N(\mu, 1)$ data at level $\alpha$.
2. **(Exam-style)** Prove the Neyman-Pearson Lemma.
3. **(Exam-style)** Show that the Poisson family has MLR in $\sum X_i$ and derive the UMP test for $H_0: \lambda \leq \lambda_0$ vs. $H_1: \lambda > \lambda_0$.
4. **(Proof)** Prove that for exponential families with natural parameter $\eta(\theta)$ increasing in $\theta$, the UMP test rejects for large values of the natural sufficient statistic.
5. **(Challenge)** Show that no UMP test exists for $H_0: \mu = 0$ vs. $H_1: \mu \neq 0$ in the $N(\mu, 1)$ family.

### Problem Set 2: Likelihood Ratio Tests

1. **(Casella & Berger 8.2)** Derive the LRT for $H_0: \mu = \mu_0$ vs. $H_1: \mu \neq \mu_0$ when $X_i \sim N(\mu, \sigma^2)$ with $\sigma^2$ known.
2. **(Exam-style)** Prove Wilks' theorem in the one-dimensional case.
3. **(Exam-style)** Construct the LRT for testing independence in a $2 \times 2$ contingency table.
4. **(Application)** Compare the Wald, Score, and LRT for testing $p = 0.5$ vs. $p \neq 0.5$ in a $\text{Binomial}(n, p)$ model.
5. **(Proof)** Show that the three test statistics (Wald, Score, LRT) are asymptotically equivalent under $H_0$.

### Problem Set 3: MLE Asymptotics

1. **(van der Vaart, Ch. 5)** Prove the consistency of the MLE using the Kullback-Leibler divergence argument.
2. **(Exam-style)** Derive $\sqrt{n}(\hat{p} - p) \xrightarrow{d} N(0, p(1-p))$ for $\hat{p} = \bar{X}$ when $X_i \sim \text{Bernoulli}(p)$.
3. **(Exam-style)** Use the delta method to find the asymptotic distribution of $\log(\hat{p})$ and construct a 95% confidence interval for $\log(p)$.
4. **(Proof)** Prove the asymptotic normality of the MLE via the score function Taylor expansion.
5. **(Challenge)** Show that the MLE is not always consistent/asymptotically normal: consider the case where the parameter is on the boundary of the parameter space, e.g., $X_i \sim \text{Uniform}(0, \theta)$.
