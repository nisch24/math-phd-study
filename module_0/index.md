---
layout: default
title: "Module 0 — Foundations"
nav_order: 3
has_children: true
permalink: /module_0/
---

<div class="hero-section" style="background: linear-gradient(135deg, #002D72, #475569);">
  <h1>🧱 Module 0 — Foundations</h1>
  <p>The bridge from computational mathematics to proof-based mathematics. This is the material every graduate course assumes and none of them teaches.</p>
</div>

> Many strong applicants come from computer science, engineering, data science, or analytics. Their calculus, linear algebra, and statistics were taught as **techniques**: compute the eigenvalues, run the regression, apply the test. Graduate programs in applied mathematics and statistics instead assume these subjects were learned as **theory**: why the eigenvalues exist, why the estimator is consistent, why the test controls error. Module 0 closes that gap.

{: .important }
> **Who should take Module 0?** Do the [readiness self-check]({{ site.baseurl }}/readiness/) first. If you can't write the proofs it asks for in a few minutes each without notes, start here. Module 0 is not remedial: proof-based analysis and linear algebra are what admissions committees read as evidence of mathematical maturity.

---

## Courses

<div class="module-grid">
  <a href="{{ site.baseurl }}/module_0/proofs/" class="module-card">
    <span class="module-label label-foundation">0.1</span>
    <div class="module-title">Proofs, Logic &amp; Sets</div>
    <div class="module-desc">Quantifiers and negation, proof techniques, induction, functions and preimages, countability.</div>
  </a>
  <a href="{{ site.baseurl }}/module_0/undergraduate_analysis/" class="module-card">
    <span class="module-label label-foundation">0.2</span>
    <div class="module-title">Analysis on the Real Line</div>
    <div class="module-desc">Completeness of ℝ, sequences and series, continuity, the Mean Value Theorem, Riemann integration.</div>
  </a>
  <a href="{{ site.baseurl }}/module_0/linear_algebra/" class="module-card">
    <span class="module-label label-foundation">0.3</span>
    <div class="module-title">Proof-Based Linear Algebra</div>
    <div class="module-desc">Vector spaces, linear maps, rank–nullity, eigenvalues, inner products, the spectral theorem.</div>
  </a>
  <a href="{{ site.baseurl }}/module_0/probability_statistics/" class="module-card">
    <span class="module-label label-foundation">0.4</span>
    <div class="module-title">Probability &amp; Mathematical Statistics</div>
    <div class="module-desc">Random variables, joint distributions, limit theorems, sampling distributions, estimation.</div>
  </a>
</div>

---

## Suggested Order and Pace

| Order | Course | Typical time (10–12 hrs/week) | Unlocks |
|-------|--------|-------------------------------|---------|
| 1 | 0.1 Proofs, Logic &amp; Sets | 3–4 weeks | Everything else |
| 2 | 0.2 Analysis on the Real Line | 8–10 weeks | Module A Real Analysis, Module B |
| 2 | 0.3 Proof-Based Linear Algebra (in parallel with 0.2) | 8–10 weeks | Module A Matrix Analysis, Module D |
| 3 | 0.4 Probability &amp; Mathematical Statistics | 6–8 weeks | Module B, Module C |

These estimates assume you write out solutions to most of the problems. Reading proofs without writing them builds familiarity, not skill.

## How to Study Proof-Based Material

1. **Read actively.** Before reading a proof, cover it and try for 10 minutes. Even a failed attempt tells you what the key step must accomplish.
2. **Find the one idea.** Most proofs have a single trick (an $\varepsilon/3$ split, a clever function, a dimension count) and the rest is bookkeeping. After each proof, write that one idea in a sentence.
3. **Test the hypotheses.** For every theorem, drop one hypothesis and find the counterexample. This is the fastest way to understand why the hypothesis is there.
4. **Write, then rewrite.** A first draft finds the argument; the second makes it readable. Graders and admissions readers only see the second.
5. **Get feedback.** Self-study's biggest weakness is that nobody checks your proofs. Trade solutions with a study partner, post to Math StackExchange, or take a for-credit course (see the [readiness page]({{ site.baseurl }}/readiness/#making-it-visible-to-admissions)).
