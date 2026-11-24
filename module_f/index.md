---
layout: default
title: "Module F — Differential Equations & Numerical Analysis"
nav_order: 9
has_children: true
permalink: /module_f/
---

<div class="hero-section" style="background: linear-gradient(135deg, #002D72, #0F766E);">
  <h1>🌊 Module F — Differential Equations &amp; Numerical Analysis</h1>
  <p>How continuous systems evolve, and how to compute them reliably. This is the core of an applied-mathematics background.</p>
</div>

> Modules A–E prepare you for a statistics-oriented or optimization-oriented program. **Applied mathematics** programs also expect fluency with differential equations, both the theory (existence, stability, qualitative behavior) and the numerics (accuracy, stability, conditioning). This module supplies both. It is also valuable for statisticians: diffusions, gradient flows, and Monte Carlo methods all live here.

{: .note }
> **Which track needs this?** If you are aiming at applied mathematics, treat Module F as core. If you are aiming at statistics, treat it as an elective, but do the numerical analysis unit on conditioning and floating point, because every statistical computation depends on it.

---

## Courses

<div class="module-grid">
  <a href="{{ site.baseurl }}/module_f/differential_equations/" class="module-card">
    <span class="module-label label-core">F.1</span>
    <div class="module-title">Ordinary &amp; Partial Differential Equations</div>
    <div class="module-desc">Existence and uniqueness (Picard–Lindelöf), linear systems, stability and Lyapunov functions, the heat, wave, and Laplace equations.</div>
  </a>
  <a href="{{ site.baseurl }}/module_f/numerical_analysis/" class="module-card">
    <span class="module-label label-core">F.2</span>
    <div class="module-title">Numerical Analysis</div>
    <div class="module-desc">Floating point and conditioning, root finding, interpolation, quadrature, ODE solvers and stiffness, numerical linear algebra.</div>
  </a>
</div>

---

## Learning Outcomes at a Glance

| Topic | Differential Equations (F.1) | Numerical Analysis (F.2) |
|-------|-----------------------------|--------------------------|
| Core object | Flows $\dot{x} = f(x)$ and PDE solutions $u(t,x)$ | Algorithms and their error |
| Key theorem | Picard–Lindelöf (via the Contraction Mapping Principle) | Convergence = consistency + stability |
| Key tool | Eigenvalues of the linearization; energy estimates | Condition numbers; truncation-error analysis |
| Primary text | Strogatz; Strauss | Süli &amp; Mayers; Trefethen &amp; Bau |

## Prerequisites

- [Module 0.2 — Analysis on the Real Line]({{ site.baseurl }}/module_0/undergraduate_analysis/) and [0.3 — Proof-Based Linear Algebra]({{ site.baseurl }}/module_0/linear_algebra/)
- Module A Real Analysis Unit 3 (the Contraction Mapping Principle) is used directly in F.1

## Connections

- **Module A**: Picard–Lindelöf is the Banach Fixed-Point Theorem applied to an integral operator; stability of $\dot{x} = Ax$ is a statement about the spectrum of $A$.
- **Module B**: the heat equation is the PDE of Brownian motion: $u(t,x) = E[g(x + B_t)]$ solves $u_t = \tfrac{1}{2}u_{xx}$.
- **Module D**: gradient descent is the forward-Euler discretization of the gradient flow $\dot{x} = -\nabla f(x)$, and its step-size limit is a numerical stability condition.
