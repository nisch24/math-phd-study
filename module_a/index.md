---
layout: default
title: "Module A — Analysis & Linear Algebra"
nav_order: 4
has_children: true
permalink: /module_a/
---

<div class="hero-section" style="background: linear-gradient(135deg, #002D72, #3B82F6);">
  <h1>📊 Module A — Analysis &amp; Linear Algebra</h1>
  <p>The Introductory Exam Foundation. These two courses establish the mathematical bedrock for the entire PhD program.</p>
</div>

> Real Analysis provides the rigorous language of limits, convergence, and continuity in abstract spaces, while Matrix Analysis supplies the algebraic and spectral tools deployed across statistics, optimization, and all areas of applied mathematics. Mastery of both is required before the Introductory Qualifying Exam.

---

## Courses

<div class="module-grid">
  <a href="{{ site.baseurl }}/module_a/real_analysis/" class="module-card">
    <span class="module-label label-foundation">EN.553.701</span>
    <div class="module-title">Real Analysis</div>
    <div class="module-desc">Metric spaces, uniform convergence, Inverse and Implicit Function Theorems, Contraction Mapping Principle.</div>
  </a>
  <a href="{{ site.baseurl }}/module_a/matrix_analysis/" class="module-card">
    <span class="module-label label-foundation">EN.553.792</span>
    <div class="module-title">Matrix Analysis</div>
    <div class="module-desc">Spectral decomposition, SVD, variational eigenvalue characterizations, positive definiteness, perturbation theory.</div>
  </a>
</div>

---

## Learning Outcomes at a Glance

| Topic | Real Analysis (701) | Matrix Analysis (792) |
|-------|--------------------|-----------------------|
| Core object | Metric and function spaces | Linear operators on $\mathbb{C}^n$ |
| Key theorem | Inverse Function Theorem | Spectral Theorem (Hermitian) |
| Key tool | Banach Fixed-Point Theorem | Courant-Fischer min-max theorem |
| Exam paper | Real Analysis paper of the Introductory Exam | Linear Algebra paper of the Introductory Exam |
| Primary text | Rudin, *Principles of Mathematical Analysis* | Horn &amp; Johnson, *Matrix Analysis* |

---

## Prerequisites

- Undergraduate real analysis on $\mathbb{R}$: sequences, series, continuity, differentiation, Riemann integration (Abbott, or Rudin Chapters 1–6)
- Proof-based linear algebra at the level of Axler or Friedberg–Insel–Spence
- Comfort with $\varepsilon$-$\delta$ proofs and abstract mathematical reasoning

If any of these are missing, especially if your linear algebra and calculus were computational rather than proof-based, start with [Module 0 — Foundations]({{ site.baseurl }}/module_0/). Module A assumes that material; it does not teach it.

## Why This Module First?

The JHU Introductory Exam has separate Real Analysis, Linear Algebra, and Probability papers; this module prepares the first two (Module B, Probability Theory I, prepares the third). The concepts developed here — metric space topology, spectral theory, matrix decompositions — recur throughout every subsequent module:

- **Module B (Probability)**: Measure spaces generalize metric spaces; $L^p$ spaces are infinite-dimensional analogs of $\mathbb{R}^n$.
- **Module C (Statistics)**: Covariance matrices, PCA, and the Fisher Information matrix are all matrix-analytic objects.
- **Module D (Optimization)**: Convergence of algorithms relies on the Contraction Mapping Principle; the Hessian and its eigenvalues determine local behavior.

A strong foundation in Module A makes every subsequent course substantially more approachable.
