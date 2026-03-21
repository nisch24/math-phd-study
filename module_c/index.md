---
layout: default
title: "Module C — Statistics & Statistical Learning"
nav_order: 4
has_children: true
permalink: /module_c/
---

<div class="hero-section" style="background: linear-gradient(135deg, #002D72, #7C3AED);">
  <h1>📈 Module C — Statistics & Statistical Learning</h1>
  <p>From data to inference. The rigorous framework for estimation, hypothesis testing, and asymptotic behavior of estimators.</p>
</div>

> Statistical Theory bridges probability theory with the practical tools used in every area of applied mathematics — from maximum likelihood estimation to the bootstrap.

---

## Courses

<div class="module-grid">
  <a href="{{ site.baseurl }}/module_c/statistical_theory_1/" class="module-card">
    <span class="module-label label-core">EN.553.730</span>
    <div class="module-title">Statistical Theory I</div>
    <div class="module-desc">Sufficiency, Fisher Information, Cramér-Rao bound, UMVUE, exponential families.</div>
  </a>
  <a href="{{ site.baseurl }}/module_c/statistical_theory_2/" class="module-card">
    <span class="module-label label-core">EN.553.731</span>
    <div class="module-title">Statistical Theory II</div>
    <div class="module-desc">Neyman-Pearson lemma, likelihood ratio tests, MLE asymptotics, Bayesian inference.</div>
  </a>
</div>

---

## Prerequisites

- **Module B**: Probability Theory I & II (measure-theoretic probability, convergence theorems)
- **Module A**: Matrix Analysis (covariance matrices, spectral decomposition)

## Connection to Other Modules

- **Module D (Optimization)** — Maximum likelihood estimation is an optimization problem; Fisher scoring is Newton's method on the log-likelihood.
- **Computing Lab** — R and Python implementations of estimators, bootstrap methods, and simulation studies.
