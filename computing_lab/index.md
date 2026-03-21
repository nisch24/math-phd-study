---
layout: default
title: "Computing Laboratory"
nav_order: 7
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
    <div class="module-desc">NumPy, SciPy, and Eigen implementations of linear algebra, optimization, and probability simulations.</div>
  </a>
  <a href="{{ site.baseurl }}/computing_lab/matlab/" class="module-card">
    <span class="module-label label-foundation">📊 MATLAB</span>
    <div class="module-title">Matrix & Optimization</div>
    <div class="module-desc">Matrix decompositions, eigenvalue problems, and optimization toolbox tutorials.</div>
  </a>
  <a href="{{ site.baseurl }}/computing_lab/latex_tutorial/" class="module-card">
    <span class="module-label label-elective">📄 LaTeX</span>
    <div class="module-title">Technical Writing</div>
    <div class="module-desc">Document structure, mathematical typesetting, TikZ diagrams, and BibTeX bibliography management.</div>
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
    <div class="step-desc"><a href="https://eigen.tuxfamily.org/">Eigen</a> — header-only, no installation needed.</div>
  </div>
  <div class="step-card">
    <div class="step-number">📊</div>
    <div class="step-title">MATLAB R2023a+</div>
    <div class="step-desc">Requires the Optimization Toolbox for Module D exercises.</div>
  </div>
  <div class="step-card">
    <div class="step-number">📄</div>
    <div class="step-title">LaTeX</div>
    <div class="step-desc">TeX Live 2023 or MiKTeX. Editor: TeXstudio, Overleaf, or VS Code with LaTeX Workshop.</div>
  </div>
</div>
