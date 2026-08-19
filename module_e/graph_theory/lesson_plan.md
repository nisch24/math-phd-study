---
layout: default
title: "EN.553.672 — Graph Theory"
parent: "Module E — Discrete Mathematics"
nav_order: 2
permalink: /module_e/graph_theory/
---

# EN.553.672 — Graph Theory

> *Structural properties of graphs and networks. This course covers Eulerian and Hamiltonian circuits, planarity, graph coloring, network flows (Max-Flow Min-Cut), and matching theory — the discrete backbone of network optimization and algorithm design.*

---

## Learning Objectives

Upon completing this module, the student will be able to:

1. **Characterize graph connectivity** and apply necessary and sufficient criteria for Eulerian and Hamiltonian circuits.
2. **Determine planarity** using Kuratowski's theorem and derive bounds from Euler's formula.
3. **Apply graph coloring results** including Brooks' theorem and the chromatic polynomial.
4. **Solve network flow problems** via Ford-Fulkerson and prove the Max-Flow Min-Cut theorem.
5. **Apply matching theory** through Hall's theorem, König's theorem, and the Hungarian algorithm.

---

## Core Theory

### Unit 1: Fundamental Graph Properties

#### 1.1 Basic Definitions

A **graph** $G = (V, E)$ consists of a vertex set $V$ and edge set $E \subseteq \binom{V}{2}$.

- **Degree**: $\deg(v) = |\{e \in E : v \in e\}|$.
- **Handshaking Lemma**: $\sum_{v \in V} \deg(v) = 2|E|$ (each edge contributes to two degrees).
- **Walk**: a sequence $v_0 e_1 v_1 e_2 \cdots e_k v_k$ of alternating vertices and edges.
- **Path**: a walk with no repeated vertices. **Cycle**: a closed walk ($v_0 = v_k$) with no other repeated vertices.
- **Connected**: every pair of vertices is joined by a path.

#### 1.2 Trees

A **tree** is a connected acyclic graph. The following are equivalent for a graph on $n$ vertices:

1. $G$ is connected and acyclic.
2. $G$ is connected with exactly $n - 1$ edges.
3. $G$ is acyclic with exactly $n - 1$ edges.
4. Every pair of vertices is connected by a **unique** path.

**Cayley's Formula**: The number of labeled trees on $n$ vertices is $n^{n-2}$.

*Proof via Prüfer Sequences*: There is a bijection between labeled trees on $[n]$ and sequences in $[n]^{n-2}$. Each tree produces a unique sequence by iteratively removing the smallest leaf and recording its neighbor.

---

### Unit 2: Eulerian and Hamiltonian Circuits

#### 2.1 Eulerian Circuits and Paths

**Definition**: An **Eulerian circuit** traverses every edge exactly once and returns to the starting vertex. An **Eulerian path** traverses every edge exactly once (but need not return to the start).

**Theorem (Euler, 1736)**: A connected graph has an Eulerian circuit if and only if every vertex has even degree. It has an Eulerian path if and only if exactly 0 or 2 vertices have odd degree.

*Proof (circuit, sufficiency)*: Construct a circuit greedily from any starting vertex. If edges remain after completing a circuit, the graph remains connected (since all vertices have even degree), and a sub-circuit starting at a vertex of the original circuit can be spliced in (Hierholzer's algorithm). Iterate until all edges are traversed.

#### 2.2 Hamiltonian Circuits

**Definition**: A **Hamiltonian cycle** visits every vertex exactly once and returns to the start.

**Key Results**:
- **Dirac's Theorem**: If $|V| \geq 3$ and $\deg(v) \geq |V|/2$ for all $v$, then $G$ has a Hamiltonian cycle.
- **Ore's Theorem**: If $\deg(u) + \deg(v) \geq |V|$ for every pair of non-adjacent vertices $u, v$, then $G$ is Hamiltonian.
- Determining Hamiltonicity in general is **NP-complete** — no efficiently checkable characterization is known.

---

### Unit 3: Planarity and Graph Coloring

#### 3.1 Planar Graphs and Euler's Formula

**Euler's Formula**: For any connected planar graph with $v$ vertices, $e$ edges, and $f$ faces (including the outer face):

$$v - e + f = 2.$$

**Corollaries for Simple Planar Graphs** (with $v \geq 3$):
- $e \leq 3v - 6$ (using that each face is bounded by at least 3 edges).
- If additionally triangle-free: $e \leq 2v - 4$.

#### 3.2 Kuratowski's Theorem

**Theorem (Kuratowski, 1930)**: A graph is planar if and only if it contains no subdivision of $K_5$ or $K_{3,3}$ as a subgraph.

**Wagner's Theorem**: Equivalently, $G$ is planar if and only if it has no $K_5$ or $K_{3,3}$ as a graph minor.

#### 3.3 Graph Coloring

**Definition**: A **proper $k$-coloring** assigns one of $k$ colors to each vertex so that adjacent vertices receive distinct colors. The **chromatic number** $\chi(G)$ is the minimum $k$ for which a proper $k$-coloring exists.

**Key Results**:
- **Greedy bound**: $\chi(G) \leq \Delta(G) + 1$, where $\Delta$ is the maximum degree.
- **Brooks' Theorem**: $\chi(G) \leq \Delta(G)$ unless $G$ is a complete graph or an odd cycle.
- **Five Color Theorem**: Every planar graph satisfies $\chi(G) \leq 5$ (provable by elementary means using Euler's formula).
- **Four Color Theorem**: Every planar graph satisfies $\chi(G) \leq 4$ (requires a computer-assisted proof; the Five Color Theorem is the proof-by-hand analog).

**Chromatic Polynomial**: $P(G, k)$ counts the number of proper $k$-colorings. It satisfies the deletion-contraction recurrence:

$$P(G, k) = P(G - e, k) - P(G/e, k),$$

where $G - e$ is $G$ with edge $e$ deleted and $G/e$ is $G$ with $e$ contracted.

---

### Unit 4: Network Flows

#### 4.1 Flow Networks

A **flow network** $(G, c, s, t)$ consists of a directed graph with a **source** $s$, a **sink** $t$, and a **capacity** function $c: E \to \mathbb{R}_{\geq 0}$.

A **flow** $f: E \to \mathbb{R}_{\geq 0}$ satisfies:
1. **Capacity constraint**: $0 \leq f(e) \leq c(e)$ for all $e \in E$.
2. **Flow conservation**: $\sum_{u \to v} f(u,v) = \sum_{v \to w} f(v,w)$ for all $v \neq s, t$.

The **value** of the flow: $|f| = \sum_{s \to v} f(s,v) - \sum_{v \to s} f(v,s)$.

#### 4.2 The Max-Flow Min-Cut Theorem

**Definition**: An **$s$-$t$ cut** is a partition $(S, T)$ of $V$ with $s \in S$ and $t \in T$. Its **capacity** is $c(S, T) = \sum_{u \in S,\, v \in T} c(u, v)$.

**Theorem (Ford-Fulkerson Max-Flow Min-Cut)**: The maximum flow value equals the minimum cut capacity:

$$\max_f |f| = \min_{(S,T) \text{ cut}} c(S,T).$$

*Proof*: (1) **Weak duality**: For any flow and any cut, $|f| \leq c(S,T)$ by the conservation law. (2) **Equality**: When no augmenting path exists in the residual graph, the set $S$ of vertices reachable from $s$ in the residual graph defines a cut whose capacity equals the current flow value.

#### 4.3 The Ford-Fulkerson Algorithm

```
Initialize f(e) = 0 for all e ∈ E
While there exists an augmenting path P in the residual graph:
    δ = min{ residual capacity along P }
    Augment f along P by δ
Return f
```

Using BFS to find shortest augmenting paths (**Edmonds-Karp**), the algorithm runs in $O(VE^2)$ time.

#### 4.4 Applications

- **Bipartite matching**: via a unit-capacity flow network (Hall's theorem follows from Max-Flow Min-Cut).
- **Edge-disjoint paths**: the maximum number of edge-disjoint $s$-$t$ paths equals the minimum edge cut (Menger's Theorem).
- **Minimum vertex cut**: vertex splitting reduces this to the edge-disjoint case.

---

### Unit 5: Matching Theory

#### 5.1 Matchings in Bipartite Graphs

**Definition**: A **matching** $M \subseteq E$ is a set of pairwise non-incident edges. A **perfect matching** covers every vertex of $G$.

**Theorem (Hall, 1935)**: A bipartite graph $G = (A \cup B, E)$ has a matching that saturates every vertex of $A$ if and only if for every $S \subseteq A$:

$$|N(S)| \geq |S|,$$

where $N(S)$ is the set of neighbors of $S$ in $B$.

*Proof (sufficiency)*: By induction on $|A|$, or directly via the Max-Flow Min-Cut theorem applied to a unit-capacity network.

#### 5.2 König's Theorem

**Theorem (König, 1931)**: In a bipartite graph, the size of a maximum matching equals the size of a minimum vertex cover.

**Connection to LP**: This is equivalent to the LP relaxation of maximum matching being integral for bipartite graphs, which follows from total unimodularity of the bipartite incidence matrix.

#### 5.3 The Hungarian Algorithm

The **assignment problem** asks for a minimum-weight perfect matching in a complete bipartite graph. The **Hungarian algorithm** solves this in $O(n^3)$ time using a primal-dual approach: it maintains dual variables (node potentials) that certify optimality via complementary slackness.

---

## Primary Textbooks

| Text | Author(s) | Role |
|------|-----------|------|
| *Introduction to Graph Theory* (2nd ed.) | Douglas B. West | **Primary** — Clear exposition with comprehensive exercises |
| *Graph Theory* | J.A. Bondy &amp; U.S.R. Murty | **Primary Alternative** — More encyclopedic; excellent reference |
| *Graph Theory* (5th ed.) | Reinhard Diestel | **Supplementary** — Graduate level; freely available online |
| *Combinatorial Optimization* | Bernhard Korte &amp; Jens Vygen | **Advanced** — Algorithms and polyhedral theory |

---

## Problem Sets

### Problem Set 1: Trees and Eulerian/Hamiltonian Graphs

1. **(West 1.2.18)** Prove that a connected graph has an Eulerian circuit if and only if every vertex has even degree.
2. **(Exam-style)** Verify Cayley's formula $n^{n-2}$ for $n = 4$ by listing all labeled trees on 4 vertices.
3. **(Exam-style)** Check whether the Petersen graph satisfies the hypothesis of Dirac's theorem. Is the Petersen graph Hamiltonian?
4. **(Proof)** Prove that every tree with $n \geq 2$ vertices has at least 2 leaves.
5. **(Challenge)** Prove Ore's theorem.

### Problem Set 2: Planarity and Coloring

1. **(West 6.1)** Use Euler's formula and the edge-bound $e \leq 3v - 6$ to prove $K_5$ is nonplanar.
2. **(Exam-style)** Prove the Five Color Theorem by induction using Euler's formula and a contraction argument.
3. **(Exam-style)** Compute the chromatic polynomial $P(C_4, k)$ of the 4-cycle.
4. **(Proof)** Prove Brooks' theorem for connected graphs that are neither complete graphs nor odd cycles.
5. **(Challenge)** State Lovász's theorem: the chromatic number of the Kneser graph $K(n,r)$ is $n - 2r + 2$. Verify it for $K(5,2)$ (the Petersen graph, which has $\chi = 3 = 5-4+2$).

### Problem Set 3: Network Flows and Matching

1. **(West 4.3)** Apply Ford-Fulkerson to find the maximum flow in a specific network. Identify the minimum cut and verify Max-Flow = Min-Cut.
2. **(Exam-style)** Prove the Max-Flow Min-Cut theorem using the augmenting path characterization of a maximum flow.
3. **(Exam-style)** Prove Hall's Theorem using the Max-Flow Min-Cut theorem.
4. **(Application)** Model the assignment of 5 workers to 5 tasks (with cost matrix) as a bipartite matching problem. Solve using the Hungarian algorithm and interpret the dual variables.
5. **(Challenge)** Prove König's Theorem using LP duality and total unimodularity of the bipartite incidence matrix.

---

## Study Guide &amp; Exam Preparation

> [!IMPORTANT]
> **Key Theorems for Graph Theory**
>
> - **Euler's Circuit Theorem** — even degrees $\Leftrightarrow$ Eulerian circuit; proof via Hierholzer's algorithm
> - **Euler's Formula** — $v - e + f = 2$ for connected planar graphs; leads to the edge-count bound $e \leq 3v-6$
> - **Kuratowski's Theorem** — planarity characterized by forbidden minors $K_5$ and $K_{3,3}$
> - **Brooks' Theorem** — $\chi(G) \leq \Delta(G)$ except for complete graphs and odd cycles
> - **Max-Flow Min-Cut Theorem** — maximum flow = minimum cut capacity; the central result of network theory
> - **Hall's Marriage Theorem** — bipartite matching saturating $A$ $\Leftrightarrow$ Hall's condition $|N(S)| \geq |S|$
> - **König's Theorem** — max matching = min vertex cover in bipartite graphs; dual to Max-Flow Min-Cut

**Proof-Writing Tips**:
- For Euler's circuit theorem: the necessity direction is easy; sufficiency requires constructing the circuit and showing no edges are missed.
- For Max-Flow Min-Cut: weak duality is one line; the hard direction uses the residual graph reachability argument.
- For Hall's Theorem via flows: construct the bipartite flow network, apply Max-Flow Min-Cut, and interpret the minimum cut in terms of Hall's condition.
