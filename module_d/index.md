---
layout: default
title: "Module D — Optimization & Operations Research"
nav_order: 7
has_children: true
permalink: /module_d/
---

<div class="hero-section" style="background: linear-gradient(135deg, #002D72, #D97706);">
  <h1>⚡ Module D — Optimization &amp; Operations Research</h1>
  <p>Finding the best solution. The algorithms and convergence theory behind machine learning, statistical estimation, engineering design, and operations research.</p>
</div>

> This module covers both unconstrained and constrained optimization with a focus on rigorous convergence theory and practical algorithms — from steepest descent and Newton's method to interior-point methods and semidefinite programming. These tools are ubiquitous across applied mathematics.

---

## Courses

<div class="module-grid">
  <a href="{{ site.baseurl }}/module_d/nonlinear_optimization_1/" class="module-card">
    <span class="module-label label-core">EN.553.761</span>
    <div class="module-title">Nonlinear Optimization I</div>
    <div class="module-desc">Optimality conditions, line search methods, steepest descent, Newton's method, quasi-Newton (BFGS), convergence rates.</div>
  </a>
  <a href="{{ site.baseurl }}/module_d/nonlinear_optimization_2/" class="module-card">
    <span class="module-label label-core">EN.553.762</span>
    <div class="module-title">Nonlinear Optimization II</div>
    <div class="module-desc">KKT conditions, Lagrangian duality, interior-point methods, sequential quadratic programming, semidefinite programming.</div>
  </a>
</div>

---

## Learning Outcomes at a Glance

| Topic | Nonlinear Optimization I (761) | Nonlinear Optimization II (762) |
|-------|-------------------------------|--------------------------------|
| Core object | Unconstrained smooth optimization | Constrained and structured optimization |
| Key theorem | Quadratic convergence of Newton's method | Strong duality (Slater's condition) |
| Key tool | Wolfe conditions, BFGS update | KKT conditions, barrier methods |
| Primary text | Nocedal &amp; Wright, *Numerical Optimization* (Ch. 2–7) | Nocedal &amp; Wright (Ch. 12–19) + Boyd &amp; Vandenberghe |

---

## Prerequisites

- **Module A**: Real Analysis (continuity, compactness, Inverse Function Theorem)
- **Module A**: Matrix Analysis (positive definiteness, eigenvalue characterizations of the Hessian)
- Multivariable calculus (gradients, Hessians, Taylor expansions in $\mathbb{R}^n$)

## Connection to Other Modules

- **Module C (Statistics)** — Maximum likelihood estimation, the EM algorithm, and penalized regression are all optimization problems. Newton's method on the log-likelihood is Fisher scoring.
- **Module B (Probability)** — Stochastic gradient descent and Monte Carlo optimization bridge probability theory with optimization algorithms.
- **Computing Lab** — BFGS, interior-point methods, and constrained solvers are implemented and compared on canonical problems from statistics and machine learning.
