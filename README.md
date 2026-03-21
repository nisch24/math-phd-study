---
layout: default
title: Home
nav_order: 1
permalink: /
---

# JHU Applied Mathematics & Statistics — PhD Self-Study Guide

> A complete, open-source self-study framework for the **Johns Hopkins University PhD in Applied Mathematics and Statistics**. Every lesson plan, problem set, and computing tutorial is written in Markdown with full LaTeX support for mathematical notation.

---

## Program Roadmap

The curriculum is organized into **five modules** that mirror the department's core areas. Each module contains detailed lesson plans with learning objectives, rigorous theory, primary textbook references, and curated problem sets.

| Module | Area | Courses | Status |
|--------|------|---------|--------|
| [**A**]({{ site.baseurl }}/module_a/) | Analysis & Linear Algebra | EN.553.701, EN.553.792 | Foundation |
| [**B**]({{ site.baseurl }}/module_b/) | Probability & Stochastic Processes | EN.553.720, EN.553.721 | Core |
| [**C**]({{ site.baseurl }}/module_c/) | Statistics & Statistical Learning | EN.553.730, EN.553.731 | Core |
| [**D**]({{ site.baseurl }}/module_d/) | Optimization & Operations Research | EN.553.761, EN.553.762 | Core |
| [**E**]({{ site.baseurl }}/module_e/) | Discrete Mathematics | EN.553.671, EN.553.672 | Elective |

---

## Recommended Study Sequence

```
Semester 1          Semester 2          Semester 3          Semester 4
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│ Real         │    │ Probability │    │ Statistical │    │ Nonlinear   │
│ Analysis     │───▶│ Theory II   │───▶│ Theory II   │    │ Optim. II   │
│ (553.701)    │    │ (553.721)   │    │ (553.731)   │    │ (553.762)   │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│ Matrix       │    │ Statistical │    │ Nonlinear   │    │ Graph       │
│ Analysis     │───▶│ Theory I    │───▶│ Optim. I    │    │ Theory      │
│ (553.792)    │    │ (553.730)   │    │ (553.761)   │    │ (553.672)   │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
┌─────────────┐    ┌─────────────┐
│ Probability  │    │ Combinat.   │
│ Theory I     │    │ Analysis    │
│ (553.720)    │    │ (553.671)   │
└─────────────┘    └─────────────┘
```

---

## Quick-Start Guide

1. **Prerequisites** — Undergraduate-level linear algebra, multivariable calculus, probability, and mathematical maturity (comfort with proofs).
2. **Begin with Module A** — Real Analysis and Matrix Analysis form the language used throughout the program.
3. **Parallel study is encouraged** — Probability Theory I can be taken concurrently with Module A courses.
4. **Use the Computing Lab** — Each theory module is paired with hands-on computational exercises in the [Computing Laboratory]({{ site.baseurl }}/computing_lab/).
5. **Prepare for quals** — After completing Modules A and B, attempt the [Qualifying Exam Simulations]({{ site.baseurl }}/qualifying_exam/).

---

## Additional Resources

| Section | Description |
|---------|-------------|
| [Computing Laboratory]({{ site.baseurl }}/computing_lab/) | Python/C++, MATLAB, and LaTeX tutorials |
| [Qualifying Exam Simulation]({{ site.baseurl }}/qualifying_exam/) | Mock exams with formal proof-writing |
| [Resources]({{ site.baseurl }}/resources/) | Open-access lecture notes (MIT OCW, Stanford, etc.) |

---

## Technical Notes

- **Math Rendering**: All LaTeX notation uses MathJax. Equations are written inline with `$...$` and in display mode with `$$...$$`.
- **GitHub Pages**: Push this repository to GitHub and enable Pages from `Settings → Pages` to host at `https://<username>.github.io/jhu-math-phd-study/`.
- **Local Preview**: Install Jekyll (`gem install jekyll bundler`), then run `bundle exec jekyll serve`.

---

*This resource is not affiliated with Johns Hopkins University. It is an independent study guide based on publicly available course descriptions and standard graduate-level textbooks.*
