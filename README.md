---
layout: default
title: Home
nav_order: 1
permalink: /
---

<div class="hero-section">
  <h1>📐 JHU Applied Mathematics &amp; Statistics</h1>
  <p>A complete, open-source self-study framework for the Johns Hopkins University PhD in Applied Mathematics and Statistics. Every lesson plan, problem set, and computing tutorial features full LaTeX support via MathJax for rigorous mathematical notation.</p>
</div>

## Program Modules

<div class="module-grid">

  <a href="{{ site.baseurl }}/module_a/" class="module-card">
    <span class="module-label label-foundation">Foundation</span>
    <div class="module-title">Module A — Analysis &amp; Linear Algebra</div>
    <div class="module-desc">Real Analysis (553.701) and Matrix Analysis (553.792). The mathematical bedrock for the entire program.</div>
  </a>

  <a href="{{ site.baseurl }}/module_b/" class="module-card">
    <span class="module-label label-core">Core</span>
    <div class="module-title">Module B — Probability &amp; Stochastic Processes</div>
    <div class="module-desc">Probability Theory I &amp; II (553.720, 553.721). Measure-theoretic probability and martingale theory.</div>
  </a>

  <a href="{{ site.baseurl }}/module_c/" class="module-card">
    <span class="module-label label-core">Core</span>
    <div class="module-title">Module C — Statistics &amp; Statistical Learning</div>
    <div class="module-desc">Statistical Theory I &amp; II (553.730, 553.731). Estimation, hypothesis testing, and asymptotic theory.</div>
  </a>

  <a href="{{ site.baseurl }}/module_d/" class="module-card">
    <span class="module-label label-core">Core</span>
    <div class="module-title">Module D — Optimization &amp; Operations Research</div>
    <div class="module-desc">Nonlinear Optimization I &amp; II (553.761, 553.762). Convergence theory and practical algorithms.</div>
  </a>

  <a href="{{ site.baseurl }}/module_e/" class="module-card">
    <span class="module-label label-elective">Elective</span>
    <div class="module-title">Module E — Discrete Mathematics</div>
    <div class="module-desc">Combinatorial Analysis (553.671) and Graph Theory (553.672). Counting, structure, and algorithms.</div>
  </a>

</div>

---

## Recommended Study Sequence

<div class="timeline">
  <div class="semester-col">
    <h4>Semester 1</h4>
    <div class="course-chip"><strong>553.701</strong> Real Analysis</div>
    <div class="course-chip"><strong>553.792</strong> Matrix Analysis</div>
    <div class="course-chip"><strong>553.720</strong> Probability Theory I</div>
  </div>
  <div class="semester-col">
    <h4>Semester 2</h4>
    <div class="course-chip"><strong>553.721</strong> Probability Theory II</div>
    <div class="course-chip"><strong>553.730</strong> Statistical Theory I</div>
    <div class="course-chip"><strong>553.671</strong> Combinatorial Analysis</div>
  </div>
  <div class="semester-col">
    <h4>Semester 3</h4>
    <div class="course-chip"><strong>553.731</strong> Statistical Theory II</div>
    <div class="course-chip"><strong>553.761</strong> Nonlinear Optim. I</div>
  </div>
  <div class="semester-col">
    <h4>Semester 4</h4>
    <div class="course-chip"><strong>553.762</strong> Nonlinear Optim. II</div>
    <div class="course-chip"><strong>553.672</strong> Graph Theory</div>
  </div>
</div>

---

## Quick-Start Guide

<div class="steps-grid">
  <div class="step-card">
    <div class="step-number">1</div>
    <div class="step-title">Prerequisites</div>
    <div class="step-desc">Undergraduate-level linear algebra, multivariable calculus, probability, and mathematical maturity (comfort with $\varepsilon$-$\delta$ proofs and abstract argumentation).</div>
  </div>
  <div class="step-card">
    <div class="step-number">2</div>
    <div class="step-title">Begin with Module A</div>
    <div class="step-desc">Real Analysis and Matrix Analysis establish the shared language — metric spaces, spectral theory, and functional notation — used throughout all subsequent modules.</div>
  </div>
  <div class="step-card">
    <div class="step-number">3</div>
    <div class="step-title">Parallel Study</div>
    <div class="step-desc">Probability Theory I may be taken concurrently with Module A; its measure-theoretic foundation reinforces and extends the real analysis material.</div>
  </div>
  <div class="step-card">
    <div class="step-number">4</div>
    <div class="step-title">Computing Lab</div>
    <div class="step-desc">Each theory module is paired with hands-on exercises in the <a href="{{ site.baseurl }}/computing_lab/">Computing Laboratory</a> — Python, C++, MATLAB, and LaTeX.</div>
  </div>
  <div class="step-card">
    <div class="step-number">5</div>
    <div class="step-title">Qualifying Exam Prep</div>
    <div class="step-desc">After completing Modules A &amp; B, begin timed practice with the <a href="{{ site.baseurl }}/qualifying_exam/">Qualifying Exam Simulations</a>. Aim for 45 minutes per problem under exam conditions.</div>
  </div>
</div>

---

## Additional Resources

| Section | Description |
|---------|-------------|
| [🖥️ Computing Laboratory]({{ site.baseurl }}/computing_lab/) | Python/C++, MATLAB, and LaTeX tutorials paired with each theory module |
| [📝 Qualifying Exam Simulation]({{ site.baseurl }}/qualifying_exam/) | Three full mock exams with grading rubrics and exam-writing guidance |
| [📚 Resources]({{ site.baseurl }}/resources/) | Curated open-access lecture notes from MIT OCW, Stanford, and arXiv |

---

## Technical Notes

- **Math Rendering** — All LaTeX notation is rendered client-side by [MathJax 3](https://www.mathjax.org/). Use `$...$` for inline math and `$$...$$` for displayed equations. All standard AMS math commands (`\mathbb`, `\mathcal`, `\operatorname`, etc.) are supported.
- **GitHub Pages** — Push this repository to GitHub and enable Pages from **Settings → Pages → Branch: main → / (root)**. The site builds automatically via Jekyll.
- **Local Preview** — Install Ruby and run `gem install jekyll bundler`, then `bundle exec jekyll serve`. The site will be available at `http://localhost:4000`.
