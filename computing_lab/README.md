---
layout: default
title: "Computing Laboratory"
nav_order: 7
has_children: true
permalink: /computing_lab/
---

# Computing Laboratory

> *Bridging theory and practice.* This section provides hands-on tutorials for implementing the mathematical theories studied in Modules A–E. Each tutorial pairs a theoretical concept with working code in Python/C++, MATLAB, or LaTeX.

---

## Tutorials

| Tutorial | Tools | Connected Modules |
|----------|-------|-------------------|
| [Python & C++ Numerical Algorithms](python_cpp) | Python (NumPy/SciPy), C++ (Eigen) | A, B, D |
| [MATLAB Matrix & Optimization](matlab) | MATLAB | A, D |
| [LaTeX Technical Writing](latex_tutorial) | LaTeX, BibTeX, TikZ | All |

## Setup Requirements

### Python
```bash
# Recommended: Python 3.10+
pip install numpy scipy matplotlib
```

### C++
- Compiler: GCC 11+ or MSVC 2022
- Library: [Eigen](https://eigen.tuxfamily.org/) (header-only, no installation needed)

### MATLAB
- MATLAB R2023a+ with Optimization Toolbox

### LaTeX
- TeX Live 2023 or MiKTeX (Windows)
- Editor: TeXstudio, Overleaf, or VS Code with LaTeX Workshop
