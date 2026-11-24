---
layout: default
title: "Module E — Discrete Mathematics"
nav_order: 8
has_children: true
permalink: /module_e/
---

<div class="hero-section" style="background: linear-gradient(135deg, #002D72, #DC2626);">
  <h1>🔢 Module E — Discrete Mathematics</h1>
  <p>Counting, structure, and algorithms. Essential tools for combinatorial probability, algorithm analysis, and network optimization.</p>
</div>

> This module covers enumerative combinatorics — generating functions, Pólya counting, and inclusion-exclusion — alongside structural graph theory including network flows, coloring, and matching. Together they form the discrete backbone of probabilistic and algorithmic reasoning.

---

## Courses

<div class="module-grid">
  <a href="{{ site.baseurl }}/module_e/combinatorial_analysis/" class="module-card">
    <span class="module-label label-elective">EN.553.671</span>
    <div class="module-title">Combinatorial Analysis</div>
    <div class="module-desc">Generating functions, Pólya counting theorem, inclusion-exclusion, Ramsey theory, Catalan numbers.</div>
  </a>
  <a href="{{ site.baseurl }}/module_e/graph_theory/" class="module-card">
    <span class="module-label label-elective">EN.553.672</span>
    <div class="module-title">Graph Theory</div>
    <div class="module-desc">Eulerian and Hamiltonian circuits, planarity (Kuratowski), network flows (Max-Flow Min-Cut), coloring, matching theory.</div>
  </a>
</div>

---

## Learning Outcomes at a Glance

| Topic | Combinatorial Analysis (671) | Graph Theory (672) |
|-------|-----------------------------|--------------------|
| Core object | Sequences, sets, and labeled structures | Graphs, networks, and matchings |
| Key theorem | Pólya Enumeration Theorem | Max-Flow Min-Cut theorem |
| Key tool | Generating functions (OGF, EGF) | Ford-Fulkerson algorithm |
| Primary text | Brualdi, *Introductory Combinatorics* + Stanley Vol. I | West, *Introduction to Graph Theory* |

---

## Prerequisites

- Undergraduate discrete mathematics or combinatorics
- Mathematical maturity: induction, the pigeonhole principle, and basic proof-writing

## Connection to Other Modules

- **Module B (Probability)** — Combinatorial arguments are fundamental to discrete probability distributions, occupancy problems, and random graph theory.
- **Module D (Optimization)** — Network flows, shortest paths, and bipartite matching are combinatorial optimization problems; LP duality connects to König's theorem.
