---
layout: default
title: "Module C — Statistics & Statistical Learning"
nav_order: 6
has_children: true
permalink: /module_c/
---

<div class="hero-section" style="background: linear-gradient(135deg, #002D72, #7C3AED);">
  <h1>📈 Module C — Statistics &amp; Statistical Learning</h1>
  <p>From data to inference. The rigorous framework for estimation, hypothesis testing, and the asymptotic behavior of estimators.</p>
</div>

> Statistical Theory bridges measure-theoretic probability with the practical tools used throughout applied mathematics — from maximum likelihood estimation and the Cramér-Rao bound to likelihood-ratio tests, Bayesian inference, and decision theory (the bootstrap is covered as a simulation exercise in the Computing Lab). These courses develop the theoretical justification for why statistical procedures work.

---

## Courses

<div class="module-grid">
  <a href="{{ site.baseurl }}/module_c/statistical_theory_1/" class="module-card">
    <span class="module-label label-core">EN.553.730</span>
    <div class="module-title">Statistical Theory I</div>
    <div class="module-desc">Sufficiency, Fisher Information, Cramér-Rao bound, UMVUE, exponential families, maximum likelihood estimation.</div>
  </a>
  <a href="{{ site.baseurl }}/module_c/statistical_theory_2/" class="module-card">
    <span class="module-label label-core">EN.553.731</span>
    <div class="module-title">Statistical Theory II</div>
    <div class="module-desc">Neyman-Pearson lemma, likelihood ratio tests, MLE asymptotics, delta method, Bayesian inference.</div>
  </a>
</div>

---

## Learning Outcomes at a Glance

| Topic | Statistical Theory I (730) | Statistical Theory II (731) |
|-------|---------------------------|-----------------------------|
| Core object | Estimators and sufficient statistics | Hypothesis tests and asymptotic distributions |
| Key theorem | Lehmann-Scheffé (UMVUE) | Wilks' theorem ($\chi^2$ asymptotics of LRT) |
| Key tool | Rao-Blackwell, Cramér-Rao bound | Neyman-Pearson lemma, delta method |
| Primary text | Casella &amp; Berger, *Statistical Inference* (Ch. 5–7) | Casella &amp; Berger (Ch. 8–10) + van der Vaart |

---

## Prerequisites

- **Module B**: Probability Theory I &amp; II (measure-theoretic probability, conditional expectation, convergence theorems)
- **Module A**: Matrix Analysis (covariance matrices, positive definiteness, spectral decomposition)

## Connection to Other Modules

- **Module D (Optimization)** — Maximum likelihood estimation is fundamentally an optimization problem; Fisher scoring is Newton's method applied to the log-likelihood surface.
- **Computing Lab** — Python and R implementations of estimators, bootstrap methods, hypothesis tests, and simulation studies that verify asymptotic theory.
