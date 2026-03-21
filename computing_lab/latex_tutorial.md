---
layout: default
title: "LaTeX Technical Writing"
parent: "Computing Laboratory"
nav_order: 3
permalink: /computing_lab/latex_tutorial/
---

# LaTeX Technical Writing Tutorial

> *Professional mathematical typesetting for dissertations, papers, and technical reports. This tutorial covers document structure, theorem environments, mathematical notation, bibliographies, and TikZ diagrams.*

---

## 1. Document Structure

### Dissertation/Thesis Template

```latex
\documentclass[12pt, letterpaper]{report}

% Packages
\usepackage[margin=1in]{geometry}
\usepackage{amsmath, amssymb, amsthm}
\usepackage{mathtools}
\usepackage{enumerate}
\usepackage{hyperref}
\usepackage{graphicx}
\usepackage{tikz}
\usepackage{algorithm2e}
\usepackage[backend=biber, style=numeric-comp, sorting=nyt]{biblatex}
\addbibresource{references.bib}

% Theorem environments
\theoremstyle{plain}
\newtheorem{theorem}{Theorem}[chapter]
\newtheorem{lemma}[theorem]{Lemma}
\newtheorem{proposition}[theorem]{Proposition}
\newtheorem{corollary}[theorem]{Corollary}

\theoremstyle{definition}
\newtheorem{definition}[theorem]{Definition}
\newtheorem{example}[theorem]{Example}

\theoremstyle{remark}
\newtheorem{remark}[theorem]{Remark}

% Custom commands
\newcommand{\R}{\mathbb{R}}
\newcommand{\E}{\mathbb{E}}
\newcommand{\Var}{\operatorname{Var}}
\newcommand{\Cov}{\operatorname{Cov}}
\newcommand{\norm}[1]{\left\| #1 \right\|}
\newcommand{\inner}[2]{\left\langle #1, #2 \right\rangle}
\DeclareMathOperator*{\argmin}{arg\,min}
\DeclareMathOperator*{\argmax}{arg\,max}

\title{Dissertation Title}
\author{Your Name}
\date{\today}

\begin{document}
\maketitle
\tableofcontents

\chapter{Introduction}
...

\chapter{Theoretical Framework}
\begin{theorem}[Martingale Convergence]
\label{thm:martingale}
Let $(M_n, \mathcal{F}_n)$ be a submartingale with
$\sup_n \E[M_n^+] < \infty$. Then $M_n \to M_\infty$
almost surely for some integrable $M_\infty$.
\end{theorem}

\begin{proof}
By Doob's upcrossing inequality...
\end{proof}

\printbibliography
\end{document}
```

---

## 2. Mathematical Notation Reference

### Common Constructions

```latex
% Inline math
The MLE satisfies $\hat{\theta}_n \xrightarrow{P} \theta_0$.

% Display math
\[
  \sqrt{n}(\hat{\theta} - \theta) \xrightarrow{d} N(0, I(\theta)^{-1})
\]

% Aligned equations
\begin{align}
  \mathcal{L}(x, \lambda) &= f(x) - \lambda^T c(x) \\
  \nabla_x \mathcal{L} &= \nabla f(x) - \lambda^T \nabla c(x) = 0 \\
  c(x) &= 0
\end{align}

% Cases
\[
  \phi(x) = \begin{cases}
    1 & \text{if } T(x) > c \\
    \gamma & \text{if } T(x) = c \\
    0 & \text{if } T(x) < c
  \end{cases}
\]

% Matrices
\[
  A = \begin{pmatrix}
    a_{11} & a_{12} \\
    a_{21} & a_{22}
  \end{pmatrix}, \quad
  \det(A) = a_{11}a_{22} - a_{12}a_{21}
\]

% Sums and products
\[
  L(\theta | x) = \prod_{i=1}^n f(x_i | \theta), \quad
  \ell(\theta) = \sum_{i=1}^n \log f(x_i | \theta)
\]
```

### Probability and Statistics

```latex
% Sigma-algebras and measure theory
$(\Omega, \mathcal{F}, P)$, \quad $\sigma$-algebra $\mathcal{B}(\R)$

% Convergence modes
$X_n \xrightarrow{\text{a.s.}} X$, \quad
$X_n \xrightarrow{P} X$, \quad
$X_n \xrightarrow{L^p} X$, \quad
$X_n \xrightarrow{d} X$

% Conditional expectation
$\E[X | \mathcal{G}]$, \quad $\E[X | Y = y]$

% Fisher Information
$I(\theta) = -\E\left[\frac{\partial^2}{\partial\theta^2}
  \log f(X|\theta)\right]$
```

---

## 3. Bibliographies with BibTeX

### `references.bib`

```bibtex
@book{rudin1976,
  author    = {Walter Rudin},
  title     = {Principles of Mathematical Analysis},
  edition   = {3rd},
  publisher = {McGraw-Hill},
  year      = {1976},
}

@book{durrett2019,
  author    = {Rick Durrett},
  title     = {Probability: Theory and Examples},
  edition   = {5th},
  publisher = {Cambridge University Press},
  year      = {2019},
}

@book{casella2002,
  author    = {George Casella and Roger L. Berger},
  title     = {Statistical Inference},
  edition   = {2nd},
  publisher = {Duxbury Press},
  year      = {2002},
}

@book{nocedal2006,
  author    = {Jorge Nocedal and Stephen J. Wright},
  title     = {Numerical Optimization},
  edition   = {2nd},
  publisher = {Springer},
  year      = {2006},
}

@book{horn2013,
  author    = {Roger A. Horn and Charles R. Johnson},
  title     = {Matrix Analysis},
  edition   = {2nd},
  publisher = {Cambridge University Press},
  year      = {2013},
}
```

### Usage

```latex
As shown in \cite{rudin1976}, every compact subset of
a metric space is closed and bounded.

The MLE theory follows \cite{casella2002, nocedal2006}.
```

---

## 4. TikZ Diagrams

### Optimization Landscape

```latex
\begin{tikzpicture}
  % Contour plot of a quadratic
  \draw[->] (-2.5, 0) -- (2.5, 0) node[right] {$x_1$};
  \draw[->] (0, -2.5) -- (0, 2.5) node[above] {$x_2$};

  % Elliptical contours
  \foreach \r in {0.5, 1.0, 1.5, 2.0} {
    \draw[blue!50, thick] (0,0) ellipse ({\r} and {\r*0.5});
  }

  % Gradient descent path
  \draw[->, red, very thick] (2, 0.8) -- (1.2, 0.3);
  \draw[->, red, very thick] (1.2, 0.3) -- (0.7, -0.1);
  \draw[->, red, very thick] (0.7, -0.1) -- (0.3, 0.05);

  \fill[red] (0, 0) circle (2pt) node[below right] {$x^*$};
  \fill[red] (2, 0.8) circle (2pt) node[above] {$x_0$};
\end{tikzpicture}
```

### Probability Tree

```latex
\begin{tikzpicture}[
  level 1/.style={sibling distance=4cm},
  level 2/.style={sibling distance=2cm},
  edge from parent/.style={draw, -latex}
]
  \node {Start}
    child { node {$H$}
      child { node {$HH$} edge from parent node[left] {$p$} }
      child { node {$HT$} edge from parent node[right] {$q$} }
      edge from parent node[left] {$p$}
    }
    child { node {$T$}
      child { node {$TH$} edge from parent node[left] {$p$} }
      child { node {$TT$} edge from parent node[right] {$q$} }
      edge from parent node[right] {$q$}
    };
\end{tikzpicture}
```

---

## 5. Best Practices

1. **Use `\newcommand`** for repeated notation — makes global changes trivial.
2. **Label everything**: `\label{thm:clt}`, `\label{eq:kkt}`, `\label{fig:contour}`.
3. **Cross-reference**: `Theorem~\ref{thm:clt}`, `Equation~\eqref{eq:kkt}`.
4. **Use `\operatorname`** for multi-letter operators: `\operatorname{tr}`, `\operatorname{diag}`.
5. **Compile cycle**: `pdflatex → biber → pdflatex → pdflatex`.

---

## Exercises

1. **Typeset a proof**: Write the complete proof of the Inverse Function Theorem in LaTeX, including a theorem environment, labeled equations, and at least one lemma.
2. **Create a bibliography**: Build a `.bib` file with all textbooks from Module A and cite them in a short document.
3. **Draw a TikZ diagram**: Create a diagram illustrating the contraction mapping iteration $x_{n+1} = T(x_n)$ converging to a fixed point.
4. **Homework template**: Create a reusable LaTeX template for weekly problem sets with numbered problems and sub-parts.
5. **Beamer presentation**: Create a 5-slide Beamer presentation summarizing the Central Limit Theorem with theorem environments and a convergence diagram.
