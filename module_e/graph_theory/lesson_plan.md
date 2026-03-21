---
layout: default
title: "EN.553.672 — Graph Theory"
parent: "Module E — Discrete Mathematics"
nav_order: 2
permalink: /module_e/graph_theory/
---

# EN.553.672 — Graph Theory

> *Structural properties of graphs and networks. This course covers Eulerian and Hamiltonian circuits, planarity, graph coloring, network flows (max-flow min-cut), and matching theory — the discrete backbone of network optimization and algorithm design.*

---

## Learning Objectives

1. **Characterize graph connectivity** and apply criteria for Eulerian and Hamiltonian circuits.
2. **Determine planarity** using Kuratowski's theorem and Euler's formula.
3. **Apply graph coloring** results including Brooks' theorem and the chromatic polynomial.
4. **Solve network flow problems** using Ford-Fulkerson and prove the Max-Flow Min-Cut theorem.
5. **Apply matching theory** via Hall's theorem and the Hungarian algorithm.

---

## Core Theory

### Unit 1: Fundamental Graph Properties

#### 1.1 Basic Definitions

A **graph** $G = (V, E)$ consists of a vertex set $V$ and edge set $E \subseteq \binom{V}{2}$.

- **Degree**: $\deg(v) = |\{e \in E : v \in e\}|$. **Handshaking Lemma**: $\sum_{v \in V} \deg(v) = 2|E|$.
- **Walk**: a sequence $v_0 e_1 v_1 e_2 \cdots e_k v_k$ of alternating vertices and edges.
- **Path**: a walk with no repeated vertices. **Cycle**: a closed walk with no repeated vertices except $v_0 = v_k$.
- **Connected**: every pair of vertices is joined by a path.

#### 1.2 Trees

A **tree** is a connected acyclic graph.

**Characterizations** (equivalent for a graph on $n$ vertices):
1. Connected and acyclic.
2. Connected with exactly $n - 1$ edges.
3. Acyclic with exactly $n - 1$ edges.
4. Every pair of vertices is connected by a unique path.

**Cayley's Formula**: The number of labeled trees on $n$ vertices is $n^{n-2}$.

*Proof via Prüfer sequences*: There is a bijection between labeled trees on $[n]$ and sequences in $[n]^{n-2}$.

---

### Unit 2: Eulerian and Hamiltonian Circuits

#### 2.1 Eulerian Circuits and Paths

**Definition**: An **Eulerian circuit** traverses every edge exactly once and returns to the start. An **Eulerian path** traverses every edge exactly once.

**Theorem (Euler, 1736)**: A connected graph has an Eulerian circuit if and only if every vertex has even degree. It has an Eulerian path if and only if exactly 0 or 2 vertices have odd degree.

*Proof (circuit)*: Necessity: each visit to a vertex uses one entering and one leaving edge, so degrees must be even. Sufficiency: construct a circuit greedily; if edges remain, splice in sub-circuits (Hierholzer's algorithm).

#### 2.2 Hamiltonian Circuits

**Definition**: A **Hamiltonian cycle** visits every vertex exactly once (and returns to the start).

**Key results**:
- **Dirac's Theorem**: If $|V| \geq 3$ and $\deg(v) \geq n/2$ for all $v$, then $G$ has a Hamiltonian cycle.
- **Ore's Theorem**: If $\deg(u) + \deg(v) \geq n$ for every pair of non-adjacent vertices $u, v$, then $G$ is Hamiltonian.
- Determining Hamiltonicity is **NP-complete** (no known efficient criterion).

---

### Unit 3: Planarity and Coloring

#### 3.1 Planar Graphs and Euler's Formula

**Euler's Formula**: For a connected planar graph with $v$ vertices, $e$ edges, and $f$ faces:

$$v - e + f = 2$$

**Corollary**: For a simple planar graph with $v \geq 3$: $e \leq 3v - 6$. If also triangle-free: $e \leq 2v - 4$.

#### 3.2 Kuratowski's Theorem

**Theorem (Kuratowski, 1930)**: A graph is planar if and only if it contains no subdivision of $K_5$ or $K_{3,3}$.

**Wagner's Theorem**: Equivalently, $G$ is planar iff it has no $K_5$ or $K_{3,3}$ minor.

#### 3.3 Graph Coloring

**Definition**: A **proper $k$-coloring** assigns one of $k$ colors to each vertex so that adjacent vertices receive different colors. The **chromatic number** $\chi(G)$ is the minimum $k$.

**Key results**:
- **Greedy bound**: $\chi(G) \leq \Delta(G) + 1$ where $\Delta$ is the maximum degree.
- **Brooks' Theorem**: $\chi(G) \leq \Delta(G)$ unless $G$ is a complete graph or an odd cycle.
- **Four Color Theorem**: Every planar graph satisfies $\chi(G) \leq 4$.
- **Five-Color Theorem** (provable by elementary means): Every planar graph satisfies $\chi(G) \leq 5$.

**Chromatic Polynomial**: $P(G, k)$ counts the number of proper $k$-colorings. Satisfies the deletion-contraction recurrence:

$$P(G, k) = P(G - e, k) - P(G / e, k)$$

---

### Unit 4: Network Flows

#### 4.1 Flow Networks

A **flow network** $(G, c, s, t)$ has a directed graph with source $s$, sink $t$, and capacity function $c: E \to \mathbb{R}_{\geq 0}$.

A **flow** $f: E \to \mathbb{R}_{\geq 0}$ satisfies:
1. **Capacity**: $0 \leq f(e) \leq c(e)$ for all $e$.
2. **Conservation**: $\sum_{u \to v} f(u,v) = \sum_{v \to w} f(v,w)$ for all $v \neq s, t$.

The **value** of the flow: $|f| = \sum_{s \to v} f(s,v) - \sum_{v \to s} f(v,s)$.

#### 4.2 The Max-Flow Min-Cut Theorem

**Definition**: An **$s$-$t$ cut** is a partition $(S, T)$ of $V$ with $s \in S$, $t \in T$. Its **capacity** is $c(S, T) = \sum_{u \in S, v \in T} c(u, v)$.

**Theorem (Ford-Fulkerson)**: The maximum flow value equals the minimum cut capacity:

$$\max_f |f| = \min_{(S,T)} c(S,T)$$

*Proof*: (1) For any flow and cut, $|f| \leq c(S,T)$ (weak duality). (2) When no augmenting path exists in the residual graph, the reachable set from $s$ defines a cut achieving equality.

#### 4.3 Ford-Fulkerson Algorithm

```
Initialize f(e) = 0 for all e
While there exists an augmenting path P in the residual graph:
    δ = min capacity along P
    Augment f along P by δ
Return f
```

With BFS for shortest augmenting paths (**Edmonds-Karp**), the algorithm runs in $O(VE^2)$.

#### 4.4 Applications

- **Bipartite matching** via unit-capacity flow.
- **Edge-disjoint paths** (Menger's theorem).
- **Minimum vertex cut** (vertex splitting).
- **Project selection** / closure problems.

---

### Unit 5: Matching Theory

#### 5.1 Matchings in Bipartite Graphs

**Definition**: A **matching** $M$ is a set of pairwise non-adjacent edges. A **perfect matching** covers all vertices.

**Theorem (Hall, 1935)**: A bipartite graph $G = (A \cup B, E)$ has a matching that saturates $A$ if and only if for every $S \subseteq A$:

$$|N(S)| \geq |S|$$

where $N(S)$ is the set of neighbors of $S$.

*Proof*: Necessity is clear. Sufficiency by induction or via max-flow min-cut.

#### 5.2 König's Theorem

**Theorem (König, 1931)**: In a bipartite graph, the maximum matching size equals the minimum vertex cover size.

**Equivalence**: This is equivalent to the LP relaxation of maximum matching being integral for bipartite graphs, which follows from total unimodularity.

#### 5.3 The Hungarian Algorithm

For **weighted bipartite matching** (assignment problem): find a perfect matching of minimum total weight. The Hungarian algorithm solves this in $O(n^3)$ using a primal-dual approach.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Introduction to Graph Theory* (2nd ed.) | Douglas B. West | **Primary** |
| *Graph Theory* | J.A. Bondy & U.S.R. Murty | **Primary Alternative** |
| *Graph Theory* (5th ed.) | Reinhard Diestel | **Supplementary** — Graduate-level, freely available |
| *Combinatorial Optimization* | Bernhard Korte & Jens Vygen | **Advanced** — Algorithms on graphs |

---

## Problem Sets

### Problem Set 1: Eulerian/Hamiltonian and Trees

1. **(West 1.2.18)** Prove that a connected graph has an Eulerian circuit iff every vertex has even degree.
2. **(Exam-style)** Verify Cayley's formula for $n = 4$ by listing all labeled trees.
3. **(Exam-style)** Use Dirac's theorem to determine if the Petersen graph is Hamiltonian.
4. **(Proof)** Prove that every tree with $n \geq 2$ vertices has at least 2 leaves.
5. **(Challenge)** Prove Ore's theorem.

### Problem Set 2: Planarity and Coloring

1. **(West 6.1)** Use Euler's formula to prove $K_5$ is not planar.
2. **(Exam-style)** Prove the Five Color Theorem using induction and Euler's formula.
3. **(Exam-style)** Compute the chromatic polynomial of the cycle $C_4$.
4. **(Proof)** Prove Brooks' theorem for connected graphs.
5. **(Challenge)** Show that the chromatic number of the Kneser graph $K(n,k)$ is $n - 2k + 2$ (Lovász's theorem statement).

### Problem Set 3: Network Flows and Matching

1. **(West 4.3)** Use Ford-Fulkerson to find the maximum flow in a given network. Identify the minimum cut.
2. **(Exam-style)** Prove the Max-Flow Min-Cut theorem using augmenting paths.
3. **(Exam-style)** Prove Hall's Theorem using König's Theorem.
4. **(Application)** Model the assignment of 5 workers to 5 jobs (with preferences) as a bipartite matching problem. Solve using the Hungarian algorithm.
5. **(Challenge)** Prove König's Theorem using LP duality and total unimodularity.
