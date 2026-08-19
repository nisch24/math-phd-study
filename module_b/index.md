---
layout: default
title: "Module B — Probability & Stochastic Processes"
nav_order: 3
has_children: true
permalink: /module_b/
---

<div class="hero-section" style="background: linear-gradient(135deg, #002D72, #059669);">
  <h1>🎲 Module B — Probability &amp; Stochastic Processes</h1>
  <p>Measure-theoretic probability forms the theoretical core of modern statistics and stochastic modeling.</p>
</div>

> This module develops probability from the ground up using $\sigma$-algebras and Lebesgue integration, culminating in martingale theory and an introduction to Brownian motion. The language established here is the foundation upon which all of statistical theory (Module C) is built.

---

## Courses

<div class="module-grid">
  <a href="{{ site.baseurl }}/module_b/probability_theory_1/" class="module-card">
    <span class="module-label label-core">EN.553.720</span>
    <div class="module-title">Probability Theory I</div>
    <div class="module-desc">$\sigma$-algebras, Lebesgue integration, Laws of Large Numbers, modes of convergence, Central Limit Theorem.</div>
  </a>
  <a href="{{ site.baseurl }}/module_b/probability_theory_2/" class="module-card">
    <span class="module-label label-core">EN.553.721</span>
    <div class="module-title">Probability Theory II</div>
    <div class="module-desc">Radon-Nikodym theorem, conditional expectation, martingales, Brownian motion, stochastic calculus foundations.</div>
  </a>
</div>

---

## Learning Outcomes at a Glance

| Topic | Probability Theory I (720) | Probability Theory II (721) |
|-------|---------------------------|------------------------------|
| Core object | Probability spaces, random variables | Filtrations, martingales, Brownian motion |
| Key theorem | Strong Law of Large Numbers | Martingale Convergence Theorem |
| Key tool | Characteristic functions (CLT proof) | Radon-Nikodym theorem |
| Exam weight | Foundational for all subsequent modules | Essential for statistical theory and stochastic calculus |
| Primary text | Durrett, *Probability: Theory and Examples* | Durrett (Ch. 4–8) + Williams |

---

## Prerequisites

- **Module A**: Real Analysis (measure theory builds directly on metric space topology and the Lebesgue integral)
- Undergraduate probability at the level of Ross or Bertsekas &amp; Tsitsiklis

## Connection to Other Modules

- **Module C (Statistics)** — All of statistical theory is built on probability; conditional expectation and the Radon-Nikodym theorem are essential for sufficiency and likelihood ratios.
- **Module D (Optimization)** — Stochastic optimization and Monte Carlo methods rely on the convergence results from this module.
- **Computing Lab** — Simulating random walks, Brownian motion, and verifying limit theorems numerically reinforces the theory.
