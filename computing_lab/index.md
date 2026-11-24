---
layout: default
title: "Computing Laboratory"
nav_order: 10
has_children: true
permalink: /computing_lab/
---

<div class="hero-section" style="background: linear-gradient(135deg, #002D72, #0891B2);">
  <h1>🖥️ Computing Laboratory</h1>
  <p>Bridging theory and practice. Hands-on tutorials for implementing the mathematical theories from Modules A–E in Python, C++, MATLAB, and LaTeX.</p>
</div>

---

## Tutorials

<div class="module-grid">
  <a href="{{ site.baseurl }}/computing_lab/python_cpp/" class="module-card">
    <span class="module-label label-core">🐍 Python · C++</span>
    <div class="module-title">Numerical Algorithms</div>
    <div class="module-desc">NumPy, SciPy, and Eigen implementations of linear algebra, optimization, and probability simulations — directly paired with Module theory.</div>
  </a>
  <a href="{{ site.baseurl }}/computing_lab/matlab/" class="module-card">
    <span class="module-label label-foundation">📊 MATLAB</span>
    <div class="module-title">Matrix &amp; Optimization</div>
    <div class="module-desc">Matrix decompositions, eigenvalue problems, convergence visualization, and optimization toolbox tutorials for Modules A and D.</div>
  </a>
  <a href="{{ site.baseurl }}/computing_lab/latex_tutorial/" class="module-card">
    <span class="module-label label-elective">📄 LaTeX</span>
    <div class="module-title">Technical Writing</div>
    <div class="module-desc">Document structure, mathematical typesetting, theorem environments, TikZ diagrams, and BibTeX bibliography management for PhD-level writing.</div>
  </a>
</div>

---

## Setup Requirements

<div class="steps-grid">
  <div class="step-card">
    <div class="step-number">🐍</div>
    <div class="step-title">Python 3.10+</div>
    <div class="step-desc"><code>pip install numpy scipy matplotlib</code></div>
  </div>
  <div class="step-card">
    <div class="step-number">⚙️</div>
    <div class="step-title">C++ (GCC 11+ / MSVC)</div>
    <div class="step-desc"><a href="https://eigen.tuxfamily.org/">Eigen</a> — header-only linear algebra library; no installation beyond copying the headers.</div>
  </div>
  <div class="step-card">
    <div class="step-number">📊</div>
    <div class="step-title">MATLAB R2023a+</div>
    <div class="step-desc">Requires the Optimization Toolbox for Module D exercises. Student licenses are usually available through your university; GNU Octave runs most of the non-toolbox examples for free.</div>
  </div>
  <div class="step-card">
    <div class="step-number">📄</div>
    <div class="step-title">LaTeX</div>
    <div class="step-desc">TeX Live 2023 or MiKTeX. Recommended editors: TeXstudio (desktop), Overleaf (browser), or VS Code with the LaTeX Workshop extension.</div>
  </div>
</div>
