---
layout: default
title: "0.4 — Probability & Mathematical Statistics"
parent: "Module 0 — Foundations"
nav_order: 4
permalink: /module_0/probability_statistics/
---

# 0.4 — Probability &amp; Mathematical Statistics

> *An applied statistics course teaches which test to run. This course teaches where the tests come from: random variables as mathematical objects, the distributions of sample statistics, and the reasons estimators work. It is the calculus-based bridge to the measure-theoretic treatment in Modules B and C.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Compute with random variables**: distributions, expectations, variances, and moment generating functions.
2. **Handle joint distributions**: marginals, conditionals, covariance, transformations, and the laws of total expectation and variance.
3. **Prove and apply** Markov's and Chebyshev's inequalities and the Weak Law of Large Numbers, and apply the Central Limit Theorem.
4. **Derive sampling distributions** ($\chi^2$, $t$, $F$) for normal samples.
5. **Construct and evaluate estimators** using bias, variance, MSE, the method of moments, and maximum likelihood.

---

## Core Theory

### Unit 1: Probability Foundations

**Axioms**: $P(A) \geq 0$, $P(\Omega) = 1$, and $P$ is additive over disjoint events.

**Conditional probability and Bayes' rule**:

$$P(A \mid B) = \frac{P(A \cap B)}{P(B)}, \qquad P(A \mid B) = \frac{P(B \mid A)\,P(A)}{P(B)}.$$

**Intuition**: conditioning on $B$ shrinks the universe to $B$ and rescales. **Classic trap (base rates)**: a test that is 99% accurate for a disease with 1% prevalence gives a positive patient only a 50% chance of being sick. $P(\text{sick} \mid +) = \frac{0.99 \times 0.01}{0.99 \times 0.01 + 0.01 \times 0.99} = 0.5$.

**Independence**: $P(A \cap B) = P(A)P(B)$. Independence is not the same as disjointness: disjoint events with positive probability are always *dependent*.

---

### Unit 2: Random Variables and Expectation

A **random variable** $X$ has a CDF $F(x) = P(X \leq x)$, and either a pmf (discrete) or a pdf (continuous) $f = F'$.

**Expectation**: $E[X] = \sum x\,p(x)$ or $\int x f(x)\,dx$, defined when absolutely convergent. **LOTUS**: $E[g(X)] = \int g(x) f(x)\,dx$, with no need to find the distribution of $g(X)$.

**Linearity**: $E[aX + bY] = aE[X] + bE[Y]$ **always**, even for dependent variables. Many hard-looking expectations become easy when written as a sum of indicators. *Example*: the expected number of fixed points of a random permutation of $n$ items is $\sum_{i=1}^n P(\sigma(i) = i) = n \cdot \frac{1}{n} = 1$.

**Variance**: $\operatorname{Var}(X) = E[X^2] - (E[X])^2$.

**Moment generating function**: $M_X(t) = E[e^{tX}]$. If it is finite near $0$, it determines the distribution, and $M_{X+Y} = M_X M_Y$ for independent $X, Y$.

| Distribution | Mean | Variance | Story |
|--------------|------|----------|-------|
| $\operatorname{Bernoulli}(p)$ | $p$ | $p(1-p)$ | One trial |
| $\operatorname{Binomial}(n,p)$ | $np$ | $np(1-p)$ | Successes in $n$ independent trials |
| $\operatorname{Geometric}(p)$ on $\{1,2,\ldots\}$ | $1/p$ | $(1-p)/p^2$ | Trials until first success |
| $\operatorname{Poisson}(\lambda)$ | $\lambda$ | $\lambda$ | Rare events; limit of $\operatorname{Bin}(n, \lambda/n)$ |
| $\operatorname{Uniform}(a,b)$ | $(a+b)/2$ | $(b-a)^2/12$ | Equally likely on an interval |
| $\operatorname{Exponential}(\lambda)$ | $1/\lambda$ | $1/\lambda^2$ | Memoryless waiting time |
| $N(\mu, \sigma^2)$ | $\mu$ | $\sigma^2$ | Sums of many small effects (CLT) |
| $\operatorname{Gamma}(\alpha, \lambda)$ | $\alpha/\lambda$ | $\alpha/\lambda^2$ | Sum of $\alpha$ independent $\operatorname{Exp}(\lambda)$ (integer $\alpha$) |

---

### Unit 3: Joint Distributions

For a joint density $f(x,y)$: the marginal is $f_X(x) = \int f(x,y)\,dy$, and the conditional is $f_{Y|X}(y|x) = f(x,y)/f_X(x)$.

**Covariance and correlation**: $\operatorname{Cov}(X,Y) = E[XY] - E[X]E[Y]$, $\rho = \operatorname{Cov}(X,Y)/(\sigma_X\sigma_Y) \in [-1, 1]$. Independent implies uncorrelated, **but not conversely**: if $X \sim N(0,1)$, then $X$ and $X^2$ are uncorrelated but dependent.

**Laws of total expectation and variance**:

$$E[Y] = E\big[E[Y \mid X]\big], \qquad \operatorname{Var}(Y) = E\big[\operatorname{Var}(Y \mid X)\big] + \operatorname{Var}\big(E[Y \mid X]\big).$$

**Intuition**: total variability = average variability *within* groups + variability *between* group means. This identity is the core of ANOVA, of Rao–Blackwell (Module C), and of hierarchical models.

**Change of variables**: if $Y = g(X)$ with $g$ invertible and differentiable, then $f_Y(y) = f_X(g^{-1}(y))\,\left|\det D g^{-1}(y)\right|$. The Jacobian factor corrects for how $g$ stretches or compresses volume.

**Multivariate normal**: $X \sim N(\mu, \Sigma)$ iff every linear combination $a^T X$ is normal. Within this family, and only for jointly normal vectors, uncorrelated coordinates are independent.

---

### Unit 4: Inequalities and Limit Theorems

- **Markov**: for $X \geq 0$, $P(X \geq a) \leq E[X]/a$.
- **Chebyshev**: $P(|X - \mu| \geq k) \leq \sigma^2/k^2$ (Markov applied to $(X - \mu)^2$).
- **Weak Law of Large Numbers**: for i.i.d. $X_i$ with finite variance, $\bar{X}_n \to \mu$ in probability (Chebyshev with $\operatorname{Var}(\bar{X}_n) = \sigma^2/n$).
- **Central Limit Theorem**: $\sqrt{n}(\bar{X}_n - \mu)/\sigma \xrightarrow{d} N(0,1)$.

**Intuition**: averaging $n$ independent errors shrinks their spread by a factor of $\sqrt{n}$, not $n$. That is why halving a margin of error costs four times the data. The CLT adds that the shape of the averaged error is nearly always Gaussian, whatever the shape of the individual errors.

**Sampling distributions for normal data**: if $X_1, \ldots, X_n \overset{\text{iid}}{\sim} N(\mu, \sigma^2)$, then
1. $\bar{X} \sim N(\mu, \sigma^2/n)$;
2. $(n-1)S^2/\sigma^2 \sim \chi^2_{n-1}$;
3. $\bar{X}$ and $S^2$ are **independent** (a special property of the normal family);
4. $\dfrac{\bar{X} - \mu}{S/\sqrt{n}} \sim t_{n-1}$.

The degrees of freedom drop to $n-1$ because one degree of freedom is used up estimating $\mu$ by $\bar{X}$.

---

### Unit 5: Estimation

An **estimator** $\hat{\theta}$ is a function of the data. Its quality is measured by

$$\operatorname{MSE}(\hat{\theta}) = E[(\hat{\theta} - \theta)^2] = \operatorname{Var}(\hat{\theta}) + \operatorname{Bias}(\hat{\theta})^2.$$

**Intuition — the bias–variance trade-off**: a slightly biased estimator with much lower variance can have smaller MSE. Shrinkage, ridge regression, and the James–Stein estimator (Module C) all exploit this.

- **Method of moments**: equate sample moments to population moments and solve for the parameters.
- **Maximum likelihood**: choose $\hat{\theta}$ to maximize $L(\theta) = \prod f(x_i \mid \theta)$, usually via $\frac{d}{d\theta}\log L = 0$.
- **Confidence interval**: a random interval that covers the fixed true $\theta$ with probability $1 - \alpha$, computed before the data are seen. A 95% interval does **not** mean "$\theta$ is in this particular interval with probability 0.95".
- **Hypothesis test**: the $p$-value is the probability, *computed assuming $H_0$*, of a result at least as extreme as the one observed. It is not the probability that $H_0$ is true.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| [*Introduction to Probability*](https://www.probabilitybook.net/) (2nd ed.) | Joseph Blitzstein &amp; Jessica Hwang | **Primary (probability)** — Free online; outstanding intuition and "stories" |
| *Statistical Inference* (2nd ed.), Ch. 1–5 | George Casella &amp; Roger Berger | **Primary (statistics)** — The same text Module C continues from |
| *A First Course in Probability* | Sheldon Ross | **Alternative** — Many worked problems |
| *Mathematical Statistics with Applications* | Wackerly, Mendenhall &amp; Scheaffer | **Alternative** — Gentler path into estimation and testing |

---

## Problem Sets

### Problem Set 1: Probability and Random Variables

1. **(Core)** A family has two children. Given that at least one is a girl, what is the probability both are girls? Given that the *older* child is a girl? Explain why the answers differ.
2. **(Core)** Use indicator variables to find the expected number of distinct values seen when rolling a fair die $n$ times.
3. **(Core)** Prove the memoryless property of the exponential: $P(X > s + t \mid X > s) = P(X > t)$.
4. **(Proof)** Using MGFs, prove that the sum of independent $\operatorname{Poisson}(\lambda_1)$ and $\operatorname{Poisson}(\lambda_2)$ variables is $\operatorname{Poisson}(\lambda_1 + \lambda_2)$.
5. **(Challenge)** Show that $\operatorname{Bin}(n, \lambda/n) \to \operatorname{Poisson}(\lambda)$ pointwise in the pmf as $n \to \infty$.

### Problem Set 2: Joint Distributions

1. **(Core)** Let $X, Y \overset{\text{iid}}{\sim} \operatorname{Uniform}(0,1)$. Find the density of $X + Y$ and compute $P(X + Y > 1.5)$.
2. **(Core)** Let $X \sim N(0,1)$. Show that $X$ and $X^2$ are uncorrelated but not independent.
3. **(Proof)** Prove the law of total variance.
4. **(Core)** If $N \sim \operatorname{Poisson}(\lambda)$ and, given $N$, $Y$ is a sum of $N$ i.i.d. variables with mean $\mu$ and variance $\sigma^2$, find $E[Y]$ and $\operatorname{Var}(Y)$.
5. **(Challenge)** Let $X, Y \overset{\text{iid}}{\sim} N(0,1)$. Use polar coordinates and the change-of-variables formula to show that $R^2 = X^2 + Y^2 \sim \operatorname{Exponential}(1/2)$ and that the angle is uniform and independent of $R$. Use this to explain the Box–Muller method.

### Problem Set 3: Limit Theorems and Estimation

1. **(Proof)** Prove Markov's and Chebyshev's inequalities, then the WLLN for finite-variance i.i.d. samples.
2. **(Core)** A fair coin is flipped 10,000 times. Use the CLT to approximate $P(\text{heads} \geq 5100)$, and compare with Chebyshev's bound.
3. **(Core)** For $X_1, \ldots, X_n \overset{\text{iid}}{\sim} \operatorname{Uniform}(0, \theta)$, find the method-of-moments estimator and the MLE of $\theta$. Compute the bias and MSE of each. Which is better?
4. **(Proof)** Prove $\operatorname{MSE} = \operatorname{Var} + \operatorname{Bias}^2$, and show that $S^2 = \frac{1}{n-1}\sum (X_i - \bar{X})^2$ is unbiased for $\sigma^2$.
5. **(Challenge)** Show that for normal samples the MLE $\hat{\sigma}^2 = \frac{1}{n}\sum(X_i - \bar{X})^2$ has smaller MSE than the unbiased $S^2$, so the "better" unbiased estimator is worse in MSE.

---

## Study Guide

{: .important }
> **What you must be able to do on demand**
>
> - Compute expectations with linearity and indicators, even for dependent variables
> - Apply the laws of total expectation and variance, and the change-of-variables formula
> - Prove Markov, Chebyshev, and the WLLN; apply the CLT with correct standardization
> - State the four sampling-distribution facts for normal samples
> - Derive MoM and ML estimators and compare them by bias, variance, and MSE

**Ready for Module B when** you can do Problem Set 2 #5 and Problem Set 3 #3 without notes. Probability Theory I will rebuild all of this on measure theory, and it is far easier to learn when the calculus-level picture is already solid.
