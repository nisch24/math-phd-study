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
6. **Compute posterior distributions** for conjugate models and use decision theory (Bayes risk, admissibility, minimaxity) to compare estimators.

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

**Definition**: A test $\phi$ is **UMP** at level $\alpha$ for $H_0: \theta \leq \theta_0$ vs. $H_1: \theta > \theta_0$ if $\sup_{\theta \leq \theta_0} E_\theta[\phi] \leq \alpha$ and, for every $\theta_1 > \theta_0$, $E_{\theta_1}[\phi] \geq E_{\theta_1}[\phi']$ for every other level-$\alpha$ test $\phi'$.

#### 2.2 Monotone Likelihood Ratio

**Definition**: A family $\{f(x|\theta)\}$ has **Monotone Likelihood Ratio (MLR)** in $T(x)$ if, for $\theta_1 > \theta_0$, the ratio $f(x|\theta_1)/f(x|\theta_0)$ is a nondecreasing function of $T(x)$.

**Theorem (Karlin-Rubin)**: If the family has MLR in $T(x)$, then the UMP level-$\alpha$ test for $H_0: \theta \leq \theta_0$ vs. $H_1: \theta > \theta_0$ is:

$$\phi(x) = \begin{cases} 1 & \text{if } T(x) > c \\ \gamma & \text{if } T(x) = c \\ 0 & \text{if } T(x) < c \end{cases}$$

where $c$ and $\gamma$ are chosen so the size equals $\alpha$.

**Key Fact**: A one-parameter exponential family $f(x|\theta) = h(x)\exp(\eta(\theta)T(x) - B(\theta))$ has MLR in $T(x)$ whenever $\eta(\theta)$ is nondecreasing in $\theta$. (If $\eta$ is decreasing, it has MLR in $-T(x)$.)

#### 2.3 Limitations and Two-Sided Tests

For two-sided alternatives ($H_1: \theta \neq \theta_0$), UMP tests generally do not exist. Standard approaches include:
- **Unbiased tests**: Require $\pi(\theta) \geq \alpha$ for all $\theta \in \Theta_1$.
- **UMP unbiased (UMPU) tests**: Exist for exponential families via Neyman structure.
- **Likelihood ratio tests**: A general-purpose approach with known asymptotic behavior.

---

### Unit 3: Likelihood Ratio Tests

#### 3.1 The Generalized Likelihood Ratio Statistic

$$\Lambda(x) = \frac{\sup_{\theta \in \Theta_0} L(\theta|x)}{\sup_{\theta \in \Theta} L(\theta|x)}.$$

Reject $H_0$ when $\Lambda(x) \leq c$, equivalently when $-2\log\Lambda(x) \geq c'$. Wilks' theorem below supplies the asymptotic cutoff $c' = \chi^2_{r,\alpha}$, the upper-$\alpha$ quantile of $\chi^2_r$.

#### 3.2 Wilks' Theorem

**Theorem (Wilks)**: Let $\Theta \subseteq \mathbb{R}^k$ be open, and let $\Theta_0$ be defined by $r$ independent smooth constraints (so $\Theta_0$ is a $(k-r)$-dimensional submanifold). Under $H_0$, with $\theta_0$ in the interior and standard regularity conditions:

$$-2 \log \Lambda(X) \xrightarrow{d} \chi^2_{r} \quad \text{as } n \to \infty.$$

**Degrees of freedom** = number of constraints = $\dim \Theta - \dim \Theta_0$. For example, testing $H_0: \mu = \mu_0$ in $N(\mu, \sigma^2)$ with both parameters unknown has $k = 2$, $\dim\Theta_0 = 1$, so the limit is $\chi^2_1$.

This provides an asymptotic calibration for the LRT without requiring the exact null distribution. Wilks fails when $\theta_0$ is on the boundary of $\Theta$ (e.g. testing a variance component $=0$), where the limit becomes a mixture of $\chi^2$ distributions.

#### 3.3 The Trinity of Asymptotically Equivalent Tests

For the simple null $H_0: \theta = \theta_0$ with $\theta \in \mathbb{R}^k$ (so $r = k$), write $S_n$ for the total score of the sample and $I_n(\theta) = n I_1(\theta)$ for the total Fisher information. Three tests are asymptotically equivalent under $H_0$:

| Test | Statistic | Intuition |
|------|-----------|-----------|
| **Likelihood Ratio** | $-2\log\Lambda$ | Compare maximum likelihoods under $H_0$ vs. $\Theta$ |
| **Wald** | $(\hat{\theta}_n - \theta_0)^T I_n(\hat{\theta}_n)(\hat{\theta}_n - \theta_0)$ | Is the MLE far from $\theta_0$? |
| **Score (Rao)** | $S_n(\theta_0)^T I_n(\theta_0)^{-1} S_n(\theta_0)$ | Is the score nonzero when evaluated at $\theta_0$? |

All three converge in distribution to $\chi^2_{k}$ under $H_0$; for a composite null with $r$ constraints, the appropriately generalized statistics converge to $\chi^2_r$.

---

### Unit 4: Asymptotic Theory of Estimation

#### 4.1 Consistency of the MLE

**Theorem**: Under regularity conditions, $\hat{\theta}_{\text{MLE}} \xrightarrow{P} \theta_0$.

*Proof Strategy* (Wald's argument): For each fixed $\theta$, the SLLN gives $\frac{1}{n}\ell_n(\theta) - \frac{1}{n}\ell_n(\theta_0) \to E_{\theta_0}[\log f(X|\theta)/f(X|\theta_0)] = -D_{\text{KL}}(\theta_0 \| \theta) \leq 0$ a.s. By Jensen's inequality, equality holds iff $f(\cdot|\theta) = f(\cdot|\theta_0)$, which by **identifiability** means $\theta = \theta_0$. Pointwise convergence is not enough to control the argmax. The proof needs convergence that is **uniform** in $\theta$, which requires a uniform law of large numbers (e.g. compact $\Theta$, continuity in $\theta$, and an integrable envelope). Then the maximizer of the empirical criterion converges to the unique maximizer $\theta_0$ of the limit (van der Vaart, Thm. 5.7).

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

### Unit 6: Bayesian Inference and Decision Theory

#### 6.1 Posterior Distributions

Given a prior density $\pi(\theta)$ and likelihood $L(\theta|x)$, the **posterior** is

$$\pi(\theta | x) = \frac{L(\theta|x)\,\pi(\theta)}{\int L(\vartheta|x)\,\pi(\vartheta)\,d\vartheta} \;\propto\; L(\theta|x)\,\pi(\theta).$$

**Conjugate pairs** (posterior in the same family as the prior):

| Likelihood | Prior | Posterior |
|------------|-------|-----------|
| $X \sim \operatorname{Binomial}(n, p)$ | $p \sim \operatorname{Beta}(a, b)$ | $\operatorname{Beta}(a + x,\; b + n - x)$ |
| $X_1, \ldots, X_n \sim \operatorname{Poisson}(\lambda)$ | $\lambda \sim \operatorname{Gamma}(a, b)$ (rate $b$) | $\operatorname{Gamma}(a + \sum x_i,\; b + n)$ |
| $X_1, \ldots, X_n \sim N(\theta, \sigma^2)$, $\sigma^2$ known | $\theta \sim N(\mu_0, \tau^2)$ | $N\!\left(\dfrac{\mu_0/\tau^2 + n\bar{x}/\sigma^2}{1/\tau^2 + n/\sigma^2},\; \dfrac{1}{1/\tau^2 + n/\sigma^2}\right)$ |

#### 6.2 Decision Theory

A **decision rule** $\delta(X)$ incurs **loss** $L(\theta, \delta(X))$; its **risk** is $R(\theta, \delta) = E_\theta[L(\theta, \delta(X))]$.

- **Bayes rule**: minimizes the Bayes risk $r(\pi, \delta) = \int R(\theta, \delta)\,\pi(\theta)\,d\theta$. Under squared-error loss the Bayes estimator is the **posterior mean**; under absolute-error loss it is the **posterior median**.
- **Admissibility**: $\delta$ is inadmissible if some $\delta'$ has $R(\theta, \delta') \leq R(\theta, \delta)$ for all $\theta$, with strict inequality for some $\theta$. A unique Bayes rule is admissible.
- **Minimaxity**: $\delta^*$ is minimax if it minimizes $\sup_\theta R(\theta, \delta)$. **Theorem**: a Bayes rule whose risk is constant in $\theta$ is minimax.

#### 6.3 Bernstein–von Mises Theorem

Under the regularity conditions of Unit 4, and a prior that is continuous and positive at $\theta_0$, the posterior satisfies

$$\left\| \pi(\cdot | X_1, \ldots, X_n) - N\!\left(\hat{\theta}_n,\; \tfrac{1}{n} I(\theta_0)^{-1}\right) \right\|_{TV} \xrightarrow{P_{\theta_0}} 0.$$

Consequently, Bayesian credible intervals are asymptotically valid frequentist confidence intervals in regular parametric models. The equivalence breaks down in high dimensions and in nonparametric settings.

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

1. **(cf. Casella &amp; Berger §8.3)** Derive the most powerful test of $H_0: \mu = 0$ vs. $H_1: \mu = 1$ for $N(\mu, 1)$ data at level $\alpha = 0.05$.
2. **(Exam-style)** Prove the Neyman-Pearson Lemma.
3. **(Exam-style)** Show that the Poisson family has MLR in $\sum X_i$ and derive the UMP test for $H_0: \lambda \leq \lambda_0$ vs. $H_1: \lambda > \lambda_0$.
4. **(Proof)** Prove that for exponential families with natural parameter $\eta(\theta)$ increasing in $\theta$, the UMP test rejects for large values of the natural sufficient statistic.
5. **(Challenge)** Show that no UMP test exists for $H_0: \mu = 0$ vs. $H_1: \mu \neq 0$ in the $N(\mu, 1)$ family.

### Problem Set 2: Likelihood Ratio Tests

1. **(cf. Casella &amp; Berger §8.2)** Derive the LRT for $H_0: \mu = \mu_0$ vs. $H_1: \mu \neq \mu_0$ when $X_i \overset{\text{iid}}{\sim} N(\mu, \sigma^2)$ with $\sigma^2$ known.
2. **(Exam-style)** Prove Wilks' theorem for a scalar parameter and simple null ($k = 1$, $r = 1$, limit $\chi^2_1$).
3. **(Exam-style)** Construct the LRT for independence in a $2 \times 2$ contingency table.
4. **(Application)** Compare the Wald, Score, and LRT statistics for testing $p = 1/2$ vs. $p \neq 1/2$ in a $\operatorname{Binomial}(n, p)$ model.
5. **(Proof)** Show that the three test statistics (Wald, Score, LRT) are asymptotically equivalent under $H_0$.

### Problem Set 3: MLE Asymptotics

1. **(van der Vaart, Ch. 5)** Prove the consistency of the MLE using the Kullback-Leibler divergence argument.
2. **(Exam-style)** Derive the asymptotic distribution $\sqrt{n}(\hat{p} - p) \xrightarrow{d} N(0, p(1-p))$ for $\hat{p} = \bar{X}$ when $X_i \overset{\text{iid}}{\sim} \operatorname{Bernoulli}(p)$.
3. **(Exam-style)** Use the delta method to find the asymptotic distribution of $\log(\hat{p})$ and construct an approximate 95% confidence interval for $\log(p)$.
4. **(Proof)** Prove asymptotic normality of the MLE via the score function Taylor expansion.
5. **(Challenge)** (a) For $X_i \overset{\text{iid}}{\sim} \operatorname{Uniform}(0, \theta)$, the MLE $\hat{\theta}_n = X_{(n)}$ is consistent but *not* asymptotically normal: show that $n(\theta - \hat{\theta}_n) \xrightarrow{d} \operatorname{Exponential}(\text{mean } \theta)$, and identify which regularity condition fails (the support depends on $\theta$). (b) The MLE can also be inconsistent. In the **Neyman–Scott problem**, $X_{i1}, X_{i2} \overset{\text{iid}}{\sim} N(\mu_i, \sigma^2)$ for $i = 1, \ldots, n$, show that $\hat{\sigma}^2_{\text{MLE}} \xrightarrow{P} \sigma^2/2$. Explain why a growing number of nuisance parameters breaks the standard theory.

### Problem Set 4: Bayesian Inference and Decision Theory

1. **(Exam-style)** For $X \sim \operatorname{Binomial}(n, p)$ with a $\operatorname{Beta}(a, b)$ prior, show that the posterior mean is a weighted average of the prior mean $a/(a+b)$ and the MLE $x/n$, and identify the weights.
2. **(Proof)** Prove that under squared-error loss, the Bayes estimator is the posterior mean $E[\theta | X]$.
3. **(Exam-style)** Show that $\delta(X) = \dfrac{X + \sqrt{n}/2}{n + \sqrt{n}}$ is the Bayes estimator of $p$ under a $\operatorname{Beta}(\sqrt{n}/2, \sqrt{n}/2)$ prior, that its risk is constant in $p$, and hence that it is minimax. Compare its risk with that of the MLE $X/n$.
4. **(Proof)** Prove that a Bayes rule with constant risk is minimax.

---

## Study Guide &amp; Exam Preparation

{: .important }
> **Key Theorems for Statistical Theory II**
>
> - **Neyman-Pearson Lemma** — most powerful test for simple vs. simple hypotheses; full proof required
> - **Karlin-Rubin Theorem** — MLR $\Rightarrow$ UMP test; know what MLR means and verify it for exponential families
> - **Wilks' Theorem** — $-2\log\Lambda \xrightarrow{d} \chi^2_{r}$; degrees of freedom = number of constraints = $\dim\Theta - \dim\Theta_0$
> - **Consistency of MLE** — KL divergence + identifiability + a uniform LLN; know why pointwise convergence alone is not enough
> - **Asymptotic Normality of MLE** — score expansion proof; know both CLT and LLN roles
> - **Delta Method** — linearization; apply to get asymptotic intervals for transformations of $\theta$
> - **Bayes and minimax** — posterior mean is Bayes under squared error; a constant-risk Bayes rule is minimax

**Proof-Writing Strategy**:
- For NP problems, always verify the size condition explicitly.
- For Wilks, state the regularity conditions and the $\chi^2$ degrees of freedom.
- For MLE asymptotics, the two key ingredients are: (i) CLT applied to the score, (ii) LLN applied to the observed information.
